# Casos de Uso Detallados - Aplicación Emprende Con Xoán

## 1. Introducción

Este documento describe los casos de uso principales del sistema, detallando los flujos de interacción entre los actores y el sistema.

## 2. Actores del Sistema

### 2.1 Actores Principales
- **Estudiante:** Usuario que compra y accede a cursos
- **Administrador:** Usuario con permisos de gestión completa
- **Sistema:** Procesos automáticos del sistema

### 2.2 Actores Secundarios
- **Instructor:** (Futuro) Usuario que crea contenido
- **Proveedor:** (Futuro) Usuario que gestiona información de proveedores

## 3. Casos de Uso de Autenticación

### CU-001: Registro de Nuevo Usuario

**Actor:** Estudiante (no autenticado)

**Precondiciones:**
- El usuario no tiene cuenta en el sistema

**Flujo Principal:**
1. El usuario accede a la página de registro
2. El sistema muestra el formulario de registro
3. El usuario ingresa:
   - Email
   - Contraseña
   - Confirmación de contraseña
   - Nombre completo
   - Teléfono (opcional)
   - País
4. El usuario hace clic en "Registrarse"
5. El sistema valida los datos:
   - Email único
   - Contraseña cumple requisitos
   - Todos los campos obligatorios completos
6. El sistema crea la cuenta
7. El sistema envía email de verificación
8. El sistema muestra mensaje de confirmación
9. El usuario recibe email con enlace de verificación
10. El usuario hace clic en el enlace
11. El sistema marca el email como verificado
12. El sistema redirige al usuario al login

**Flujos Alternativos:**
- 5a. Email ya existe:
  - El sistema muestra error "Este email ya está registrado"
  - El usuario puede ir a login o recuperar contraseña
- 5b. Contraseña no cumple requisitos:
  - El sistema muestra los requisitos
  - El usuario corrige la contraseña
- 5c. Campos inválidos:
  - El sistema muestra errores específicos
  - El usuario corrige los campos

**Postcondiciones:**
- El usuario tiene una cuenta creada
- El email está verificado
- El usuario puede iniciar sesión

---

### CU-002: Inicio de Sesión

**Actor:** Estudiante/Administrador

**Precondiciones:**
- El usuario tiene una cuenta registrada

**Flujo Principal:**
1. El usuario accede a la página de login
2. El usuario ingresa email y contraseña
3. El usuario hace clic en "Iniciar Sesión"
4. El sistema valida las credenciales
5. El sistema genera tokens de autenticación
6. El sistema registra el último login
7. El sistema redirige al usuario al dashboard

**Flujos Alternativos:**
- 4a. Credenciales inválidas:
  - El sistema muestra error "Email o contraseña incorrectos"
  - El usuario puede intentar nuevamente o recuperar contraseña
- 4b. Cuenta no verificada:
  - El sistema muestra mensaje para verificar email
  - El sistema ofrece reenviar email de verificación
- 4c. Cuenta bloqueada:
  - El sistema muestra mensaje de cuenta bloqueada
  - El sistema indica contacto con soporte

**Postcondiciones:**
- El usuario está autenticado
- El usuario tiene acceso a sus cursos y perfil

---

### CU-003: Recuperación de Contraseña

**Actor:** Estudiante/Administrador

**Precondiciones:**
- El usuario tiene una cuenta registrada

**Flujo Principal:**
1. El usuario accede a "Olvidé mi contraseña"
2. El usuario ingresa su email
3. El usuario hace clic en "Enviar"
4. El sistema valida que el email existe
5. El sistema genera token de recuperación
6. El sistema envía email con enlace de recuperación
7. El usuario recibe el email
8. El usuario hace clic en el enlace
9. El sistema muestra formulario de nueva contraseña
10. El usuario ingresa nueva contraseña y confirmación
11. El usuario hace clic en "Cambiar Contraseña"
12. El sistema valida la nueva contraseña
13. El sistema actualiza la contraseña
14. El sistema invalida el token de recuperación
15. El sistema redirige al login

**Flujos Alternativos:**
- 4a. Email no existe:
  - El sistema muestra mensaje genérico (por seguridad)
- 9a. Token expirado:
  - El sistema muestra error
  - El usuario debe solicitar nuevo enlace

**Postcondiciones:**
- La contraseña ha sido actualizada
- El usuario puede iniciar sesión con la nueva contraseña

---

## 4. Casos de Uso de Cursos

