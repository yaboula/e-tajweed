# Auditoría de `DECISION_LOGIC_MEEM_SAKINAH.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_MEEM_SAKINAH.md`
- **SHA-256:** `3de93a57b05db1c56bf0e35233a96de8f82f3e1361de4ccdf17efb75f8f26e67`
- **Estado:** `rejected`
- **Decisión:** rechazado como guía directa de implementación; el núcleo respaldado por REL-001 deberá reescribirse como especificación candidata.
- **Fuente local contrastada:** REL-001 / `Parte 7.md`.

## Veredicto

El documento reproduce las tres categorías presentadas en la Parte 7 y conserva la advertencia específica de iẓhār ante fāʾ y wāw. Sin embargo, añade relaciones posicionales, transformaciones y ramas algorítmicas que la fuente no demuestra.

El detector tampoco funciona sobre el propio corpus heredado: exige una mīm seguida de U+0652, mientras que ejemplos de ikhfāʾ e idghām del corpus omiten ese sukūn visual. Además, clasifica como caso de una sola palabra una secuencia que contiene una frontera de palabra visible.

La parte religiosa continúa pendiente de validación por un profesor, qāriʾ o especialista cualificado. El archivo no puede alimentar el motor, los golden tests ni una política Unicode.

## Elementos respaldados provisionalmente por REL-001

### Definición y categorías

REL-001, líneas 141–146, define la mīm sākinah como la mīm sin movimiento, presenta tres reglas —ikhfāʾ shafawī, iẓhār shafawī e idghām shafawī— y explica el uso de `shafawī`. El documento heredado recoge ese núcleo en sus líneas 8–18.

La definición religiosa no autoriza a identificarla mediante un único patrón Unicode. “Sin movimiento” y “contiene literalmente U+0652” no son condiciones equivalentes en todas las convenciones editoriales.

### Ikhfāʾ shafawī

REL-001, líneas 148–152, describe ikhfāʾ de la mīm sākinah ante bāʾ, conservando la ghunnah. Los ejemplos citados por el documento heredado proceden de esa sección.

La fuente no respalda la clasificación posicional que el legado añade a esos ejemplos.

### Idghām shafawī

REL-001, líneas 154–158, describe idghām de la mīm sākinah ante una mīm vocalizada, cuidando ghunnah y tashdīd. Los dos ejemplos del documento heredado coinciden con la fuente.

La fuente mostrada sólo proporciona ejemplos entre dos palabras. Esto no autoriza a inventar el resultado de una supuesta secuencia interna que no ha sido documentada.

### Iẓhār shafawī y advertencia ante fāʾ/wāw

REL-001, líneas 160–171, define iẓhār ante las letras restantes y pide especial cuidado ante fāʾ y wāw por proximidad de los puntos de articulación. El documento heredado conserva provisionalmente esta advertencia y sus ejemplos.

La advertencia es una instrucción de pronunciación dentro de iẓhār; no constituye una cuarta regla ni una excepción que cambie la clasificación.

## Hallazgos bloqueantes

### MEM-001 — El requisito de U+0652 contradice el corpus heredado

Las líneas 9, 26–28, 64, 109, 140, 197, 280 y 282–284 exigen detectar la secuencia literal `مْ`. Esa condición no reconoce varios ejemplos del propio conjunto de datos heredado.

En `warshData_v2-1.json`:

- Al-Fīl 105:4 contiene `تَرْمِيهِم بِحِجَارَةٍ`. La mīm final es U+0645 y va seguida directamente por espacio U+0020 y bāʾ U+0628; no contiene sukūn U+0652.
- Al-Baqarah 2:19 contiene `لَهُم مَّشَوْاْ`. La primera mīm es U+0645 y va seguida por espacio y otra mīm; tampoco contiene U+0652. La segunda mīm sí lleva shaddah U+0651.
- En cambio, `هُمْ فِيهَا` sí representa la mīm mediante U+0645 seguido de sukūn U+0652.

Por tanto, la presencia del sukūn es una señal dependiente de la regla y de la convención del muṣḥaf, no un prerrequisito universal de entrada. El detector heredado produciría falsos negativos precisamente en ikhfāʾ e idghām.

### MEM-002 — Un ejemplo entre dos palabras está etiquetado como una sola palabra

Las líneas 31, 66, 73 y 227 clasifican `تَرْمِيهِم بِحِجَارَةٍ` como `كلمة واحدة`. Hay una separación explícita entre `تَرْمِيهِم` y `بِحِجَارَةٍ`; la mīm y la bāʾ pertenecen a dos palabras.

Los tres ejemplos de ikhfāʾ de REL-001, líneas 150–152, muestran la mīm al final de una palabra y la bāʾ al inicio de la siguiente. La fuente citada no demuestra el supuesto caso interno.

Esta etiqueta no puede migrarse ni utilizarse como golden test.

