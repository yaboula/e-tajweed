# Auditoría de `DECISION_LOGIC_MUDUD.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_MUDUD.md`
- **SHA-256:** `a0949ddd6474e3593bdb6fc70a634a5f497465d37ff440ec4c248002e5cecaa9`
- **Estado:** `rejected`
- **Decisión:** rechazado como guía directa de implementación; las categorías respaldadas por REL-001 requieren un modelo por ocurrencia de madd y por configuración de lectura.
- **Fuente local contrastada:** REL-001 / `parte 11.md`.

## Veredicto

El documento recoge una cantidad importante de la Parte 11: clases de madd, duraciones, excepciones y algunas matrices de compatibilidad. Sin embargo, su algoritmo pierde varios de esos mismos datos al resolverlos: borra excepciones de badal, elimina un wajh de ʿayn, no retorna correctamente madd al-layn y hace inalcanzables ramas de hamzat al-waṣl.

También trata una palabra completa como si tuviera un único madd ganador, aunque puede contener varios intervalos independientes. Las duraciones de Warsh y sus combinaciones necesitan un perfil de lectura coherente, no elecciones locales libres.

La parte religiosa continúa pendiente de validación por un profesor, qāriʾ o especialista cualificado. Las duraciones son unidades relativas de ḥarakāt, no tiempos absolutos.

## Elementos respaldados provisionalmente por REL-001

### Definición y letras de madd

REL-001, líneas 11–28, respalda provisionalmente la definición y las tres letras de madd bajo sus condiciones vocálicas. El documento heredado conserva ese núcleo en sus líneas 8–20.

Estas condiciones son lingüísticas. No equivalen a exigir un sukūn U+0652 visible ni a tomar el siguiente índice UTF-16.

### Grupos por duración

REL-001, líneas 22–129, respalda provisionalmente los grupos pedagógicos de dos, seis y duración variable, junto con las categorías y excepciones enumeradas. El documento reproduce gran parte de ese inventario.

La categoría por duración no sustituye la causa, el intervalo afectado, el modo waṣl/waqf ni las compatibilidades con otras elecciones.

### Layn, badal y combinaciones

REL-001, líneas 106–177, respalda provisionalmente:

- Los tres niveles de madd ʿāriḍ li-l-sukūn y su matriz con badal.
- La definición y excepciones citadas de badal.
- Layn en waqf y layn ante hamzah.
- La discusión de `سَوْءَاتٍ` y los cuatro awjuh atribuidos a la posición de Ibn al-Jazarī.
- El orden pedagógico de causas más fuertes y los ejemplos combinados.

La futura especificación deberá preservar alternativas, autoridad y compatibilidad, no convertirlas en una única cifra prematura.

## Hallazgos bloqueantes

### MUD-001 — Las excepciones de badal vuelven a convertirse en `2/4/6`

Las líneas 470–475 agregan correctamente `بدل - 2 فقط` cuando detectan una excepción. Sin embargo, las líneas 505–506 sólo comprueban si la lista contiene badal y retornan `2/4/6` para cualquier caso.

La comprobación posterior de “casos especiales 2” en las líneas 508–510 es inalcanzable porque la función ya retornó. Las seis categorías de excepción que el documento inventaría no sobreviven a su algoritmo.

### MUD-002 — El wajh de cuatro ḥarakāt de ʿayn se elimina

Las líneas 443–444 agregan `لازم حرفي مخفف - 4/6` para ʿayn, con seis preferido. Después, las líneas 489–491 reducen cualquier entrada que contenga lāzim a `6`.

REL-001, línea 98, conserva ambos awjuh. Una preferencia no permite borrar la alternativa de cuatro.

### MUD-003 — Madd al-layn no tiene resolución en la fase de prioridad

Las líneas 477–487 detectan layn ante hamzah como `4/6` y layn en waqf como `2/4/6`. La fase de salida de las líneas 489–512 no contiene ninguna rama para layn.

