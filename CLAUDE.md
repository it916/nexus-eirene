# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Qué es este repositorio

Sitio de marketing para **Nexus Eirene Wellness Hub LLC** — un programa de bienestar emocional **no médico** (Florida, EE.UU.). Cinco páginas estáticas: `index.html` (landing), `privacidad.html`, `terminos.html`, `404.html` (error page), `gracias.html` (Stripe success URL). En producción en **https://nexuseirene.com** vía GitHub Pages (repo `it916/nexus-eirene`, rama `main`). Los PDFs y el docx referenciados abajo son **documentos fuente** de marca y contenido que viven **solo en local** (excluidos del repo vía `.gitignore`), no insumos de build.

⚠️ **Los documentos legales (`privacidad.html`, `terminos.html`) son borradores generados por IA**, no fueron redactados por un abogado. **Deben ser revisados por un abogado licenciado en Florida antes de considerarse vinculantes** — especialmente las cláusulas de limitación de responsabilidad, indemnidad, jurisdicción, y la referencia a Florida Statutes Title XXXII.

**Archivos del repo:**

- `index.html` — landing principal con `<style>` inline + JSON-LD Schema.org + JS para lang toggle, hamburger menu, mobile CTA, form submission.
- `privacidad.html`, `terminos.html` — páginas legales bilingües (cada una autosuficiente).
- `404.html` — página de error custom (la sirve GitHub Pages para URLs inexistentes).
- `gracias.html` — página de éxito tras Stripe checkout (Success URL).
- `sunior-sanchez.jpg` — retrato del fundador (40 KB, 720×877).
- `nuestro-espacio.jpg` — banner del espacio (520 KB, 2048×1152, 16:9). Pasa por cache-bust `?v=N` en el src.
- `favicon.svg` — lotus dorado de la marca.
- `og-image.svg` — 1200×630 para Open Graph (Twitter, Facebook, LinkedIn).
- `robots.txt` + `sitemap.xml` — SEO, apuntan a las 3 páginas principales.

**Documentos fuente (solo en local, en `.gitignore`):**

- `Guia_Marca_Nexus_Eirene.pdf` — guía de marca v1.0 (junio 2026). Las variables CSS corresponden a esta guía (ver tabla más abajo). **No introducir colores nuevos sin consultar el PDF.**
- `Nexus_Eirene_Contenido_Web.docx` — copy web bilingüe canónico.
- `NE - Paquete_Ingreso.pdf` — paquete de ingreso/onboarding. Origen de los avisos legales (no médico, no diagnóstico, Florida Statutes Title XXXII, retención 2 años).

## Cómo "ejecutarlo"

**Local:** servir la carpeta como estática (por ejemplo `python -m http.server 8080` — el puerto 8000 suele estar ocupado por otro proyecto del equipo). Sin servidor de desarrollo, hot reload ni paso de compilación.

