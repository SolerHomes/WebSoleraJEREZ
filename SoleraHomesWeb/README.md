# Solera Homes

Web de Solera Homes y landings de sus promociones en régimen de cooperativa.

Sitio estático: HTML, CSS y JS planos, sin build ni dependencias. Vercel lo sirve tal cual y GitHub admite subir los archivos arrastrándolos.

## Estructura

```
/index.html                        solerahomes.es
/assets/base.css                   andamiaje compartido por todas las landings
/assets/home.css                   estilos de la home
/assets/reveal.js                  animación de entrada de secciones
/assets/img/<proyecto>/            fotos de cada promoción
/assets/img/logos/                 logotipos
/proyectos/<slug>/index.html       landing del proyecto
/proyectos/<slug>/estilos.css      paleta y secciones propias del proyecto
```

Cada carpeta bajo `/proyectos/` se convierte en una URL: `/proyectos/bodega-cristal/` sirve su `index.html` sin necesidad de configuración.

Todos los enlaces internos son **relativos** (`proyectos/bodega-cristal/index.html`, `../../index.html`). Así el sitio se puede revisar abriendo `index.html` con doble clic, sin servidor. Si los cambias a rutas absolutas, el doble clic dejará de funcionar: en `file://`, `/` apunta a la raíz del disco.

## Proyectos publicados

| Slug | Promoción | Ubicación | Superform de Clientify |
|---|---|---|---|
| `bodega-cristal` | Bodega Cristal | Jerez de la Frontera | `293404` |
| `a47-living` | A47 Living | Madrid, Tetuán | `293387` |

## Añadir un proyecto nuevo

Duplica una carpeta de `/proyectos/`, cambia el slug y ajusta cuatro cosas: el `<title>` y la `<meta name="description">`, la paleta en `estilos.css` (las variables de `:root`), el `id` del Superform de Clientify, y las imágenes en `/assets/img/<slug>/`. Después, añade la tarjeta correspondiente en la sección `#proyectos` de `/index.html`.

`base.css` no debería necesitar cambios. Contiene solo las reglas idénticas en todas las landings: reset, `.wrap`, `section`, la cabecera, el contenedor `.form` y la animación `.reveal`. Si una regla deja de ser común a todos los proyectos, sácala de ahí en vez de sobrescribirla.

## Captación de leads

Los formularios de contacto son embeds de Clientify, el CRM del proyecto. Cada landing carga su Superform desde `api.clientify.net` dentro de `<div class="form">`, y los envíos entran directamente en Clientify.

**No añadas lógica de envío propia en el HTML.** Interceptaría o duplicaría los leads. Los campos, la validación y los textos se editan desde el editor de Superforms en Clientify, no aquí.

Si el script externo no carga, la sección de contacto se queda vacía. No hay fallback.

## Desarrollo

Abre `index.html` con doble clic. Para algo más parecido a producción:

```bash
python3 -m http.server 8000
```

## Despliegue

Vercel lo detecta como sitio estático. Framework Preset: **Other**. Sin build command ni output directory. Cada push a `main` despliega a producción.

## Pendiente

- Los logotipos de Solera Homes son dos archivos distintos (`solera-homes.png`, 430×157, y `solera-homes-a47.png`, 492×205). Conviene unificarlos.
- El correo de contacto no coincide entre landings: `info@solerahomes.es` en Bodega Cristal, `gerencia@solerahomes.es` en A47 Living.
- Las imágenes son JPEG a resolución completa (2,2 MB en total). Convertirlas a WebP y añadir `loading="lazy"` reduciría bastante la carga.
- Falta un fallback en la sección de contacto por si Clientify no responde: un `mailto:` visible, como mínimo.

## Aviso legal

La información publicada tiene carácter informativo y no contractual. Los proyectos pueden estar sujetos a modificaciones técnicas, administrativas o comerciales. Las imágenes pueden corresponder a renders orientativos.
