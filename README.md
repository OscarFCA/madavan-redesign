# MADAVAN — rediseño de sitio (propuesta)

Rediseño del sitio de **MADAVAN Multilogística Internacional** (madavan.com.mx):
7 páginas responsivas para móvil, tablet y escritorio, en español e inglés.

**En vivo:** https://oscarfca.github.io/madavan-redesign/

| Página | Español | English |
|---|---|---|
| Home | `/` | `/en/` |
| Transporte Marítimo | `/transporte-maritimo.html` | `/en/transporte-maritimo.html` |
| Transporte Aéreo | `/transporte-aereo.html` | `/en/transporte-aereo.html` |
| Transporte Terrestre | `/transporte-terrestre.html` | `/en/transporte-terrestre.html` |
| Carga Sobredimensionada | `/carga-sobredimensionada.html` | `/en/carga-sobredimensionada.html` |
| Mercancía Peligrosa HAZMAT | `/mercancia-peligrosa-hazmat.html` | `/en/mercancia-peligrosa-hazmat.html` |
| Seguro de Mercancías y Carga | `/seguro-de-carga.html` | `/en/seguro-de-carga.html` |

### Academia MADAVAN

Los 7 cursos viven en el mismo sitio, bajo `/cursos/`:

| Curso | URL | Duración |
|---|---|---|
| Índice | `/cursos/` | — |
| Incoterms 2020 | `/cursos/incoterms-2020.html` | 5 h |
| Break Bulk Cargo | `/cursos/break-bulk-cargo.html` | 5 h |
| HAZMAT | `/cursos/hazmat.html` | 4 h |
| Importación | `/cursos/importacion.html` | 4 h |
| Exportación | `/cursos/exportacion.html` | 4 h |
| SNIC | `/cursos/snic.html` | — |
| Normas Oficiales Mexicanas | `/cursos/normas-oficiales-mexicanas.html` | próximamente |

Contacto por WhatsApp al **+52 55 5293 9407**, con botón flotante en todas las páginas.

## Cómo está hecho

Cada página es un *design canvas* (`.dc.html`) que `support.js` renderiza en el
navegador con React. El sitio es estático: no hay build de node ni dependencias.

La responsividad vive en el `<style>` del `<helmet>` de cada página:

- `--gx` es el margen horizontal de todas las secciones (56 → 44 → 32 → 20 → 16 px).
- Los tamaños de título usan `clamp()`, así que escalan solos sin breakpoints.
- Los hooks `data-r="..."` son los únicos selectores que usan las media queries —
  `support.js` reescribe los estilos inline, así que `[style*=...]` no funciona aquí.
- Debajo de 1024 px la navegación se convierte en menú hamburguesa.

Las ilustraciones (`assets/ilu-*.svg`) las genera `ilustraciones.py`.

## Idiomas

La fuente está en español. `traducciones.py` tiene el diccionario completo
español → inglés y `build.py` genera `/en/` sustituyendo cadena por cadena.
Si un texto no está en el diccionario, el build lo reporta en pantalla.

## Publicar cambios

Este repo es la salida del build. La fuente editable está en
`Hel3na/documentos/Madavan Home Redesign/*.dc.html`; para regenerar:

```bash
python3 ilustraciones.py   # sólo si cambian los dibujos
python3 cursos_gen.py      # sólo si cambia el catálogo de cursos
python3 build.py           # escribe deploy/, deploy/en/ y deploy/cursos/
cd deploy && git add -A && git commit -m "..." && git push
```

El catálogo de Academia vive en `cursos.py` y es la única fuente: los
`MADAVAN Curso *.dc.html` **están generados y no se editan a mano**. Al terminar,
`build.py` reporta qué datos faltan del cliente (enlaces de Hotmart, precios).

El sitio está marcado `noindex` por ser una propuesta.
