# Modelo de Datos - Aplicación Emprende Con Xoán

## 1. Introducción

Este documento detalla el modelo de datos completo para la aplicación, incluyendo todas las entidades, relaciones, restricciones y reglas de negocio.

## 2. Diagrama Entidad-Relación

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│    Users    │────────<│    Orders    │>────────│   Courses   │
└─────────────┘         └──────────────┘         └─────────────┘
      │                        │                        │
      │                        │                        │
      │                        │                        │
      │                  ┌─────▼─────┐                │
      │                  │OrderItems  │                │
      │                  └────────────┘                │
      │                                                │
      │                        │                        │
      │                        │                        │
┌─────▼────────┐         ┌─────▼────────┐      ┌──────▼──────────┐
│ UserCourses  │         │  Certificates│      │ CourseContent   │
└──────────────┘         └──────────────┘      └─────────────────┘
      │
      │
┌─────▼────────┐
│  Providers   │
└──────────────┘
```

## 3. Entidades Principales

### 3.1 Users (Usuarios)

**Descripción:** Almacena información de todos los usuarios del sistema.

```sql
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    country VARCHAR(100) DEFAULT 'Dominican Republic',
    role VARCHAR(20) DEFAULT 'student' CHECK (role IN ('student', 'admin', 'instructor')),
    avatar_url TEXT,
    email_verified BOOLEAN DEFAULT FALSE,
    email_verification_token VARCHAR(255),
    email_verification_expires TIMESTAMP,
    password_reset_token VARCHAR(255),
    password_reset_expires TIMESTAMP,
    last_login TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role ON users(role);
