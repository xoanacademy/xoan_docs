# Arquitectura y Diseño Técnico - Aplicación Emprende Con Xoán

## 1. Introducción

Este documento describe la arquitectura técnica, diseño de sistema y decisiones tecnológicas para la aplicación de Emprende Con Xoán.

## 2. Arquitectura General

### 2.1 Arquitectura de Alto Nivel

```
┌─────────────────────────────────────────────────────────────┐
│                    CLIENTE (Frontend)                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Web App    │  │  Mobile App   │  │  Admin Panel │     │
│  │  (React/Vue) │  │  (React Native│  │  (React/Vue)  │     │
│  │              │  │   / Flutter)  │  │              │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            │
                            │ HTTPS/REST API
                            │
┌─────────────────────────────────────────────────────────────┐
│                    SERVIDOR (Backend)                        │
│  ┌──────────────────────────────────────────────────────┐   │
│  │              API Gateway / Load Balancer              │   │
│  └──────────────────────────────────────────────────────┘   │
│                            │                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │  Auth Service│  │ Course Service│  │Payment Service│     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │Content Service│  │Notification │  │  File Service │     │
│  └──────────────┘  │   Service    │  └──────────────┘     │
│                     └──────────────┘                        │
└─────────────────────────────────────────────────────────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼──────┐   ┌────────▼────────┐  ┌──────▼──────┐
│   Database   │   │  File Storage   │  │   Cache      │
│  (PostgreSQL)│   │   (S3/Cloud)    │  │  (Redis)     │
└──────────────┘   └─────────────────┘  └─────────────┘
        │
┌───────▼──────┐
│  External    │
│  Services    │
│  - WhatsApp  │
│  - Email     │
│  - Payment   │
└──────────────┘
```

### 2.2 Patrón Arquitectónico

**Arquitectura:** Microservicios (modular) o Monolito Modular
- **Recomendación inicial:** Monolito Modular (más simple, escalable a microservicios)
- **Razón:** Facilita desarrollo inicial, menor complejidad operativa
- **Migración futura:** Separar en microservicios cuando sea necesario

### 2.3 Principios de Diseño

1. **Separación de Responsabilidades:** Cada módulo tiene una responsabilidad única
2. **Escalabilidad:** Diseño que permite crecimiento horizontal
3. **Seguridad:** Seguridad por capas
4. **Rendimiento:** Optimización desde el inicio
5. **Mantenibilidad:** Código limpio y documentado
6. **Testabilidad:** Arquitectura que facilita testing

## 3. Stack Tecnológico

### 3.1 Frontend

#### Opción A: React (Recomendada)
- **Framework:** React 18+
- **Estado:** Redux Toolkit / Zustand
- **Routing:** React Router v6
- **UI Library:** Material-UI / Ant Design / Tailwind CSS
- **Formularios:** React Hook Form + Yup
- **HTTP Client:** Axios
- **Build Tool:** Vite / Create React App

**Ventajas:**
- Gran ecosistema
- Muchos recursos disponibles
- Buen rendimiento
- Fácil de encontrar desarrolladores

#### Opción B: Vue.js
- **Framework:** Vue 3
- **Estado:** Pinia
- **Routing:** Vue Router
- **UI Library:** Vuetify / Quasar
- **Formularios:** VeeValidate
- **HTTP Client:** Axios

**Ventajas:**
- Curva de aprendizaje más suave
- Excelente documentación
- Buen rendimiento

#### Opción C: Next.js (SSR)
- **Framework:** Next.js 14+
- **Ventajas:** SEO mejorado, SSR, optimizaciones automáticas

### 3.2 Backend

#### Opción A: Node.js (Recomendada)
- **Runtime:** Node.js 20 LTS
- **Framework:** Express.js / NestJS
- **ORM:** Prisma / TypeORM / Sequelize
- **Validación:** Joi / Zod
- **Autenticación:** JWT + Passport.js
- **Documentación API:** Swagger/OpenAPI

**Ventajas:**
- Mismo lenguaje que frontend (JavaScript/TypeScript)
- Gran ecosistema
- Buen rendimiento
- Fácil integración con servicios

#### Opción B: Python
- **Framework:** FastAPI / Django
- **ORM:** SQLAlchemy / Django ORM
- **Ventajas:** Excelente para ML/AI futuro, sintaxis clara

