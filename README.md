# compercreativo.com

Sitio web de **Comper Creativo S.A.S.**: agencia de marketing digital, e-commerce y automatización con IA en Bogotá, Colombia. Es un sitio estático publicado con GitHub Pages.

## Estructura

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La página completa, con SEO, Open Graph y datos estructurados (negocio y preguntas frecuentes) |
| `404.html` | Página de error con la marca |
| `CNAME` | Le dice a GitHub Pages que el dominio es `compercreativo.com` |
| `.nojekyll` | Publica los archivos tal cual, sin procesarlos con Jekyll |
| `sitemap.xml` | Mapa del sitio para Google y Bing |
| `robots.txt` | Permite el rastreo a buscadores e IA (Google, Bing, ChatGPT, Claude, Perplexity) |
| `llms.txt` | Ficha de la agencia para que las IA la citen bien |
| `site.webmanifest` | Nombre, colores e íconos para instalar el sitio en el móvil |
| `og-image.jpg` | Imagen que sale al compartir el enlace (1200×630) |
| `assets/` | Logos, íconos y logos de clientes |

---

## 1. Empaquetado y publicación en GitHub Pages

1. En GitHub crea un repositorio público llamado, por ejemplo, `compercreativo-web`.
2. Sube **el contenido** de esta carpeta a la raíz del repositorio (no la carpeta en sí). Desde la Terminal:
   ```bash
   cd ~/Downloads/compercreativo-web
   git init
   git add .
   git commit -m "Sitio Comper Creativo v2"
   git branch -M main
   git remote add origin https://github.com/christianmanrike-spec/compercreativo-web.git
   git push -u origin main
   ```
   `.nojekyll` es un archivo oculto. Si subes por arrastre en la web de GitHub, revisa que haya quedado; con `git` sube solo.
3. En el repositorio ve a **Settings → Pages**:
   - **Source:** Deploy from a branch → `main` → `/ (root)` → Save.
   - **Custom domain:** `compercreativo.com` → Save. Se toma del archivo `CNAME`.
4. Recomendado: verifica el dominio para evitar que alguien más lo use en GitHub. Ve a tu foto de perfil → **Settings → Pages → Add a domain**. GitHub te dará un registro TXT `_github-pages-challenge-christianmanrike-spec`. Créalo en el DNS (paso 2) y pulsa **Verify**.

## 2. Dominio y DNS

Google Domains pasó a **Squarespace Domains**, así que el DNS se administra ahora en [account.squarespace.com/domains](https://account.squarespace.com/domains) con la misma cuenta de Google. Entra a **compercreativo.com → DNS → DNS Settings → Custom records → Add record**.

**Crea estos registros:**

| Host | Tipo | Valor |
|---|---|---|
| `@` | A | `185.199.108.153` |
| `@` | A | `185.199.109.153` |
| `@` | A | `185.199.110.153` |
| `@` | A | `185.199.111.153` |
| `www` | CNAME | `christianmanrike-spec.github.io` |

**Opcional (IPv6):** registros `AAAA` en `@` con `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153` y `2606:50c0:8003::153`.

**Qué no debes tocar:**

- **No borres ni cambies** los registros **MX** ni los **TXT** existentes (SPF, DKIM, verificación de Google Workspace, etc.). De ellos depende el correo `administracion@compercreativo.com`.
- **Sí borra** cualquier registro A o CNAME viejo de `@` o `www` que apunte a otro hosting (Lovable, Squarespace u otro). Si quedan, el dominio no carga bien.
- El valor del CNAME de `www` no lleva el nombre del repositorio: solo `christianmanrike-spec.github.io`.

**Activa HTTPS:** cuando el DNS propague (de minutos a 24 h), vuelve a **Settings → Pages**. Cuando aparezca "DNS check successful", marca **Enforce HTTPS**. GitHub puede tardar hasta 24 h en emitir el certificado.

**Comprueba que funciona:**

- `https://compercreativo.com` carga el sitio con candado.
- `https://www.compercreativo.com` redirige al dominio principal.
- `https://compercreativo.com/sitemap.xml` y `/robots.txt` abren.
- Envía un correo a `administracion@compercreativo.com` para confirmar que el correo sigue llegando.

## 3. Indexación y presencia

### Google Search Console

1. Ve a [search.google.com/search-console](https://search.google.com/search-console) → **Agregar propiedad → Dominio** → `compercreativo.com`.
2. Google te da un registro **TXT** `google-site-verification=...`. Agrégalo como registro **nuevo** en Squarespace, sin modificar los TXT existentes, y pulsa **Verificar**.
3. En **Sitemaps** envía `https://compercreativo.com/sitemap.xml`.
4. En **Inspección de URLs** pega `https://compercreativo.com/` y pulsa **Solicitar indexación**.

### Bing Webmaster Tools

1. Ve a [bing.com/webmasters](https://www.bing.com/webmasters) → **Importar desde Google Search Console**. Así se verifica y trae el sitemap en un paso.
2. Si no importa el sitemap, envía `https://compercreativo.com/sitemap.xml` en **Sitemaps**. Bing alimenta también a Copilot y a otros buscadores con IA.

### Google Business Profile

1. Entra a [business.google.com](https://business.google.com). Como ya existe la ficha en Maps (`https://maps.app.goo.gl/d2knArkiNGx9ULUk8`), **reclámala o verifícala** en vez de crear una nueva, para no duplicarla.
2. Categoría principal: *Agencia de marketing*. Secundarias: *Diseñador de sitios web*, *Servicio de marketing en Internet*.
3. **Sitio web:** `https://compercreativo.com`. **Teléfono / WhatsApp:** `+57 301 5531822`.
4. Usa el mismo nombre, dirección y teléfono que en la web. Esa coincidencia exacta es la que mejora el posicionamiento local en Bogotá.
5. Agrega los servicios (incluida *Automatización de procesos con IA*), el horario, fotos y el logo.
6. Cuando tengas la dirección exacta, las coordenadas y el horario, agrégalos también al bloque de datos estructurados de `index.html` (tipo `ProfessionalService`: `address`, `geo`, `openingHoursSpecification`).

---

## Actualizar el sitio

Edita los archivos, luego `git add . && git commit -m "cambio" && git push`. GitHub Pages publica en uno o dos minutos. Cuando cambies el contenido, actualiza `<lastmod>` en `sitemap.xml` y `dateModified` en `index.html`.