### CU-004: Explorar Catálogo de Cursos

**Actor:** Estudiante (autenticado o no)

**Precondiciones:**
- Ninguna

**Flujo Principal:**
1. El usuario accede a la página de cursos
2. El sistema muestra lista de cursos disponibles
3. El usuario puede:
   - Ver cursos destacados
   - Filtrar por categoría
   - Filtrar por nivel
   - Filtrar por precio
   - Buscar por nombre
   - Ordenar por precio, popularidad, fecha
4. El usuario hace clic en un curso
5. El sistema muestra detalles del curso

**Flujos Alternativos:**
- 3a. Usuario no autenticado:
  - El sistema muestra todos los cursos
  - El sistema muestra botón de login para comprar

**Postcondiciones:**
- El usuario puede ver información de cursos
- El usuario puede proceder a comprar

---

### CU-005: Ver Detalles de Curso

**Actor:** Estudiante

**Precondiciones:**
- El curso existe y está activo

**Flujo Principal:**
1. El usuario selecciona un curso del catálogo
2. El sistema muestra:
   - Título y descripción
   - Precio (USD y RD$)
   - Lista de productos incluidos
   - Duración estimada
   - Nivel de dificultad
   - Qué incluye (certificado, proveedores, soporte)
   - Imágenes/videos de preview
   - Testimonios (si hay)
3. El usuario puede:
   - Ver preview del contenido
   - Ver lista de productos
   - Ver información de proveedores (si aplica)
   - Agregar al carrito
   - Comprar directamente

**Flujos Alternativos:**
- 3a. Usuario ya compró el curso:
  - El sistema muestra botón "Ir al Curso"
   - El sistema muestra progreso
- 3b. Curso inactivo:
  - El sistema muestra mensaje "Curso no disponible"

**Postcondiciones:**
- El usuario tiene información completa del curso
- El usuario puede decidir comprar

---

### CU-006: Comprar Curso

**Actor:** Estudiante

**Precondiciones:**
- El usuario está autenticado
- El usuario tiene email verificado
- El curso está activo y disponible

**Flujo Principal:**
1. El usuario selecciona "Comprar" en un curso
2. El sistema agrega el curso al carrito
3. El usuario puede agregar más cursos o proceder a checkout
4. El usuario hace clic en "Finalizar Compra"
5. El sistema muestra resumen de compra:
   - Cursos seleccionados
   - Precio de cada curso
   - Total
   - Campo para código de descuento (opcional)
6. El usuario ingresa código de descuento (opcional)
7. El sistema aplica descuento si es válido
8. El usuario selecciona método de pago
9. El usuario confirma la compra
10. El sistema crea la orden
11. El sistema procesa el pago según método seleccionado
12. Si el pago es exitoso:
    - El sistema marca la orden como pagada
    - El sistema otorga acceso a los cursos
    - El sistema envía email de confirmación
    - El sistema muestra confirmación en pantalla
13. El usuario es redirigido a "Mis Cursos"

**Flujos Alternativos:**
- 6a. Código de descuento inválido:
  - El sistema muestra error
  - El usuario puede corregir o continuar sin descuento
- 11a. Pago con tarjeta:
  - El sistema redirige a pasarela de pago
  - El usuario completa pago
  - El sistema recibe confirmación
- 11b. Pago manual (transferencia):
  - El sistema muestra datos bancarios
  - El sistema genera número de referencia
  - El usuario sube comprobante
  - El sistema marca orden como pendiente
  - Admin aprueba manualmente
  - El sistema otorga acceso cuando se aprueba
- 11c. Pago fallido:
  - El sistema muestra error
  - El usuario puede intentar otro método
  - La orden queda como pendiente

**Postcondiciones:**
- Se crea una orden
- Si el pago es exitoso, el usuario tiene acceso a los cursos
- Se envía confirmación por email

---

### CU-007: Acceder a Contenido del Curso

**Actor:** Estudiante

**Precondiciones:**
- El usuario ha comprado el curso
- El curso está activo
- El pago fue aprobado

**Flujo Principal:**
1. El usuario accede a "Mis Cursos"
2. El sistema muestra lista de cursos comprados
3. El usuario selecciona un curso
4. El sistema muestra:
   - Información del curso
   - Progreso actual
   - Lista de contenido disponible
   - Certificado (si completó)
