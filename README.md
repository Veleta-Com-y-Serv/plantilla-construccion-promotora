# Plantilla NoExpertise · Construcción y promotora

Web rotunda para constructoras y promotoras, con promociones en venta, obra terminada y cifras.

- Sectores: construccion, promotora, obra-nueva, ingenieria, aparejador. Estilo: sólido. Plan mínimo: presencia.
- Secciones: hero, promociones, servicios, trabajos, cifras, proceso, equipo, cta, preguntas, contacto (+ `texto` genérico).
- Campos propios: `hero.items[]` (titulo, texto, url), `promociones[]` (titulo, lugar, estado, precio, viviendas, tipologia, texto, imagen, destacado), `servicios.imagen`, `trabajos[]` (titulo, lugar, anio, categoria, texto, imagen), `cta` (imagen, cta, cta_secundario), `contacto.opciones`.
- Diseño a ancho completo: bandas a sangre (grafito, hormigón visto, acero, acento), hero casi a pantalla completa, promociones en zigzag 50/50, mosaico de obra de borde a borde, cifras gigantes. Brief en `DISEÑO.md`.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`GeneralContractor`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.
