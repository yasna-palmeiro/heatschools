# HeatSchools — sitio web (trilingüe ES / EN / PT)

Sitio web del proyecto **HeatSchools** (Wellcome Climate Impacts Award, 331072/Z/25/Z).

Está hecho con **Jekyll** (que GitHub compila automáticamente, sin que instales nada) y un **editor visual** (Sveltia CMS) para que cualquier miembro del equipo pueda actualizar el contenido desde el navegador, sin escribir código. El sitio funciona en **tres idiomas** —español (por defecto), inglés y portugués— con un selector de idioma en la cabecera.

Esta guía te lleva de cero a un sitio publicado en tu dominio `.org`, con editor visual funcionando. Sigue los pasos **en orden**. No necesitas saber programar; sí necesitas seguirlos con cuidado.

---

## Cómo funciona lo multilingüe

- El sitio abre en **español** en la raíz (`/`). El inglés vive bajo `/en/` y el portugués bajo `/pt/`.
- En la cabecera hay un selector **ES · EN · PT** que lleva a la misma sección en el otro idioma.
- No se usa ningún plugin especial: GitHub compila el sitio de forma **nativa**, sin GitHub Actions. Es la opción con menos piezas que se puedan romper.
- Cada idioma tiene su propio contenido, que se edita por separado en el CMS (verás listas como *"Noticias · Español"*, *"News · English"*, *"Notícias · Português"*).

> **Importante:** al traducir o añadir contenido, hazlo en las tres listas de idioma si quieres que aparezca en los tres. Las **publicaciones** son una sola lista común a los tres idiomas (los artículos no suelen traducirse).

---

## Qué contiene esta carpeta

| Elemento | Para qué sirve |
|---|---|
| `index.md`, `en/index.md`, `pt/index.md` | Páginas de inicio (una por idioma). |
| `equipo.html`, `en/team.html`, `pt/equipe.html` | Sección Equipo (plantillas). **No hace falta tocarlas.** |
| `publicaciones.html`, `en/publications.html`, `pt/publicacoes.html` | Sección Publicaciones (plantillas). |
| `noticias.html`, `en/news.html`, `pt/noticias.html` | Sección Noticias (plantillas). |
| `_team/` | Fichas de equipo (cada archivo tiene un campo `lang`: es/en/pt). |
| `_publications/` | Publicaciones (lista común). |
| `_news_es/`, `_news_en/`, `_news_pt/` | Noticias por idioma. |
| `_data/i18n.yml` | Textos de menús y botones en los tres idiomas. |
| `_layouts/`, `_includes/`, `assets/` | Plantillas y estilos. **No hace falta tocarlos.** |
| `admin/` | El editor visual (Sveltia CMS). |
| `_config.yml` | Configuración general del sitio. |

---

## Resumen de los pasos

1. Subir esta carpeta a un repositorio de GitHub.
2. Activar GitHub Pages (publica el sitio gratis).
3. Comprar el dominio `.org`.
4. Conectar el dominio a GitHub.
5. Rellenar `_config.yml` con tu dominio.
6. Crear el "portero" de autenticación (una vez).
7. Activar el editor visual (CMS).

Tras los pasos 1–2 ya tendrás el sitio online en una URL de GitHub. Los pasos 3–5 le ponen tu dominio propio. Los pasos 6–7 activan el editor para no-técnicos.

---

## Paso 1 — Subir la carpeta a GitHub

La forma más sencilla sin usar la línea de comandos es **GitHub Desktop**:

1. Descarga e instala **GitHub Desktop** desde <https://desktop.github.com> e inicia sesión con tu cuenta.
2. Menú **File → New repository**:
   - **Name:** `heatschools` (usa exactamente este nombre; el CMS lo espera).
   - **Local path:** elige una ubicación. GitHub Desktop creará una carpeta `heatschools`.
   - Pulsa **Create repository**.
3. Abre esa carpeta `heatschools` recién creada y **copia dentro TODO el contenido** de esta carpeta `heatschools-web` (es decir, `index.md`, `_config.yml`, las carpetas `_team`, `_news_es`, `en`, `pt`, `admin`, etc.). El contenido debe quedar en la **raíz** del repositorio, no dentro de una subcarpeta.
4. Vuelve a GitHub Desktop: verás los archivos como cambios. Abajo escribe un resumen (p. ej. *"Sitio inicial"*) y pulsa **Commit to main**.
5. Arriba pulsa **Publish repository**. Desmarca *"Keep this code private"* (recomendado para un sitio web) y pulsa **Publish**.

> Alternativa sin instalar nada: en <https://github.com/new> crea el repositorio `heatschools`, entra, pulsa **Add file → Upload files** y arrastra los archivos.

---

## Paso 2 — Activar GitHub Pages

1. Ve a `https://github.com/TU_USUARIO/heatschools`.
2. Pestaña **Settings** → menú lateral **Pages**.
3. En **Build and deployment → Source** elige **Deploy from a branch**.
4. En **Branch** selecciona `main` y carpeta `/ (root)`. Pulsa **Save**.
5. Espera 1–2 minutos y recarga. Aparecerá el enlace: `https://TU_USUARIO.github.io/heatschools/`.

(En esta URL provisional algunos estilos y enlaces pueden verse raros porque el sitio está configurado para tu dominio propio; se verá perfecto tras el paso 5.)

---

## Paso 3 — Comprar el dominio `.org`

Registradores recomendados por precio y sencillez:

- **Cloudflare** (<https://dash.cloudflare.com>) — al coste, sin sobreprecios.
- **Namecheap** (<https://www.namecheap.com>) — interfaz simple.
- **Gandi** (<https://www.gandi.net>) — europeo, buen soporte.

Busca el dominio (p. ej. `heatschools.org`) y complétalo. Coste aproximado: **10–15 € al año**.

---

## Paso 4 — Conectar el dominio a GitHub

**4a. En GitHub:** Repositorio → **Settings → Pages → Custom domain**. Escribe tu dominio (p. ej. `heatschools.org`) y **Save**. GitHub creará un archivo `CNAME` automáticamente.

**4b. En tu registrador (panel DNS):** añade cuatro registros **A** para el dominio raíz:

```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

Y un registro para `www`:

```
CNAME   www   TU_USUARIO.github.io
```

**4c.** Vuelve a GitHub → **Settings → Pages**, espera a que verifique el dominio (de minutos a 24 h) y marca **Enforce HTTPS**.

---

## Paso 5 — Poner tu dominio en la configuración

Edita `_config.yml` (en GitHub: abre el archivo → icono del lápiz):

```yaml
url: "https://heatschools.org"    # <-- tu dominio real
baseurl: ""                       # déjalo vacío
```

Guarda (**Commit changes**). En 1–2 minutos el sitio se recompila y se verá correctamente.

---

## Paso 6 — Crear el "portero" de autenticación del editor

El editor (`/admin/`) necesita un pequeño servicio gratuito para poder guardar cambios en GitHub. Se configura **una sola vez**.

**6a. Crear una OAuth App en GitHub:**

1. Ve a <https://github.com/settings/developers> → **OAuth Apps → New OAuth App**.
2. Rellena:
   - **Application name:** `HeatSchools CMS`
   - **Homepage URL:** `https://TU_DOMINIO.org`
   - **Authorization callback URL:** `https://TU-WORKER.workers.dev/callback` (valor provisional; lo ajustas tras 6b).
3. **Register application.** Anota el **Client ID** y genera un **Client secret** (guárdalo, no se vuelve a mostrar).

**6b. Desplegar el "portero" en Cloudflare (gratis):**

1. Crea una cuenta gratuita en <https://dash.cloudflare.com>.
2. Usa el proyecto oficial **sveltia-cms-auth**: <https://github.com/sveltia/sveltia-cms-auth>. Tiene un botón **Deploy to Cloudflare Workers**; síguelo.
3. Cuando pida variables de entorno, pega el **Client ID** y el **Client secret** del paso 6a.
4. Cloudflare te dará la URL del worker, algo como `https://sveltia-cms-auth.TU-SUBDOMINIO.workers.dev`.
5. Vuelve a la OAuth App (6a) y corrige el **Authorization callback URL** a esa URL + `/callback`.

---

## Paso 7 — Conectar el editor

Edita `admin/config.yml` con tus valores reales:

```yaml
backend:
  name: github
  repo: TU_USUARIO/heatschools
  branch: main
  base_url: https://sveltia-cms-auth.TU-SUBDOMINIO.workers.dev
```

Guarda (**Commit changes**). Listo: entra en `https://TU_DOMINIO.org/admin/`, pulsa **Iniciar sesión con GitHub** y ya puedes editar.

---

## Uso diario — cómo edita el equipo

1. Entra en `https://TU_DOMINIO.org/admin/` e inicia sesión con GitHub.
2. Elige la lista según idioma y sección (p. ej. *"Noticias · Español"* o *"News · English"*).
3. Para añadir algo nuevo pulsa **New**, rellena los campos y **Publish**.
4. Los cambios se guardan en GitHub y el sitio se actualiza solo en 1–2 minutos.

No hay que tocar HTML ni archivos: todo son formularios. Recuerda repetir la entrada en cada idioma que quieras cubrir.

---

## Dar acceso a colaboradores (equipo y estudiantes)

1. Cada persona necesita una cuenta de GitHub (gratuita).
2. Repositorio → **Settings → Collaborators → Add people** → escribe su usuario.
3. Dale rol **Write**. Con eso podrá entrar al `/admin/` y editar. Para revocar, quítala de esa lista.

---

## Próximo paso previsto: dashboard de políticas (WP1)

Está previsto añadir un **panel interactivo con las políticas recabadas en el análisis de políticas (WP1)**. El enfoque planificado:

- El análisis en R exporta la base de políticas a un archivo **CSV** (o se mantiene en una Google Sheet).
- Una nueva página del sitio (p. ej. `/politicas/`) leerá ese archivo y mostrará una **tabla interactiva filtrable** (por país, tipo de política, sector, año…) más gráficos o un mapa.
- Al actualizar el CSV, el panel se actualiza solo.

Se montará cuando la estructura de datos de WP1 esté definida, para ajustarlo a las columnas reales.

---

## Solución de problemas

- **El sitio no aparece / 404:** revisa Paso 2 (rama `main`, carpeta root). Espera 1–2 min tras cada cambio.
- **Se ve sin estilos o los enlaces fallan:** falta el Paso 5 (`url` correcto y `baseurl` vacío) o el dominio aún no propaga.
- **El `/admin/` no deja iniciar sesión:** revisa Pasos 6–7 (Client ID/secret, callback con `/callback`, `base_url` en `admin/config.yml`).
- **Falta un idioma en el menú de un contenido:** recuerda crear la entrada en cada lista de idioma.

---

## Coste anual estimado

| Concepto | Coste |
|---|---|
| Hosting (GitHub Pages) | Gratis |
| Editor visual + autenticación (Cloudflare Workers) | Gratis |
| Dominio `.org` | ~10–15 € / año |
| **Total** | **~10–15 € / año** |