5. El usuario selecciona un contenido (video, PDF, etc.)
6. El sistema verifica acceso
7. El sistema muestra/reproduce el contenido
8. El usuario visualiza el contenido
9. El sistema registra progreso automáticamente
10. El sistema actualiza porcentaje de completitud

**Flujos Alternativos:**
- 6a. Contenido bloqueado:
  - El sistema muestra mensaje
  - El usuario debe completar contenido previo (si es secuencial)
- 9a. Usuario completa contenido:
  - El sistema marca como completado
  - El sistema actualiza progreso del curso
  - Si el curso se completa, se genera certificado

**Postcondiciones:**
- El usuario puede acceder al contenido
- El progreso se actualiza
- Si completa, se genera certificado

---

### CU-008: Descargar Materiales del Curso

**Actor:** Estudiante

**Precondiciones:**
- El usuario tiene acceso al curso
- El material está disponible para descarga

**Flujo Principal:**
1. El usuario accede al contenido del curso
2. El usuario encuentra material descargable (PDF, etc.)
3. El usuario hace clic en "Descargar"
4. El sistema verifica acceso
5. El sistema genera URL firmada (si es necesario)
6. El sistema inicia descarga
7. El sistema registra la descarga
8. El archivo se descarga al dispositivo del usuario

**Flujos Alternativos:**
- 4a. Límite de descargas alcanzado:
  - El sistema muestra mensaje
  - El usuario puede contactar soporte
- 5a. Archivo no disponible:
  - El sistema muestra error
  - El usuario puede contactar soporte

**Postcondiciones:**
- El usuario tiene el archivo descargado
- Se registra la descarga

---

### CU-009: Obtener Certificado

**Actor:** Estudiante

**Precondiciones:**
- El usuario completó el curso (100% progreso)
- El curso incluye certificado

**Flujo Principal:**
1. El usuario completa el curso
2. El sistema detecta que el curso está completo
3. El sistema genera certificado automáticamente
4. El sistema envía notificación al usuario
5. El usuario accede a "Mis Certificados"
6. El sistema muestra lista de certificados
7. El usuario selecciona un certificado
8. El sistema muestra:
   - Certificado en PDF
   - Código de verificación
   - Opción de descargar
   - Opción de compartir
9. El usuario descarga el certificado
10. El usuario puede compartir en redes sociales

**Flujos Alternativos:**
- 2a. Certificado ya generado:
  - El sistema muestra certificado existente
- 4a. Error al generar:
  - El sistema registra error
  - Admin puede regenerar manualmente

**Postcondiciones:**
- El usuario tiene certificado descargable
- El certificado es verificable públicamente

---

## 5. Casos de Uso de Administración

### CU-010: Crear Nuevo Curso

**Actor:** Administrador

**Precondiciones:**
- El administrador está autenticado
- El administrador tiene permisos de administración

**Flujo Principal:**
1. El administrador accede al panel de administración
2. El administrador selecciona "Cursos" > "Nuevo Curso"
3. El sistema muestra formulario de creación
4. El administrador completa:
   - Título
   - Slug (generado automáticamente)
   - Descripción
   - Precio USD
   - Precio RD$ (opcional)
   - Categoría
   - Nivel
   - Duración
   - Qué incluye (checkboxes)
   - Imagen principal
   - Video preview (opcional)
5. El administrador agrega productos incluidos
6. El administrador sube contenido:
   - Videos
   - PDFs de fórmulas
   - Imágenes
7. El administrador organiza el orden del contenido
8. El administrador selecciona proveedores asociados (opcional)
9. El administrador guarda como borrador o publica
10. El sistema valida los datos
11. El sistema crea el curso
12. El sistema muestra confirmación

**Flujos Alternativos:**
- 4a. Slug duplicado:
  - El sistema sugiere alternativa
  - El administrador puede modificar
- 9a. Guardar como borrador:
  - El curso no es visible públicamente
  - El administrador puede editarlo después
- 10a. Validación falla:
  - El sistema muestra errores
  - El administrador corrige

**Postcondiciones:**
- El curso está creado
- Si está publicado, es visible en el catálogo

---

### CU-011: Gestionar Órdenes y Pagos

**Actor:** Administrador

**Precondiciones:**
- El administrador está autenticado

**Flujo Principal:**
1. El administrador accede a "Órdenes"
2. El sistema muestra lista de órdenes con filtros:
   - Estado (pendiente, pagada, cancelada)
   - Fecha
   - Usuario
   - Método de pago
