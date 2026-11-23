# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Objetivo

CV web como "Desarrollador Web Jr Backend | Python · Node.js · SQL", publicado en GitHub Pages. Secciones: titular, formación (UnADM en curso), 3 a 5 tarjetas de proyectos, comparación de paradigmas y contacto.

## Alcance de Claude en este repo

Solo diseño, SEO y accesibilidad de la página.

## Reglas

- Solo HTML, CSS y JavaScript puro, sin frameworks.
- Usar las variables CSS existentes (ej. `--fondo-tags`) en vez de colores sueltos.
- Colores nuevos con contraste WCAG AA verificado.
- HTML semántico, textos alternativos y navegación con teclado.
- Explicar cada cambio antes de hacerlo.
- Escribir el CLAUDE.md y los textos del sitio en español.

## Ejecutar en local

No hay gestor de paquetes, build, linter ni tests. Las páginas se sirven por HTTP desde la raíz del repo, no con `file://`.

- VS Code Live Server ya está configurado en el puerto 5501 (`.vscode/settings.json`): http://127.0.0.1:5501/index.html
- Sin VS Code: `python3 -m http.server 5501` desde la raíz del repo.

## Publicación en GitHub Pages

El remoto es `lulince/my.web`, así que GitHub Pages lo sirve como sitio de proyecto en `https://lulince.github.io/my.web/`.

- Las rutas que empiezan con `/` apuntan a `lulince.github.io/` y no al repo. Todas las rutas actuales ya son relativas (`css/...` desde `index.html`, `../css/...` desde `form/`); mantenerlo así en cualquier enlace, imagen u hoja nueva.
- GitHub Pages distingue mayúsculas: la hoja es `css/Index.css` (con I mayúscula) y la página es `index.html`.

## Estructura

- `index.html` contiene todo el sitio: header fijo con menú y selector ES/EN, sección "Sobre mí", tarjetas de stack (`.stack-grid` > `.stack-card` > `.badge--blue|slate|mint`) y tres filas `.proyectos-destacados` de `.proyecto-card` con franja de color (`strip-js`, `strip-py`, `strip-sql`).
- `css/Index.css` estiliza solo `index.html`. Los tokens están en `:root` (`--fondo-tags`, `--fuente-pixel`, `--fuente-texto-estandar`, `--dregadado-secundario`...). Los degradados se llaman `--dregadado-*`; reutilizar esos nombres tal cual. Muchos colores siguen escritos como hex sueltos (`#080f18`, `#1a4f7a`, `#2d7bb5`, `#7eb8e0`, `#3ecfb2`); al tocarlos, pasarlos a variables.
- `form/forms.html` es un formulario de contacto independiente que envía a Formspree (`https://formspree.io/f/mnqvkwqk`). Solo carga `css/form.css`, que es el único archivo donde se define `.btn`.
- `js/main.js` está vacío y ninguna página lo incluye.
- `icinos/` (sic) guarda las imágenes; `descarga.jpg` no se usa.
- Los nombres de clases, variables y comentarios están en español; los commits también.

## Pendientes conocidos

Verificar antes de dar algo por hecho; borrar cada punto cuando se resuelva.

**Contenido frente al objetivo**
- El título y la descripción dicen "Full Stack en Formación", no el titular del objetivo.
- Hay 9 tarjetas de proyecto en lugar de 3 a 5, y sus descripciones no corresponden a sus títulos.
- Faltan las secciones de formación (UnADM) y comparación de paradigmas. El formulario de contacto no está enlazado desde `index.html`.

**Contraste (WCAG AA pide 4.5:1 en texto normal)**

| Elemento | Texto sobre fondo | Contraste |
|---|---|---|
| `.chip--linkein` | `#0f27df` sobre `#031f34` | 1.90 |
| `.btn` | `#ffffff` sobre `#fc1515` | 3.99 |
| `.btn:hover` | `#ffffff` sobre `#e60096` | 4.37 |
| `.section-title` | `#2d7bb5` sobre `#080f18` | 4.22 |
| `cite` de la cita | `#2d7bb5` sobre `#0a1520` | 4.04 |

**CSS**
- `index.html` usa `.btn` pero no carga `css/form.css`, así que esos botones no tienen estilo.
- Solo se cargan "Geist Pixel" y "Plus Jakarta Sans". El CSS también usa "DM Sans", "DM Mono" y "Cormorant Garamond", que caen al respaldo sin avisar.
- `.section-title` está definido dos veces en `css/Index.css`; gana la segunda regla y la primera usa `--c-blue-dark`, que no existe.
- `.stack-grid` usa `display: flex` con `grid-template-columns`, que se ignora. `.proyectos-destacados` usa una variable de color como `margin-bottom`.

**SEO y accesibilidad**
- `<html lang="en">` aunque el contenido está en español.
- La meta de descripción usa un `name` no estándar, `author` está escrito `outhor` y `canonical` tiene texto de relleno.
- El favicon usa `rel="icinos"` en vez de `rel="icon"`, así que no carga.
- Los enlaces "Como lo hice?" tienen `href` vacío. El selector ES/EN no hace nada.
- Todos los enlaces del menú abren con `target="_blank"`, incluido "Inicio".
