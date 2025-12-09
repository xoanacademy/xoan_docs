# Requisitos Funcionales - Aplicación Emprende Con Xoán

## 1. Introducción

Este documento describe los requisitos funcionales detallados para la aplicación web/móvil de Emprende Con Xoán. Los requisitos están organizados por módulos y priorizados según la importancia para el negocio.

## 2. Módulo de Autenticación y Gestión de Usuarios

### 2.1 Registro de Usuarios
**RF-001: Registro de Nuevo Usuario**
- El sistema debe permitir el registro con:
  - Email (obligatorio, único)
  - Contraseña (mínimo 8 caracteres, al menos 1 mayúscula, 1 número)
  - Nombre completo
  - Teléfono (opcional, para WhatsApp)
  - País (por defecto: República Dominicana)
- Validación de email único
- Verificación de email mediante enlace
- Opción de registro con Google/Facebook (futuro)

**RF-002: Inicio de Sesión**
- Login con email y contraseña
- Opción "Recordar sesión"
- Recuperación de contraseña vía email
- Límite de intentos fallidos (5 intentos, bloqueo temporal de 15 min)

**RF-003: Perfil de Usuario**
- Edición de información personal
- Cambio de contraseña
- Foto de perfil
- Historial de cursos comprados
- Certificados obtenidos
- Configuración de notificaciones

### 2.4 Roles y Permisos
**RF-004: Tipos de Usuario**
- **Estudiante:** Acceso a cursos comprados, descarga de materiales
- **Administrador:** Gestión completa del sistema
- **Instructor:** Creación y edición de contenido (futuro)
- **Proveedor:** Gestión de información de proveedores (futuro)

## 3. Módulo de Catálogo de Cursos

### 3.1 Visualización de Cursos
**RF-005: Listado de Cursos**
- Mostrar todos los cursos disponibles
- Filtros por:
  - Categoría (Básico, Avanzado, Especializado)
  - Precio
  - Duración
  - Nivel de dificultad
- Búsqueda por nombre o palabras clave
- Ordenamiento (precio, popularidad, fecha)

**RF-006: Detalle de Curso**
- Información completa del curso:
  - Título y descripción
  - Precio (mostrar en USD y RD$)
  - Contenido del curso (lista de productos/fórmulas)
  - Duración estimada
  - Nivel requerido
  - Certificado incluido (sí/no)
  - Lista de proveedores incluida (sí/no)
  - Soporte WhatsApp incluido (sí/no)
- Galería de imágenes/videos
- Testimonios de estudiantes
- Botón de compra

**RF-007: Cursos Destacados**
- Mostrar cursos en oferta
- Cursos más populares
- Nuevos cursos
- Recomendaciones basadas en historial

### 3.2 Gestión de Cursos (Admin)
**RF-008: Creación de Curso**
- Formulario completo:
  - Título, descripción, precio
  - Categoría y nivel
  - Imágenes/videos
  - Lista de productos incluidos
  - Archivos digitales (PDFs, videos)
  - Configuración de certificado
  - Estado (activo/inactivo/borrador)

**RF-009: Edición de Curso**
- Modificar cualquier campo del curso
- Historial de cambios
- Versiones del curso

**RF-010: Eliminación de Curso**
- Eliminación lógica (no física)
- Notificación a estudiantes inscritos
- Opción de reembolso

## 4. Módulo de Compras y Pagos

### 4.1 Proceso de Compra
**RF-011: Carrito de Compras**
- Agregar múltiples cursos al carrito
- Ver resumen antes de comprar
- Aplicar códigos de descuento
- Calcular total en múltiples monedas
- Eliminar items del carrito

**RF-012: Checkout**
- Revisar información de compra
- Seleccionar método de pago
- Ingresar información de facturación (opcional)
- Confirmar compra
- Generar orden de compra

### 4.2 Métodos de Pago
**RF-013: Pagos Online**
- Tarjeta de crédito/débito (Stripe, PayPal)
- Transferencia bancaria (mostrar datos)
- Pago móvil (Airtime, Orange Money - si aplica)
- PayPal
- Criptomonedas (futuro)

**RF-014: Pagos Manuales**
- Opción de pago en efectivo
- Código de referencia para pago
- Subir comprobante de pago
- Aprobación manual por administrador
- Notificación al usuario cuando se apruebe

**RF-015: Gestión de Pagos (Admin)**
- Ver todas las transacciones
- Filtrar por estado (pendiente, aprobado, rechazado)
- Aprobar/rechazar pagos manuales
- Reembolsos
- Exportar reportes

### 4.3 Órdenes
**RF-016: Historial de Órdenes**
- Usuario puede ver todas sus compras
- Estado de cada orden
- Descargar factura/comprobante
- Reenviar materiales si se pierden

**RF-017: Gestión de Órdenes (Admin)**
- Ver todas las órdenes
- Cambiar estado de orden
- Enviar materiales manualmente si es necesario
- Cancelar orden con reembolso

## 5. Módulo de Contenido y Aprendizaje