Salvo el retorno especial de `سَوْءَاتٍ`, esos casos caen hasta `2 (طبيعي)`. El algoritmo contradice directamente sus tablas y REL-001.

### MUD-004 — La rama de hamzat al-waṣl para mīm al-jamʿ es inalcanzable

El bloque de mīm al-jamʿ está dentro de la condición exterior `همز قطع en otra كلمة`, líneas 456–468. Dentro de ese bloque, las líneas 463–464 preguntan si la hamzah es waṣl.

Una entrada que ya fue clasificada como hamzat al-qaṭʿ no puede ser simultáneamente hamzat al-waṣl. La regla de ḍamm ante hamzat al-waṣl nunca se ejecuta.

### MUD-005 — Los casos no-hamzah de `أَنَا` tampoco llegan a su función

`verificar_ana_madd` contempla hamzat al-waṣl y ausencia de hamzah en las líneas 530–534. Pero sólo se llama desde el bloque exterior de munfaṣil, que exige hamzat al-qaṭʿ.

Por tanto, dos de sus cuatro ramas son inalcanzables. El tratamiento de `أَنَا` debe iniciarse desde la identidad del pronombre y luego clasificar el contexto siguiente.

### MUD-006 — Los `if` independientes pueden añadir a la vez un caso especial y munfaṣil general

Dentro de las líneas 456–468, `أَنَا`, mīm al-jamʿ y ṣilah se comprueban con condiciones independientes; el `SINO` final parece vinculado sólo a la última condición. Una entrada especial puede agregar su resultado y además `منفصل - 6`.

Esto es especialmente grave para `أَنَا` ante hamzah kasrada: la función auxiliar devuelve “sin madd en waṣl”, pero el fallback general puede añadir seis y ganar después en prioridad.

La clasificación debe ser mutuamente exclusiva o producir alternativas justificadas, nunca duplicados accidentales.

### MUD-007 — La validación inicial no admite varios fenómenos que luego intenta detectar

La función exige que el objetivo sea alif, wāw o yāʾ de madd en las líneas 426–428. Más tarde pregunta si el objetivo es hāʾ de pronombre, mīm al-jamʿ o una construcción de ṣilah.

Esas unidades no son el mismo tipo de entrada. La API mezcla detector de letra de madd con detectores morfosintácticos que crean una vocal de enlace. Deben ser reglas separadas que produzcan una realización de madd común.

### MUD-008 — Ṣilah ṣughrā, ʿiwaḍ y fawātiḥ de dos ḥarakāt no están modelados explícitamente

El algoritmo principal no contiene una detección completa de ṣilah ṣughrā, madd al-ʿiwaḍ ni las letras de apertura agrupadas en `حَيٌّ طُهْر`. Sólo existe un placeholder tardío `es caso especial 2`.

No define precondiciones, excepciones ni evidencia. El supuesto algoritmo completo no cubre todo el grupo de dos ḥarakāt que el documento enumera.

### MUD-009 — El caso especial de `الٓمٓ` queda absorbido por lāzim general

Las tablas conservan dos awjuh —seis o dos— al unir determinadas aperturas con hamzat al-waṣl. El algoritmo no implementa esa excepción antes de las líneas 489–491, donde todo lāzim retorna seis.

Además, el alcance exacto de las aperturas y las dos suras deberá contrastarse cuidadosamente con la redacción de REL-001, líneas 99–104, y con una autoridad especializada.

### MUD-010 — La prioridad se aplica a la palabra, no a cada intervalo de madd

`مدود_presentes` agrega fenómenos y luego devuelve un único ganador. Una palabra o frase puede contener más de una ocurrencia de madd en posiciones distintas. El propio ejemplo `ءَآمِّينَ` de las líneas 417 y REL-001, línea 177, conserva un madd lāzim en una posición y un ʿāriḍ potencial en otra.