#### Opción C: .NET
- **Framework:** ASP.NET Core
- **ORM:** Entity Framework
- **Ventajas:** Excelente rendimiento, tipado fuerte

### 3.3 Base de Datos

#### Base de Datos Principal: PostgreSQL
- **Versión:** PostgreSQL 15+
- **Razón:** 
  - Open source y robusto
  - Excelente para relaciones complejas
  - Soporte JSON para datos flexibles
  - Escalable

#### Base de Datos de Caché: Redis
- **Uso:** 
  - Sesiones
  - Caché de consultas frecuentes
  - Rate limiting
  - Colas de trabajos

#### Base de Datos de Búsqueda (Opcional): Elasticsearch
- **Uso:** Búsqueda avanzada de cursos y contenido

### 3.4 Almacenamiento de Archivos

#### Opción A: AWS S3 (Recomendada)
- **Uso:** Videos, PDFs, imágenes
- **CDN:** CloudFront
- **Ventajas:** Escalable, confiable, integración fácil

#### Opción B: Cloudinary
- **Ventajas:** Optimización automática de imágenes/videos
- **Uso:** Mejor para contenido multimedia

#### Opción C: Google Cloud Storage
- Similar a S3, buena alternativa

### 3.5 Servicios Externos

#### Pagos
- **Stripe:** Pagos con tarjeta internacional
- **PayPal:** Pagos alternativos
- **Transferencias locales:** Integración con bancos locales (API si disponible)

#### Email
- **SendGrid / Mailgun / AWS SES:** Envío de emails transaccionales
- **Templates:** Handlebars / MJML

#### Notificaciones Push
- **Firebase Cloud Messaging (FCM):** Para Android/iOS
- **OneSignal:** Alternativa multiplataforma

#### WhatsApp
- **WhatsApp Business API:** Integración oficial
- **Twilio WhatsApp API:** Alternativa
- **Inicialmente:** Enlaces directos (más simple)

### 3.6 Infraestructura

#### Hosting
- **Opción A: Cloud (Recomendada)**
  - AWS (EC2, RDS, S3)
  - Google Cloud Platform
  - Azure
  - DigitalOcean (más económico)

- **Opción B: VPS**
  - DigitalOcean Droplets
  - Linode
  - Vultr

#### CI/CD
- **GitHub Actions / GitLab CI:** Automatización de despliegues
- **Docker:** Containerización
- **Docker Compose:** Desarrollo local

#### Monitoreo
- **Sentry:** Error tracking
- **LogRocket:** Session replay
- **New Relic / Datadog:** Performance monitoring
- **Google Analytics:** Analytics de usuario

## 4. Arquitectura de Base de Datos

### 4.1 Modelo de Datos Principal

```
Users
├── id (PK)
├── email (unique)
├── password_hash
├── name
├── phone
├── country
├── role (enum: student, admin, instructor)
├── avatar_url
├── email_verified
├── created_at
└── updated_at

Courses
├── id (PK)
├── title
├── description
├── slug (unique)
├── price_usd
├── price_rd
├── category (enum: basic, advanced, specialized)
├── level (enum: beginner, intermediate, advanced)
├── duration_hours
├── includes_certificate (boolean)
├── includes_providers (boolean)
├── includes_support (boolean)
├── status (enum: draft, active, inactive)
├── image_url
├── created_at
└── updated_at

CourseContent
├── id (PK)
├── course_id (FK)
├── type (enum: video, pdf, image, text)
├── title
├── description
├── file_url
├── order_index
├── duration_minutes (for videos)
├── created_at
└── updated_at

CourseProducts
├── id (PK)
├── course_id (FK)
├── product_name
├── description
└── order_index

Orders
├── id (PK)
├── user_id (FK)
├── order_number (unique)
├── total_amount
├── currency
├── status (enum: pending, paid, cancelled, refunded)
├── payment_method
├── payment_reference
├── created_at
└── updated_at

OrderItems
├── id (PK)
├── order_id (FK)
├── course_id (FK)
├── price
└── currency

UserCourses
├── id (PK)
├── user_id (FK)
├── course_id (FK)
├── order_id (FK)
├── progress_percentage
├── completed_at
├── certificate_url
├── access_granted_at
└── updated_at

Certificates
├── id (PK)
├── user_id (FK)
├── course_id (FK)
├── certificate_number (unique)
├── pdf_url
├── issued_at
└── verification_code

Providers
├── id (PK)
├── name
├── description
├── phone
├── email
├── whatsapp
├── address
├── website
├── category
├── products (JSON array)
├── status (enum: active, inactive)
└── created_at

DiscountCodes
├── id (PK)
├── code (unique)
├── type (enum: percentage, fixed)
├── value
├── min_purchase
├── max_uses
├── used_count
├── valid_from
├── valid_until
├── applicable_courses (JSON array, null = all)
└── status

Notifications
├── id (PK)
├── user_id (FK)
├── type (enum: email, push, in_app)
├── title
├── message
├── link
├── read (boolean)
├── sent_at
└── created_at

SupportTickets
├── id (PK)
├── user_id (FK)
├── subject
├── message
├── category
├── status (enum: open, in_progress, resolved, closed)
├── priority
├── created_at
└── updated_at

TicketReplies
├── id (PK)
├── ticket_id (FK)
├── user_id (FK)
├── message
├── attachments (JSON array)
└── created_at
```

