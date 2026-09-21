# Auditoría de `DECISION_LOGIC_QALQALAH.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_QALQALAH.md`
- **SHA-256:** `76410c10d1a3c21f249a49eeb4e1b00686700c69619eaa0b7ddb33c950b05537`
- **Estado:** `resolved`; correcciones aplicadas al documento migrado
- **Decisión:** conservar el documento, corregir sus errores y validarlo manualmente antes de usarlo para el desarrollo.
- **Fuente local contrastada:** REL-001 / `Parte 6 Cualidades de las Letras (Sifat al-Huruf) (Páginas 56-64)..md`.

## Veredicto

El documento reproducía de forma razonable la descripción básica de qalqalah del libro de trabajo, pero añadía un algoritmo Unicode y una detección de waqf que no eran seguros. Esos puntos se corrigieron en [DECISION_LOGIC_QALQALAH.md](./DECISION_LOGIC_QALQALAH.md).

La validación operativa se realizará durante el desarrollo mediante comparación manual del propietario con el muṣḥaf coloreado y certificado adoptado. La revisión del especialista queda reservada como control final de la aplicación.

## Elementos respaldados provisionalmente por REL-001

### Definición y causa

REL-001, líneas 150–159, define qalqalah, enumera `قطب جد` y atribuye su causa a la combinación de shiddah y jahr. El documento heredado reproduce estas ideas en sus líneas 8–33.

### División principal

REL-001, líneas 160–165, divide qalqalah en ṣughrā y kubrā. El documento heredado conserva esa división en sus líneas 37–54.

### Grados

REL-001, líneas 167–173, presenta tres grados:

- Más fuerte: letra detenida con shaddah.
- Intermedio: letra detenida sin shaddah.
- Menor: letra sākinah en posición interna.

El documento heredado reproduce esos grados en sus líneas 164–172.

### Condición de sukūn

REL-001, línea 173, afirma que no hay qalqalah salvo cuando la letra está sākinah. El documento heredado conserva esa condición. Lo que no está validado es su método informático para determinar el sukūn.

## Hallazgos corregidos

### QAL-001 — Referencias de página imprecisas

Las líneas 9, 10 y 15 atribuyen definición y causa a la página 62. En la copia REL-001, la página 62 empieza en la línea 162; la definición, letras y causa aparecen antes, en la página 61, líneas 150–161. Los tipos, ejemplos y grados sí continúan en la página 62.

La especificación futura deberá citar página 61 para definición/causa y página 62 para clases/grados, sujeto a contraste con la edición impresa.

### QAL-002 — Ausencia de vocal no demuestra sukūn

Las líneas 90, 109, 195–197 y 214–217 permiten considerar sākinah cualquier letra “sin harakat vocal”. Esto no es válido como regla Unicode general.

La ausencia de fatḥah, ḍammah o kasrah puede deberse, entre otras causas, a vocalización incompleta, convención editorial, marcas coránicas distintas, composición mediante grafemas o datos defectuosos. El motor deberá distinguir al menos:

- Sukūn explícito del corpus.
- Sukūn contextual producido por waqf.
- Sukūn conocido mediante datos lingüísticos autorizados.
- Estado desconocido.

“No veo una vocal” deberá producir incertidumbre, no qalqalah automática.

### QAL-003 — Waqf no se deduce automáticamente de una marca

Las líneas 69, 73–74, 126–159 y 219–222 tratan la pausa como una propiedad deducible del texto. Waqf es también una decisión o modo de recitación. Una marca puede orientar, pero no demuestra que el lector se detendrá; del mismo modo, puede haber pausa en posiciones que el algoritmo no contempla.

La API futura deberá recibir explícitamente el contexto de recitación, por ejemplo `wasl`, `waqf` o `unknown`, en lugar de inventarlo a partir del texto.

### QAL-004 — U+06D6–U+06ED no es un rango de “marcas de pausa” homogéneo

La línea 220 propone detectar waqf mediante todo el rango U+06D6–U+06ED. Según las tablas oficiales de Unicode, ese intervalo contiene signos coránicos con funciones distintas, entre ellos ligaduras anotativas, fin de āyah, marcas de rubʿ, pequeña mīm, pequeña wāw, pequeña yāʾ y otros signos. No todos significan pausa.

Cada code point deberá modelarse por su nombre y función documentada. Queda prohibido convertir el intervalo completo en un booleano `isWaqf`.

Referencia técnica: <https://unicode.org/charts/nameslist/n_0600.html>.

### QAL-005 — Los supuestos marcadores `ﰀ-ﰘ` no son marcadores Unicode estándar de āyah

La línea 221 utiliza caracteres del rango U+FC00–U+FC18 como marcadores de fin de āyah. Unicode los define dentro de Arabic Presentation Forms-A como ligaduras árabes, no como números de āyah.