La regla de causa más fuerte sólo puede aplicarse cuando dos causas afectan al mismo intervalo pertinente. El motor deberá identificar cada span antes de resolver solapamientos.

### MUD-011 — Las matrices requieren un perfil coherente de lectura

La matriz badal/ʿāriḍ depende de la duración de badal elegida. Esa elección no debe hacerse de forma aleatoria en cada palabra si el método de recitación exige consistencia.

La API necesitará una configuración de lectura o un conjunto de awjuh globalmente compatibles. Cada resultado indicará qué elecciones previas restringe o hereda.

### MUD-012 — “Más fuerte” no significa borrar toda evidencia de las otras causas

Las líneas 397–417 y 489–506 convierten la jerarquía en un único resultado. Aunque una causa determine la duración audible de un intervalo, las causas coincidentes siguen siendo importantes para explicación, pruebas y trazabilidad.

La salida deberá conservar:

- Todas las causas detectadas.
- La causa resolutiva.
- La duración o conjunto de duraciones.
- La regla de precedencia aplicada.
- La fuente de cada conclusión.

### MUD-013 — Hamzah no puede identificarse mediante una única forma gráfica

Las reglas distinguen hamzat al-qaṭʿ, hamzat al-waṣl, vocal de hamzah, hamzah estable o transformada por tashīl, naql o ibdāl. Estas propiedades no se obtienen comparando sólo `ء`, `أ` o `إ`.

Se necesita una representación lingüística versionada que conserve la grafía original y describa la realización de Warsh sin normalización destructiva.

### MUD-014 — La presencia de sukūn o shaddah no basta para lāzim

Lāzim depende de un sukūn inherente que permanece en waṣl y waqf, y el caso mushaddad implica estructura fonética interna. La función no define cómo distinguirlo de sukūn contextual, omisión editorial o shaddah de otro origen.

La causa deberá proceder de análisis aprobado y no de la mera ausencia de vocal o presencia de U+0651.

### MUD-015 — Las fawātiḥ se leen como nombres de letras, no como caracteres aislados

Los madds ḥarfī dependen de la ortografía pronunciada del nombre de la letra inicial y de su relación con la siguiente. El algoritmo consulta `حرف` sin modelar esa expansión ni el contexto de sura.

Cada apertura deberá ser una unidad de conocimiento con forma escrita, nombre recitado, segmentos fonéticos, sura y awjuh.

### MUD-016 — Las transformaciones de waqf son fonéticas, no ediciones del corpus

El documento escribe `غَفُورًا → غَفُورَا` y habla de eliminar alif o ṣilah. Estas notaciones son pedagógicas. La implementación no sustituirá tanwīn, añadirá alif ni eliminará signos en el texto fuente.

Waqf y waṣl producirán anotaciones de realización sobre el mismo texto inmutable.

### MUD-017 — Madd al-layn requiere modo y siguiente unidad pronunciada

La condición `después == متحرك + وقف` de la línea 486 no formaliza si la letra es final, qué queda sākin por waqf ni cómo se atraviesan marcas. Layn ante hamzah también puede ocurrir en posición medial o final según la fuente.

Se necesitan grafemas, fronteras, posición dentro de palabra y modo explícito de recitación.

### MUD-018 — `سَوْءَاتٍ` mezcla desacuerdo transmitido y política elegida

REL-001, líneas 141–165, presenta opiniones y después adopta los cuatro awjuh asociados a los investigadores encabezados por Ibn al-Jazarī. El legado llama “prohibidas” a combinaciones fuera de esa matriz.

La especificación deberá registrar autoridad, método adoptado y alternativas históricas. “No permitido” sólo será válido dentro del perfil doctrinal aprobado, no como afirmación sin alcance.

### MUD-019 — Las excepciones por string no son portables al rasm Warsh

