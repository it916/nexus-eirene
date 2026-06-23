# Nexus Eirene Wellness Hub

Sitio web de **Nexus Eirene Wellness Hub LLC** — un programa de bienestar emocional **no médico** con base en Florida, EE.UU.

🌐 **En producción:** [nexuseirene.com](https://nexuseirene.com)

> Conéctate contigo mismo · Find your calm

## Sobre el programa

Nexus Eirene es un espacio de apoyo emocional, coaching de bienestar y comunidad, culturalmente sensible y bilingüe (español/inglés). **No es un servicio médico**: no diagnostica, no trata enfermedades, no prescribe medicamentos y no realiza psicoterapia clínica. Es complemento, no sustituto, de la atención médica o psicológica profesional.

En caso de emergencia médica o de salud mental, llamar al **911** o al **988 (Suicide & Crisis Lifeline)**.

## Características del sitio

- Sitio estático multi-página, sin framework ni gestor de paquetes.
- **Bilingüe ES/EN con toggle**: el visitante elige idioma; preferencia persistida en `localStorage`, auto-detección del navegador en primera visita.
- **Formulario de inscripción operativo**: envíos enrutados a `operations@nexuseirene.com` vía Web3Forms (sin backend propio).
- **Diseño responsive** con menú hamburguesa en móvil y CTA flotante.
- **Accesibilidad**: skip-to-content link, focus rings visibles (WCAG 2.4.7), contraste AA en todos los textos.
- **SEO**: meta tags completos, Open Graph, JSON-LD Schema.org (Organization + FAQPage), sitemap, robots.txt, favicon SVG.
- **Stripe preparado** (no activado todavía) — placeholders listos para pegar Payment Links.
- **Consentimiento de marketing TCPA-compliant** opcional en el form.

## Estructura

```
.
├── index.html              ← landing principal
├── privacidad.html         ← Política de Privacidad
├── terminos.html           ← Términos y Condiciones
├── 404.html                ← página de error custom
├── gracias.html            ← Stripe success URL
├── favicon.svg             ← lotus dorado de la marca
├── og-image.svg            ← 1200×630 para redes sociales
├── sunior-sanchez.jpg      ← retrato del fundador (40 KB)
├── nuestro-espacio.jpg     ← banner del espacio (520 KB, 16:9)
├── robots.txt              ← apunta al sitemap
├── sitemap.xml             ← URLs indexables
├── CNAME                   ← dominio custom (nexuseirene.com)
├── CLAUDE.md               ← guía técnica para asistentes de IA
└── README.md               ← este archivo
```

Cada `.html` es autosuficiente: lleva su propio bloque `<style>` inline y JS al final. **No hay archivos CSS o JS compartidos.** Si cambias una variable de marca, actualízala en las cinco páginas.

## Desarrollo local

```bash
python -m http.server 8080
```

Luego abre [http://localhost:8080/](http://localhost:8080/). (Se usa el puerto 8080 porque el 8000 suele estar ocupado por otros proyectos.)

No hay paso de build, hot reload ni gestor de paquetes. Edita los `.html` directamente y recarga.

## Despliegue

```bash
git push origin main
```

GitHub Pages reconstruye el sitio en ~1 min y lo publica en `https://nexuseirene.com`. El dominio custom está en `CNAME`, HTTPS lo gestiona Let's Encrypt vía GitHub.

## Marca

Paleta y tipografía siguen la **Guía de Marca Nexus Eirene v1.0**. Las variables CSS expuestas en cada página corresponden a la guía:

- **Dorado loto** `#AC8129` — logo y titulares (no usar en texto pequeño)
- **Turquesa sereno** `#40A193` — acento, iconos
- **Crema lino** `#F5F2EC` — fondo por defecto (nunca blanco puro)
- **Dorado profundo** `#7A5A1C` — enlaces y texto dorado (AA)
- **Turquesa profundo** `#256B61` — botones primarios (AA)
- **Marino tinta** `#1C2B3A` — cuerpo de texto

Tipografías: **Cinzel** (display, mayúsculas con interletrado) + **Montserrat** (cuerpo), ambas vía Google Fonts.

## ⚠️ Documentos legales

`privacidad.html` y `terminos.html` son **borradores generados por IA**. No fueron redactados por un abogado. Deben ser revisados por un **abogado licenciado en Florida** antes de considerarse vinculantes — especialmente las cláusulas de limitación de responsabilidad, indemnidad, jurisdicción y la referencia a Florida Statutes Title XXXII.

## Aviso de cumplimiento

Programa conforme a Florida Statutes Title XXXII y las regulaciones aplicables de servicios de bienestar no médico en el Estado de Florida. Toda la información compartida por participantes es estrictamente confidencial.

## Contacto

- Email: [info@nexuseirene.com](mailto:info@nexuseirene.com)
- Teléfono · WhatsApp: [(786) 981-3006](tel:+17869813006)
- Horario: Lun – Vie, 10 AM – 6 PM ET

---

© 2025 Nexus Eirene Wellness Hub LLC · Todos los derechos reservados
