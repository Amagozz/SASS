# INSTRUCCIONES
## 01) INTRODUCCIÓN
### ¿Qué es Sass?
Sass (Syntactically Awesome Stylesheets) es una extensión de CSS que añade funcionalidades poderosas y elegantes al lenguaje. Fue creado para facilitar la escritura y el mantenimiento de hojas de estilo, permitiendo el uso de variables, anidamiento, mixins, herencia y otras funcionalidades que no están presentes en CSS puro.

### Historia
- **2006**: Creado por Hampton Catlin e inicialmente implementado por Natalie Weizenbaum, Sass comenzó como un proyecto en Ruby.
- **2010**: Se introdujo SCSS (Sassy CSS) como una nueva sintaxis más cercana a CSS, facilitando la transición a los nuevos usuarios.
- **2012**: Se desarrolló LibSass como una implementación en C, proporcionando una alternativa más rápida que podría integrarse con más herramientas.
- **2019**: Dart Sass se convirtió en la implementación oficial recomendada, trayendo mejoras significativas en rendimiento y compatibilidad.

### Características Principales
#### 1. **Variables**
Permiten almacenar valores que pueden ser reutilizados a lo largo de la hoja de estilo.

```scss
$primary-color: #3498db;

body {
  color: $primary-color;
}
```

#### 2. **Anidamiento**
Permite escribir selectores de una forma más clara y jerárquica.

```scss
nav {
  ul {
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    text-decoration: none;
  }
}
```

#### 3. **Partials e Importaciones**
Permiten dividir el CSS en múltiples archivos más pequeños que pueden ser importados a un archivo principal.

```scss
// _reset.scss
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

// style.scss
@import 'reset';

body {
  font-family: Helvetica, sans-serif;
}
```

#### 4. **Mixins**
Permiten definir estilos reutilizables que pueden ser incluidos en otros selectores.

```scss
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

button {
  @include border-radius(10px);
}
```

#### 5. **Herencia**
Permite que un selector herede los estilos de otro, evitando la duplicación de código.

```scss
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}
```

#### 6. **Funciones**
Permiten crear funciones personalizadas que devuelven valores basados en parámetros.

```scss
@function calculate-em($pixels, $base-font-size: 16px) {
  @return $pixels / $base-font-size * 1em;
}

.container {
  font-size: calculate-em(24px);
}
```

### ¿Cómo Configurar y Usar?
1. **Instalar Node.js y npm**: [nodejs.org](https://nodejs.org/)
2. **Instalar Sass**:

   ```sh
   npm install -g sass
   ```

3. **Compilar Archivos Sass**:

   ```sh
   sass input.scss output.css
   ```

4. **Automatizar la Compilación** (opcional):

   ```sh
   sass --watch input.scss:output.css
   ```

### Conclusión
Sass es una herramienta poderosa que amplía las capacidades de CSS, haciendo que el desarrollo de estilos sea más eficiente, organizado y sostenible. Con sus funcionalidades avanzadas, puedes escribir hojas de estilo más complejas de una manera más simple y mantener el código más limpio y reutilizable.

## 02) PRIMER CONTACTO
Vamos a comenzar con un ejemplo básico para entender cómo funciona Sass.

### Configurando el Entorno
#### 1. Instalar Node.js y npm
Si aún no tienes instalado Node.js, descarga e instala la versión LTS desde el [sitio oficial de Node.js](https://nodejs.org/). El npm se instalará automáticamente con Node.js.

#### 2. Instalar Sass
Abre la terminal y ejecuta el siguiente comando para instalar Sass globalmente:

```sh
npm install -g sass
```

#### 3. Verificar la Instalación de Sass
Verifica si Sass se instaló correctamente ejecutando:

```sh
sass --version
```

Deberías ver la versión instalada de Sass, lo que confirma que la instalación fue exitosa.

### Escribiendo el Primer Código Sass
Vamos a crear un proyecto simple para ver Sass en acción.

#### 1. Crear la Estructura de Carpetas
Crea una estructura de carpetas para tu proyecto:

```sh
mkdir mi-proyecto-sass
cd mi-proyecto-sass
mkdir scss css
```

#### 2. Crear un Archivo SCSS
Crea un archivo llamado `style.scss` dentro de la carpeta `scss`:

```sh
touch scss/style.scss
```

Abre el archivo `scss/style.scss` en tu editor de texto preferido y agrega el siguiente código:

```scss
// Variable de color primario
$primary-color: #3498db;

// Estilos para el cuerpo
body {
  font-family: Arial, sans-serif;
  background-color: #f0f0f0;
  color: $primary-color;
}

// Estilos para el encabezado
header {
  background-color: darken($primary-color, 10%);
  padding: 20px;
  text-align: center;
  
  h1 {
    margin: 0;
    color: white;
  }
}

// Estilos para enlaces
a {
  color: $primary-color;
  text-decoration: none;
  
  &:hover {
    text-decoration: underline;
  }
}
```

#### 3. Compilar el SCSS a CSS
Usa el comando Sass para compilar `style.scss` a `style.css`:

```sh
sass scss/style.scss css/style.css
```

Esto generará un archivo `style.css` en la carpeta `css` con el CSS compilado.

#### 4. Usar el CSS en el HTML
Crea un archivo `index.html` en el directorio raíz de tu proyecto y agrega el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="css/style.css">
  <title>Mi Proyecto Sass</title>
</head>
<body>
  <header>
    <h1>Bienvenido a Mi Proyecto Sass</h1>
  </header>
  <main>
    <p>Este es un párrafo estilizado con Sass.</p>
    <a href="#">Este es un enlace estilizado con Sass</a>
  </main>
</body>
</html>
```

### Automatizando la Compilación
Para facilitar el desarrollo, puedes usar la opción `--watch` de Sass para compilar automáticamente cada vez que realices cambios en tu archivo SCSS:

```sh
sass --watch scss/style.scss:css/style.css
```

## 03) ANIDAMIENTO (NESTING)
El anidamiento es una característica importante de Sass que permite escribir CSS de forma más jerárquica y organizada, siguiendo la estructura del HTML. Con el anidamiento, puedes ahorrar tiempo y hacer tu código más legible.

### Sintaxis de Anidamiento
En Sass, puedes anidar selectores dentro de otros selectores para representar de manera más clara la estructura HTML. Por ejemplo:

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
    
    li {
      display: inline-block;
    }

    a {
      text-decoration: none;
    }
  }
}
```

Este código Sass se compila en el siguiente CSS:

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav ul li {
  display: inline-block;
}

nav ul li a {
  text-decoration: none;
}
```

### Ventajas del Anidamiento
- **Legibilidad**: El anidamiento hace que el código sea más fácil de entender, reflejando la estructura del HTML.
- **Organización**: Ayuda a mantener el código organizado, especialmente para selectores anidados.
- **Reducción de Repetición**: Evita la repetición de selectores, ahorrando tiempo y esfuerzo al escribir el código.

### Consideraciones al Usar Anidamiento
- **No exageres**: Anidar selectores en exceso puede generar una especificidad elevada y dificultar el mantenimiento del código.
- **Mantén un nivel plano**: Evita anidar muchos niveles de selectores. Si el anidamiento se vuelve demasiado profundo, considera dividir el código en partes más pequeñas.

### Ejemplo Práctico
Vamos a crear un ejemplo práctico de anidamiento para estilizar un menú de navegación simple:

```scss
nav {
  background-color: #333;
  padding: 10px;

  ul {
    margin: 0;
    padding: 0;
    list-style: none;

    li {
      display: inline