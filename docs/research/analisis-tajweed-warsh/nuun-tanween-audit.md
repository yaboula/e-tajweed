# Auditoría de `DECISION_LOGIC_NUUN_TANWEEN.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_NUUN_TANWEEN.md`
- **SHA-256:** `d1f38e4c8629a8ddd65e007b5bbf2cc7ecafc5fdaac0f0d9742575efc791727e`
- **Estado:** `resolved`; correcciones aplicadas al documento migrado
- **Decisión:** conservar el documento, corregirlo contra REL-001 y mantener separadas sus decisiones semánticas aunque compartan color.
- **Fuente local contrastada:** REL-001 / `Parte 7.md`.

## Veredicto

El documento conservaba buena parte de la clasificación básica de nūn sākinah y tanwīn expuesta en el libro de trabajo. Su antiguo «algoritmo completo» no representaba con seguridad el texto coránico ni el contexto de recitación; esos puntos se corrigieron en [DECISION_LOGIC_NUUN_TANWEEN.md](./DECISION_LOGIC_NUUN_TANWEEN.md).

La corrección incorpora waṣl/waqf, identidad basada en el corpus, incertidumbre, preservación del texto y los casos `يس`/`ن` antes de la rama general de wāw.

La validación manual se realizará durante el desarrollo contra el muṣḥaf coloreado y certificado. La revisión del profesor, qāriʾ o especialista cualificado queda como control final futuro y no bloquea el desarrollo.

## Elementos respaldados provisionalmente por REL-001

### Definiciones y división principal

REL-001, líneas 13–23, define nūn sākinah y tanwīn y presenta cuatro categorías: iẓhār, idghām, iqlāb e ikhfāʾ. El documento heredado reproduce esta estructura en sus líneas 8–19 y 23–65.

La formulación heredada de que el tanwīn se encuentra «siempre en dos palabras» no debe conservarse literalmente. El tanwīn está al final de la primera palabra; es la aplicación contextual de la regla la que puede depender del siguiente elemento pronunciado en otra palabra.

### Iẓhār

REL-001, líneas 25–43, respalda provisionalmente las seis letras faríngeas de iẓhār y describe la pronunciación clara sin ghunnah añadida. El documento heredado recoge este núcleo en sus líneas 71–97.

La prioridad que el documento asigna a naql no queda validada por esa mención breve. Las condiciones y excepciones completas de naql pertenecen al estudio específico de hamz y deberán modelarse allí.

### Idghām

REL-001, líneas 45–89, respalda provisionalmente:

- Las seis letras reunidas en `يرملون`.
- La división general con y sin ghunnah expuesta por el libro.
- Las cuatro palabras de iẓhār shādhdh dentro de una sola palabra.
- Los casos especiales de Yā-Sīn y Nūn seguidos por wāw, con condiciones distintas en waṣl y waqf.

El libro no basta, por sí solo, para validar todas las etiquetas algorítmicas que añade el documento heredado ni para demostrar que su lista de excepciones sea universalmente completa.

### Iqlāb

REL-001, líneas 93–105, respalda provisionalmente el iqlāb ante bāʾ y la convención visual de una pequeña mīm en el muṣḥaf descrito. El documento heredado recoge ese núcleo en sus líneas 194–217.

La pequeña mīm es una señal editorial posible, no la definición normativa de la regla ni un requisito portable a todos los corpus.

### Ikhfāʾ

REL-001, líneas 107–127, respalda provisionalmente las quince letras de ikhfāʾ. También distingue una ghunnah más gruesa ante las cinco letras de istiʿlāʾ incluidas y una ghunnah fina ante las diez restantes. El documento heredado recoge esa división en sus líneas 220–260.

## Hallazgos corregidos

### NUN-001 — El detector exige signos literales que el corpus no garantiza

Las líneas 27, 75, 104, 148, 198, 224, 280 y 403–404 parten de la presencia literal de `نْ` o de uno de los tres signos estándar de tanwīn. Esa condición no es válida como modelo general de un muṣḥaf digital.

En determinadas convenciones, la nūn puede no llevar sukūn visible cuando se aplica idghām o ikhfāʾ. El iqlāb puede representarse mediante una vocal simple acompañada por una pequeña mīm, en lugar del code point esperado de tanwīn.

Existe una prueba concreta en el corpus heredado `warshData_v2-1.json`. En Al-Baqarah 2:18, la secuencia `مُحِيطُۢ` termina con:

- ḍammah U+064F.
- Arabic Small High Meem Isolated Form U+06E2.

No contiene ḍammatān U+064C. Por tanto, el algoritmo heredado no detectaría correctamente una representación que el propio conjunto de datos utiliza.

### NUN-002 — Falta una política general de waṣl y waqf

La definición de las líneas 16–19 reconoce que el tanwīn se considera en waṣl, pero el algoritmo de las líneas 398–459 no recibe ni comprueba el modo de recitación, salvo dentro del caso especial de Yā-Sīn y Nūn.