### MEM-003 — Una hipótesis no verificada se ejecuta como regla

Las líneas 122–132 reconocen que la fuente no documenta `مْ + م` dentro de una palabra y formulan como hipótesis que “probablemente” se aplique idghām. Sin embargo, las líneas 206–208 y 297–302 convierten esa hipótesis en una rama ejecutable que devuelve idghām.

Esto viola la regla central del proyecto: ante una situación desconocida, el motor debe devolver incertidumbre. El resultado deberá permanecer `requires_review` hasta que exista fuente precisa, evidencia corpus y aprobación humana.

### MEM-004 — Waṣl y waqf están modelados de forma contradictoria

La línea 13 afirma que la regla es válida en waṣl y waqf, pero las reglas dependen de una letra siguiente pronunciada. Las líneas 414–416 reconocen después que el efecto de una pausa no está resuelto.

Cuando se hace waqf al final de la primera palabra, la relación con la letra inicial siguiente no puede tratarse como si hubiera continuidad. La futura API deberá recibir `wasl`, `waqf` o `unknown`; el árbol actual no dispone de esa dimensión.

### MEM-005 — La secuencia iqlāb → ikhfāʾ shafawī no está respaldada como dos reglas

Las líneas 76–100, 183–189, 200–203, 427–445 y 451–455 afirman que nūn/tanwīn ante bāʾ activa primero iqlāb y después una segunda regla de ikhfāʾ shafawī.

REL-001, líneas 93–105, define iqlāb como la realización de nūn sākinah o tanwīn como mīm sākinah ante bāʾ con ghunnah. No afirma en ese pasaje que el mismo intervalo deba etiquetarse mediante dos reglas secuenciales.

La relación fonética puede ser útil para explicar el fenómeno, pero convertirla en dos detecciones normativas podría duplicar anotaciones, evidencia y presentación. La taxonomía deberá resolverse con fuentes autorizadas y el especialista.

### MEM-006 — El algoritmo propone transformar letras del texto

Las líneas 81, 93–96, 202, 293, 431–445 describen `نْ → مْ` como una conversión interna. El motor no puede sustituir la nūn o el signo de tanwīn del corpus por una mīm.

La realización fonética se expresará como una anotación no destructiva. El texto original y el orden de todos sus code points permanecerán intactos.

### MEM-007 — U+06E2 no demuestra por sí solo el “origen” de una mīm

Las líneas 88, 96, 202, 317–324, 355 y 445 consideran U+06E2 prueba suficiente de que una mīm proviene de iqlāb. U+06E2 es un signo editorial, no una mīm léxica transformada dentro del texto.

La función `origen_es_iqlāb` sólo comprueba si el contexto “contiene” la marca, sin proximidad, anclaje al grafema ni alcance definido. Podría atribuir a la posición actual una señal perteneciente a otro lugar.

La detección deberá partir de la estructura lingüística y usar el signo como evidencia adicional de una edición identificada.

### MEM-008 — “Siguiente letra” no está definido sobre Unicode ni recitación

El documento no define cómo `letra_siguiente` atraviesa marcas combinantes, espacios, signos coránicos, fin de āyah o anotaciones. Tampoco define si busca el siguiente code unit, code point, grafema, letra base o unidad pronunciada.

Los ejemplos atraviesan fronteras de palabra, de modo que esta omisión es esencial. La futura capa analítica deberá conservar todos los code points y registrar explícitamente qué frontera se ha atravesado.

### MEM-009 — `tiene_harakat` mezcla letra base y grafema

La línea 298 comprueba `letra == م AND tiene_harakat(letra)`. Una letra base U+0645 no “contiene” sus marcas combinantes; éstas son code points separados dentro de un grafema. La función no tiene semántica suficiente para distinguir una mīm vocalizada, una secuencia incompleta o una convención que omite marcas.

La condición deberá operar sobre una representación analítica documentada y permitir un estado desconocido.

### MEM-010 — Shaddah no es una prueba universal de origen ni de regla

Las líneas 112–113, 207, 302, 354 y 455 asocian U+0651 directamente con idghām shafawī. La shaddah es una marca ortográfica que también aparece por otras razones; a su vez, las convenciones editoriales pueden representar fenómenos de manera distinta.

Puede comprobarse como señal esperada en un corpus concreto, pero no sustituye la condición religiosa ni prueba por sí sola el origen de la geminación.

### MEM-011 — Las afirmaciones de “sin excepciones” no están demostradas

Las líneas 33, 68, 114–116 y 340 declaran ausencia de excepciones. REL-001 no ofrece una demostración de exhaustividad con ese alcance. La ausencia de excepciones en un manual de trabajo no permite afirmar que no existan en todas las fuentes, riwāyāt, ṭuruq o convenciones editoriales.

Estas afirmaciones deberán reformularse como “no se menciona una excepción en esta sección de REL-001” hasta completar la revisión experta.

