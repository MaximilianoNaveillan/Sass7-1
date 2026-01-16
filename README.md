# 🧪 Demo práctica: Estructura básica con SASS + Patrón 7-1

## 🎯 ¿En qué consistirá la Demo?

En esta demo vamos a construir desde cero una estructura base con SASS, aplicando buenas prácticas de organización y escalabilidad.

El objetivo principal es comprender cómo y por qué se organiza un proyecto con SASS, no solo que “funcione”.

Trabajaremos con:

- Patrón 7-1
- Variables
- Mixins
- Parciales
- Anidamiento
- Compilación automática con Live Sass Compiler

👉 No se entrega código base: todo se construye paso a paso.

---

## 🧠 Objetivos de aprendizaje

Al finalizar la demo, podrás:

- Comprender la arquitectura 7-1
- Crear y usar variables globales
- Implementar mixins reutilizables
- Modularizar estilos en parciales
- Anidar selectores correctamente
- Compilar SASS a CSS
- Reflexionar sobre mantenibilidad y escalabilidad

---

## 1️⃣ Crear la estructura de carpetas (Patrón 7-1)

Estructura inicial del proyecto:

```txt
project/
│
├── index.html
└── scss/
    ├── abstracts/
    ├── base/
    ├── components/
    ├── layout/
    ├── pages/
    ├── themes/
    ├── vendors/
    └── main.scss
```

## 📁 Explicación de la estructura (Patrón 7-1)

- **abstracts**: variables y mixins
- **base**: estilos base (reset, tipografía)
- **components**: componentes reutilizables
- **layout**: estructura general
- **pages**: estilos por página
- **themes**: temas visuales
- **vendors**: librerías externas
- **main.scss**: punto de entrada único

---

## 2️⃣ Definir variables globales

Archivo: `scss/abstracts/_variables.scss`

```scss
// ==========================
// COLORS
// ==========================
$color-primary: #2563eb;
$color-secondary: #64748b;
$color-bg: #f8fafc;
$color-text: #0f172a;
$color-white: #ffffff;

// ==========================
// TYPOGRAPHY
// ==========================
$font-base: 'Arial', sans-serif;
$font-size-base: 16px;
$font-size-title: 1.25rem;

// ==========================
// SPACING
// ==========================
$space-xs: 0.25rem;
$space-sm: 0.5rem;
$space-md: 1rem;
$space-lg: 2rem;

// ==========================
// BORDER RADIUS
// ==========================
$radius-sm: 4px;
$radius-md: 8px;
```

## 3️⃣ Crear un mixin para media queries

Archivo: `scss/abstracts/_mixins.scss`

```scss
// ==========================
// MEDIA QUERIES MIXIN
// ==========================
@mixin respond-to($breakpoint) {
  @if $breakpoint == mobile {
    @media (max-width: 480px) {
      @content;
    }
  } @else if $breakpoint == tablet {
    @media (max-width: 768px) {
      @content;
    }
  } @else if $breakpoint == desktop {
    @media (max-width: 1200px) {
      @content;
    }
  }
}
```

# 4️⃣ Crear un componente con anidamiento (Card)

Archivo: `scss/components/_card.scss`

```scss
@use '../abstracts/variables' as v;
@use '../abstracts/mixins' as m;

// ==========================
// CARD COMPONENT
// ==========================
.card {
  background-color: v.$color-white;
  border-radius: v.$radius-md;
  padding: v.$space-md;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
  font-family: v.$font-base;
  color: v.$color-text;

  &__title {
    font-size: v.$font-size-title;
    margin-bottom: v.$space-sm;
  }

  &__text {
    font-size: v.$font-size-base;
    color: v.$color-secondary;
  }

  // Responsive behavior
  @include m.respond-to(mobile) {
    padding: v.$space-sm;

    &__title {
      font-size: 1rem;
    }
  }
}
```

## 5️⃣ Importar parciales en `main.scss`

**Archivo:** `scss/main.scss`

```scss
// ==========================
// ABSTRACTS
// ==========================
@use 'abstracts/variables';
@use 'abstracts/mixins';

// ==========================
// BASE
// ==========================
// (vacío por ahora)

// ==========================
// COMPONENTS
// ==========================
@use 'components/card';
```

## 6️⃣ Compilar con Live Sass Compiler

### Pasos

1. Instalar la extensión **Live Sass Compiler** en Visual Studio Code.
2. Abrir el archivo `main.scss`.
3. Hacer clic en **Watch Sass** (en la barra inferior de VS Code).

### Resultado esperado

Se genera automáticamente la carpeta y archivo:

```txt
css/
└── main.css
```

📌 **Importante:**  
El navegador **solo recibe `main.css`**, pero este archivo contiene la **combinación de todos los parciales SASS** definidos en el proyecto.

---

## 7️⃣ Crear HTML para visualizar el resultado

**Archivo:** `index.html`

```html
<!DOCTYPE html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <title>Demo SASS 7-1</title>
    <link rel="stylesheet" href="css/main.css" />
  </head>
  <body>
    <div class="card">
      <h2 class="card__title">Título de la tarjeta</h2>
      <p class="card__text">Este es un ejemplo de componente construido con SASS y patrón 7-1.</p>
    </div>
  </body>
</html>
```

## 8️⃣ Mostrar el resultado en el navegador

### Observa

- 📱 El diseño se adapta a **mobile** gracias al mixin de media queries.
- 🧩 Los estilos están **separados por responsabilidad**.
- 📦 El navegador carga **un solo archivo CSS final**.
- ♻️ El componente es **reutilizable y escalable**.

---

## 9️⃣ Reflexión final (discusión en clase)

### Preguntas para el grupo

- 🤔 ¿Dónde cambiarías el **color principal** del proyecto?
- 📦 ¿Qué pasa si el proyecto crece a **50 componentes**?
- ⚖️ ¿Qué ventaja tiene esta estructura frente a un solo archivo CSS?
- 👥 ¿Cómo ayuda esta organización al trabajo en equipo?

---

## ✅ Conclusión

**SASS no es solo sintaxis.**  
Es **arquitectura**, **orden** y **mantenibilidad**.

Usar el patrón **7-1**, junto con **variables**, **mixins** y **componentes bien definidos**, permite que un proyecto crezca sin volverse caótico.