### 4.2 Índices Recomendados

```sql
-- Performance críticos
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_user_courses_user_id ON user_courses(user_id);
CREATE INDEX idx_user_courses_course_id ON user_courses(course_id);
CREATE INDEX idx_course_content_course_id ON course_content(course_id);
CREATE INDEX idx_certificates_user_id ON certificates(user_id);
CREATE INDEX idx_certificates_verification_code ON certificates(verification_code);
```

### 4.3 Relaciones Principales

- Users 1:N Orders
- Users 1:N UserCourses
- Users 1:N Certificates
- Courses 1:N CourseContent
- Courses 1:N CourseProducts
- Courses 1:N OrderItems
- Orders 1:N OrderItems
- Orders 1:N UserCourses
- Users 1:N SupportTickets
- SupportTickets 1:N TicketReplies

## 5. Arquitectura de API

### 5.1 Estructura RESTful

```
Base URL: https://api.emprendeconxoan.com/v1

Autenticación:
POST   /auth/register
POST   /auth/login
POST   /auth/logout
POST   /auth/refresh
POST   /auth/forgot-password
POST   /auth/reset-password

Usuarios:
GET    /users/me
PUT    /users/me
PUT    /users/me/password
GET    /users/me/courses
GET    /users/me/certificates
GET    /users/me/orders

Cursos:
GET    /courses
GET    /courses/:id
GET    /courses/:id/content
GET    /courses/:id/providers
POST   /courses (admin)
PUT    /courses/:id (admin)
DELETE /courses/:id (admin)

Compras:
POST   /cart/add
GET    /cart
DELETE /cart/:itemId
POST   /checkout
GET    /orders
GET    /orders/:id
POST   /orders/:id/payment-proof

Contenido:
GET    /content/:id/download
POST   /content/:id/mark-complete

Certificados:
GET    /certificates
GET    /certificates/:id
GET    /certificates/:id/download
GET    /certificates/verify/:code

Proveedores:
GET    /providers
GET    /providers/:id

Soporte:
POST   /support/tickets
GET    /support/tickets
GET    /support/tickets/:id
POST   /support/tickets/:id/reply

Admin:
GET    /admin/dashboard
GET    /admin/users
GET    /admin/orders
GET    /admin/courses
GET    /admin/analytics
POST   /admin/discount-codes
```

### 5.2 Autenticación y Autorización

#### JWT (JSON Web Tokens)
- **Access Token:** Válido 15 minutos
- **Refresh Token:** Válido 7 días
- **Almacenamiento:** 
  - Access Token: Memory (frontend)
  - Refresh Token: HttpOnly Cookie

#### Roles y Permisos
```javascript
Roles:
- student: Acceso a cursos comprados
- admin: Acceso completo
- instructor: Crear/editar contenido (futuro)

Permisos:
- courses:read, courses:write, courses:delete
- users:read, users:write, users:delete
- orders:read, orders:write
- content:read, content:write
- certificates:read, certificates:write
```

### 5.3 Versionado de API
- **Estrategia:** URL versioning (`/v1/`, `/v2/`)
- **Razón:** Permite cambios sin romper clientes existentes

### 5.4 Rate Limiting
- **Público:** 100 requests/minuto
- **Autenticado:** 1000 requests/minuto
- **Admin:** Sin límite

## 6. Seguridad

### 6.1 Medidas de Seguridad

#### Autenticación
- Passwords hasheados con bcrypt (cost factor 12)
- JWT con firma segura
- Refresh tokens rotados
- Protección contra brute force

