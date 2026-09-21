# Auditoría de `ARBOL_COMPLETO_REGLAS_TAJWEED.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `ARBOL_COMPLETO_REGLAS_TAJWEED.md`
- **SHA-256:** `9fbdc5d22c6841fd26aea92686702d4506ae4975c140d3e6cfe8db8e03e41be1`
- **Estado:** `rejected`
- **Decisión:** rechazado como árbol completo, especificación normativa, fuente de golden tests o base directa de implementación.
- **Conservación:** se mantiene intacto como evidencia histórica; algunas afirmaciones podrán recuperarse individualmente después de verificarlas.

## Base de la auditoría

Se comparó el documento con:

- REL-001 / `Parte 7.md`, páginas declaradas 65–76.
- El archivo heredado `data/unicode_characters_export.csv` disponible actualmente.
- El archivo heredado `data/warshData_v2-1.json` disponible actualmente.
- Los propios enunciados y ejemplos internos del árbol.

No se ha utilizado el código antiguo como autoridad. La exactitud religiosa final de las afirmaciones recuperables continúa pendiente de especialista.

## Contenido que coincide de forma general con la Parte 7

Las siguientes estructuras principales sí reflejan el contenido básico del libro de trabajo:

- Las cuatro categorías de nūn sākinah y tanwīn: iẓhār, idghām, iqlāb e ikhfāʾ.
- Las seis letras de iẓhār y las quince de ikhfāʾ.
- La división de idghām en ناقص con ghunnah y تام sin ghunnah.
- Las cuatro palabras citadas para iẓhār shādhdh.
- Iqlāb ante bāʾ y el uso de la pequeña mīm en el material de trabajo.
- Las tres categorías de mīm sākinah.
- La ghunnah de nūn y mīm mushaddadah.

Esta coincidencia general no valida los ejemplos añadidos, las frecuencias, el modelo Unicode ni el pseudomodelo de detección.

## Hallazgos críticos

### ARB-001 — El título y el alcance son falsamente exhaustivos

La línea 1 lo llama “árbol completo de reglas de tajweed Warsh”, pero la línea 2 declara como base únicamente la Parte 7, un CSV Unicode y Al-Baqarah. Las líneas 399–410 confirman que el contenido religioso estudiado fue la Parte 7 y que sólo las primeras 100 āyāt se analizaron en detalle.

La línea 416 declara el árbol como completo sin evidencia que cubra las Partes 8–12, el resto del libro, todo el Corán, waqf/ibtidāʾ o revisión humana.

### ARB-002 — La sección de iẓhār contiene ejemplos de otras reglas

Las líneas 32–36 están bajo “Ejemplos de Al-Baqarah” para iẓhār, pero:

- `مَنْ يَّقُولُ` contiene nūn ante yāʾ y el mismo documento clasifica yāʾ entre las letras de idghām.
- `مِنۢ بَعْدِ` está marcado y descrito como iqlāb.
- `وَأَنِّے` no representa “tanwīn + hamza” como afirma el comentario.
- `تُنۢبِتُ` contiene la señal que el propio documento usa para iqlāb ante bāʾ.

Por tanto, ninguno de esos cuatro elementos puede aceptarse como golden test de iẓhār.

### ARB-003 — Los ejemplos añadidos de idghām nāqiṣ no prueban la regla declarada

Las líneas 70–74 incluyen `يُومِنُونَ` y `يُوقِنُونَ`, que no muestran por sí mismas nūn sākinah o tanwīn seguido de una letra de `ينمو`. También colocan `مِّن رَّبِّهِمْ` bajo idghām con ghunnah aunque rāʾ se clasifica en el propio árbol entre las letras de idghām sin ghunnah, y mezclan `يُنفِقُونَ`, donde nūn ante fāʾ corresponde a otra categoría.

### ARB-004 — Los ejemplos añadidos de idghām tām mezclan fenómenos distintos

Las líneas 89–92 incluyen `لِّلْمُتَّقِينَ` y `لَّا يَشْعُرُونَ`, que no son ejemplos de nūn sākinah o tanwīn ante lām/rāʾ. Sólo deben conservarse los ejemplos que vuelvan a demostrarse desde el corpus con contexto completo.

### ARB-005 — La sección de ikhfāʾ contiene contradicciones internas

Las líneas 197–208 contienen varios problemas verificables sin interpretación externa:

- `لَا رَيْبَ فِيهِ` se justifica mediante `ب + ف`, aunque la regla definida exige nūn sākinah o tanwīn.
- `عَذَابٌ عَظِيم` y `لِبَعْضٍ عَدُوّ` tienen `ع` después del tanwīn, pero el propio árbol enumera `ع` entre las letras de iẓhār.
- `أَنفُسَهُمْ` se describe como ikhfāʾ “antes de أ”; el contexto de la nūn dentro de la palabra es la fāʾ posterior.
- `رِزْقاٗ لَّكُمْ` se incluye aunque el propio comentario reconoce que corresponde a idghām.

Esta sección no puede utilizarse para entrenar, probar ni validar el futuro motor.

### ARB-006 — Los ejemplos de mīm sākinah no respetan el disparador de la regla

Entre las líneas 224–269 se añaden ejemplos que el propio documento reconoce como negativos o pertenecientes a otras reglas. En particular:

- La sección de ikhfāʾ shafawī termina diciendo que aún hay que buscar casos reales de mīm sākinah ante bāʾ.
- Bajo idghām shafawī aparecen casos de nūn/tanwīn o de otra regla, no necesariamente mīm sākinah seguida de mīm.
- Bajo iẓhār shafawī aparece `يُومِنُونَ`, donde la mīm no es sākinah.

