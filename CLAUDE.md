# Plantilla «Construcción y promotora» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **sólido**
(hormigón visto + azul acero + blanco; bandas a sangre de borde a borde; títulos en palo seco negro tipo Arial Black,
rótulos técnicos en monoespaciada; esquinas vivas; botones macizos con sombra de bloque). Brief completo en `DISEÑO.md`.
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa (listas propias `promociones` y `trabajos` normalizadas con `lista<T>()`); no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = azul acero, acento = acero claro, fondo, texto = grafito). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). Los derivados (`--c-grafito`, `--c-grafito-2`, `--c-hormigon`, `--c-hormigon-2`, `--c-acento-texto`, `--c-tenue`, `--c-borde`, `--c-sobre-acento`) se calculan con `color-mix` (y `oklch(from …)` para el texto sobre el acento: blanco o negro según su luz) en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos` Arial Black, `--fuente-tecnica` monoespaciada, `--fuente-texto` del sistema; bandas `.banda-grafito`, `.banda-acero`, `.banda-acento`, `.hormigon` (textura de hormigón visto con berenjenos), `.hormigon-oscuro`; botones `.btn` (acero), `.btn-acento`, `.btn-sec` (contorno); `.rotulo`, `.estado`, `.dato-tecnico`, `.icono-bloque`; cabecera `.cabecera--obra` y pie `.pie--obra`). Fuentes del sistema: no añadas fuentes externas.
- **Cabecera**: `src/components/Header.astro`. Grafito, fija, a todo el ancho; teléfono y botón `boton_cabecera`.
- **Pie**: `src/components/Footer.astro`. Columnas de servicios y promociones (salen de esas secciones), contacto y zócalo de tres franjas.
- **Imágenes**: en `public/`. Fotos en `public/fotos/` (las genera el coordinador desde `fotos.json`); respaldo en `public/placeholders/` (`hero.svg`, `obra.svg`, `persona.svg`). En `site.yaml` se referencian con ruta absoluta (`/fotos/promocion-moreras.jpg`). Si una foto falta, `Imagen.astro` muestra su SVG de respaldo. Las fotos de personas son siempre `/placeholders/persona.svg` salvo que el cliente aporte la suya.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en bloque de acero + nombre en texto.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (se oculta solo con `false`).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`. Todas son bandas a todo el ancho; el número «01, 02…» del rótulo sale solo del orden (`numeroSeccion`).
- `hero` → `secciones/hero.astro` · foto a sangre casi a pantalla completa con velo grafito, título enorme, dos botones y franja de acero con los accesos (`items`).
- `promociones` → `secciones/promociones.astro` · filas 50/50 en zigzag con la foto a sangre.
- `servicios` → `secciones/servicios.astro` · banda de hormigón: foto a sangre + titular y servicios como «pilares» a 4 columnas.
- `trabajos` → `secciones/trabajos.astro` · banda grafito con mosaico de fotos de borde a borde sin huecos.
- `cifras` → `secciones/cifras.astro` · banda de acero con cifras enormes (sin cifras no se pinta).
- `proceso` → `secciones/proceso.astro` · cronograma de fases con viga de acero.
- `equipo` → `secciones/equipo.astro` · retratos 3:4 a 4 columnas sobre hormigón.
- `cta` → `secciones/cta.astro` · llamada a la acción 50/50: foto a sangre + banda del color de acento.
- `preguntas` → `secciones/preguntas.astro` · acordeón `details/summary` (sin preguntas no se pinta).
- `contacto` → `secciones/contacto.astro` · 50/50 a sangre: datos y teléfono grande en acero, formulario en grafito.
- `texto` → `secciones/texto.astro` · apartado genérico para secciones nuevas (`tipo: texto`); con imagen, fila 50/50 a sangre.

## Campos propios de esta plantilla (además del esquema común)
- `hero.items[]`: accesos de la franja de acero: `{ titulo, texto, url }` (`url` opcional; sin ella no es enlace). Sin items, no hay franja.
- `promociones.promociones[]`: `{ titulo, lugar, estado, precio, viviendas, tipologia, texto, imagen, destacado }`, todo cadenas salvo `destacado`.
  - `precio` siempre **cadena** (`"Desde 214.000 €"`); vacío = no se muestra. Nunca inventes precios.
  - `estado`: texto libre («En construcción», «Entrega 2027», «Disponible»). El que contenga solo «Disponible» sale en el color de acento (clase `estado--disponible`).
  - `destacado: true` = bloque con estrella junto al título.
  - Lista vacía (`promociones: []`) = franja con el `texto` y el botón `cta`, sin filas.
- `promociones.cta`: botón de cada fila (p. ej. «Pedir información» → `/#contacto`).
- `servicios.imagen` (opcional, foto a sangre junto al titular) y `servicios.items[]`: `{ titulo, texto, icono }`.
- `trabajos.trabajos[]`: `{ titulo, lugar, anio, categoria, texto, imagen }` (`anio` cadena; el texto solo se ve en escritorio). `trabajos.cta` opcional bajo el mosaico.
- `cifras.items[]`: `{ titulo = la cifra, texto }`. Nunca inventes cifras.
- `proceso.items[]`: `{ titulo, texto, icono }`; `proceso.cta` opcional.
- `cta`: `antetitulo`, `titulo`, `texto`, `imagen` (opcional), `cta`, `cta_secundario`.
- `contacto.opciones`: cadena con valores separados por «;» para el desplegable «Me interesa». Vacía = sin desplegable.
- Iconos disponibles: ver `src/components/ui/Icono.astro` (edificio, grua, casco, ladrillos, nivel, plano, lupa, escudo, llave, herramienta, casa…).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml` (los números de los rótulos se recalculan solos).
3. **Cambiar textos, teléfonos, horarios, fotos, promociones u obras**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: ningún elemento de lista puede llevar otra lista dentro. Máximo 24 elementos por lista. Precios siempre entre comillas.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: promociones`…) y un id propio en `site.yaml`. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` copiando la estructura de una existente (`seccion(Astro.props.id)`, `Titular`, banda a todo el ancho con `.contenedor` dentro). `src/pages/index.astro` la recoge sola.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` no se cambian. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay uno mínimo: cierre del menú móvil), 16 px de margen lateral del texto en móvil (`.contenedor` o `px-4`), fotos y fondos a sangre, sin scroll horizontal en móvil. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altSeccion` de `src/lib/seo.ts`, o el `titulo`/`nombre` de la ficha); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.promociones.promociones` → `/promociones/<slug>/` (promoción).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/promociones/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).

## Varias páginas
- `paginas:` (raíz de site.yaml, opcional): `[{ ruta, titulo, secciones: "servicios; planes" }]`, como mucho 6, cada sección en una sola página y nunca `hero`. Con ella la web pasa a Inicio (hero + lo que no esté en ninguna página) y una página por entrada (`/servicios/`…); el menú se hace solo con las páginas (las entradas `/#…` de `menu` no salen) y los enlaces `/#id` del site.yaml se cambian solos por la dirección de su sección. Sin ella, una sola página larga. Una orden «haz la web de varias páginas» = escribir `paginas`; nunca crees páginas a mano para eso.
- No tocar `src/lib/multipagina.ts`, `src/pages/index.astro` ni `src/pages/[...pagina].astro` (comunes a todas las plantillas). En un componente, un enlace fijo a una sección va con `enlace('/#contacto')` (de `src/lib/multipagina.ts`).