El documento compara formas como `يُؤَاخِذُ`, `إِسْرَائِيلَ`, `الْمَوْءُودَةُ` y `سَوْءَاتٍ`. El corpus heredado puede usar alif pequeña, hamzah separada, signos magrebíes y distintas terminaciones gramaticales.

Las excepciones deberán anclarse a lema y ocurrencias verificadas, con texto fuente intacto, no a igualdad de cadenas vocalizadas.

### MUD-020 — Duración en ḥarakāt no es una constante temporal

Dos, cuatro o seis ḥarakāt expresan proporción dentro del tempo de recitación. No deberán convertirse en milisegundos fijos ni validarse mediante una tolerancia absoluta sin un protocolo fonético aprobado.

Las futuras pruebas de audio necesitarán referencia humana y normalización de tempo separada de la regla simbólica.

### MUD-021 — “Catorce tipos” y recuentos no validan cobertura

Las líneas 624–654 cuentan categorías y letras. La suma no demuestra que las excepciones sean alcanzables, que las matrices se respeten ni que todo el corpus esté cubierto. Los fallos anteriores existen a pesar de ese recuento.

La verificación deberá medir ocurrencias, ramas positivas/negativas, awjuh preservados y coherencia global.

### MUD-022 — Faltan estados explícitos de incertidumbre

Las funciones auxiliares pueden terminar sin retorno y el algoritmo principal usa fallbacks como `2 (طبيعي)`. Una entrada no reconocida no debe convertirse automáticamente en madd natural.

La salida deberá distinguir `not_applicable`, `unknown`, `unsupported_input` y `requires_review`.

## Modelo mínimo que deberá reemplazarlo

La futura especificación deberá operar por ocurrencia:

```text
texto coránico inmutable + span objetivo
  + unidad fonética y causa de madd
  + estructura de palabra y frontera
  + modo: wasl | waqf | unknown
  + realización de hamzah/sukun/shaddah aprobada
  + perfil coherente de Warsh por tariq al-Azraq
  + causas coincidentes sobre el mismo span
  → conjunto de duraciones permitidas en harakat
  → restricciones con otras elecciones
  → preferencia, si existe
  → evidencia y revisión humana
```

Las causas no ganadoras permanecerán en la explicación. Las transformaciones fonéticas nunca modificarán el corpus.

## Casos que la nueva especificación deberá incluir

- Cada letra de madd con positivos, negativos y grafías editoriales distintas.
- Las cuatro categorías de dos ḥarakāt y todas sus excepciones.
- `أَنَا` ante cada tipo y vocal de hamzah, ante no-hamzah, en waṣl y waqf.
- Mīm al-jamʿ ante hamzat al-qaṭʿ, hamzat al-waṣl y waqf.
- Ṣilah ṣughrā/kubrā, `هَٰذِهِ` y los contextos sin ṣilah.
- Cada clase de lāzim y los dos awjuh de ʿayn.
- Las aperturas `الٓمٓ` bajo cada contexto transmitido.
- Badal general y cada categoría de qaṣr exclusivo.
- ʿĀriḍ con cada elección compatible de badal.
- Layn general, ante hamzah y en las excepciones citadas.
- Los cuatro awjuh de `سَوْءَاتٍ` como configuraciones separadas.
- Dos causas sobre el mismo span y causas en spans distintos de una palabra.
- Waqf/waṣl sin cambiar un solo code point.
- Resultados desconocidos cuando falte análisis.

## Decisión de migración

- Conservar el archivo original como legado y catálogo provisional.
- No migrar el algoritmo de acumulación/prioridad actual.
- Recuperar cada clase y excepción respaldada en especificaciones separadas.
- Modelar una ocurrencia de madd por span, no una decisión única por palabra.
- Mantener perfiles de awjuh globalmente compatibles.
- Representar ḥarakāt como duración relativa, no milisegundos.
- Mantener toda conclusión religiosa como candidata hasta revisión del especialista.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_HAMZ.md` contra las Partes 12-A y 12-B.
