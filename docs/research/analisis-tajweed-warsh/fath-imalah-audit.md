# Auditoría de `DECISION_LOGIC_FATH_IMALAH.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_FATH_IMALAH.md`
- **SHA-256:** `95ecb58ffc913d675061b7dda49044cefb30e90b4c1ddc6c2585ac5a38e24829`
- **Estado:** `rejected`
- **Decisión:** rechazado como guía directa de implementación; conserva un inventario amplio de REL-001, pero su orden de evaluación contradice reglas y excepciones que el mismo documento registra.
- **Fuente local contrastada:** REL-001 / `parte10.md`.

> **Actualización tras la corrección del archivo migrado:** `rejected` describe el **original heredado** (SHA-256 indicado arriba), no la versión ahora corregida de `DECISION_LOGIC_FATH_IMALAH.md`. Los hallazgos FIM-001–022 se atendieron allí con comentarios de revisión, precedencia explícita, salidas de incertidumbre y rasm inmutable. Estado del documento corregido: `corrected` contra pp. 97–101; faltan la validación de ocurrencias dentro de la verificación exhaustiva previa al motor, la decisión de presentación porque la paleta no asigna color propio a fatḥ/imālah y el aval final del especialista. Este informe se conserva como historial, no como nueva especificación.

## Veredicto

El documento recoge muchas categorías, ejemplos y awjuh de la Parte 10. Su algoritmo, sin embargo, retorna una decisión por tipo de alif antes de consultar casos especiales y antes de resolver iltiqāʾ al-sākinayn. Como consecuencia, puede conceder imālah en waṣl donde la fuente la elimina fonéticamente y puede ocultar excepciones específicas.

También intenta inferir origen etimológico, función morfológica, caso gramatical, finales de āyah y tipos de pronombre sin definir los datos necesarios. Las comparaciones por palabra vocalizada no coinciden de forma estable con el rasm del corpus heredado.

La parte religiosa continúa pendiente de validación por un profesor, qāriʾ o especialista cualificado. Los awjuh deberán conservarse como alternativas estructuradas y correlacionadas, no como strings.

## Elementos respaldados provisionalmente por REL-001

### Definiciones y grados

REL-001, líneas 13–39, respalda provisionalmente las definiciones de fatḥ, imālah kubrā e imālah ṣughrā/taqlīl. También atribuye a Warsh la imālah kubrā únicamente en la hāʾ de `طَهَ` “según lo conocido” y presenta el resto del capítulo como detalle de taqlīl.

La expresión `على المشهور` debe conservar su matiz. No se transformará en una afirmación absoluta sin contrastar las autoridades de la ṭarīq seleccionada.

### Categorías de alif terminal

REL-001, líneas 41–70, respalda provisionalmente las categorías de:

- Alif terminal procedente de yāʾ.
- Alif terminal escrita como yāʾ en nombres no árabes.
- Alif terminal procedente de wāw y escrita como yāʾ.
- Alif de origen desconocido.
- Alif terminal añadida para femenino y sus cinco patrones.

También respalda las condiciones generales, excepciones y relación con ruʾūs al-āy que el documento inventaría.

### Alif medial seguida de rāʾ terminal

REL-001, líneas 72–85, respalda provisionalmente la condición principal, los dos lugares de `الْجَارِ`, los ejemplos de kasrah original y los casos negativos enumerados.

Esta sección depende de iʿrāb, morfología y estructura de palabra; no puede resolverse mediante búsqueda de caracteres.

### Casos especiales e iltiqāʾ al-sākinayn

REL-001, líneas 86–102, respalda provisionalmente los casos especiales citados, la interacción de `رَأَىٰ` con badal y pronombres, y la supresión fonética de imālah cuando el alif no se pronuncia en waṣl por encuentro de dos sākin.

La fuente aclara expresamente que el alif permanece en el rasm. Ningún algoritmo puede borrarlo del texto fuente.

## Hallazgos bloqueantes

### FIM-001 — Iltiqāʾ al-sākinayn se evalúa después de retornos definitivos

`aplicar_regla_imalah`, líneas 359–432, retorna dentro de casi cada caso de `tipo_alif`. La comprobación de iltiqāʾ al-sākinayn no aparece hasta las líneas 426–428, cuando la mayoría de las entradas ya han salido de la función.

Ejemplos afectados por el propio documento:

- `مُوسَى الْكِتَابَ` puede devolver dos awjuh en la línea 385 antes de que se suprima imālah en waṣl.
- `هُدَى اللَّهِ` puede devolver dos awjuh en la línea 382 antes de comprobar el encuentro.
- `الْقُرَى الَّتِي` puede devolver taqlīl en la línea 372 antes de aplicar la supresión de waṣl.

REL-001, líneas 96–102, exige lo contrario en waṣl. La precedencia debe situar el contexto fonético antes de la salida final.

### FIM-002 — Los casos especiales también quedan detrás de retornos generales

`verificar_casos_especiales` sólo se llama en las líneas 421–424, después de la clasificación por tipo. `رَأَىٰ`, por ejemplo, encaja antes como alif terminal con rāʾ y puede retornar taqlīl en las líneas 370–372, sin alcanzar las condiciones de pronombre, badal o siguiente sākin de las líneas 463–471.

Una excepción específica debe evaluarse antes o formar parte de una resolución declarativa de precedencias. Añadirla al final no la hace ejecutable.

### FIM-003 — `ذِكْرَاهَا` es inalcanzable incluso dentro de su propia rama

En las líneas 374–380, el algoritmo comprueba primero si existe hāʾ de femenino y retorna `وجهان` en la línea 376. La excepción `ذِكْرَاهَا` sólo se comprueba después, en las líneas 377–378.

REL-001, línea 45, le asigna taqlīl únicamente por pertenecer a dhawāt al-rāʾ. El algoritmo devolvería el resultado general contrario antes de leer la excepción.

### FIM-004 — El caso de alif medial tiene un fallback que concede taqlīl sin demostrar la condición

Las líneas 411–419 comprueban si la kasrah de rāʾ no es de iʿrāb y rechazan cuatro palabras conocidas. Para cualquier otra entrada no reconocida, la función continúa y retorna taqlīl de un solo wajh en la línea 419.

La falta de coincidencia con una lista negativa no demuestra kasrah de iʿrāb ni kasrah original autorizada. Debe producir `unknown` o exigir un análisis gramatical positivo.

### FIM-005 — La función usa contexto que no recibe

`aplicar_regla_imalah(palabra, contexto)` y `verificar_casos_especiales(palabra)` consultan variables como:

- `letra`, `sura`, `aya` y `raíz`.
- Caso nominativo/acusativo/genitivo.
- Tipo de pronombre.
- Presencia de siguiente sākin.
- Waṣl/waqf.
- Fin de āyah y pertenencia a una de once suras.

Esos datos no forman parte de los parámetros ni de un contrato de contexto definido. El pseudocódigo no es ejecutable ni reproducible.

### FIM-006 — Los awjuh de badal se devuelven como texto libre

Las líneas 281–285, 294–295 y 463–468 resumen `رَأَىٰ` como taqlīl de rāʾ y hamzah con tres awjuh de badal. El resultado es un string que no identifica cada longitud, su evidencia ni sus condiciones de compatibilidad.

Los tres awjuh deberán ser alternativas tipadas y correlacionadas con la realización de imālah, sin permitir combinaciones inventadas por la interfaz.

### FIM-007 — “Eliminar el alif” debe limitarse al plano fonético

Las líneas 307–311 y 489–492 dicen que el alif se elimina por iltiqāʾ al-sākinayn. REL-001, línea 96, aclara que se elimina en la pronunciación durante waṣl pero permanece en el rasm.

La implementación no borrará, sustituirá ni ocultará silenciosamente el code point fuente. Emitirá una anotación de realización fonética ligada al modo de recitación.

### FIM-008 — Las comparaciones por string no son compatibles con el corpus

Las líneas 362, 377, 388, 400, 413, 416, 443, 447, 460 y 474 comparan formas totalmente vocalizadas. El corpus heredado usa rasm y signos magrebíes distintos. Por ejemplo:

- `مُوسَىٰ` aparece como `مُوس۪ىٰ`.
- `رَأَىٰ` aparece como `ر۪ء۪ا` en una de las ocurrencias inspeccionadas.
- Otras formas emplean alif pequeña, signos bajos y composiciones diferentes.

Las reglas deberán anclarse a tokens u ocurrencias verificadas mediante identificadores estables. No se normalizará destructivamente el texto para forzar igualdad.

### FIM-009 — El origen del alif no puede inferirse sólo de su glifo