Una lista que mezcla positivos, negativos y casos ajenos sin un campo de resultado esperado es inservible como conjunto de prueba.

### ARB-007 — La sección de nūn/mīm mushaddadah incluye contraejemplos como ejemplos

Las líneas 288–302 incluyen expresamente dos casos “sin Shadda” y un caso de yāʾ con shaddah dentro de una sección definida para nūn o mīm con shaddah. Los casos no están tipados como positivos o negativos y no deben migrarse.

### ARB-008 — Se pierde una condición explícita de waqf

Las líneas 106–108 resumen los casos de `يس` y `ن والقلم`, pero omiten que REL-001 / `Parte 7.md`, líneas 87–89, limita esos awjuh al waṣl y establece iẓhār al hacer waqf en ambos lugares.

La omisión modifica la aplicabilidad de la regla y demuestra que un resumen aparentemente correcto puede ser peligroso al convertirse en algoritmo.

## Hallazgos de corpus y Unicode

### ARB-009 — La dependencia de corpus no es reproducible tal como se cita

Las líneas 409–412 citan `data/warshData_v2-1.sql`, pero en el proyecto heredado localizado existe `data/warshData_v2-1.json`, con SHA-256 `44478993e0ff818b009a07602bd9902560abf1bf92a58b3cc5c5713822370796` y 6214 registros.

Sin el archivo exacto, su hash, esquema, procedencia, licencia y proceso de conversión no puede reproducirse la supuesta verificación.

### ARB-010 — La cifra de caracteres únicos no coincide con el CSV actual

Las líneas 404–407 afirman que `unicode_characters_export.csv` contiene 248 caracteres únicos. El archivo actualmente localizado tiene SHA-256 `d2f6312566aed06efe249d3ac92d3e4846fa191b881123c50f118b66376c5a11` y 351 filas con 351 code points distintos.

Esto puede indicar una versión distinta, un filtro no documentado o una cifra incorrecta. En cualquiera de los tres casos, el resultado no es reproducible.

### ARB-011 — Las estadísticas se presentan como verificación aunque son estimaciones

Las líneas 352–359 denominan “verificación” a cifras expresadas con `~` y rangos aproximados. No se incluye consulta, script, versión del corpus ni resultado firmado. Las cifras quedan anuladas hasta poder reproducirlas.

### ARB-012 — El corpus heredado mezcla texto con caracteres de presentación

De los 6214 registros de `warshData_v2-1.json`, 6185 terminan en un code point del rango U+FC00–U+FCFF, que Unicode reserva para formas de presentación y ligaduras árabes. En el dataset parecen actuar como glifos numerales o marcadores de āyah dependientes de una fuente.

Estos code points no pueden asumirse como letras del texto coránico ni incluirse sin separación en estadísticas lingüísticas. El futuro corpus deberá guardar el texto, el número de āyah y la presentación como datos distintos o documentar formalmente una codificación autorizada.

### ARB-013 — Se confunde una señal visual con la definición de la regla

Las líneas 313 y 373–381 convierten la presencia o ausencia visual de sukūn en una clave de detección. REL-001 define nūn sākinah fonética y ortográficamente; no establece que un detector universal pueda depender exclusivamente de la marca visible de un muṣḥaf concreto.

La convención puede utilizarse como señal adicional de un dataset identificado, pero nunca como definición portátil de iẓhār, idghām o ikhfāʾ.

### ARB-014 — Las frecuencias cuentan code points, no reglas

Las frecuencias de letras o marcas en las líneas 306–348 no miden ocurrencias de tajwīd. Una letra puede aparecer con otra vocalización, en otro contexto o como parte de una secuencia que activa una regla diferente. Ninguna frecuencia de code point valida por sí sola un detector.

## Hallazgos de trazabilidad

### ARB-015 — No existe trazabilidad por afirmación

El documento cita recursos completos al final, pero no vincula cada ejemplo añadido, frecuencia o inferencia con una consulta reproducible y una ubicación exacta. La distinción entre “del libro”, “observado en corpus” e “inferido por el autor” es insuficiente.

### ARB-016 — Una transformación añadida no está respaldada en la página citada

La línea 26 añade `عَنْ أَنفُسِهِمْ → عَنَ نْفُسِهِمْ`. REL-001 / `Parte 7.md`, páginas 67–68, documenta el principio general de naql y muestra otros ejemplos, pero no respalda allí esa representación concreta. Debe revisarse contra la sección completa de hamz y un corpus autorizado antes de conservarla.

## Decisión de migración

El documento completo queda `rejected` para cualquiera de estos usos:

- Especificación del motor.
- Fuente religiosa.
- Árbol completo de reglas.
- Casos esperados.
- Estadísticas del Corán.
- Política Unicode.

Puede utilizarse únicamente como índice de afirmaciones que deberán volver a investigarse. Las definiciones que coinciden con REL-001 se redactarán desde cero, con fuente y página, al construir las especificaciones candidatas.

## Consecuencias para el proyecto

- Ningún ejemplo añadido por el árbol entrará automáticamente en `tests/golden`.
- Ninguna frecuencia del árbol se publicará.
- No se implementará detección basada únicamente en signos visuales.
- Los datasets citados deberán pasar por una migración de custodia separada antes de utilizarlos.
- La aplicación no mostrará el título “árbol completo” para este artefacto.
- La próxima auditoría seguirá con `DECISION_LOGIC_QALQALAH.md`, según el orden aprobado.

## Revisión humana

No se solicita al especialista que apruebe este árbol. Primero se crearán especificaciones pequeñas y trazables. El especialista revisará esas especificaciones y sus casos, no el artefacto rechazado en bloque.