CREATE INDEX idx_users_email_verified ON users(email_verified);
```

**Campos:**
- `id`: Identificador único (UUID)
- `email`: Email único del usuario
- `password_hash`: Hash de la contraseña (bcrypt)
- `name`: Nombre completo
- `phone`: Teléfono (opcional, para WhatsApp)
- `country`: País del usuario
- `role`: Rol del usuario (student, admin, instructor)
- `avatar_url`: URL de la foto de perfil
- `email_verified`: Si el email fue verificado
- `email_verification_token`: Token para verificación
- `password_reset_token`: Token para reset de contraseña
- `last_login`: Último inicio de sesión
- `is_active`: Si la cuenta está activa

**Reglas de Negocio:**
- Email debe ser único
- Password mínimo 8 caracteres
- Email debe ser verificado para comprar
- Solo admins pueden cambiar roles

### 3.2 Courses (Cursos)

**Descripción:** Catálogo de cursos disponibles.

```sql
CREATE TABLE courses (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    title VARCHAR(255) NOT NULL,
    slug VARCHAR(255) UNIQUE NOT NULL,
    description TEXT,
    short_description VARCHAR(500),
    price_usd DECIMAL(10, 2) NOT NULL,
    price_rd DECIMAL(10, 2),
    category VARCHAR(50) CHECK (category IN ('basic', 'advanced', 'specialized')),
    level VARCHAR(50) CHECK (level IN ('beginner', 'intermediate', 'advanced')),
    duration_hours INTEGER,
    includes_certificate BOOLEAN DEFAULT FALSE,
    includes_providers BOOLEAN DEFAULT FALSE,
    includes_support BOOLEAN DEFAULT FALSE,
    image_url TEXT,
    video_preview_url TEXT,
    status VARCHAR(20) DEFAULT 'draft' CHECK (status IN ('draft', 'active', 'inactive')),
    featured BOOLEAN DEFAULT FALSE,
    sort_order INTEGER DEFAULT 0,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_courses_slug ON courses(slug);
CREATE INDEX idx_courses_status ON courses(status);
CREATE INDEX idx_courses_category ON courses(category);
CREATE INDEX idx_courses_featured ON courses(featured);
```

**Campos:**
- `id`: Identificador único
- `title`: Título del curso
- `slug`: URL amigable (único)
- `description`: Descripción completa
- `short_description`: Descripción breve
- `price_usd`: Precio en USD
- `price_rd`: Precio en pesos dominicanos
- `category`: Categoría del curso
- `level`: Nivel de dificultad
- `duration_hours`: Duración estimada
- `includes_certificate`: Si incluye certificado
- `includes_providers`: Si incluye lista de proveedores
- `includes_support`: Si incluye soporte WhatsApp
- `image_url`: Imagen principal
- `video_preview_url`: Video de preview
- `status`: Estado del curso
- `featured`: Si está destacado
- `sort_order`: Orden de visualización

**Reglas de Negocio:**
- Slug debe ser único
- Precio debe ser mayor a 0
- Solo cursos activos son visibles públicamente
- Cursos inactivos no se pueden comprar

### 3.3 CourseContent (Contenido del Curso)

**Descripción:** Archivos y materiales de cada curso.

```sql
CREATE TABLE course_content (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    course_id UUID NOT NULL REFERENCES courses(id) ON DELETE CASCADE,
    type VARCHAR(50) NOT NULL CHECK (type IN ('video', 'pdf', 'image', 'text', 'link')),
    title VARCHAR(255) NOT NULL,
    description TEXT,
    file_url TEXT,
    file_size BIGINT,
    duration_minutes INTEGER, -- Para videos
    order_index INTEGER NOT NULL DEFAULT 0,
    is_preview BOOLEAN DEFAULT FALSE, -- Si es contenido de preview
    is_required BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_course_content_course_id ON course_content(course_id);
CREATE INDEX idx_course_content_order ON course_content(course_id, order_index);
```

**Campos:**
- `id`: Identificador único
- `course_id`: Curso al que pertenece
- `type`: Tipo de contenido
- `title`: Título del contenido
- `description`: Descripción
- `file_url`: URL del archivo
- `file_size`: Tamaño en bytes
- `duration_minutes`: Duración (videos)
- `order_index`: Orden de visualización
- `is_preview`: Si es contenido de preview (gratis)
- `is_required`: Si es obligatorio verlo

**Reglas de Negocio:**
- Solo usuarios con acceso al curso pueden ver contenido
- Videos deben tener duración
- PDFs deben tener tamaño válido

### 3.4 CourseProducts (Productos del Curso)

**Descripción:** Lista de productos que se enseñan en cada curso.

```sql
CREATE TABLE course_products (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    course_id UUID NOT NULL REFERENCES courses(id) ON DELETE CASCADE,
    product_name VARCHAR(255) NOT NULL,
    description TEXT,
    order_index INTEGER NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_course_products_course_id ON course_products(course_id);
```

**Campos:**
- `id`: Identificador único
- `course_id`: Curso al que pertenece
- `product_name`: Nombre del producto
- `description`: Descripción del producto
- `order_index`: Orden de visualización

### 3.5 Orders (Órdenes)

**Descripción:** Registro de todas las compras.

```sql
CREATE TABLE orders (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    order_number VARCHAR(50) UNIQUE NOT NULL,
    total_amount DECIMAL(10, 2) NOT NULL,
    currency VARCHAR(3) NOT NULL CHECK (currency IN ('USD', 'DOP')),
    status VARCHAR(20) DEFAULT 'pending' CHECK (status IN ('pending', 'paid', 'cancelled', 'refunded')),
    payment_method VARCHAR(50),
    payment_reference VARCHAR(255), -- Referencia de pago externo
    payment_proof_url TEXT, -- URL de comprobante subido
    payment_approved_by UUID REFERENCES users(id), -- Admin que aprobó
    payment_approved_at TIMESTAMP,
    billing_name VARCHAR(255),
    billing_email VARCHAR(255),
    billing_phone VARCHAR(20),
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_order_number ON orders(order_number);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_orders_created_at ON orders(created_at);
```

**Campos:**
- `id`: Identificador único
- `user_id`: Usuario que compró
- `order_number`: Número de orden único (formato: ORD-YYYYMMDD-XXXXX)
- `total_amount`: Monto total
- `currency`: Moneda (USD o DOP)
- `status`: Estado de la orden
- `payment_method`: Método de pago usado
- `payment_reference`: Referencia del pago externo
- `payment_proof_url`: URL del comprobante subido
- `payment_approved_by`: Admin que aprobó el pago manual
- `billing_name`: Nombre de facturación
- `billing_email`: Email de facturación
- `notes`: Notas adicionales

**Reglas de Negocio:**
- Order number debe ser único
- Solo órdenes pagadas dan acceso a cursos
- Órdenes canceladas no dan acceso
- Reembolsos cambian status a 'refunded'

### 3.6 OrderItems (Items de la Orden)

**Descripción:** Cursos incluidos en cada orden.

```sql
CREATE TABLE order_items (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    order_id UUID NOT NULL REFERENCES orders(id) ON DELETE CASCADE,
    course_id UUID NOT NULL REFERENCES courses(id),
    price DECIMAL(10, 2) NOT NULL,
    currency VARCHAR(3) NOT NULL,
    discount_applied DECIMAL(10, 2) DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_order_items_order_id ON order_items(order_id);
CREATE INDEX idx_order_items_course_id ON order_items(course_id);
```

**Campos:**
- `id`: Identificador único
- `order_id`: Orden a la que pertenece
- `course_id`: Curso comprado
- `price`: Precio al momento de la compra
- `currency`: Moneda
- `discount_applied`: Descuento aplicado

**Reglas de Negocio:**
- Precio se guarda al momento de compra (no cambia)
- Descuentos se aplican a nivel de item

### 3.7 UserCourses (Cursos del Usuario)

**Descripción:** Relación entre usuarios y cursos comprados.

```sql
CREATE TABLE user_courses (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    course_id UUID NOT NULL REFERENCES courses(id) ON DELETE CASCADE,
    order_id UUID NOT NULL REFERENCES orders(id),
    progress_percentage INTEGER DEFAULT 0 CHECK (progress_percentage >= 0 AND progress_percentage <= 100),
    last_accessed_at TIMESTAMP,
    access_granted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    completed_at TIMESTAMP,
    certificate_id UUID REFERENCES certificates(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, course_id)
);

CREATE INDEX idx_user_courses_user_id ON user_courses(user_id);
CREATE INDEX idx_user_courses_course_id ON user_courses(course_id);
CREATE INDEX idx_user_courses_order_id ON user_courses(order_id);
```

**Campos:**
- `id`: Identificador único
- `user_id`: Usuario
- `course_id`: Curso
- `order_id`: Orden que dio acceso
- `progress_percentage`: Progreso (0-100)
- `last_accessed_at`: Último acceso
- `access_granted_at`: Cuando se otorgó acceso
- `completed_at`: Cuando se completó
- `certificate_id`: Certificado asociado (si existe)

**Reglas de Negocio:**
- Un usuario solo puede tener un registro por curso
- Progreso se calcula automáticamente
- Completar curso genera certificado (si aplica)

### 3.8 Certificates (Certificados)

**Descripción:** Certificados emitidos a estudiantes.

```sql
CREATE TABLE certificates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    course_id UUID NOT NULL REFERENCES courses(id),
    user_course_id UUID NOT NULL REFERENCES user_courses(id),
    certificate_number VARCHAR(50) UNIQUE NOT NULL,
    verification_code VARCHAR(20) UNIQUE NOT NULL,
    pdf_url TEXT NOT NULL,
    issued_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, course_id)
);

CREATE INDEX idx_certificates_user_id ON certificates(user_id);
CREATE INDEX idx_certificates_course_id ON certificates(course_id);
CREATE INDEX idx_certificates_verification_code ON certificates(verification_code);
CREATE INDEX idx_certificates_certificate_number ON certificates(certificate_number);
```

**Campos:**
- `id`: Identificador único
- `user_id`: Usuario que recibió el certificado
- `course_id`: Curso completado
- `user_course_id`: Relación con user_courses
- `certificate_number`: Número único del certificado
- `verification_code`: Código para verificación pública
- `pdf_url`: URL del PDF del certificado
- `issued_at`: Fecha de emisión

**Reglas de Negocio:**
- Un usuario solo puede tener un certificado por curso
- Certificado se genera automáticamente al completar
- Verification code debe ser único y aleatorio

### 3.9 Providers (Proveedores)

**Descripción:** Directorio de proveedores de materias primas.

```sql
CREATE TABLE providers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    phone VARCHAR(20),
    email VARCHAR(255),
    whatsapp VARCHAR(20),
    address TEXT,
    city VARCHAR(100),
    country VARCHAR(100) DEFAULT 'Dominican Republic',
    website VARCHAR(255),
    category VARCHAR(100), -- Tipo de productos que vende
    products JSONB, -- Array de productos que ofrece
    rating DECIMAL(3, 2) DEFAULT 0 CHECK (rating >= 0 AND rating <= 5),
    total_reviews INTEGER DEFAULT 0,
    status VARCHAR(20) DEFAULT 'active' CHECK (status IN ('active', 'inactive', 'pending')),
    featured BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_providers_status ON providers(status);
CREATE INDEX idx_providers_category ON providers(category);
CREATE INDEX idx_providers_featured ON providers(featured);
CREATE INDEX idx_providers_products ON providers USING GIN(products);
```

**Campos:**
- `id`: Identificador único
- `name`: Nombre del proveedor
- `description`: Descripción
- `phone`: Teléfono
- `email`: Email
- `whatsapp`: WhatsApp
- `address`: Dirección
- `city`: Ciudad
- `country`: País
- `website`: Sitio web
- `category`: Categoría de productos
- `products`: Array JSON de productos
- `rating`: Calificación promedio
- `total_reviews`: Total de reseñas
- `status`: Estado
- `featured`: Si está destacado

**Reglas de Negocio:**
- Al menos un método de contacto requerido
- Rating se calcula automáticamente

### 3.10 CourseProviders (Proveedores por Curso)

**Descripción:** Relación entre cursos y proveedores recomendados.

```sql
CREATE TABLE course_providers (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    course_id UUID NOT NULL REFERENCES courses(id) ON DELETE CASCADE,
    provider_id UUID NOT NULL REFERENCES providers(id) ON DELETE CASCADE,
    order_index INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(course_id, provider_id)
);

CREATE INDEX idx_course_providers_course_id ON course_providers(course_id);
CREATE INDEX idx_course_providers_provider_id ON course_providers(provider_id);
```

### 3.11 DiscountCodes (Códigos de Descuento)

**Descripción:** Códigos promocionales y descuentos.

```sql
CREATE TABLE discount_codes (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    code VARCHAR(50) UNIQUE NOT NULL,
    type VARCHAR(20) NOT NULL CHECK (type IN ('percentage', 'fixed')),
    value DECIMAL(10, 2) NOT NULL,
    min_purchase DECIMAL(10, 2) DEFAULT 0,
    max_discount DECIMAL(10, 2), -- Máximo descuento (para porcentajes)
    max_uses INTEGER,
    used_count INTEGER DEFAULT 0,
    valid_from TIMESTAMP NOT NULL,
    valid_until TIMESTAMP NOT NULL,
    applicable_courses JSONB, -- Array de course_ids, null = todos
    applicable_users JSONB, -- Array de user_ids, null = todos
    status VARCHAR(20) DEFAULT 'active' CHECK (status IN ('active', 'inactive', 'expired')),
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_discount_codes_code ON discount_codes(code);
CREATE INDEX idx_discount_codes_status ON discount_codes(status);
CREATE INDEX idx_discount_codes_valid_dates ON discount_codes(valid_from, valid_until);
```

**Campos:**
- `id`: Identificador único
- `code`: Código único (mayúsculas, sin espacios)
- `type`: Tipo (percentage o fixed)
- `value`: Valor del descuento
- `min_purchase`: Compra mínima requerida
- `max_discount`: Descuento máximo (para porcentajes)
- `max_uses`: Usos máximos
- `used_count`: Veces usado
- `valid_from`: Válido desde
- `valid_until`: Válido hasta
- `applicable_courses`: Cursos aplicables (null = todos)
- `applicable_users`: Usuarios aplicables (null = todos)
- `status`: Estado

**Reglas de Negocio:**
- Código debe ser único
- No se puede usar si expiró
- No se puede usar si alcanzó max_uses
- Validar min_purchase antes de aplicar

### 3.12 DiscountCodeUsage (Uso de Códigos)

**Descripción:** Registro de uso de códigos de descuento.

```sql
CREATE TABLE discount_code_usage (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    discount_code_id UUID NOT NULL REFERENCES discount_codes(id),
    order_id UUID NOT NULL REFERENCES orders(id),
    user_id UUID NOT NULL REFERENCES users(id),
    discount_amount DECIMAL(10, 2) NOT NULL,
    used_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_discount_code_usage_code_id ON discount_code_usage(discount_code_id);
CREATE INDEX idx_discount_code_usage_order_id ON discount_code_usage(order_id);
CREATE INDEX idx_discount_code_usage_user_id ON discount_code_usage(user_id);
```

### 3.13 Notifications (Notificaciones)

**Descripción:** Notificaciones del sistema.

```sql
CREATE TABLE notifications (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    type VARCHAR(50) NOT NULL CHECK (type IN ('email', 'push', 'in_app')),
    category VARCHAR(50), -- order, course, certificate, etc.
    title VARCHAR(255) NOT NULL,
    message TEXT NOT NULL,
    link TEXT,
    read BOOLEAN DEFAULT FALSE,
    sent BOOLEAN DEFAULT FALSE,
    sent_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_notifications_user_id ON notifications(user_id);
CREATE INDEX idx_notifications_read ON notifications(user_id, read);
CREATE INDEX idx_notifications_created_at ON notifications(created_at);
```

### 3.14 SupportTickets (Tickets de Soporte)

**Descripción:** Sistema de tickets de soporte.

```sql
CREATE TABLE support_tickets (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id),
    ticket_number VARCHAR(50) UNIQUE NOT NULL,
    subject VARCHAR(255) NOT NULL,
    message TEXT NOT NULL,
    category VARCHAR(50) CHECK (category IN ('technical', 'content', 'payment', 'other')),
    status VARCHAR(20) DEFAULT 'open' CHECK (status IN ('open', 'in_progress', 'resolved', 'closed')),
    priority VARCHAR(20) DEFAULT 'medium' CHECK (priority IN ('low', 'medium', 'high', 'urgent')),
    assigned_to UUID REFERENCES users(id), -- Admin asignado
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_support_tickets_user_id ON support_tickets(user_id);
CREATE INDEX idx_support_tickets_status ON support_tickets(status);
CREATE INDEX idx_support_tickets_ticket_number ON support_tickets(ticket_number);
```

### 3.15 TicketReplies (Respuestas de Tickets)

**Descripción:** Respuestas a tickets de soporte.

```sql
CREATE TABLE ticket_replies (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    ticket_id UUID NOT NULL REFERENCES support_tickets(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES users(id),
    message TEXT NOT NULL,
    attachments JSONB, -- Array de URLs de archivos
    is_internal BOOLEAN DEFAULT FALSE, -- Nota interna (solo admin)
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_ticket_replies_ticket_id ON ticket_replies(ticket_id);
CREATE INDEX idx_ticket_replies_user_id ON ticket_replies(user_id);
```

### 3.16 ContentProgress (Progreso de Contenido)

**Descripción:** Seguimiento de contenido visto por usuario.

```sql
CREATE TABLE content_progress (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    user_course_id UUID NOT NULL REFERENCES user_courses(id) ON DELETE CASCADE,
    content_id UUID NOT NULL REFERENCES course_content(id) ON DELETE CASCADE,
    completed BOOLEAN DEFAULT FALSE,
    progress_percentage INTEGER DEFAULT 0 CHECK (progress_percentage >= 0 AND progress_percentage <= 100),
    time_spent_minutes INTEGER DEFAULT 0,
    last_position INTEGER DEFAULT 0, -- Para videos (segundos)
    completed_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, content_id)
);

CREATE INDEX idx_content_progress_user_course ON content_progress(user_course_id);
CREATE INDEX idx_content_progress_content ON content_progress(content_id);
```

### 3.17 UserActivity (Actividad de Usuarios)

**Descripción:** Log de actividad de usuarios (opcional, para analytics).

```sql
CREATE TABLE user_activity (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE SET NULL,
    activity_type VARCHAR(50) NOT NULL,
    activity_data JSONB,
    ip_address VARCHAR(45),
    user_agent TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_user_activity_user_id ON user_activity(user_id);
CREATE INDEX idx_user_activity_type ON user_activity(activity_type);
CREATE INDEX idx_user_activity_created_at ON user_activity(created_at);
```

## 4. Vistas Útiles

### 4.1 Vista de Cursos con Estadísticas

```sql
CREATE VIEW courses_with_stats AS
SELECT 
    c.*,
    COUNT(DISTINCT uc.id) as total_students,
    COUNT(DISTINCT CASE WHEN uc.completed_at IS NOT NULL THEN uc.id END) as completed_count,
    AVG(uc.progress_percentage) as avg_progress
FROM courses c
LEFT JOIN user_courses uc ON c.id = uc.course_id
GROUP BY c.id;
```

### 4.2 Vista de Usuarios con Cursos

```sql
CREATE VIEW users_with_courses AS
SELECT 
    u.*,
    COUNT(DISTINCT uc.course_id) as total_courses,
    COUNT(DISTINCT c.id) as total_certificates
FROM users u
LEFT JOIN user_courses uc ON u.id = uc.user_id
LEFT JOIN certificates c ON u.id = c.user_id
GROUP BY u.id;
```

## 5. Triggers

### 5.1 Actualizar Progreso de Curso

```sql
CREATE OR REPLACE FUNCTION update_course_progress()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE user_courses
    SET progress_percentage = (
        SELECT COALESCE(AVG(progress_percentage), 0)
        FROM content_progress
        WHERE user_course_id = NEW.user_course_id
    ),
    updated_at = CURRENT_TIMESTAMP
    WHERE id = NEW.user_course_id;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_course_progress
AFTER INSERT OR UPDATE ON content_progress
FOR EACH ROW
EXECUTE FUNCTION update_course_progress();
```

### 5.2 Generar Certificado al Completar

```sql
CREATE OR REPLACE FUNCTION generate_certificate_on_completion()
RETURNS TRIGGER AS $$
DECLARE
    cert_id UUID;
    cert_number VARCHAR(50);
    verify_code VARCHAR(20);
BEGIN
    IF NEW.progress_percentage = 100 AND OLD.progress_percentage < 100 THEN
        -- Verificar si el curso incluye certificado
        IF EXISTS (
            SELECT 1 FROM courses 
            WHERE id = NEW.course_id 
            AND includes_certificate = TRUE
        ) THEN
            -- Generar códigos únicos
            cert_number := 'CERT-' || TO_CHAR(CURRENT_DATE, 'YYYYMMDD') || '-' || SUBSTRING(REPLACE(gen_random_uuid()::TEXT, '-', ''), 1, 8);
            verify_code := UPPER(SUBSTRING(REPLACE(gen_random_uuid()::TEXT, '-', ''), 1, 12));
            
            -- Crear certificado
            INSERT INTO certificates (user_id, course_id, user_course_id, certificate_number, verification_code, pdf_url)
            VALUES (NEW.user_id, NEW.course_id, NEW.id, cert_number, verify_code, '')
            RETURNING id INTO cert_id;
            
            -- Actualizar user_course
            UPDATE user_courses
            SET completed_at = CURRENT_TIMESTAMP,
                certificate_id = cert_id
            WHERE id = NEW.id;
        END IF;
    END IF;
    
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_generate_certificate
AFTER UPDATE OF progress_percentage ON user_courses
FOR EACH ROW
WHEN (NEW.progress_percentage = 100 AND OLD.progress_percentage < 100)
EXECUTE FUNCTION generate_certificate_on_completion();
```

## 6. Funciones de Utilidad

### 6.1 Generar Número de Orden

```sql
CREATE OR REPLACE FUNCTION generate_order_number()
RETURNS VARCHAR(50) AS $$
DECLARE
    order_num VARCHAR(50);
    date_part VARCHAR(8);
    seq_num INTEGER;
BEGIN
    date_part := TO_CHAR(CURRENT_DATE, 'YYYYMMDD');
    
    -- Obtener siguiente número secuencial del día
    SELECT COALESCE(MAX(CAST(SUBSTRING(order_number FROM 14) AS INTEGER)), 0) + 1
    INTO seq_num
    FROM orders
    WHERE order_number LIKE 'ORD-' || date_part || '-%';
    
    order_num := 'ORD-' || date_part || '-' || LPAD(seq_num::TEXT, 5, '0');
    
    RETURN order_num;
END;
$$ LANGUAGE plpgsql;
```

### 6.2 Calcular Total de Orden

```sql
CREATE OR REPLACE FUNCTION calculate_order_total(order_uuid UUID)
RETURNS DECIMAL(10, 2) AS $$
DECLARE
    total DECIMAL(10, 2);
BEGIN
    SELECT COALESCE(SUM(price - discount_applied), 0)
    INTO total
    FROM order_items
    WHERE order_id = order_uuid;
    
    RETURN total;
END;
$$ LANGUAGE plpgsql;
```

## 7. Migraciones y Versionado

### 7.1 Estrategia de Migraciones
- Usar herramienta de migraciones (Prisma, TypeORM, Flyway)
- Versionar todas las migraciones
- No modificar migraciones ya ejecutadas
- Crear nuevas migraciones para cambios

### 7.2 Backup y Restauración
- Backup diario automático
- Retención de 30 días
- Backup antes de migraciones importantes
- Pruebas de restauración periódicas

## 8. Consideraciones de Rendimiento

### 8.1 Índices Críticos
- Todos los FOREIGN KEYS deben tener índices
- Campos usados en WHERE frecuentemente
- Campos usados en JOIN
- Campos usados en ORDER BY

### 8.2 Particionamiento (Futuro)
- `user_activity` por fecha (si crece mucho)
- `notifications` por fecha
- `orders` por fecha

### 8.3 Optimizaciones
- Usar JSONB para datos flexibles (products, attachments)
- Índices GIN para búsquedas en JSONB
- Paginación en todas las consultas de listado
- Caché de consultas frecuentes (Redis)

## 9. Seguridad de Datos

### 9.1 Datos Sensibles
- Passwords: Hash con bcrypt (nunca en texto plano)
- Tokens: Encriptados o hasheados
- Información de pago: No almacenar datos completos de tarjetas

### 9.2 Encriptación
- Datos sensibles en reposo (opcional, según requerimientos)
- Conexiones SSL/TLS obligatorias
- Backup encriptados

### 9.3 Auditoría
- Log de cambios importantes (opcional)
- Timestamps en todas las tablas
- User tracking en acciones críticas

