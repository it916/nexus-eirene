# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Qué es este repositorio

Sitio de marketing para **Nexus Eirene Wellness Hub LLC** — un programa de bienestar emocional **no médico** (Florida, EE.UU.). Tres páginas estáticas: `index.html` (landing), `privacidad.html` (Política de Privacidad), `terminos.html` (Términos y Condiciones). Los PDFs y el docx referenciados abajo son **documentos fuente** de marca y contenido que viven **solo en local** (excluidos del repo vía `.gitignore`), no insumos de build.

⚠️ **Los documentos legales (`privacidad.html`, `terminos.html`) son borradores generados por IA**, no fueron redactados por un abogado. **Deben ser revisados por un abogado licenciado en Florida antes de considerarse vinculantes** — especialmente las cláusulas de limitación de responsabilidad, indemnidad, jurisdicción, y la referencia a Florida Statutes Title XXXII.

- `index.html` — el sitio completo (HTML + `<style>` inline + 2 imágenes `data:image` embebidas). Sin paso de build, sin framework JS, sin gestor de paquetes, sin pruebas.
- `Guia_Marca_Nexus_Eirene.pdf` — guía de marca v1.0 (junio 2026). Define paleta, tipografía y uso del logo. Las variables CSS en `index.html` corresponden a esta guía (ver tabla más abajo). **No introducir colores nuevos sin consultar el PDF.**
- `Nexus_Eirene_Contenido_Web.docx` — copy web bilingüe canónico. Cuando se pida editar texto del cuerpo, tratar este documento como la fuente.
- `NE - Paquete_Ingreso.pdf` — paquete de ingreso/onboarding (consentimiento, acuerdo de membresía). Es el origen de los avisos legales del `index.html` (no médico, no diagnóstico, referencia a Florida Statutes Title XXXII, retención de registros por 2 años).

**No es un repositorio git.**

## Cómo "ejecutarlo"

Abrir `index.html` directamente en un navegador, o servir la carpeta como estática (por ejemplo `python -m http.server` desde este directorio). No hay servidor de desarrollo, ni hot reload, ni paso de compilación.

## Convenciones de edición propias del sitio

- **Patrón bilingüe ES/EN.** Cada cadena visible para el usuario lleva el español como texto principal y la traducción al inglés inmediatamente después, envuelta en `<span class="en">…</span>`. Mantener este emparejamiento en cualquier copy nuevo. **Primero español, después inglés** — nunca al revés.
- **Los `id` de sección son anclas de navegación.** El header sticky enlaza a `#nosotros`, `#equipo`, `#planes`, `#como`, `#lanzamiento`. Si se renombra un `<section id="…">`, hay que actualizar también el bloque `<nav class="navlinks">`.
- **El estilo va inline en un bloque `<style>` por página.** Cada página (`index.html`, `privacidad.html`, `terminos.html`) tiene su propio bloque autosuficiente. Las páginas legales duplican un subconjunto reducido del CSS de `index.html` (variables, nav, footer, tipografía); no extraer a stylesheet compartido sin petición explícita. Si cambias variables de marca, actualizar las tres páginas.
- **Dos blobs `data:image` embebidos** viven aproximadamente en las líneas 165 y 179 (la marca y el logo del hero). Estas líneas son extremadamente largas; no intentar `Read` sobre ellas sin una ventana `offset`/`limit` ajustada, porque la herramienta rechaza chunks de ese tamaño. Usar `Grep` primero para localizar marcadores estructurales y luego leer alrededor.
- **El copy legal/cumplimiento es estructural.** El encuadre como "programa de bienestar no médico", la aclaración de que no reemplaza atención clínica, la referencia al 911 y la línea de Florida Statutes Title XXXII son requisitos de posicionamiento del programa — no suavizarlos ni eliminarlos sin confirmación.
- **El comentario sobre fecha de lanzamiento cerca de la línea 161** (`fecha de lanzamiento original (15 ago 2025) ya pasó`) documenta que el banner del hero se cambió de una fecha fija a "Inscripciones abiertas". Si piden volver a poner una fecha, confirmar cuál.