#### Autorización
- RBAC (Role-Based Access Control)
- Verificación de permisos en cada endpoint
- Validación de ownership (usuario solo accede a sus recursos)

#### Protección de Datos
- HTTPS obligatorio (TLS 1.3)
- Encriptación de datos sensibles en BD
- Sanitización de inputs
- Protección SQL Injection (ORM)
- Protección XSS (escaping)
- Protección CSRF (tokens)

#### Seguridad de Archivos
- Validación de tipos de archivo
- Escaneo de malware
- Límites de tamaño
- URLs firmadas para descargas

### 6.2 Cumplimiento
- **GDPR:** Si hay usuarios europeos
- **LGPD:** Si aplica
- **Política de Privacidad:** Obligatoria
- **Términos y Condiciones:** Obligatorio

## 7. Rendimiento y Escalabilidad

### 7.1 Optimizaciones

#### Frontend
- Code splitting
- Lazy loading de rutas
- Lazy loading de imágenes
- Caché de assets (Service Workers)
- Minificación y compresión

#### Backend
- Caché de consultas frecuentes (Redis)
- Índices de base de datos
- Paginación de resultados
- Compresión de respuestas (gzip)
- CDN para assets estáticos

#### Base de Datos
- Índices optimizados
- Consultas optimizadas
- Connection pooling
- Read replicas (futuro)

### 7.2 Escalabilidad

#### Horizontal
- Load balancer
- Múltiples instancias de aplicación
- Base de datos con replicación

#### Vertical
- Aumento de recursos del servidor

#### Caché
- Redis para sesiones y datos frecuentes
- CDN para contenido estático
- Caché de consultas de BD

## 8. Monitoreo y Logging

### 8.1 Logging
- **Niveles:** Error, Warn, Info, Debug
- **Formato:** JSON estructurado
- **Almacenamiento:** Archivos rotados + servicio de logs (CloudWatch, etc.)

### 8.2 Monitoreo
- **Health checks:** `/health` endpoint
- **Métricas:** CPU, memoria, requests, errores
- **Alertas:** Email/Slack para errores críticos

### 8.3 Error Tracking
- **Sentry:** Captura de errores en producción
- **Logs estructurados:** Para debugging

## 9. Testing

### 9.1 Estrategia de Testing

#### Unit Tests
- **Cobertura objetivo:** 70%+
- **Frameworks:**
  - Frontend: Jest + React Testing Library
  - Backend: Jest / Mocha

#### Integration Tests
- Tests de API endpoints
- Tests de flujos completos

#### E2E Tests
- **Framework:** Cypress / Playwright
- **Casos críticos:** Login, compra, acceso a contenido

### 9.2 CI/CD Pipeline

```
1. Lint y format check
2. Unit tests
3. Build
4. Integration tests
5. Deploy to staging
6. E2E tests
7. Deploy to production (manual approval)
```

## 10. Despliegue

### 10.1 Ambiente de Desarrollo
- Docker Compose local
- Base de datos local o Docker
- Hot reload para desarrollo

### 10.2 Ambiente de Staging
- Réplica de producción
- Datos de prueba
- Testing antes de producción

### 10.3 Ambiente de Producción
- Servidor dedicado o cloud
- SSL/HTTPS
- Backup automático
- Monitoreo activo

## 11. Documentación

### 11.1 Documentación de API
- **Swagger/OpenAPI:** Documentación interactiva
- **Postman Collection:** Para testing

### 11.2 Documentación de Código
- **Comentarios:** En funciones complejas
- **README:** Por módulo
- **Guías:** Para desarrolladores nuevos

## 12. Roadmap Técnico

### Fase 1: MVP
- Backend básico (Node.js + Express)
- Frontend básico (React)
- Base de datos (PostgreSQL)
- Autenticación
- Catálogo de cursos
- Proceso de compra básico
- Acceso a contenido

### Fase 2: Funcionalidades Completas
- Panel de administración
- Gestión de contenido
- Sistema de certificados
- Integración de pagos completa
- Notificaciones

### Fase 3: Optimización
- Caché y optimizaciones
- Mobile app (React Native)
- Analytics avanzado
- Mejoras de UX

### Fase 4: Escalabilidad
- Microservicios (si necesario)
- CDN y optimizaciones
- Internacionalización
- Features avanzadas (comunidad, referidos)