### 5.1 Acceso a Contenido
**RF-018: Biblioteca de Cursos**
- Lista de cursos comprados por el usuario
- Progreso de cada curso
- Acceso directo a materiales
- Marcar como completado

**RF-019: Visualización de Contenido**
- Ver videos en reproductor integrado
- Descargar PDFs de fórmulas
- Ver imágenes en galería
- Navegación entre lecciones/contenidos
- Marcar como visto

**RF-020: Descarga de Materiales**
- Descargar fórmulas en PDF
- Descargar videos (si está permitido)
- Descargar lista de proveedores
- Límite de descargas (configurable)
- Formato de archivos (PDF, DOCX, etc.)

### 5.2 Progreso de Aprendizaje
**RF-021: Seguimiento de Progreso**
- Porcentaje de completitud por curso
- Tiempo invertido
- Última actividad
- Certificado disponible cuando se complete

**RF-022: Certificados**
- Generación automática al completar curso
- Descarga en PDF
- Compartir en redes sociales
- Verificación de autenticidad (código único)

### 5.3 Gestión de Contenido (Admin)
**RF-023: Subida de Archivos**
- Videos (formatos: MP4, AVI, MOV)
- PDFs (fórmulas, guías)
- Imágenes (JPG, PNG)
- Límite de tamaño por archivo
- Organización por carpetas/categorías

**RF-024: Editor de Contenido**
- Editor WYSIWYG para descripciones
- Organización de lecciones
- Orden de contenido
- Preview antes de publicar

## 6. Módulo de Proveedores

### 6.1 Directorio de Proveedores
**RF-025: Lista de Proveedores**
- Ver todos los proveedores disponibles
- Búsqueda por nombre, producto, ubicación
- Filtros por categoría de producto
- Información de contacto
- Calificación (si aplica)

**RF-026: Detalle de Proveedor**
- Nombre y descripción
- Productos que ofrece
- Información de contacto (teléfono, email, WhatsApp)
- Ubicación/dirección
- Horarios de atención
- Precios de referencia (si disponibles)

### 6.2 Gestión de Proveedores (Admin)
**RF-027: CRUD de Proveedores**
- Crear, editar, eliminar proveedores
- Categorizar proveedores
- Asignar a cursos específicos
- Verificar información
- Activar/desactivar proveedores

## 7. Módulo de Soporte y Comunicación

### 7.1 WhatsApp Integration
**RF-028: Integración con WhatsApp**
- Botón de contacto directo vía WhatsApp
- Mensaje pre-configurado con información del curso
- Enlace directo desde la aplicación
- Historial de conversaciones (si se integra API)

**RF-029: Chat Interno (Futuro)**
- Sistema de mensajería dentro de la app
- Notificaciones de nuevos mensajes
- Respuestas automáticas para preguntas frecuentes

### 7.2 Soporte Técnico
**RF-030: Sistema de Tickets**
- Crear ticket de soporte
- Categorías (técnico, contenido, pago)
- Adjuntar archivos
- Seguimiento de estado
- Respuestas del administrador

**RF-031: FAQ**
- Preguntas frecuentes
- Búsqueda en FAQ
- Categorías de preguntas
- Actualización por administrador

## 8. Módulo de Notificaciones

### 8.1 Notificaciones del Sistema
**RF-032: Notificaciones por Email**
- Confirmación de registro
- Confirmación de compra
- Envío de materiales
- Certificado disponible
- Recordatorios de cursos sin completar
- Ofertas y promociones

**RF-033: Notificaciones Push (Móvil)**
- Nuevos cursos disponibles
- Ofertas especiales
- Recordatorios
- Mensajes de soporte
- Actualizaciones de contenido

**RF-034: Notificaciones In-App**
- Centro de notificaciones
- Marcar como leídas
- Eliminar notificaciones
- Configuración de preferencias

## 9. Módulo de Administración

### 9.1 Dashboard
**RF-035: Panel Principal**
- Resumen de métricas:
  - Total de usuarios
  - Cursos vendidos (hoy, semana, mes)
  - Ingresos (hoy, semana, mes)
  - Cursos más populares
  - Usuarios activos
- Gráficos de tendencias
- Actividad reciente

### 9.2 Gestión de Usuarios
**RF-036: Administración de Usuarios**
- Lista de todos los usuarios
- Búsqueda y filtros
- Ver perfil completo
- Editar información
- Bloquear/desbloquear usuarios
- Ver historial de compras
- Enviar mensajes masivos

### 9.3 Reportes y Analytics
**RF-037: Reportes de Ventas**
- Ventas por período
- Ventas por curso
- Métodos de pago más usados
- Tasa de conversión
- Exportar a Excel/PDF

**RF-038: Analytics de Contenido**
- Cursos más vistos
- Tiempo promedio de visualización
- Tasa de completitud
- Contenido más descargado

**RF-039: Reportes de Usuarios**
- Nuevos registros
- Usuarios activos
- Retención
- Cursos más populares entre usuarios