`identificar_tipo_alif(palabra)` debe distinguir alif procedente de yāʾ, de wāw, de origen desconocido, añadida para femenino y escrita como yāʾ en nombre extranjero. Es una clasificación etimológica y morfológica, no una propiedad suficiente de U+0649/U+0670.

La función no define fuente, diccionario, versión ni estado de incertidumbre. Ese conocimiento deberá ser un dataset citado y revisado.

### FIM-010 — Hāʾ de femenino no equivale a “la palabra contiene hāʾ”

Las ramas de ruʾūs al-āy dependen de `هاء التأنيث`, una función morfológica. El documento no diferencia hāʾ de femenino, pronombre sufijado u otra hāʾ léxica.

La decisión requiere análisis aprobado del token y no puede deducirse mediante presencia del carácter ه.

### FIM-011 — “Palabra tiene rāʾ” es una condición insuficientemente definida

Las líneas 58–64, 80–82, 122, 130, 137, 203 y 405–409 usan `ذوات الراء` como si fuera una búsqueda simple. La fuente distingue categorías y posiciones concretas; el documento no define si rāʾ debe pertenecer a la raíz, preceder inmediatamente al alif o cumplir otra relación.

La especificación futura deberá formalizar cada uso con ejemplos positivos y negativos aprobados.

### FIM-012 — Ruʾūs al-āy necesita metadatos, no una inspección visual

Las líneas 60–64, 70–73, 128–138, 160–165 y 374–395 dependen de si la ocurrencia es final de āyah y de una lista de once suras. No definen:

- Edición y sistema de numeración.
- Identificador exacto de la ocurrencia.
- Cómo se reconoce el final.
- Cómo se trata una palabra idéntica fuera del final.

No se usarán las ligaduras U+FCxx del corpus heredado como semántica de fin de āyah. La posición será metadato verificado.

### FIM-013 — Una misma palabra puede cambiar según su ocurrencia

Formas como `الْعُلَىٰ` aparecen en la regla general de dos awjuh y también como ejemplos de ruʾūs al-āy con taqlīl único. Por tanto, la palabra escrita no identifica la regla completa.

La clave mínima necesita sura, āyah, token, posición y modo de recitación. Una whitelist por texto sería ambigua.

### FIM-014 — La tabla de iltiqāʾ deja una salida incompleta

La línea 328 asigna `-` a la columna de waqf para `نَرَى اللَّهَ`, aunque la regla general del propio documento dice que al detenerse sobre el alif se aplica la regla original de la palabra. La ausencia de valor no puede interpretarse como “sin imālah”, “no aplicable” o “dato pendiente”.

La futura evidencia deberá usar estados explícitos y no guiones ambiguos.

### FIM-015 — La función auxiliar puede terminar sin resultado

`aplicar_regla_iltiqaa_sakinayn`, líneas 487–498, no devuelve nada para waṣl sin encuentro ni para un modo desconocido. La función principal termina además con `RETORNAR resultado` en la línea 430 sin haber inicializado `resultado`.

Esto impide distinguir caso no aplicable, contexto insuficiente y error de modelado.

### FIM-016 — La imālah kubrā se presenta con más certeza que la fuente

REL-001, línea 33, limita la afirmación sobre la hāʾ de `طَهَ` mediante `على المشهور`. El legado usa “única”, “solo” y “no existe” en las líneas 33–38, 539–541 y 579.

La futura especificación conservará el método, la autoridad y el grado de certeza exacto de la fuente. El especialista deberá confirmar el alcance para Warsh por ṭarīq al-Azraq.

### FIM-017 — El inventario de letras iniciales no se implementa de forma simétrica

REL-001, línea 88, enumera `ح، ر، ي، هـ`, con excepciones para hāʾ de `طَهَ` y yāʾ de `يس`. La función de las líneas 450–457 implementa ramas para ḥāʾ/rāʾ, yāʾ de Yā-Sīn y hāʾ fuera de Ṭā-Hā, pero no ofrece un modelo general de cada ocurrencia de fawātiḥ ni sus nombres recitados.

Una letra aislada de apertura no se procesará como un carácter ordinario sin contexto de sura y realización.

### FIM-018 — El recuento de “cuatro palabras” contiene cinco entradas

El encabezado de la línea 505 anuncia cuatro palabras con fatḥ único, pero las líneas 507–511 enumeran cinco al añadir `زَكَا`. El resumen de la línea 582 habla correctamente de cinco.