3. El administrador selecciona una orden pendiente
4. El sistema muestra detalles:
   - Información del usuario
   - Cursos comprados
   - Monto total
   - Método de pago
   - Comprobante subido (si aplica)
5. El administrador verifica el pago
6. El administrador aprueba o rechaza el pago
7. Si aprueba:
   - El sistema marca orden como pagada
   - El sistema otorga acceso a cursos
   - El sistema envía notificación al usuario
8. Si rechaza:
   - El administrador ingresa motivo
   - El sistema notifica al usuario
   - El usuario puede subir nuevo comprobante

**Flujos Alternativos:**
- 5a. Comprobante no válido:
  - El administrador rechaza
  - El sistema solicita nuevo comprobante
- 6a. Reembolso necesario:
  - El administrador procesa reembolso
  - El sistema revoca acceso
  - El sistema marca orden como reembolsada

**Postcondiciones:**
- La orden tiene estado actualizado
- Si aprobada, el usuario tiene acceso

---

### CU-012: Ver Dashboard y Analytics

**Actor:** Administrador

**Precondiciones:**
- El administrador está autenticado

**Flujo Principal:**
1. El administrador accede al dashboard
2. El sistema muestra métricas principales:
   - Total de usuarios
   - Cursos vendidos (hoy, semana, mes)
   - Ingresos (hoy, semana, mes)
   - Cursos más populares
   - Usuarios activos
   - Órdenes pendientes
3. El sistema muestra gráficos:
   - Ventas por período
   - Cursos más vendidos
   - Métodos de pago más usados
   - Tasa de conversión
4. El administrador puede:
   - Filtrar por período
   - Exportar reportes
   - Ver detalles de métricas

**Flujos Alternativos:**
- 2a. Sin datos:
  - El sistema muestra mensaje
  - El sistema muestra datos de ejemplo o vacío

**Postcondiciones:**
- El administrador tiene visión general del negocio

---

### CU-013: Gestionar Usuarios

**Actor:** Administrador

**Precondiciones:**
- El administrador está autenticado

**Flujo Principal:**
1. El administrador accede a "Usuarios"
2. El sistema muestra lista de usuarios con búsqueda y filtros
3. El administrador puede:
   - Ver perfil completo
   - Ver cursos comprados
   - Ver certificados
   - Ver historial de órdenes
   - Editar información
   - Bloquear/desbloquear cuenta
   - Cambiar rol
   - Enviar mensaje
4. El administrador selecciona acción
5. El sistema ejecuta la acción
6. El sistema muestra confirmación

**Flujos Alternativos:**
- 3a. Bloquear usuario:
  - El sistema revoca sesiones activas
  - El usuario no puede iniciar sesión
- 3b. Cambiar rol:
  - El sistema valida permisos
  - El sistema actualiza permisos

**Postcondiciones:**
- Los cambios se aplican
- El usuario es notificado si aplica

---

## 6. Casos de Uso de Soporte

### CU-014: Crear Ticket de Soporte

**Actor:** Estudiante

**Precondiciones:**
- El usuario está autenticado

**Flujo Principal:**
1. El usuario accede a "Soporte"
2. El usuario selecciona "Nuevo Ticket"
3. El sistema muestra formulario
4. El usuario completa:
   - Asunto
   - Categoría (técnico, contenido, pago, otro)
   - Mensaje
   - Archivos adjuntos (opcional)
5. El usuario envía el ticket
6. El sistema crea el ticket
7. El sistema genera número de ticket
8. El sistema envía confirmación
9. El sistema notifica a administradores
10. El usuario puede ver estado del ticket

**Flujos Alternativos:**
- 4a. FAQ disponible:
  - El sistema sugiere artículos relacionados
  - El usuario puede resolver sin crear ticket

**Postcondiciones:**
- Se crea un ticket
- El usuario puede seguirlo
- Los administradores son notificados

---

### CU-015: Responder Ticket de Soporte

**Actor:** Administrador

**Precondiciones:**
- Existe un ticket abierto
- El administrador está autenticado

**Flujo Principal:**
1. El administrador accede a "Soporte" > "Tickets"
2. El sistema muestra lista de tickets
3. El administrador selecciona un ticket
4. El sistema muestra:
   - Información del usuario
   - Historial de mensajes
   - Estado actual
5. El administrador lee el mensaje
6. El administrador responde:
   - Escribe respuesta
   - Adjunta archivos si necesario
   - Marca como resuelto (si aplica)