**Producción:** `git push origin main` despliega automáticamente a `https://nexuseirene.com` vía GitHub Pages (~1 min de rebuild). El `CNAME` en root contiene el dominio. HTTPS está activo (Let's Encrypt vía GitHub Pages).

## Convenciones de edición propias del sitio

- **Patrón bilingüe ES/EN con toggle.** Cada cadena visible para el usuario va envuelta en **dos spans**: `<span class="es">Texto</span><span class="en">Text</span>`. Por defecto se ve solo español; el botón ES/EN del nav cambia a inglés (clase `lang-en` en `<body>`). La preferencia se persiste en `localStorage` con clave `ne-lang` y se auto-detecta del navegador en primera visita. **No usar el patrón antiguo de texto-plano-más-`<span class="en">`-suelto** — ese formato no oculta el español al toggle.
  - Para `<select>`: usa atributos `data-es="..." data-en="..."` en cada `<option>` y `data-bilingual` en el select; el JS los intercambia.
  - Para `placeholder` de inputs/textarea: usa `data-placeholder-es="..." data-placeholder-en="..."`.
  - Para mensajes generados en JS (errores/éxito del form): usar el helper `txt(es, en)` que ya está definido en index.html.
  - `<title>` y `<meta name="description">` se actualizan dinámicamente desde el diccionario `meta` al inicio del bloque `<script>` de cada página. Si cambias el title de una página, edita ambas entradas.
- **Los `id` de sección son anclas de navegación.** El header sticky enlaza a `#nosotros`, `#equipo`, `#planes`, `#como`, `#faq`, `#contacto`, `#inscripcion`. El panel móvil hamburguesa replica los mismos anchors. Si se renombra un `<section id="…">`, hay que actualizar **el nav desktop + el panel hamburguesa + cualquier `data-plan`/`data-stripe-link` que apunte ahí**.
- **El estilo va inline en un bloque `<style>` por página.** Las cinco páginas (`index`, `privacidad`, `terminos`, `404`, `gracias`) tienen su propio bloque autosuficiente. Las cuatro páginas no-landing duplican un subconjunto del CSS de `index.html` (variables, tipografía, nav, footer, focus rings). No extraer a stylesheet compartido sin petición explícita. **Si cambias variables de marca o el toggle de idioma, actualizar las cinco páginas.**
- **Meta tags están duplicados en cada página.** Cualquier cambio de canonical URL, `og:image`, title o description debe replicarse. `favicon.svg`, `og-image.svg`, `nuestro-espacio.jpg`, `sunior-sanchez.jpg` son archivos compartidos en root.
- **`og-image.svg` usa fuentes del sistema** (Georgia/Helvetica) en vez de Cinzel/Montserrat porque los crawlers de OG no cargan webfonts. Funciona en Twitter, Facebook, LinkedIn, Slack, Discord; WhatsApp puede caer a fallback de solo texto.
- **El lotus inline en el divider** (entre hero y "Nosotros") es un SVG suelto dentro del HTML, no un archivo. Las mismas paths SVG aparecen también en `favicon.svg`, `og-image.svg`, `404.html`, `gracias.html` — si cambia el logo, actualizar en los cinco lugares.
- **El copy legal/cumplimiento es estructural.** El encuadre como "programa de bienestar no médico", la aclaración de que no reemplaza atención clínica, la referencia al 911 y la línea de Florida Statutes Title XXXII son requisitos de posicionamiento del programa — no suavizarlos ni eliminarlos sin confirmación. Está repetido en hero, footer, aviso legal del index, checkbox de consentimiento del form, sección 2 de Términos y secciones 1+11 de Política.

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

## Servicios externos del sitio

| Servicio | Para qué | Notas |
|---|---|---|
| **GitHub Pages** | Hosting estático | Push a `main` → deploy automático. Dominio custom `nexuseirene.com` vía CNAME en root. |
| **Cloudflare → Squarespace** | DNS autoritativo | NS legacy `ns-cloud-*.googledomains.com` apuntan a Squarespace (no a Google Cloud DNS). Los registros A se editan en Squarespace, no en Google. Ver memoria `reference_dns_topology` para detalle. |
| **Web3Forms** | Procesa el envío del form de inscripción a `operations@nexuseirene.com` | Access key `b7b50f4d-2f7b-4b02-b937-ba1ed0f644c1` está en el HTML — es **pública por diseño** (identifica destinatario, no autentica), seguro versionarla. NO usar `redirect=false` como hidden field, rompe el parser (debe omitirse para que Web3Forms devuelva JSON). |
| **Google Workspace** | Correo `@nexuseirene.com` | `info@`, `operations@`, etc. MX records ya configurados. |
| **Mailgun** | Correo transaccional desde `mail.nexuseirene.com` | MX + DKIM ya configurados en DNS. |

## Características clave del sitio (lo que ya funciona)

- **Toggle bilingüe ES/EN** en el nav, persistido en `localStorage` (clave `ne-lang`), auto-detect del navegador en primera visita. Todas las cinco páginas comparten la misma preferencia. Cambia `<title>`, `<meta description>`, opciones de `<select>` (vía `data-bilingual` + `data-es`/`data-en`), placeholders (`data-placeholder-es`/`-en`) y mensajes inline del form.
- **Hamburger menu en móvil**: panel lateral slide-in desde la derecha + backdrop oscuro + body scroll-lock + cierre por click backdrop/X/link/Esc. Aparece a ≤860px en index, ≤760px en legales (mismos breakpoints donde colapsa `.navlinks`).
- **CTA flotante en móvil**: botón "Inscríbete" sticky bottom en ≤760px. `IntersectionObserver` lo oculta cuando el form (`#inscripcion`) entra en viewport.
- **Formulario de inscripción**: envío vía `fetch` a Web3Forms, feedback inline (verde éxito / rojo error), honeypot anti-spam, pre-rellena el plan al venir de cards (`data-plan`).
- **Skip-to-content link** + focus-visible rings turquesa (WCAG 2.4.7) en las cinco páginas.
- **JSON-LD Schema.org** en `index.html` (`Organization` + `WebSite` + `FAQPage` con las 6 Q&A) y WebPage en las legales (`isPartOf` el WebSite).

## Stripe (preparación, no integración activa todavía)

Los botones de Básica y Premium en `#planes` tienen un atributo `data-stripe-link=""` vacío. Hay JS en el bloque `<script>` al final de `index.html` (busca `Stripe Payment Links`) que, si detecta una URL `https://...` en ese atributo, sobreescribe el `href` del botón y lo abre en pestaña nueva con `target="_blank"`. Si el atributo está vacío, el botón mantiene `href="#inscripcion"` y va al formulario.

**Para activar Stripe:**
1. En Stripe Dashboard, crear productos: `Básica · $54.99/mes` y `Premium · $109/mes` (modo Subscription, billing monthly).
2. Generar Payment Link para cada producto. En la configuración del Payment Link, poner como Success URL: `https://nexuseirene.com/gracias.html`.
3. En `index.html`, pegar la URL de cada Payment Link en el `data-stripe-link=""` del botón correspondiente:
   - `<a ... data-plan="Básica" data-stripe-link="">` → pegar URL de Básica
   - `<a ... data-plan="Premium" data-stripe-link="">` → pegar URL de Premium
4. **Corporativa** y **PREP** quedan en flujo de formulario (no Stripe directo) — Corporativa necesita consulta, PREP necesita verificación de elegibilidad.

`gracias.html` ya existe como la página de éxito tras Stripe checkout. La Política de Privacidad menciona Stripe como procesador (sección 4) y los Términos en la sección 5 con link a `stripe.com/legal/consumer`.

## Consentimiento de marketing (TCPA)

El formulario de inscripción tiene un segundo checkbox debajo del consentimiento legal: `name="marketing_consent"`, no es `required`. Si el usuario lo marca, Web3Forms incluye "Aceptado" en el campo `marketing_consent` del email enviado a `operations@nexuseirene.com`. El texto cumple con TCPA: opt-in expreso, no marcado por defecto, frecuencia, método de opt-out (STOP / unsubscribe link), "message and data rates may apply", y nota de "no es condición para inscribirse".

## Precios y planes (editados con frecuencia)

Tres planes + una variante subsidiada viven en la sección `#planes`: Básica `$54.99/mes`, Premium `$109/mes` (marcado `feat` / "Más popular"), Corporativa `$209/empl./mes` (mínimo 5 empleados), y el plan PREP (100% de subsidio para participantes activos de PREP). Al actualizar precios, modificar tanto el elemento `.price` como cualquier copy narrativo que cite la cifra.
