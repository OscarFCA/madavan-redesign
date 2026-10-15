# MADAVAN — rediseño de sitio (propuesta)

Rediseño del sitio de **MADAVAN Multilogística Internacional** (madavan.com.mx):
7 páginas responsivas para móvil, tablet y escritorio.

**En vivo:** https://oscarfca.github.io/madavan-redesign/

| Página | URL |
|---|---|
| Home | `/` |
| Transporte Marítimo | `/transporte-maritimo.html` |
| Transporte Aéreo | `/transporte-aereo.html` |
| Transporte Terrestre | `/transporte-terrestre.html` |
| Carga Sobredimensionada | `/carga-sobredimensionada.html` |
| Mercancía Peligrosa HAZMAT | `/mercancia-peligrosa-hazmat.html` |
| Seguro de Mercancías y Carga | `/seguro-de-carga.html` |

## Cómo está hecho

Cada página es un *design canvas* (`.dc.html`) que `support.js` renderiza en el
navegador con React. El sitio es estático: no hay build de node ni dependencias.

La responsividad vive en el `<style>` del `<helmet>` de cada página:

- `--gx` es el margen horizontal de todas las secciones (56 → 44 → 32 → 20 → 16 px).
- Los tamaños de título usan `clamp()`, así que escalan solos sin breakpoints.
- Los hooks `data-r="..."` (`navdesk`, `navact`, `burger`, `mobnav`, `heroimg`,
  `heroscrim`, `stats`, `stat`, `fdiv`) son los únicos selectores que usan las
  media queries — `support.js` reescribe los estilos inline, así que los
  selectores tipo `[style*=...]` no funcionan aquí.
- Debajo de 1024 px la navegación se convierte en menú hamburguesa.

## Publicar cambios

Este repo es la salida del build. La fuente editable está en
`Hel3na/documentos/Madavan Home Redesign/*.dc.html`; para regenerar:

```bash
python3 build.py      # escribe deploy/
cd deploy && git add -A && git commit -m "..." && git push
```

El sitio está marcado `noindex` por ser una propuesta.