El corpus heredado parece depender de una fuente que reasigna visualmente esos code points. Esto no puede trasladarse al nuevo corpus como semántica textual. El número de āyah deberá ser metadato separado y verificable.

### QAL-006 — Falta el caso “final de palabra en waṣl”

El árbol de las líneas 62–79 sólo resuelve:

- Letra interna en waṣl.
- Letra final cuando hay waqf.

No define qué ocurre con una letra de qalqalah que ya es sākinah al final de una palabra cuando la lectura continúa. Independientemente de cuál sea la resolución religiosa correcta, un árbol que no tiene rama para una entrada posible no es completo y debe devolver `unknown`.

Este caso requiere fuente precisa y validación manual del propietario contra el muṣḥaf de referencia.

### QAL-007 — “Sin excepciones” no está demostrado

Las líneas 95–97 y 131–133 declaran que no existen excepciones ni intersecciones relevantes. REL-001 no formula una prueba de exhaustividad con esos términos. La ausencia de una excepción en un resumen no permite afirmar que no existe.

Además, el propio documento reconoce interacción con shaddah, waqf y posición. La futura especificación deberá tratar esas dimensiones como contexto, no como notas laterales.

### QAL-008 — El color está mezclado con la detección

Las líneas 71–78, 93, 112, 129, 148, 153, 199–207 y 228–231 incorporan `#00BFFF` dentro del algoritmo. El color no forma parte de la regla religiosa y no debe aparecer en la salida normativa del detector.

El motor devolverá una anotación semántica; la aplicación decidirá cómo representarla de forma accesible. Cambiar una paleta nunca podrá cambiar la detección.

### QAL-009 — Los criterios de éxito incluyen presentación, pero omiten integridad y trazabilidad

Las líneas 263–273 consideran éxito aplicar un color y un nivel de intensidad, pero no exigen:

- Fuente y página en el resultado.
- Modo waṣl/waqf explícito.
- Conservación exacta de code points.
- Estado de incertidumbre.
- Casos negativos.
- Corpus identificado.
- Revisión humana.

Por tanto, esos criterios no pueden adoptarse en e-tajweed.

### QAL-010 — Las frecuencias no validan qalqalah

Las líneas 23–29 importan frecuencias globales de letras. Contar qāf, ṭāʾ, bāʾ, jīm o dāl no cuenta qalqalah: la regla depende de sukūn y contexto. Las cifras deberán eliminarse de la especificación normativa o presentarse únicamente como estadísticas de un corpus versionado.

### QAL-011 — La copia REL-001 contiene una frase que necesita verificación material

REL-001, línea 172, describe el grado menor mediante una letra en medio de palabra pero conserva la expresión `الوقف على القاف` en el ejemplo `وخلقناكم`. El documento heredado elimina silenciosamente esa tensión y presenta el ejemplo como interno.

Puede tratarse de un error de transcripción, de redacción del original o de una interpretación que requiere contexto. Debe comprobarse la página física 62 y el muṣḥaf certificado; no se corregirá de memoria.

## Modelo mínimo aplicado en la corrección

La futura especificación candidata deberá separar:

```text
identidad de la letra
  + estado de sukūn demostrado
  + posición lingüística
  + modo de recitación: wasl | waqf | unknown
  + presencia de shaddah
  → categoría candidata
  → grado candidato
  → evidencia
  → estado de revisión
```

La salida no contendrá colores. Si el modo de recitación o el sukūn no pueden determinarse, el resultado será `unknown` o `requires_review`.

## Casos que el documento corregido incluye para validación

- Cada una de las cinco letras de `قطب جد` en estado sākinah demostrado.
- Las mismas letras con vocal: resultado negativo.
- Posición interna.
- Final de palabra en waṣl.
- Final de palabra en waqf.
- Final con shaddah en waqf.
- Texto sin vocalización suficiente: incertidumbre.
- Marcas coránicas próximas que no significan waqf.
- Corpus con número de āyah almacenado como metadato, no como ligadura U+FCxx.
- Reconstrucción exacta del texto tras retirar la anotación.

## Decisión de migración

- Conservar una copia privada intacta como custodia histórica.
- Migrar el archivo con su nombre original.
- Corregir el pseudocódigo inseguro en el propio documento.
- Separar los colores de la decisión religiosa.
- Validar manualmente los resultados durante el desarrollo.
- Reservar la revisión del qāriʾ o especialista para la aprobación final de la aplicación.

## Próximo documento

La revisión documental de Qalqalah está cerrada. Según el orden aprobado, la próxima sesión podrá continuar con `DECISION_LOGIC_NUUN_TANWEEN.md` contra la Parte 7.