7. El administrador envía respuesta
8. El sistema guarda la respuesta
9. El sistema notifica al usuario
10. El sistema actualiza estado del ticket

**Flujos Alternativos:**
- 6a. Marcar como resuelto:
  - El ticket cambia a "resuelto"
  - El usuario puede reabrir si es necesario

**Postcondiciones:**
- El ticket tiene nueva respuesta
- El usuario es notificado
- El estado se actualiza

---

## 7. Casos de Uso de Proveedores

### CU-016: Ver Directorio de Proveedores

**Actor:** Estudiante

**Precondiciones:**
- El usuario tiene acceso a un curso que incluye proveedores

**Flujo Principal:**
1. El usuario accede a un curso comprado
2. El usuario selecciona "Proveedores"
3. El sistema muestra lista de proveedores asociados al curso
4. El usuario puede:
   - Ver información de cada proveedor
   - Filtrar por categoría
   - Buscar por nombre
5. El usuario selecciona un proveedor
6. El sistema muestra:
   - Nombre y descripción
   - Productos que ofrece
   - Información de contacto
   - Ubicación
   - Calificación (si hay)
7. El usuario puede contactar vía WhatsApp o email

**Postcondiciones:**
- El usuario tiene información de proveedores
- El usuario puede contactarlos

---

## 8. Casos de Uso del Sistema

### CU-017: Enviar Notificaciones

**Actor:** Sistema

**Precondiciones:**
- Evento que requiere notificación ocurre

**Flujo Principal:**
1. El sistema detecta evento (compra, certificado, etc.)
2. El sistema determina tipo de notificación
3. El sistema crea registro de notificación
4. El sistema envía según tipo:
   - Email: Envía email transaccional
   - Push: Envía notificación push
   - In-app: Crea notificación en app
5. El sistema marca como enviada
6. El sistema registra resultado

**Flujos Alternativos:**
- 4a. Error al enviar:
  - El sistema registra error
  - El sistema reintenta (hasta 3 veces)
  - El sistema notifica a admin si falla

**Postcondiciones:**
- La notificación se envía
- Se registra en historial

---

### CU-018: Generar Certificado Automáticamente

**Actor:** Sistema

**Precondiciones:**
- Usuario completa curso al 100%
- Curso incluye certificado

**Flujo Principal:**
1. El sistema detecta que curso está completo
2. El sistema verifica que incluye certificado
3. El sistema genera número único de certificado
4. El sistema genera código de verificación
5. El sistema crea PDF del certificado
6. El sistema sube PDF a almacenamiento
7. El sistema crea registro en base de datos
8. El sistema asocia certificado a user_course
9. El sistema notifica al usuario
10. El sistema actualiza progreso

**Flujos Alternativos:**
- 5a. Error al generar PDF:
  - El sistema registra error
  - El sistema notifica a admin
  - Admin puede regenerar manualmente

**Postcondiciones:**
- El certificado está generado
- El usuario puede descargarlo
- El certificado es verificable

---

## 9. Diagramas de Flujo

### 9.1 Flujo de Compra Completo

```
Usuario → Ver Catálogo → Seleccionar Curso → Agregar al Carrito
  ↓
Proceder a Checkout → Aplicar Descuento (opcional) → Seleccionar Pago
  ↓
Pago Online → Confirmación → Acceso Otorgado
  ↓
Pago Manual → Subir Comprobante → Admin Aprueba → Acceso Otorgado
```

### 9.2 Flujo de Aprendizaje

```
Usuario → Mis Cursos → Seleccionar Curso → Ver Contenido
  ↓
Ver Video/PDF → Marcar Completado → Actualizar Progreso
  ↓
Progreso 100% → Generar Certificado → Notificar Usuario
```

## 10. Priorización de Casos de Uso

### Fase 1 (MVP)
- CU-001, CU-002: Autenticación básica
- CU-004, CU-005: Explorar y ver cursos
- CU-006: Comprar curso
- CU-007: Acceder a contenido
- CU-010: Crear curso (admin básico)

### Fase 2
- CU-003: Recuperación de contraseña
- CU-008, CU-009: Descargas y certificados
- CU-011: Gestión de pagos
- CU-012: Dashboard
- CU-014, CU-015: Soporte

### Fase 3
- CU-013: Gestión avanzada de usuarios
- CU-016: Proveedores
- CU-017, CU-018: Automatizaciones
- Features adicionales