Este desajuste muestra que los conteos manuales no son una fuente fiable. Deben distinguirse categoría, lexema y ocurrencia.

### FIM-019 — “Once suras con finales imālados” puede sobregeneralizar

Las líneas 547–561 cuentan once suras, pero la regla de REL-001 se refiere a las palabras pertinentes que aparecen en ruʾūs al-āy bajo condiciones concretas, con excepción por hāʾ de femenino. No afirma que todo final de āyah de esas suras lleve automáticamente imālah.

La lista de suras es una condición contextual, no un detector suficiente.

### FIM-020 — “Intersecciones: ninguna” contradice el resto del documento

Varias tablas declaran ausencia de intersecciones, aunque las decisiones dependen de morfología, iʿrāb, rāʾ, hāʾ de femenino, ruʾūs al-āy, badal, pronombres y waṣl/waqf. La propia matriz final reconoce algunas de ellas.

La futura matriz deberá enumerar precedencias y compatibilidades de manera completa.

### FIM-021 — “Lista completa” y sumas no prueban exhaustividad

Las líneas 503–571 presentan listas y recuentos como verificación. Contar once suras o cinco patrones no valida cada ocurrencia, excepción, lectura permitida ni prioridad.

La exhaustividad sólo podrá afirmarse tras contrastar fuentes autorizadas, corpus completo, golden tests y revisión experta.

### FIM-022 — El resumen “taqlīl para todo el resto” es ambiguo

La línea 580 puede leerse como si toda palabra distinta de hāʾ de `طَهَ` recibiera taqlīl, aunque el mismo documento contiene fatḥ único y ausencia de imālah. Si pretende decir que toda imālah de Warsh fuera de ese caso es ṣughrā, deberá redactarse así de forma inequívoca.

La ambigüedad no puede trasladarse a una especificación normativa.

## Modelo mínimo que deberá reemplazarlo

La futura especificación deberá representar:

```text
token coránico inmutable + ocurrencia verificada
  + clasificación morfológica/etimológica versionada
  + función gramatical y tipo de sufijo
  + posición dentro de la palabra
  + metadatos de sura, ayah y ras al-ayah
  + modo: wasl | waqf | unknown
  + siguiente unidad pronunciada
  + interacciones: badal | fath | taqlil | imalah kubra
  → conjunto correlacionado de awjuh
  → preferencia y autoridad
  → evidencia por cada alternativa
  → estado de revisión humana
```

La resolución de iltiqāʾ al-sākinayn deberá preceder a la realización final. Ningún resultado cambiará el rasm almacenado.

## Casos que la nueva especificación deberá incluir

- Cada categoría de alif terminal con positivos, negativos y entradas ambiguas.
- Dhawāt al-rāʾ y no-dhawāt al-rāʾ con definición formal.
- Cada palabra pertinente en ruʾūs al-āy y fuera de esa posición.
- Hāʾ de femenino frente a hāʾ pronominal o léxica.
- Los nombres no árabes citados con sus grafías reales del corpus.
- `ذِكْرَاهَا` para demostrar precedencia sobre la regla general.
- Los cinco patrones de alif de femenino.
- Kasrah de iʿrāb, kasrah original y kasrah por otras causas.
- Los dos lugares de `الْجَارِ` en al-Nisāʾ 4:36.
- Cada caso negativo citado por REL-001.
- Fawātiḥ al-suwar como unidades recitadas, no caracteres aislados.
- `رَأَىٰ` sola, con cada tipo de pronombre, con tāʾ de femenino y ante sākin.
- Los tres awjuh de badal como alternativas estructuradas.
- Cada ejemplo de iltiqāʾ al-sākinayn en waṣl y waqf.
- Prueba de que el alif permanece exactamente en el texto fuente.
- Formas con U+06EA y convenciones editoriales alternativas.

## Decisión de migración

- Conservar el archivo original como legado y catálogo provisional.
- No migrar su algoritmo ni el orden actual de retornos.
- Recuperar cada afirmación respaldada en especificaciones pequeñas y trazables.
- Modelar origen del alif, iʿrāb, sufijos y ruʾūs al-āy como datos versionados.
- Representar badal e imālah mediante awjuh correlacionados.
- Aplicar primero el contexto de waṣl/waqf y sólo después resolver la realización.
- Mantener toda conclusión religiosa como candidata hasta revisión del especialista.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_MUDUD.md` contra la Parte 11.