### MEM-012 — La partición 1 + 1 + 26 no valida la implementación

Las líneas 233–248 llaman “verificación matemática” a la partición de las letras. Esa suma sólo reproduce una clasificación nominal. No verifica:

- La identificación de mīm sākinah.
- El contexto waṣl/waqf.
- Las fronteras de palabra.
- Las convenciones Unicode.
- La hipótesis de una secuencia interna.
- La relación con iqlāb.
- La corrección fonética.

Un algoritmo puede sumar 28 y seguir fallando sobre sus propios ejemplos, como ocurre aquí.

### MEM-013 — La explicación de makhārij añade conclusiones no citadas

Las líneas 359–385 afirman, entre otras cosas, que mīm y bāʾ tienen “exactamente” el mismo makhraj y derivan causalmente de ello la regla. La sección citada de REL-001 no contiene ese diagrama ni esas formulaciones técnicas.

La articulación de cada letra y la explicación causal deberán contrastarse con una fuente específica de makhārij y ṣifāt. No se migrarán como hechos sólo porque resulten plausibles.

### MEM-014 — “Misma palabra” y “dos palabras” necesitan un modelo formal

Las líneas 12, 30–40, 66, 111, 142, 206–208 y 225–229 usan categorías posicionales inconsistentes. Una mīm pertenece a una palabra; lo que debe modelarse es si la relación entre la mīm y la siguiente letra base cruza una frontera de palabra.

El motor deberá representar la frontera explícitamente, no inferirla del aspecto visual de una frase ni de una función global como `misma_palabra()` sin argumentos.

### MEM-015 — El resultado desconocido se convierte en error

Las líneas 311–312 devuelven `ERROR: letra no clasificada`. Una entrada puede estar incompleta, contener un signo no contemplado o pertenecer a un corpus no aprobado. Nada de ello autoriza a declarar que la letra o el texto coránico es erróneo.

La salida deberá distinguir `not_applicable`, `unknown`, `unsupported_input` y `requires_review`, siempre con una razón trazable.

### MEM-016 — La trazabilidad de página es parcial, no algorítmica

Las citas de las páginas 75–76 coinciden de forma general con REL-001, líneas 139–171. Sin embargo, las hipótesis sobre posición, la doble regla tras iqlāb, la detección mediante U+06E2 y las conclusiones de makhārij no aparecen respaldadas por esas páginas.

Cada futura condición deberá llevar su propia evidencia; una cita correcta de la definición no valida el pseudocódigo añadido alrededor de ella.

## Modelo mínimo que deberá reemplazarlo

La futura especificación candidata deberá separar:

```text
texto coránico inmutable
  + identidad lingüística de mīm sākinah demostrada
  + siguiente unidad pronunciada
  + frontera: misma palabra | entre palabras | fin de ayah | unknown
  + modo: wasl | waqf | unknown
  + señales editoriales del corpus versionado
  → regla candidata
  → realización fonética candidata
  → advertencia pedagógica, si corresponde
  → evidencia
  → estado de revisión
```

La advertencia ante fāʾ y wāw no alterará la clase de iẓhār. Las relaciones explicativas con iqlāb no producirán automáticamente dos anotaciones normativas.

## Casos que la nueva especificación deberá incluir

- Ikhfāʾ ante bāʾ con sukūn visible.
- Ikhfāʾ ante bāʾ sin U+0652, como `تَرْمِيهِم بِحِجَارَةٍ` en el corpus heredado.
- Idghām entre palabras con ghunnah y shaddah esperadas.
- Idghām entre palabras cuando la primera mīm no lleva sukūn visual.
- Supuesta secuencia dentro de una palabra: `requires_review` hasta disponer de evidencia.
- Iẓhār ante cada clase de letra restante.
- Casos específicos ante fāʾ y wāw con la advertencia pedagógica separada.
- Mismos ejemplos en waṣl, waqf y contexto desconocido.
- Signos combinantes y anotaciones entre las letras base.
- U+06E2 próximo y distante, para impedir atribuciones por mera presencia en el contexto.
- Entrada parcial o corpus no aprobado: incertidumbre, no error doctrinal.
- Reconstrucción exacta del texto después de retirar anotaciones.

## Decisión de migración

- Conservar el archivo original como legado.
- No migrar su árbol, pseudocódigo ni funciones auxiliares.
- Rechazar la etiqueta errónea de “una palabra” del ejemplo de Al-Fīl.
- No implementar la hipótesis interna de `مْ + م`.
- Recuperar sólo las definiciones respaldadas y volver a redactarlas.
- Tratar sukūn, shaddah y pequeña mīm como señales de un corpus versionado.
- Mantener toda conclusión religiosa como candidata hasta revisión del especialista.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_TAFKHIM_TARQIQ.md` contra la Parte 8.
