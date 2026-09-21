# Auditoría de `DECISION_LOGIC_IDGHAM.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_IDGHAM.md`
- **SHA-256:** `53bd499c5d4e45fe4bc19723751376f08b075bbd88b3b94eab9e745f44f0f055`
- **Estado:** `rejected`
- **Decisión:** rechazado como guía directa de implementación; las listas respaldadas por REL-001 deberán convertirse en reglas candidatas de alcance explícito.
- **Fuente local contrastada:** REL-001 / `parte9 .md`.

## Veredicto

El documento reproduce gran parte de la clasificación y de los pares concretos expuestos en la Parte 9. Sin embargo, presenta como exhaustivos varios ejemplos que la fuente introduce sólo con `مثل`, omite el modo waṣl/waqf, no implementa realmente idghām kabīr y usa un clasificador general que invade otras reglas de tajwīd.

La identificación de lām al-taʿrīf tampoco es segura: observar una lām y la letra siguiente no demuestra que se trate del artículo definido. Las comparaciones de letras no resuelven hamzah/alif, marcas combinantes ni convenciones distintas de rasm.

La parte religiosa continúa pendiente de validación por un profesor, qāriʾ o especialista cualificado. Las listas son candidatas respaldadas por REL-001, no reglas aprobadas.

## Elementos respaldados provisionalmente por REL-001

### Definición y división inicial

REL-001, líneas 13–31, respalda provisionalmente la definición de idghām y su división pedagógica en kabīr y ṣaghīr. También indica que los ejemplos generales de kabīr pertenecen a al-Sūsī y que Warsh sólo lo presenta en ciertas palabras cuyo origen ya contiene asimilación.

El documento heredado recoge esa distinción en sus líneas 8–44, pero transforma ejemplos no exhaustivos en una lista cerrada.

### Causas y clases de idghām ṣaghīr

REL-001, líneas 33–50, define tamāthul, tajānus y taqārub y presenta las clases mutamāthilayn, mutajānisayn y mutaqāribayn. El documento conserva estas categorías y la mayoría de los ejemplos.

La definición de una relación fonética no basta para deducir que todo par relacionado se asimila. REL-001, líneas 69–71, advierte expresamente que no todo par próximo lo hace y limita la regla a lo transmitido de los recitadores.

### Pares concretos

REL-001, líneas 50–90, respalda provisionalmente los pares enumerados para mutajānisayn y mutaqāribayn, incluida:

- La conservación de iṭbāq e istiʿlāʾ en ṭāʾ → tāʾ.
- La limitación de dhāl → tāʾ a formas derivadas de `الأخذ` y `الاتخاذ`.
- Los dos awjuh de qāf → kāf.
- La conservación de istiʿlāʾ en el wajh incompleto de qāf → kāf.

Estos datos deberán modelarse como pares transmitidos y excepciones versionadas, no inferirse sólo de una matriz de makhārij y ṣifāt.

### Lām al-taʿrīf

REL-001, líneas 92–103, añade al capítulo la división qamariyyah/shamsiyyah y las dos listas de catorce letras. El documento heredado reproduce provisionalmente esas listas.

La regla presupone que la lām ya ha sido identificada como lām del artículo definido. Esa precondición falta en el algoritmo heredado.

## Hallazgos bloqueantes

### IDG-001 — Dos ejemplos de idghām kabīr se convierten en una lista exclusiva

REL-001, línea 27, dice que Warsh lo presenta en “algunas palabras” y utiliza `مثل` antes de `تَأْمَنَّا` y `فَنِعِمَّا`. El documento heredado cambia ese alcance a “solo” en las líneas 25, 459–463 y 505.

Una fuente que aporta ejemplos no demuestra que no existan otros. Hasta contrastar fuentes autorizadas y el corpus completo, esos dos casos deben registrarse como ejemplos citados, no como lista exhaustiva.

### IDG-002 — El supuesto algoritmo general no implementa idghām kabīr

