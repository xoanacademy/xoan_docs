# Diseño UI/UX - Aplicación Emprende Con Xoán

## 1. Introducción

Este documento describe el diseño de interfaz de usuario (UI) y experiencia de usuario (UX) para la aplicación, incluyendo wireframes, guías de estilo y principios de diseño.

## 2. Principios de Diseño

### 2.1 Principios Fundamentales

1. **Simplicidad:** Interfaz limpia y fácil de entender
2. **Claridad:** Información clara y accesible
3. **Consistencia:** Diseño coherente en toda la aplicación
4. **Accesibilidad:** Diseño inclusivo para todos los usuarios
5. **Responsive:** Funciona perfectamente en todos los dispositivos
6. **Rendimiento:** Carga rápida y fluida

### 2.2 Objetivos de UX

- **Facilidad de uso:** Usuarios pueden completar tareas sin ayuda
- **Eficiencia:** Proceso de compra rápido y sencillo
- **Confianza:** Diseño profesional que inspira confianza
- **Engagement:** Contenido atractivo que mantiene interés
- **Satisfacción:** Experiencia positiva en cada interacción

## 3. Paleta de Colores

### 3.1 Colores Principales (Basados en el Logo de la Empresa)

**Nota Importante:** Esta paleta está basada en los colores identificados en el logo oficial de Emprende Con Xoán. Los valores hexadecimales proporcionados son aproximaciones basadas en la descripción visual del logo. 

**Recomendación:** Para obtener los colores exactos del logo:
1. Extraer los valores hexadecimales directamente del archivo del logo (PNG, SVG, AI)
2. Usar herramientas como Adobe Color, Coolors.co, o un selector de color
3. Verificar los colores con el diseñador o propietario de la marca
4. Ajustar estos valores según el logo oficial proporcionado

**Colores Identificados en el Logo:**
- Verde vibrante: Usado en la palabra "Emprende"
- Rosa/Magenta: Usado en "Xoán" y la línea curva decorativa
- Rojo: Usado en el lazo del diploma
- Negro: Usado en el birrete de graduación
- Blanco: Usado en contornos y la palabra "CON"
- Gris oscuro: Usado en sombras y profundidad

```
Primario (Brand - Colores del Logo):
- Verde Principal: #22C55E / #10B981 (Verde vibrante de "Emprende")
  - Verde Claro: #4ADE80 (Para hover y estados activos)
  - Verde Oscuro: #16A34A (Para estados hover/active)
  
- Rosa/Magenta Principal: #EC4899 / #F472B6 (Rosa/Magenta de "Xoán")
  - Rosa Claro: #F9A8D4 (Para fondos suaves)
  - Rosa Oscuro: #DB2777 (Para estados hover/active)

Secundario (Del Logo):
- Rojo: #EF4444 / #DC2626 (Rojo del lazo del diploma)
- Negro: #000000 / #1F2937 (Negro del birrete de graduación)
- Blanco: #FFFFFF (Blanco de contornos y "CON")
- Gris Oscuro: #374151 / #4B5563 (Gris de sombras)

Estados y Funcionalidad:
- Éxito: #22C55E (Usar verde de marca)
- Advertencia: #F59E0B (Naranja - mantener para contraste)
- Error: #EF4444 (Rojo de marca)
- Info: #3B82F6 (Azul - mantener para información)

Neutros:
- Fondo: #FFFFFF (Blanco)
- Fondo secundario: #F9FAFB (Gris muy claro)
- Fondo terciario: #F3F4F6 (Gris claro para secciones)
- Borde: #E5E7EB (Gris claro)
- Borde oscuro: #D1D5DB (Gris medio)
- Texto principal: #111827 (Gris oscuro - casi negro)
- Texto secundario: #6B7280 (Gris medio)
- Texto terciario: #9CA3AF (Gris claro)
```

### 3.2 Uso de Colores

