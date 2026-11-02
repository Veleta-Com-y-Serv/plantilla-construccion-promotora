# Construcción y promotora: brief de diseño

Plantilla `construccion-promotora` creada el 29/10/2026 a partir de `inmobiliaria` con `php artisan plantillas:nueva`
y rediseñada entera. Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: constructoras, promotoras, empresas de obra nueva y rehabilitación, ingenierías y aparejadores
  (`sectores`: construccion, promotora, obra-nueva, ingenieria, aparejador). Llegan dos clientes: quien quiere comprar
  una vivienda de una promoción (qué hay, dónde, en qué estado, desde cuánto) y quien quiere encargar una obra
  (qué hacen, qué han construido, cómo trabajan y quién firma).
- **Qué tiene que conseguir la web**: que pidan información de una promoción o que hablen con un técnico (botón de la
  cabecera, botón de cada promoción, llamada a la acción y formulario con «Me interesa»).
- **Tono y estilo** (`estilo: solido`): rotundo, técnico y fiable. Referencia que sí: losmartesnohayluna.com (bandas a
  sangre alternas, cifras y títulos gigantes); la cartelería de obra y los planos (rótulos numerados, monoespaciada).
  Que no: la caja centrada estrecha con tarjetas blancas de las plantillas antiguas; los dorados y las fichas de
  `inmobiliaria`; las mayúsculas condensadas y las franjas diagonales de `taller-mecanico` y las deportivas; las líneas
  de cota y la retícula de `arquitectura-interiorismo`.
- **Paleta de ejemplo**: primario `#244765` (azul acero), acento `#6aa6dc` (acero claro), fondo `#ffffff`, texto
  `#16191d` (grafito). Derivados en `global.css`: `--c-grafito` (texto + un toque de primario: cabecera, obra
  terminada, pie), `--c-grafito-2` (formulario), `--c-hormigon` / `--c-hormigon-2` (gris hormigón), `--c-acento-texto`
  (acento oscurecido, legible sobre blanco), `--c-sobre-acento` (blanco o negro según la luz del acento, con
  `oklch(from …)`; sin soporte, negro). El diseño aguanta que el cliente cambie los cuatro.
- **Tipografía** (del sistema, sin descargas): títulos en palo seco negro (`Arial Black`, 900, interletrado −0,035 em,
  minúsculas: «sólido», no condensado); rótulos, estados, lugares, cifras pequeñas y menú en monoespaciada
  (`ui-monospace`, Cascadia, SF Mono, Consolas) en mayúsculas espaciadas; texto en `system-ui`. Antetítulo = sillar de
  acento + número de sección «01 /» + antetítulo.
- **Motivos**: hormigón visto en CSS (poro fino, juntas de encofrado cada 240 × 120 px y berenjenos, los agujeros de
  los latiguillos); vigas de acero (filete grueso del primario con un tramo de acento) sobre los pilares de servicios,
  los retratos y el cronograma; bloques con sombra maciza (iconos, botones al pasar). Esquinas vivas en todo.
- **Ritmo de bandas** (todas de borde a borde; contenido a 90 rem como mucho, 16 px de margen del texto en móvil):
  1. `hero` — foto a sangre con velo grafito, 92 svh; título de 7,25 rem (2,6 en móvil), texto y dos botones;
     franja de acero inferior con los accesos numerados (3 columnas desde 1024 px, apilados antes).
  2. `promociones` — blanco; titular partido; cada promoción una fila 50/50 a sangre en zigzag (foto que toca el
     borde, alterna lado; el texto alterna blanco y hormigón): número hueco grande, lugar, título, texto, viviendas y
     tipología entre filetes gruesos, precio y botón. Estado en etiqueta sobre la foto.
  3. `servicios` — hormigón; foto a sangre 50/50 + titular; servicios como pilares a 4 columnas (2 en tableta).
  4. `trabajos` — grafito; mosaico de fotos de borde a borde sin huecos (piezas flexibles: 1 columna en móvil, 2 en
     tableta, 4 en escritorio con la primera de cada cuatro doble), con categoría, título y lugar · año encima.
  5. `cifras` — acero con textura de encofrado; cifras enormes separadas por filetes; zócalo de acento.
  6. `proceso` — blanco; cronograma horizontal con viga de acero y nudos cuadrados (vertical en móvil).
  7. `equipo` — hormigón; retratos 3:4 a 4 columnas (2 en móvil) con zócalo de acero.
  8. `cta` — 50/50: foto a sangre + banda del color de acento con título grande y dos botones.
  9. `preguntas` — blanco; titular fijo a la izquierda, acordeón con filetes gruesos y bloque «+» de acero.
  10. `contacto` — 50/50 a sangre: acero con el teléfono gigante y los datos; grafito claro con el formulario.
  Pie grafito a 4 columnas con zócalo de tres franjas (acento, acero, hormigón).
- **Fotos** (`fotos.json`, 12): obra en construcción con grúa al atardecer (hero 21:9), tres promociones (fachada
  nueva, pareados, salón de piso piloto), detalle de armaduras y encofrado (servicios), seis obras terminadas
  (bloque, rehabilitación, nave, unifamiliar, colegio, pareados) y mesa de obra con planos y casco (cta). Sin texto
  legible, sin logotipos ni personas reconocibles. Equipo con `/placeholders/persona.svg`.
- **Qué no hacer**: tarjetas blancas con sombra en rejilla estrecha; esquinas redondeadas; dorados; fuentes
  condensadas en mayúsculas para los títulos; inventar precios, cifras o plazos en los componentes (todo sale del
  `site.yaml`; sin dato no se pinta).

## Hecho

- [x] `site.yaml` de ejemplo: Esgueva Obras y Promociones (Valladolid), todo activo, al menos un elemento por lista,
  precios entre comillas, listas planas.
- [x] Secciones nuevas: `promociones`, `trabajos`, `cifras`, `proceso`, `cta`; rediseñadas `hero`, `servicios`,
  `equipo`, `preguntas`, `contacto` y `texto`. Fuera las de `inmobiliaria` (`inmuebles`, `zonas`, `valoracion`,
  `opiniones`).
- [x] `template.yaml` (sectores con nombre, secciones, guion del asistente de 11 pasos), `fotos.json`, `CLAUDE.md`,
  `README.md`, placeholders y favicon propios, `aviso-legal` y `404` con el diseño.
- [ ] Fotos generadas y previews definitivas (paso de fotos; las de ahora son provisionales con placeholders).
- [ ] Repo `Veleta-Com-y-Serv/plantilla-construccion-promotora` con la etiqueta `v1.0.0`; en la plataforma,
  `config/plantillas.php` (`repos` y `refs`) y `php artisan plantillas:sync --demos`.

## Páginas propias (fichas)
Con la misma piel que la portada: cabecera y pie de la plantilla, migas (Inicio › Sección › Elemento), hero con la foto del
elemento (sin foto, su icono), `detalle` en párrafos, tabla de datos, caja de contacto, galería (`imagenes`) y otros elementos
de la misma lista.