`aplicar_regla_idgham`, líneas 309–331, rechaza toda entrada cuya primera letra no sea sākinah. Esa es precisamente la condición de idghām ṣaghīr. No existe una función que modele las dos letras originalmente vocalizadas de idghām kabīr ni los casos atribuidos a Warsh.

Por tanto, el resumen declara un tipo que el “algoritmo completo” no puede procesar.

### IDG-003 — Falta el contexto general de waṣl y waqf

Muchos ejemplos cruzan una frontera de palabra, como `قَد دَّخَلُوا` y `بَل رَّانَ`. La asimilación presupone continuidad de lectura; si el lector se detiene al final de la primera palabra, la segunda letra no se alcanza en el mismo contexto fonético.

Ninguna función recibe `wasl`, `waqf` o `unknown`. El motor futuro deberá hacer explícito el modo y devolver incertidumbre cuando no se conozca.

### IDG-004 — El fallback “iẓhār” invade otras reglas

Las líneas 328–329 y numerosos fallbacks de las funciones especializadas devuelven iẓhār para cualquier par no reconocido. Pero la ausencia de una regla en este capítulo no demuestra iẓhār global.

Por ejemplo, un par puede pertenecer a nūn sākinah/tanwīn, mīm sākinah, iqlāb, ikhfāʾ o a otro módulo especializado. El alcance correcto del detector es:

- Coincidencia con un par de idghām aprobado.
- Coincidencia negativa dentro de una regla cuya fuente prescribe iẓhār.
- `not_applicable` para entradas fuera de este dominio.
- `unknown` para contexto insuficiente.

### IDG-005 — El clasificador genérico pierde parte de su propia definición de tajānus

REL-001, línea 39, define tajānus como coincidencia de makhraj con diferencia de ṣifah, **o lo contrario**. El diagrama heredado menciona ambas posibilidades en la línea 31, pero la línea 55 y el algoritmo de las líneas 322–323 sólo comprueban “mismo makhraj y distinta ṣifah”.

La mitad alternativa de la definición desaparece de la implementación. Aun corrigiéndola, los pares normativos deberán proceder de una lista transmitida, no de una inferencia automática sobre cualquier par.

### IDG-006 — “Todo mutamāthil se asimila siempre” no está demostrado

Las líneas 123–131 y 506 afirman aplicación universal, ausencia de excepciones y resultado siempre completo. REL-001 define la clase y ofrece ejemplos, pero no presenta en ese pasaje una prueba de exhaustividad con esas palabras.

Además, los pares idénticos de nūn y mīm pueden tener propiedades especializadas, como ghunnah, que un resultado genérico de “idghām completo” perdería. La precedencia y las características deberán definirse entre módulos.

### IDG-007 — El documento niega intersecciones que sí existen en su propio alcance

Las líneas 130, 170, 222, 288 y 294–302 declaran reglas independientes o sin intersecciones. Sin embargo:

- Nūn+nūn y mīm+mīm son también pares idénticos cubiertos por reglas especializadas.
- Lām shamsiyyah es una forma de idghām incluida en el mismo documento.
- Los casos de qāf → kāf tienen dos awjuh.
- Dhāl → tāʾ necesita morfología.
- Toda relación entre palabras depende de waṣl/waqf.

La ausencia de intersecciones no puede mantenerse como conclusión.

### IDG-008 — La morfología se usa mediante una variable inexistente

`aplicar_idgham_mutaqarib(letra1, letra2)`, líneas 381–425, consulta `raíz_morfológica` en la línea 402 sin recibir palabra, token, análisis morfológico ni contexto. La función no puede evaluar esa condición.

La nueva arquitectura deberá enlazar el par a un token u ocurrencia analizada y aportar evidencia del lema o raíz, con capacidad de devolver `requires_review`.

### IDG-009 — No es la única regla del documento que depende de morfología