Así, podría intentar aplicar idghām, iqlāb o ikhfāʾ a través de una frontera donde el lector se detiene. La API futura deberá recibir explícitamente `wasl`, `waqf` o `unknown`; una pausa no se deducirá silenciosamente del texto.

### NUN-003 — La rama especial de Yā-Sīn y Nūn es inalcanzable

El árbol principal envía yāʾ, nūn, mīm y wāw a la rama de idghām con ghunnah en las líneas 28 y 37–39. Después sitúa el caso especial `يس/ن + و` bajo otra rama, en las líneas 41–43.

La misma contradicción se repite en el árbol de dependencias: la segunda pregunta consume cualquier wāw en las líneas 288–294, mientras el caso especial sólo aparece después de una tercera pregunta limitada a lām y rāʾ, en las líneas 296–300.

Finalmente, el pseudocódigo de las líneas 419–427 devuelve un resultado para wāw antes de llegar a las líneas 429–442. El caso especial no puede ejecutarse. Esto basta por sí solo para rechazar el algoritmo como implementación.

### NUN-004 — La clasificación del caso especial necesita autoridad explícita

REL-001, líneas 87–89, describe los casos de Yā-Sīn y Nūn dentro del tratamiento general de idghām y especifica condiciones de waṣl y waqf. El documento heredado los etiqueta como idghām tām sin aportar una cita que fundamente específicamente esa clasificación.

La etiqueta exacta y sus awjuh deberán verificarse en fuentes autorizadas y ser aprobados por el especialista antes de modelarlos.

### NUN-005 — Naql se simplifica indebidamente

Las líneas 33–35, 80–96, 268, 282–286, 360–365 y 407–410 anteponen naql cuando el siguiente carácter es hamzah. Esa condición es demasiado amplia: naql tiene condiciones, fronteras y excepciones propias que el resumen de la Parte 7 no especifica de forma exhaustiva.

Además, las líneas 285 y 410 dicen que `نْ` «desaparece». El texto fuente no puede desaparecer. Incluso cuando la lectura transfiere una vocal o elimina el sukūn pronunciado, el motor sólo podrá describir el fenómeno mediante anotaciones; nunca borrará ni sustituirá code points coránicos.

### NUN-006 — “Siguiente letra” no está definido sobre grafemas

El documento usa repetidamente `letra_siguiente`, pero no define cómo atravesar:

- Marcas combinantes.
- Separadores y límites de palabra.
- Signos coránicos intermedios.
- Anotaciones editoriales.
- Formas precompuestas o secuencias descompuestas.
- Fin de āyah y contexto de recitación.

La siguiente unidad pronunciada no equivale al siguiente code unit de JavaScript. La futura implementación necesitará una capa de tokenización y grafemas que preserve todos los code points y haga explícitas las fronteras atravesadas.

### NUN-007 — Hamzah no puede compararse con un único carácter

Las ramas de naql parecen comparar sólo con `ء`. En los textos árabes, la hamzah puede aparecer aislada, sobre o bajo portadora, o mediante distintas secuencias Unicode. Una política de coincidencia deberá declarar exactamente qué formas acepta y por qué.

La comparación podrá usar una representación analítica auxiliar, pero no normalizará destructivamente el texto fuente.

### NUN-008 — La transformación interna de iqlāb amenaza la integridad textual

La línea 203 y el algoritmo de las líneas 303 y 446 proponen convertir internamente nūn o tanwīn en mīm. Esa sustitución no es aceptable sobre el corpus original.

El motor deberá emitir una anotación fonética vinculada a un intervalo estable del texto. Al retirar las anotaciones, la secuencia de entrada tendrá que reconstruirse byte por byte o code point por code point, según el contrato fijado para el corpus.

### NUN-009 — U+06E2 no puede ser el único criterio de iqlāb

El propio documento reconoce en la línea 216 que la pequeña mīm puede no estar presente en todas las ediciones. Por tanto, U+06E2 puede servir como evidencia o validación de una convención editorial concreta, pero no como condición religiosa primaria.

También deberá verificarse su posición exacta dentro del grafema y su interacción con la vocal precedente en cada corpus aprobado.

### NUN-010 — La shaddah no demuestra por sí sola idghām

La tabla Unicode de la línea 472 describe U+0651 como marca de idghām. Una shaddah también puede formar parte de la escritura ordinaria de una palabra y su presencia o ausencia puede depender de la edición.

No es válido inferir automáticamente la clase de idghām a partir de U+0651, ni considerar su ausencia como negación de la regla.

### NUN-011 — La lista de cuatro palabras no autoriza errores absolutos

Las líneas 121–127 y 421–425 devuelven `ERROR` para cualquier encuentro dentro de palabra que no pertenezca a las cuatro palabras enumeradas. El libro respalda provisionalmente esas cuatro excepciones dentro del corpus estudiado, pero eso no convierte cualquier entrada externa o incompleta en un error doctrinal.