## Paleta de marca (hex + reglas de uso)

Mapeo entre la guía de marca y las variables CSS de `index.html`. Las reglas de "no usar para texto" están **verificadas contra contraste WCAG AA** en el PDF — no son estilísticas, son de accesibilidad.

**Primarios — identidad (logo, titulares grandes, bloques de color):**

| Hex | Variable | Nombre de marca | Uso |
|---|---|---|---|
| `#AC8129` | `--gold` | Dorado loto | Logo, titulares grandes, acentos. **No usar en texto pequeño.** |
| `#40A193` | `--teal` | Turquesa sereno | Acento secundario, iconos, detalles. **No usar para texto.** |
| `#F5F2EC` | `--cream` | Crema lino | Fondo de página por defecto — **no usar blanco puro como fondo.** |

**Funcionales — versiones oscurecidas, sí aptas para texto:**

| Hex | Variable | Nombre de marca | Contraste sobre crema | Uso |
|---|---|---|---|---|
| `#7A5A1C` | `--gold-deep` | Dorado profundo | 6.35:1 AA | Enlaces y texto dorado sobre fondo claro |
| `#256B61` | `--teal-deep` | Turquesa profundo | 6.26:1 AA | Botones primarios, CTA, texto turquesa |
| `#1C2B3A` | `--ink` | Marino tinta | 14.4:1 AA | Cuerpo de texto |

**Neutros:**

| Hex | Variable | Nombre de marca | Uso |
|---|---|---|---|
| `#FFFFFF` | `--white` | Blanco | Superficies / tarjetas |
| `#E8E2D5` | `--arena` | Arena | Bordes y divisores |
| `#5C5648` | `--topo` | Topo | Texto secundario |

**Estado / semánticos** (propuestos en la guía, armonizados con la paleta cálida):

| Hex | Variable en `index.html` | Uso |
|---|---|---|
| `#3B7A57` | *(no existe aún)* | Éxito / confirmado |
| `#B8740E` | `--amber` | Aviso / pendiente — **solo en texto grande** |
| `#B23A2E` | *(no existe aún)* | Error / cancelado |

Si se necesita un estado de éxito o error, **añadir la variable CSS con el hex exacto de arriba** — no aproximarlo. Hoy solo `--amber` está definido.

### Tres principios no negociables (de la guía, sección 01)

1. **Calidez sobre frialdad** — el crema (`--cream`) es el fondo, no el blanco puro.
2. **El dorado es identidad, no texto** — `--gold` (`#AC8129`) solo en logo y titulares grandes; para texto/enlaces dorados usar siempre `--gold-deep` (`#7A5A1C`).
3. **Accesible siempre** — cualquier texto nuevo debe cumplir contraste AA contra su fondo.

## Tipografía

Las dos familias ya están cargadas vía Google Fonts en el `<head>` de `index.html` y expuestas como variables CSS — **reutilizar las variables, no volver a importar fuentes**:

- `--serif: 'Cinzel', Georgia, serif` — titulares display, en mayúsculas con interletrado amplio (uso: el wordmark del logo y `h2.sec-title`). La guía permite también Trajan Pro como equivalente impreso.
- `--sans: 'Montserrat', system-ui, sans-serif` — cuerpo, etiquetas, botones, formularios. Jost es alternativa aceptada por la guía.

Jerarquía sugerida por la guía: título serif 24–32 pt · subtítulo sans 500 14–18 pt · cuerpo sans 400 10–12 pt · nota 8–9 pt.

## Precios y planes (editados con frecuencia)

Tres planes + una variante subsidiada viven en la sección `#planes`: Básica `$54.99/mes`, Premium `$109/mes` (marcado `feat` / "Más popular"), Corporativa `$209/empl./mes` (mínimo 5 empleados), y el plan PREP (100% de subsidio para participantes activos de PREP). Al actualizar precios, modificar tanto el elemento `.price` como cualquier copy narrativo que cite la cifra.