Las líneas 204 y 480 afirman que dhāl → tāʾ es la única regla dependiente de raíz morfológica. Pero identificar lām al-taʿrīf exige distinguir el artículo definido de otras lāmāt, y explicar las formas originales de `تَأْمَنَّا` y `فَنِعِمَّا` también usa análisis de forma/origen.

La afirmación de unicidad no está demostrada y es internamente incompatible con el alcance del propio archivo.

### IDG-010 — Lām al-taʿrīf se clasifica sin verificar que exista artículo

`aplicar_regla_lam_tarif` recibe únicamente `letra_después_de_lam`. No recibe la lām, su sukūn, el token ni una prueba de que la secuencia sea el artículo `ال`.

Aplicar las listas de letras a cualquier lām seguida de otra letra generaría falsos positivos. La identificación morfológica/ortográfica del artículo es una precondición obligatoria.

### IDG-011 — Hamzah y alif no tienen una política Unicode

La lista qamariyyah usa `ا`, mientras ejemplos como `الْأَرْض` pueden contener `أ` U+0623 en una edición. El corpus heredado usa además convenciones magrebíes distintas, como `اَ۬لَارْض`, con signos y composición propios.

Una comparación directa de code points puede clasificar la misma palabra de forma diferente según la edición. La capa analítica deberá reconocer la identidad lingüística sin sustituir ni normalizar destructivamente el texto fuente.

### IDG-012 — “Primera sākinah” no equivale a U+0652 visible

Los fenómenos de idghām pueden representarse omitiendo el sukūn de la primera letra y colocando shaddah sobre la segunda. En el corpus heredado, por ejemplo, `بَل رَّانَ` no muestra U+0652 sobre la lām y `أَلَمْ نَخْلُقكُّم` conserva una convención gráfica específica.

La función no define si `es ساكنة` procede de la escritura, del análisis lingüístico o del estado fonético. No podrá deducirse simplemente de la presencia o ausencia de una marca.

### IDG-013 — La shaddah es evidencia editorial, no la definición del fenómeno

La definición pedagógica habla de una letra resultante mushaddadah, pero U+0651 puede omitirse, añadirse o usarse en otros contextos según la edición. Tampoco demuestra por sí sola qué primera letra se asimiló.

El motor deberá detectar la relación mediante datos lingüísticos aprobados y usar la shaddah como control de consistencia del corpus identificado.

### IDG-014 — Las salidas transformadas amenazan la integridad del texto

Las líneas 99, 217, 419 y 471–472 representan los dos awjuh de qāf → kāf mediante formas como `نَخْلُكُّم` y `نَخْلُقكُّم`. Estas formas pueden servir como notación pedagógica de pronunciación, pero no autorizan a borrar qāf ni a reescribir el token del corpus.

Cada wajh deberá ser una anotación fonética no destructiva sobre el mismo intervalo de texto.

### IDG-015 — Los dos awjuh de qāf → kāf necesitan estructura, no una cadena

La línea 419 devuelve ambos awjuh dentro de un único string. No identifica:

- Qué rasgo permanece en el idghām incompleto.
- Si existe preferencia declarada.
- La evidencia de cada wajh.
- El método o restricciones de compatibilidad.
- El estado de aprobación humana.

La salida deberá ser un conjunto de alternativas tipadas, nunca texto libre que la interfaz tenga que reinterpretar.

### IDG-016 — “Letra siguiente” ignora grafemas, signos y fronteras

Las funciones reciben letras abstractas sin definir cómo atravesar harakāt, shaddah, sukūn, espacios, signos coránicos, fin de āyah o hamzat al-waṣl. Un índice UTF-16 no equivale a una letra pronunciada.

La tokenización deberá conservar todos los code points, identificar letras base y registrar cada frontera atravesada.

### IDG-017 — Las categorías fonéticas no tienen datos versionados

