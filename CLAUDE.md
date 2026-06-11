# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Cómo ejecutar el proyecto

No hay proceso de compilación. Abre `index.html` directamente en un navegador:

```
# Windows
start index.html

# O simplemente arrastra index.html al navegador
```

React 18 y Babel se cargan desde CDN (unpkg), por lo que el JSX se transpila en el navegador en tiempo de ejecución. No hay `package.json`, bundler ni servidor de desarrollo necesario.

## Arquitectura

El proyecto es una **Single Page Application estática de un solo archivo** (`index.html`). Todo el código vive ahí:

- **`<style>`**: Media queries globales para responsividad (breakpoints en 768px y 480px). Los demás estilos son inline dentro de los componentes React.
- **`museumRooms`**: Array hardcodeado con los datos de las 6 salas y 19 objetos del museo. Es la única "fuente de datos" de la aplicación.
- **`Navigation`**: Componente con menú hamburguesa para móvil y efecto de scroll (fondo transparente → semiopaco).
- **`App`**: Componente raíz con 5 secciones de una sola página: `#inicio`, `#descargar`, `#salas`, `#instalacion`, `#encuesta`, más el footer.

La navegación usa `scrollIntoView` hacia IDs de sección — no hay React Router ni rutas.

## Datos del museo

Para agregar o modificar salas/objetos, edita el array `museumRooms` en el script. Cada sala sigue esta estructura:

```js
{
    id: 7,
    name: 'Sala 7 - Nombre',
    icon: '🏺',           // emoji
    color: '#00D9FF',     // color del tema (solo 3 colores rotativos: #00D9FF, #FF8C42, #FF6B9D)
    objects: [
        {
            name: 'Nombre del Objeto',
            description: 'Descripción corta.',
            image: 'images/sala7/sala7_nombre_objeto.jpg'
        }
    ]
}
```

Las imágenes siguen la convención `images/sala{N}/sala{N}_{nombre_objeto}.jpg`.

## Links externos

- **APK**: Google Drive — se actualiza cambiando la URL en el `onClick` del botón "Descargar APK" (línea ~535).
- **Encuesta**: Google Forms — URL en la constante `formUrl` dentro de la sección `#encuesta` (línea ~1215).