El motor deberá distinguir:

- Coincidencia con una excepción aprobada del corpus.
- Entrada fuera del corpus aprobado.
- Texto insuficiente o no reconocido.
- Caso que exige revisión.

### NUN-012 — La partición de 28 letras no valida el algoritmo

Las líneas 337–354 presentan como «verificación matemática» que las clases sumen 28 letras. Esto sólo comprueba una partición nominal del alfabeto bajo ciertos supuestos. No prueba:

- Las condiciones de aplicación.
- Waṣl y waqf.
- Las excepciones.
- La representación Unicode.
- La pronunciación de Warsh por ṭarīq al-Azraq.
- La corrección del control de flujo.

El defecto inalcanzable de Yā-Sīn/Nūn demuestra precisamente que una suma correcta de letras puede coexistir con un algoritmo incorrecto.

### NUN-013 — “Excepciones completas” no está demostrado

Las líneas 358–395 presentan una lista completa, pero el artefacto sólo cita el libro de trabajo y documentos internos. No existe todavía una matriz contrastada con fuentes autorizadas, corpus completo, variantes editoriales y revisión humana.

La palabra `completa` deberá eliminarse de la futura especificación hasta que exista evidencia de exhaustividad.

### NUN-014 — Los solapamientos no han sido probados

Las líneas 264–272 niegan determinadas intersecciones mediante afirmaciones breves. Sin embargo, el propio documento introduce prioridad con naql y contexto especial con idghām. La relación con otras reglas sólo podrá resolverse mediante una matriz explícita de solapamientos, no mediante el orden accidental de `if` ni prioridades de color.

### NUN-015 — El estado final no puede ser sólo “letra no clasificada”

La rama final del pseudocódigo devuelve un error cuando no reconoce la siguiente letra. Según la carta del proyecto, una entrada desconocida no autoriza al motor a inventar una respuesta ni a declarar que el texto religioso es erróneo.

La salida deberá incluir estados diferenciados como `unknown`, `unsupported_input` o `requires_review`, junto con la razón y la evidencia disponible.

### NUN-016 — Las páginas y afirmaciones necesitan trazabilidad granular

La correspondencia general con la Parte 7 es razonable, pero el documento cita rangos de páginas para bloques enteros y añade conclusiones algorítmicas que no aparecen como tales en el libro.

La futura especificación deberá enlazar cada condición, excepción y resultado con página exacta, edición, fragmento identificado y estado de aprobación. Una referencia general a `Parte 7` no basta.

## Modelo mínimo aplicado en la corrección

La futura especificación candidata deberá separar:

```text
unidad coránica inmutable
  + identidad lingüística de nūn/tanwīn demostrada
  + siguiente unidad pronunciada
  + fronteras atravesadas
  + modo: wasl | waqf | unknown
  + convención editorial identificada
  + excepciones versionadas
  → regla candidata
  → realización fonética candidata
  → evidencia
  → estado de revisión
```

La realización fonética no sustituirá caracteres. La pequeña mīm, el sukūn y la shaddah serán señales del corpus identificado, no atajos universales.

## Casos preparados para la validación durante la implementación

- Positivos y negativos para las seis letras de iẓhār.
- Positivos y negativos para cada grupo de idghām.
- Las cuatro palabras de iẓhār shādhdh, con referencia y posición verificadas.
- Yā-Sīn y Nūn antes de wāw en waṣl, waqf y modo desconocido.
- Iqlāb con tanwīn estándar.
- Iqlāb representado mediante U+064F y U+06E2, como en el corpus heredado.
- Iqlāb sin pequeña mīm en una convención editorial documentada.
- Las quince letras de ikhfāʾ y la división provisional de ghunnah gruesa/fina.
- Nūn sin sukūn visual en una convención que omite la marca.
- Hamzah aislada, precompuesta y representaciones admitidas por la política Unicode.
- Marcas combinantes y signos coránicos entre las unidades relevantes.
- Frontera de palabra, fin de āyah, waṣl y waqf.
- Entrada fuera del corpus: resultado de incertidumbre, no afirmación inventada.
- Reconstrucción exacta del texto tras retirar todas las anotaciones.

## Decisión de migración

- Conservar una copia privada intacta como custodia histórica.
- Migrar el archivo con su nombre original y corregir en él el árbol y el pseudocódigo.
- No utilizar sus etiquetas de completitud como evidencia.
- Conservar los enunciados respaldados por REL-001 y comentar cada corrección.
- Tratar los signos Unicode como propiedades de corpus versionados.
- Mapear iẓhār a negro, idghām con ghunnah/iqlāb/ikhfāʾ a verde e idghām sin ghunnah a gris, sin perder la identidad de cada decisión.
- Validar manualmente durante el desarrollo y reservar al especialista para el control final.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_MEEM_SAKINAH.md` contra la Parte 7.