`mismo_مخرج`, `diferente_صفة` y `próximos` se invocan como funciones, pero el documento no define matrices, fuentes, versiones ni cómo resolver desacuerdos de clasificación. Cambiar esa tabla podría cambiar resultados religiosos sin dejar rastro.

Los makhārij y ṣifāt deberán ser conocimiento versionado, citado y revisado, separado del código de control.

### IDG-018 — La partición 14 + 14 no valida lām al-taʿrīf

Las líneas 484–497 sólo verifican que dos listas pedagógicas sumen 28. No prueban que el token sea un artículo, que hamzah/alif se haya resuelto correctamente, que la letra siguiente se haya localizado ni que la lectura esté en waṣl.

La “verificación matemática” no puede sustituir pruebas sobre el corpus.

### IDG-019 — Lo desconocido se presenta como error del texto

Las líneas 447–448 devuelven `ERROR: letra no clasificada`. Una entrada puede usar una forma Unicode distinta, estar incompleta o quedar fuera del corpus aprobado. El resultado correcto debe ser `unknown`, `unsupported_input` o `requires_review`, con una razón trazable.

### IDG-020 — “Lista completa” y “única excepción” exceden la fuente

Las líneas 455 y 480 usan etiquetas de completitud que REL-001 no demuestra. El propio uso de `مثل` para idghām kabīr contradice la exhaustividad de una parte de la lista.

No se declarará completitud hasta contrastar fuentes autorizadas, todas las ocurrencias del corpus y la revisión del especialista.

## Modelo mínimo que deberá reemplazarlo

La futura especificación candidata deberá separar:

```text
texto coránico inmutable + token/ocurrencia
  + primera y segunda unidad fonética
  + estado ortográfico y estado recitado
  + frontera: interna | entre palabras | fin de ayah | unknown
  + modo: wasl | waqf | unknown
  + dominio especializado de la regla
  + par transmitido y evidencia
  + análisis morfológico, cuando corresponda
  → clase candidata
  → conjunto de awjuh
  → rasgos conservados por cada wajh
  → evidencia y estado de revisión
```

Los pares enumerados tendrán prioridad explícita. La falta de coincidencia en este módulo devolverá `not_applicable`, no iẓhār global.

## Casos que la nueva especificación deberá incluir

- Cada ejemplo de mutamāthilayn de REL-001, con caso negativo comparable.
- Nūn+nūn y mīm+mīm para comprobar la precedencia de reglas especializadas.
- Cada par enumerado de mutajānisayn y mutaqāribayn.
- Ṭāʾ → tāʾ conservando exactamente los rasgos documentados.
- Dhāl → tāʾ dentro y fuera de las familias `الأخذ`/`الاتخاذ`.
- Qāf → kāf con ambos awjuh como alternativas separadas.
- Pares fonéticamente próximos no transmitidos: resultado negativo dentro del dominio.
- Cruces de palabra en waṣl y en waqf.
- Idghām sin sukūn visible en la primera letra.
- Shaddah presente, ausente y perteneciente a otro fenómeno.
- Los casos citados de idghām kabīr, sin afirmar exhaustividad.
- Lām al-taʿrīf ante las 14 letras qamariyyah y las 14 shamsiyyah.
- Una lām que no sea artículo ante las mismas letras: no aplicar la regla.
- Hamzah/alif en distintas representaciones Unicode aprobadas.
- Reconstrucción exacta del texto al retirar anotaciones.

## Decisión de migración

- Conservar el archivo original como legado.
- No migrar sus algoritmos genéricos ni sus fallbacks de iẓhār.
- Recuperar los pares y ejemplos respaldados como candidatos individuales.
- No tratar los dos ejemplos de idghām kabīr como lista exhaustiva.
- Separar lām al-taʿrīf en una especificación con precondición morfológica propia.
- Representar los awjuh de qāf → kāf sin modificar el texto.
- Mantener toda conclusión religiosa como candidata hasta revisión del especialista.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_FATH_IMALAH.md` contra la Parte 10.