### 9.4 Configuración del Sistema
**RF-040: Configuración General**
- Información de la empresa
- Configuración de pagos
- Configuración de emails
- Monedas aceptadas
- Impuestos y comisiones
- Términos y condiciones
- Política de privacidad

## 10. Módulo de Marketing y Promociones

### 10.1 Códigos de Descuento
**RF-041: Gestión de Descuentos**
- Crear códigos de descuento
- Porcentaje o monto fijo
- Fecha de validez
- Límite de usos
- Aplicable a cursos específicos o todos
- Estado (activo/inactivo)

**RF-042: Aplicación de Descuentos**
- Usuario ingresa código en checkout
- Validación automática
- Aplicación al total
- Mostrar ahorro

### 10.2 Promociones
**RF-043: Ofertas Especiales**
- Crear ofertas con fecha límite
- Descuentos automáticos
- Banner de promoción
- Notificaciones a usuarios

### 10.3 Programa de Referidos (Futuro)
**RF-044: Sistema de Referidos**
- Código único por usuario
- Comisión por referido
- Seguimiento de referidos
- Pago de comisiones

## 11. Módulo de Comunidad (Futuro)

### 11.1 Foros de Discusión
**RF-045: Comunidad de Estudiantes**
- Foros por curso
- Preguntas y respuestas
- Búsqueda en foros
- Moderación

### 11.2 Testimonios y Reseñas
**RF-046: Sistema de Reseñas**
- Calificación de cursos (1-5 estrellas)
- Comentarios escritos
- Fotos de resultados
- Moderación de reseñas
- Mostrar en página de curso

## 12. Requisitos No Funcionales

### 12.1 Rendimiento
- Tiempo de carga de páginas < 3 segundos
- Soporte para 1000+ usuarios concurrentes
- Optimización de imágenes y videos
- CDN para contenido estático

### 12.2 Seguridad
- HTTPS obligatorio
- Encriptación de datos sensibles
- Protección contra SQL injection
- Protección CSRF
- Autenticación de dos factores (opcional)
- Backup automático diario

### 12.3 Usabilidad
- Interfaz responsive (móvil, tablet, desktop)
- Navegación intuitiva
- Accesibilidad WCAG 2.1 nivel AA
- Soporte multi-idioma (español inicial)

### 12.4 Compatibilidad
- Navegadores: Chrome, Firefox, Safari, Edge (últimas 2 versiones)
- Móviles: iOS 12+, Android 8+
- Resolución mínima: 320px

## 13. Priorización de Requisitos

### Fase 1 (MVP - Mínimo Producto Viable)
- RF-001 a RF-004: Autenticación básica
- RF-005 a RF-007: Catálogo de cursos
- RF-011, RF-012: Proceso de compra básico
- RF-013, RF-014: Pagos (al menos 2 métodos)
- RF-018 a RF-020: Acceso a contenido
- RF-021, RF-022: Certificados
- RF-035: Dashboard básico
- RF-040: Configuración mínima

### Fase 2 (Funcionalidades Esenciales)
- RF-008 a RF-010: Gestión completa de cursos
- RF-015 a RF-017: Gestión de pagos y órdenes
- RF-023, RF-024: Gestión de contenido
- RF-025 a RF-027: Módulo de proveedores
- RF-028: Integración WhatsApp
- RF-032, RF-033: Notificaciones
- RF-036 a RF-039: Reportes

### Fase 3 (Mejoras y Optimización)
- RF-030, RF-031: Soporte técnico avanzado
- RF-041 a RF-043: Marketing y promociones
- RF-044: Programa de referidos
- RF-045, RF-046: Comunidad

## 14. Casos de Uso Principales

### CU-001: Usuario compra un curso
1. Usuario navega catálogo
2. Selecciona curso
3. Agrega al carrito
4. Procede a checkout
5. Selecciona método de pago
6. Completa pago
7. Recibe confirmación
8. Accede a contenido

### CU-002: Administrador crea nuevo curso
1. Admin accede al panel
2. Crea nuevo curso
3. Sube contenido (videos, PDFs)
4. Configura precio y detalles
5. Publica curso
6. Notifica a usuarios (opcional)

### CU-003: Usuario descarga certificado
1. Usuario completa curso
2. Sistema genera certificado
3. Usuario descarga PDF
4. Comparte en redes sociales (opcional)

### CU-004: Usuario contacta soporte
1. Usuario tiene problema
2. Crea ticket o usa WhatsApp
3. Recibe respuesta
4. Problema resuelto

## 15. Glosario

- **Curso:** Producto educativo que incluye contenido, fórmulas y materiales
- **Fórmula:** Receta detallada para elaborar un producto capilar
- **Proveedor:** Empresa o persona que vende materias primas
- **Certificado:** Documento PDF que acredita la finalización de un curso
- **Orden:** Transacción de compra de uno o más cursos
- **Estudiante:** Usuario que ha comprado al menos un curso
- **Admin:** Usuario con permisos de administración del sistema