**Colores Primarios de Marca:**
- **Verde (#22C55E):** 
  - Botones principales de acción (Comprar, Inscribirse)
  - Enlaces principales
  - Elementos destacados
  - Badges de éxito
  - Indicadores positivos
  
- **Rosa/Magenta (#EC4899):**
  - Acentos y elementos decorativos
  - Botones secundarios
  - Highlights y énfasis
  - Elementos de marca (logo, iconos)
  - Gradientes y fondos suaves

**Colores Secundarios:**
- **Rojo:** Errores, advertencias críticas, elementos de urgencia
- **Negro:** Textos principales, iconos, elementos de peso visual
- **Blanco:** Fondos, espacios negativos, contraste
- **Gris Oscuro:** Sombras, profundidad, elementos sutiles

**Combinaciones Recomendadas:**
- Verde + Blanco: Para CTAs principales y acciones positivas
- Rosa + Blanco: Para elementos de marca y acentos
- Verde + Rosa: Para gradientes y elementos especiales (usar con moderación)
- Negro + Blanco: Para textos y elementos de alto contraste

**Contraste:** Mínimo 4.5:1 para texto (WCAG AA)
- Verde sobre blanco: ✅ Cumple
- Rosa sobre blanco: ✅ Cumple
- Verde sobre negro: ✅ Cumple
- Rosa sobre negro: ✅ Cumple

### 3.3 Gradientes y Efectos Especiales

**Gradientes de Marca (Usar con moderación):**
```
Gradiente Principal (Verde a Rosa):
- From: #22C55E (Verde)
- To: #EC4899 (Rosa)
- Uso: Hero sections, CTAs especiales, elementos destacados

Gradiente Verde:
- From: #22C55E
- To: #16A34A
- Uso: Botones, cards destacados

Gradiente Rosa:
- From: #EC4899
- To: #DB2777
- Uso: Acentos, elementos decorativos
```

**Sombras con Color de Marca:**
```
Sombra Verde (para elementos con verde):
- box-shadow: 0 4px 6px rgba(34, 197, 94, 0.15)

Sombra Rosa (para elementos con rosa):
- box-shadow: 0 4px 6px rgba(236, 72, 153, 0.15)
```

### 3.4 Guía de Aplicación por Sección

**Header/Navegación:**
- Fondo: Blanco (#FFFFFF)
- Logo: Colores originales del logo
- Enlaces: Verde (#22C55E) o Negro (#111827)
- Hover: Rosa (#EC4899) o Verde claro (#4ADE80)

**Hero Section:**
- Fondo: Blanco o gradiente suave (verde claro a rosa claro)
- Título: Negro (#111827) o Verde (#22C55E)
- CTA Principal: Verde (#22C55E)
- CTA Secundario: Rosa (#EC4899)

**Cards de Cursos:**
- Borde: Gris claro (#E5E7EB)
- Hover: Sombra verde o rosa
- Precio: Verde (#22C55E) o Rosa (#EC4899)
- Badge "Nuevo": Rosa (#EC4899)
- Badge "Popular": Verde (#22C55E)

**Botones de Acción:**
- Comprar/Inscribirse: Verde (#22C55E)
- Ver Detalles: Rosa (#EC4899) o Verde claro
- Cancelar: Gris (#6B7280)
- Eliminar: Rojo (#EF4444)

**Estados de Progreso:**
- Completado: Verde (#22C55E)
- En progreso: Rosa (#EC4899)
- Pendiente: Gris (#9CA3AF)

## 4. Tipografía

### 4.1 Fuentes

**Principal:** Inter / Roboto / System Font Stack
- **Razón:** Legible, moderna, amplia compatibilidad
- **Alternativa:** Open Sans

**Títulos:** Montserrat / Poppins (opcional)
- **Uso:** Headings, títulos destacados

### 4.2 Escala Tipográfica

```
H1: 2.5rem (40px) - Títulos principales
H2: 2rem (32px) - Secciones
H3: 1.5rem (24px) - Subsections
H4: 1.25rem (20px) - Subtítulos
Body: 1rem (16px) - Texto normal
Small: 0.875rem (14px) - Texto secundario
Tiny: 0.75rem (12px) - Notas, labels
```

### 4.3 Pesos

- **Regular (400):** Texto normal
- **Medium (500):** Énfasis ligero
- **Semibold (600):** Subtítulos
- **Bold (700):** Títulos, énfasis fuerte

## 5. Espaciado y Layout

### 5.1 Sistema de Espaciado

```
Base: 4px
xs: 4px
sm: 8px
md: 16px
lg: 24px
xl: 32px
2xl: 48px
3xl: 64px
```

### 5.2 Grid System

- **Desktop:** 12 columnas
- **Tablet:** 8 columnas
- **Mobile:** 4 columnas
- **Gutter:** 24px (desktop), 16px (mobile)

### 5.3 Breakpoints

```
Mobile: < 640px
Tablet: 640px - 1024px
Desktop: > 1024px
Large Desktop: > 1280px
```

## 6. Componentes de UI

### 6.1 Botones

#### Botón Primario
```
Background: #22C55E (Verde de marca)
Text: #FFFFFF
Hover: #16A34A (Verde oscuro)
Active: #15803D
Padding: 12px 24px
Border-radius: 8px
Font-weight: 600
Shadow: 0 2px 4px rgba(34, 197, 94, 0.2)
```

#### Botón Secundario
```
Background: Transparent
Text: #EC4899 (Rosa de marca)
Border: 2px solid #EC4899
Hover: Background #EC4899, Text #FFFFFF
Active: #DB2777
```

#### Botón de Texto
```
Background: Transparent
Text: #22C55E (Verde de marca)
Hover: Background #F0FDF4 (Verde muy claro)
Active: #DCFCE7
```

#### Botón Alternativo (Rosa)
```
Background: #EC4899 (Rosa de marca)
Text: #FFFFFF
Hover: #DB2777 (Rosa oscuro)
Active: #BE185D
```

### 6.2 Formularios

#### Input
```
Border: 1px solid #E5E7EB
Border-radius: 8px
Padding: 12px 16px
Focus: Border #22C55E (Verde de marca), Shadow rgba(34, 197, 94, 0.1)
Error: Border #EF4444 (Rojo de marca)
Success: Border #22C55E
```

#### Label
```
Font-size: 14px
Font-weight: 500
Color: #374151
Margin-bottom: 8px
```

#### Checkbox/Radio
```
Size: 20px
Border-radius: 4px (checkbox) / 50% (radio)
Color: #22C55E (Verde de marca)
Checked Background: #22C55E
Hover: #4ADE80 (Verde claro)
```

### 6.3 Tarjetas (Cards)

```
Background: #FFFFFF
Border: 1px solid #E5E7EB
Border-radius: 12px
Padding: 24px
Shadow: 0 1px 3px rgba(0,0,0,0.1)
Hover: Shadow 0 4px 6px rgba(0,0,0,0.1)
```

### 6.4 Badges

```
Success: Background #D1FAE5, Text #065F46 (Verde de marca)
Warning: Background #FEF3C7, Text #92400E
Error: Background #FEE2E2, Text #991B1B (Rojo de marca)
Info: Background #DBEAFE, Text #1E40AF
Brand (Verde): Background #DCFCE7, Text #166534
Brand (Rosa): Background #FCE7F3, Text #9F1239
```

### 6.5 Alertas

```
Success: Border-left 4px #22C55E (Verde de marca), Background #D1FAE5
Warning: Border-left 4px #F59E0B, Background #FEF3C7
Error: Border-left 4px #EF4444 (Rojo de marca), Background #FEE2E2
Info: Border-left 4px #3B82F6, Background #DBEAFE
Brand Highlight: Border-left 4px #EC4899 (Rosa de marca), Background #FCE7F3
```

## 7. Wireframes Principales

### 7.1 Página de Inicio / Landing

```
┌─────────────────────────────────────────────────┐
│  Header: Logo | Nav | Login/Register            │
├─────────────────────────────────────────────────┤
│                                                 │
│  Hero Section:                                  │
│  ┌─────────────────────────────────────────┐   │
│  │  Título: "Aprende a Crear Productos     │   │
│  │          Capilares Profesionales"       │   │
│  │  Subtítulo: Descripción breve           │   │
│  │  CTA: "Explorar Cursos"                │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Cursos Destacados:                            │
│  ┌──────┐ ┌──────┐ ┌──────┐                   │
│  │Card 1│ │Card 2│ │Card 3│                   │
│  └──────┘ └──────┘ └──────┘                   │
│                                                 │
│  Beneficios:                                   │
│  ┌──────┐ ┌──────┐ ┌──────┐                   │
│  │Icon 1│ │Icon 2│ │Icon 3│                   │
│  └──────┘ └──────┘ └──────┘                   │
│                                                 │
│  Testimonios:                                  │
│  ┌─────────────────────────────────────────┐   │
│  │  "Testimonio de estudiante..."          │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Footer: Links | Social | Contact              │
└─────────────────────────────────────────────────┘
```

### 7.2 Catálogo de Cursos

```
┌─────────────────────────────────────────────────┐
│  Header                                         │
├─────────────────────────────────────────────────┤
│  Breadcrumb: Inicio > Cursos                    │
│                                                 │
│  Filtros: [Categoría ▼] [Nivel ▼] [Precio ▼] │
│  Búsqueda: [________________] 🔍                │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  ┌──────┐  Curso 1                     │   │
│  │  │ Img  │  Título                      │   │
│  │  │      │  Descripción breve           │   │
│  │  └──────┘  $100 USD | [Ver Detalles]  │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  ┌──────┐  Curso 2                     │   │
│  │  │ Img  │  ...                          │   │
│  │  └──────┘                               │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Paginación: [<] 1 2 3 [>]                    │
└─────────────────────────────────────────────────┘
```

### 7.3 Detalle de Curso

```
┌─────────────────────────────────────────────────┐
│  Header                                         │
├─────────────────────────────────────────────────┤
│  Breadcrumb: Inicio > Cursos > [Nombre Curso]   │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  [Imagen/Video Principal]               │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Título del Curso                               │
│  ⭐⭐⭐⭐⭐ (4.5) - 120 reseñas              │
│                                                 │
│  Precio: $100 USD | RD$5,500                    │
│  [Comprar Ahora] [Agregar al Carrito]          │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  Incluye:                               │   │
│  │  ✓ Certificado                         │   │
│  │  ✓ Lista de Proveedores               │   │
│  │  ✓ Soporte WhatsApp                    │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Descripción:                                   │
│  [Texto completo del curso...]                  │
│                                                 │
│  Productos Incluidos:                           │
│  • Producto 1                                  │
│  • Producto 2                                  │
│  • ...                                         │
│                                                 │
│  Contenido del Curso:                           │
│  1. Video: Introducción                        │
│  2. PDF: Fórmula Producto 1                    │
│  3. ...                                        │
│                                                 │
│  Testimonios:                                   │
│  ┌─────────────────────────────────────────┐   │
│  │  "Excelente curso..." - María G.       │   │
│  └─────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

### 7.4 Checkout / Proceso de Compra

```
┌─────────────────────────────────────────────────┐
│  Header                                         │
├─────────────────────────────────────────────────┤
│  Paso 1: Carrito > Paso 2: Pago > Paso 3: Conf │
│                                                 │
│  Resumen de Compra:                             │
│  ┌─────────────────────────────────────────┐   │
│  │  Curso 1                    $100 USD    │   │
│  │  Curso 2                    $50 USD    │   │
│  │  ────────────────────────────────────   │   │
│  │  Subtotal                  $150 USD     │   │
│  │  Descuento (-10%)         -$15 USD     │   │
│  │  ────────────────────────────────────   │   │
│  │  Total                    $135 USD     │   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  Código de Descuento:                          │
│  [_____________] [Aplicar]                      │
│                                                 │
│  Método de Pago:                               │
│  ○ Tarjeta de Crédito/Débito                  │
│  ○ PayPal                                      │
│  ○ Transferencia Bancaria                     │
│                                                 │
│  [Continuar con el Pago]                       │
└─────────────────────────────────────────────────┘
```

### 7.5 Mis Cursos

```
┌─────────────────────────────────────────────────┐
│  Header: Logo | Nav | [Usuario ▼]               │
├─────────────────────────────────────────────────┤
│  Dashboard > Mis Cursos                         │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  [Imagen]  Curso 1                      │   │
│  │           Progreso: ████████░░ 80%      │   │
│  │           Último acceso: Hace 2 días    │   │
│  │           [Continuar] [Ver Certificado]│   │
│  └─────────────────────────────────────────┘   │
│                                                 │
│  ┌─────────────────────────────────────────┐   │
│  │  [Imagen]  Curso 2                      │   │
│  │           Progreso: ██████████ 100%     │   │
│  │           ✓ Completado                 │   │
│  │           [Ver Certificado] [Descargar]│   │
│  └─────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

### 7.6 Visualización de Contenido

```
┌─────────────────────────────────────────────────┐
│  [← Volver al Curso]                            │
├─────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────────────┐  │
│  │              │  │  Título del Contenido  │  │
│  │              │  │                        │  │
│  │   Video      │  │  Descripción...        │  │
│  │   Player     │  │                        │  │
│  │              │  │  [Marcar Completado]   │  │
│  │              │  │                        │  │
│  └──────────────┘  │  Contenido Relacionado│  │
│                    │  • Siguiente: ...     │  │
│                    │  • Anterior: ...      │  │
│                    └──────────────────────┘  │
│                                                 │
│  Progreso del Curso: ████████░░ 80%            │
└─────────────────────────────────────────────────┘
```

### 7.7 Panel de Administración

```
┌─────────────────────────────────────────────────┐
│  Sidebar:                                       │
│  ┌──────────────┐                              │
│  │ Dashboard    │                              │
│  │ Cursos       │                              │
│  │ Órdenes      │                              │
│  │ Usuarios     │                              │
│  │ Proveedores  │                              │
│  │ Soporte      │                              │
│  │ Configuración│                              │
│  └──────────────┘                              │
│                                                 │
│  Main Content:                                  │
│  ┌─────────────────────────────────────────┐  │
│  │  Dashboard                                │  │
│  │  ┌────┐ ┌────┐ ┌────┐ ┌────┐           │  │
│  │  │ 150│ │ $5K│ │ 45 │ │ 12 │           │  │
│  │  │User│ │Rev │ │Ord │ │Pen │           │  │
│  │  └────┘ └────┘ └────┘ └────┘           │  │
│  │                                         │  │
│  │  [Gráfico de Ventas]                    │  │
│  └─────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

## 8. Navegación

### 8.1 Estructura de Navegación

```
Header (Siempre visible):
- Logo (link a home)
- Menú: Cursos | Sobre Nosotros | Contacto
- Acciones: Login | Registro | [Usuario] (si autenticado)

Footer:
- Links: Inicio | Cursos | Términos | Privacidad
- Redes Sociales
- Contacto
- Newsletter (opcional)

Mobile:
- Hamburger menu
- Bottom navigation (opcional)
```

### 8.2 Flujos de Navegación

**Usuario No Autenticado:**
```
Home → Cursos → Detalle Curso → Login → Registro → Checkout
```

**Usuario Autenticado:**
```
Home → Cursos → Detalle Curso → Checkout → Mis Cursos → Contenido
```

## 9. Estados de UI

### 9.1 Estados de Carga

- **Skeleton Screens:** Para contenido que carga
- **Spinners:** Para acciones cortas
- **Progress Bars:** Para descargas/upload

### 9.2 Estados Vacíos

- **Sin cursos:** Ilustración + mensaje + CTA
- **Sin compras:** Ilustración + "Explora nuestros cursos"
- **Sin contenido:** Mensaje claro

### 9.3 Estados de Error

- **Error 404:** Página no encontrada con ilustración
- **Error 500:** Error del servidor con opción de reportar
- **Error de red:** Mensaje + botón de reintentar

## 10. Responsive Design

### 10.1 Mobile First

- Diseño pensado primero para móvil
- Navegación adaptada (hamburger menu)
- Botones y touch targets mínimos 44x44px
- Texto legible sin zoom

### 10.2 Adaptaciones por Dispositivo

**Mobile (< 640px):**
- Menú hamburguesa
- Cards en columna única
- Botones de ancho completo
- Imágenes optimizadas

**Tablet (640px - 1024px):**
- Menú expandido
- Cards en 2 columnas
- Más espacio horizontal

**Desktop (> 1024px):**
- Menú completo visible
- Cards en 3-4 columnas
- Sidebar en admin panel

## 11. Accesibilidad

### 11.1 Principios WCAG 2.1 AA

- **Contraste:** Mínimo 4.5:1 para texto
- **Navegación por teclado:** Todas las funciones accesibles
- **Screen readers:** Labels y ARIA apropiados
- **Focus visible:** Indicadores claros
- **Alt text:** Todas las imágenes descriptivas

### 11.2 Mejoras de Accesibilidad

- Skip to content link
- Navegación por teclado
- Focus management
- ARIA labels donde sea necesario
- Texto alternativo descriptivo

## 12. Animaciones y Transiciones

### 12.1 Principios

- **Sutiles:** No distraen
- **Funcionales:** Ayudan a entender cambios
- **Rápidas:** Máximo 300ms para transiciones
- **Opcionales:** Respetar preferencias de usuario (prefers-reduced-motion)

### 12.2 Transiciones Comunes

- **Hover:** 150ms ease-in-out
- **Click:** 100ms ease-in-out
- **Page transitions:** 200ms ease-in-out
- **Modal:** 200ms ease-in-out

## 13. Iconografía

### 13.1 Librería de Iconos

- **Recomendación:** Heroicons / Feather Icons / Material Icons
- **Estilo:** Outline para iconos regulares, Solid para énfasis
- **Tamaño:** 20px, 24px, 32px según contexto

### 13.2 Uso de Iconos

- **Navegación:** Claros y reconocibles
- **Acciones:** Consistentes (edit, delete, etc.)
- **Estados:** Success, error, warning, info
- **Contenido:** Videos, PDFs, imágenes

## 14. Guía de Estilo de Contenido

### 14.1 Tono de Voz

- **Profesional pero amigable**
- **Claro y directo**
- **Motivador y positivo**
- **Respetuoso**

### 14.2 Ejemplos de Texto

**Botones:**
- "Comprar Ahora" (no "Adquirir")
- "Continuar" (no "Proceder")
- "Explorar Cursos" (no "Ver Catálogo")

**Mensajes:**
- "¡Bienvenido! Estamos emocionados de tenerte aquí"
- "Tu curso está listo. ¡Comienza a aprender!"
- "Felicidades, has completado el curso"

## 15. Prototipos Interactivos

### 15.1 Herramientas Recomendadas

- **Figma:** Diseño y prototipado
- **Adobe XD:** Alternativa
- **InVision:** Prototipado
- **Framer:** Prototipos avanzados

### 15.2 Flujos a Prototipar

1. Registro y login
2. Exploración de cursos
3. Proceso de compra completo
4. Acceso a contenido
5. Panel de administración básico

## 16. Testing de Usabilidad

### 16.1 Métricas a Medir

- **Tiempo de tarea:** ¿Cuánto tarda en completar compra?
- **Tasa de error:** ¿Cuántos errores cometen?
- **Satisfacción:** ¿Qué tan fácil fue?
- **Tareas completadas:** ¿Pudieron completar la tarea?

### 16.2 Pruebas Recomendadas

- **A/B Testing:** Diferentes diseños de checkout
- **User Testing:** 5-8 usuarios por iteración
- **Analytics:** Heatmaps, click tracking
- **Feedback:** Encuestas post-compra

## 17. Implementación

### 17.1 Componentes Reutilizables

- Button (variantes: primary, secondary, text)
- Input (text, email, password, textarea)
- Card (course, content, etc.)
- Modal
- Alert
- Badge
- Progress Bar
- Loading Spinner

### 17.2 Sistema de Diseño

- **Storybook:** Documentación de componentes
- **Design Tokens:** Variables de diseño
- **Guía de estilo:** Documentación para desarrolladores

## 18. Consideraciones Especiales

### 18.1 Múltiples Monedas

- Mostrar ambas monedas claramente
- Convertir automáticamente según ubicación
- Permitir cambio de moneda

### 18.2 Contenido Multimedia

- Player de video optimizado
- Preview de PDFs
- Galería de imágenes
- Descarga clara y visible

### 18.3 Proceso de Pago

- Múltiples métodos visibles
- Proceso paso a paso claro
- Confirmación visible
- Opción de pago manual clara

