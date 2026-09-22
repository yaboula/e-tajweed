# Auditoría de `DECISION_LOGIC_HAMZ.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_HAMZ.md`
- **SHA-256:** `17455eb4161e488c36ab9d8d08fd0caa37e337dbc70f438b908e5dfe8d3c8c02`
- **Estado:** `rejected`
- **Decisión:** rechazado como guía directa de implementación; conserva un inventario extenso, pero el algoritmo pierde excepciones, awjuh correlacionados y diferencias entre escritura y realización oral.
- **Fuentes locales contrastadas:** REL-001 / `parte12-A.md` y `parte12-B.md`.

> **Actualización tras la corrección del archivo migrado:** `rejected` describe el **original heredado** identificado por el SHA-256 superior, no la versión corregida de `DECISION_LOGIC_HAMZ.md`. Los hallazgos HAM-001–027 se atendieron allí: precedencia de excepciones, awjuh estructurados, perfiles correlacionados, Unicode reversible, rasm inmutable y estados de incertidumbre. Estado del documento corregido: `corrected` **con retención de fuente** para Hūd 11:72, los ejemplos editoriales de p. 151 y las matrices de `ءَآلْـَٔانَ` donde intervenga ʿāriḍ omitido por el libro. Estas entradas no son normativas hasta cotejo físico, muṣḥaf certificado y revisión experta; tashīl requiere además validación oral. La paleta ya es referencia válida del propietario; no se reabre como propuesta.

## Veredicto

El documento contiene la mayor concentración de reglas, excepciones, ocurrencias y combinaciones del legado. Buena parte procede de las Partes 12-A y 12-B, pero su pseudocódigo reduce ese conocimiento a comparaciones de strings y retornos simples que no pueden representar el sistema.

Hay ramas especiales inalcanzables, ausencia de salidas para casos no clasificados, pérdida de dependencias entre awjuh y representaciones pedagógicas de pronunciación tratadas como si fueran texto. La propia REL-001 contiene notas editoriales de corrección y ejemplos reconocidos como dudosos en la sección de yāʾāt; esas páginas no pueden aprobarse sin contraste con el libro físico.

Tashīl es una realización oral que la fuente exige recibir de un shaykh autorizado. Ningún símbolo aproximado, sustitución por hāʾ ni algoritmo textual puede validarlo por sí mismo.

## Elementos respaldados provisionalmente por REL-001

### Tipos de hamzah y formas de cambio

REL-001 12-A, líneas 5–49, distingue hamzat al-qaṭʿ y hamzat al-waṣl y presenta taḥqīq, tashīl, ibdāl, naql e isqāṭ en el desarrollo posterior. El documento heredado conserva provisionalmente esta taxonomía.

La fuente usa grafías transformadas para explicar pronunciación. Esas grafías no autorizan cambios en el texto coránico almacenado.

### Hamz mufrad

REL-001 12-A, líneas 63–165, respalda provisionalmente numerosas condiciones y ocurrencias de ibdāl, naql e isqāṭ, incluidas:

- Las formas derivadas de `الإيواء` citadas como excepción.
- Los casos específicos de hamzah como fāʾ o ʿayn de palabra.
- `اللَّائِي`, `أَرَأَيْتَ` y `هَا أَنتُمْ` con sus contextos.
- La excepción interna `رِدْءًا`.
- Los awjuh correlacionados de `كِتَابِيَهْ إِنِّي` y `مَالِيَهْ هَلَكَ`.
- Las tres formas citadas con isqāṭ.

Cada grupo depende de morfología, ocurrencia y modo de recitación, no sólo de code points contiguos.

### Hamz doble y triple

REL-001 12-A, líneas 169–360, y 12-B, líneas 1–150, respaldan provisionalmente las clases por palabra/frontera y movimientos de las hamzāt, junto con listas de ocurrencias, excepciones y matrices complejas.

La fuente no reduce `ءَآلْـَٔانَ` a un único resultado: sus cinco situaciones producen conjuntos correlacionados de siete, nueve, trece o veintisiete awjuh según la ocurrencia y el contexto.

### Yāʾāt al-iḍāfah y al-zawāʾid

REL-001 12-B, líneas 153–345, presenta definiciones, categorías y listas. Este material sólo puede considerarse inventario provisional porque las líneas 254–269 contienen ejemplos problemáticos y comentarios editoriales de corrección que no son una transcripción limpia de una fuente identificada.

## Hallazgos bloqueantes

### HAM-001 — Tashīl no puede codificarse como sustitución por hāʾ

REL-001 12-A, líneas 18–27, define tashīl como una realización intermedia y declara que debe recibirse oralmente de un shaykh autorizado. Las formas con hāʾ se ofrecen sólo como aproximación pedagógica y la propia fuente recoge desacuerdo sobre esa realización.

El legado devuelve strings como `أَرَهَيْتَ`, `هَهَنْتُمْ` y formas con hāʾ. No son texto coránico alternativo ni una transcripción fonética suficientemente precisa. El motor deberá emitir una categoría de realización y enlazar audio/revisión humana aprobados, sin sustituir la hamzah fuente.

### HAM-002 — Todas las “transformaciones” deben ser anotaciones no destructivas

Ibdāl, naql e isqāṭ se explican mediante expresiones como borrar hamzah, transferir su movimiento o cambiarla por alif/wāw/yāʾ. Es una descripción de recitación. No autoriza a eliminar o reemplazar code points del muṣḥaf.

La salida almacenará el span original, la realización candidata y la evidencia. Al retirar las anotaciones deberá recuperarse exactamente la entrada.

### HAM-003 — La excepción `رِدْءًا` es inalcanzable

Las líneas 507–511 del legado entran en naql sólo si la hamzah está en la palabra siguiente y existe un sākin correcto separado. Dentro de esa condición comprueban `رِدْءًا`, cuya particularidad según REL-001 12-A, líneas 134–135, es precisamente que sākin y hamzah están unidos en una sola palabra.

La precondición exterior excluye el caso antes de evaluarlo. La excepción nunca puede ejecutarse.

### HAM-004 — Hamzat al-istifhām + hamzat al-waṣl queda detrás de ramas genéricas

En el algoritmo de hamz doble, las líneas 540–547 clasifican primero pares abierto/abierto, abierto/ḍammah y abierto/kasrah. Sólo después, en las líneas 549–554, comprueban si la segunda es hamzat al-waṣl.

Los casos especiales de REL-001 12-A, líneas 234–241, pueden ser consumidos por una rama genérica antes de alcanzar su tratamiento de ibdāl con madd, tashīl o eliminación. La identidad funcional de hamzat al-waṣl debe preceder a la clasificación superficial por vocal.

### HAM-005 — `هَا أَنتُمْ` no es una sola palabra

La función de hamz mufrad compara `palabra == "هَا أَنتُمْ"`, aunque la expresión contiene dos palabras y una frontera relevante. Esto demuestra que `palabra` no tiene una semántica consistente.

La futura especificación distinguirá token, secuencia entre tokens, frontera y modo waṣl/waqf.

### HAM-006 — Las excepciones de `الإيواء` dependen de familia morfológica, no de siete strings

REL-001 habla de formas derivadas de una familia y cita siete expresiones. El algoritmo compara strings totalmente vocalizados, sensibles a terminación, rasm y marcas editoriales.

La regla deberá usar análisis morfológico/lexical versionado y ocurrencias verificadas. Una variante de caso gramatical o de composición Unicode no puede cambiar la decisión.

### HAM-007 — Fāʾ/ʿayn de palabra no se deducen de posición visual

Las condiciones principales requieren saber si hamzah es fāʾ o ʿayn de la raíz. Esa es información morfológica, no el primer o segundo carácter visible. Prefijos, artículo, conjunciones y marcas combinantes invalidan un índice simple.

El algoritmo no define fuente ni confianza del análisis. Sin datos aprobados deberá devolver `requires_review`.

### HAM-008 — Naql necesita frontera, pronunciación y excepciones completas

La función pregunta por “hamzah en la siguiente palabra” y “letra anterior sākin correcta”, pero no modela:

- Waṣl frente a waqf.
- Hamzat al-qaṭʿ frente a al-waṣl.
- Signos y fronteras intermedias.
- Inicio de lectura sobre lām al-taʿrīf.
- La excepción interna.
- Los awjuh transmitidos en lugares específicos.

No se reutilizará esta simplificación como prioridad general en otros módulos.

### HAM-009 — `كِتَابِيَهْ` y `مَالِيَهْ` forman elecciones correlacionadas

REL-001 12-A, líneas 137–155, no permite elegir de forma independiente los dos fenómenos. Naql en el primer lugar obliga a idghām en el segundo; abandono de naql se correlaciona con iẓhār y constituye el wajh preferido.

El legado los describe en tablas, pero su función no devuelve una configuración conjunta. El perfil futuro deberá expresar ambas decisiones como un único conjunto compatible con preferencia y evidencia.

### HAM-010 — El inicio sobre lām transferida se omite del algoritmo

REL-001 12-A, líneas 157–160, presenta dos formas de inicio y restricciones distintas de badal. La función de hamz mufrad no implementa este caso.

No puede declararse completa una lógica que omite una rama con awjuh y compatibilidades explícitas de la fuente.

### HAM-011 — Las salidas por defecto confunden taḥqīq con desconocimiento

La línea 518 devuelve taḥqīq para cualquier hamzah que no coincida. Una entrada puede carecer de análisis morfológico, usar otra convención Unicode o pertenecer a un contexto especial no modelado. La falta de reconocimiento no prueba taḥqīq.

Se distinguirán `tahqiq`, `not_applicable`, `unknown`, `unsupported_input` y `requires_review`.

### HAM-012 — El algoritmo de hamz doble puede terminar sin retorno

`aplicar_regla_hamz_muzdawaj`, líneas 528–589, no tiene salida final para fronteras desconocidas, movimientos ausentes, contexto incompleto ni categorías no previstas. Tampoco explica si eso significa taḥqīq o error.

Toda entrada deberá producir un estado tipado y una razón trazable.

### HAM-013 — Los casos especiales de dos kasrah se reducen a una función inexistente

REL-001 12-A, líneas 316–335, da tres o cuatro awjuh en lugares concretos como `هَٰؤُلَاءِ إِن كُنتُمْ`, `الْبِغَاءِ إِنْ أَرَدْنَ` y `النِّسَاءِ إِنِ اتَّقَيْتُنَّ`. El legado delega en `aplicar_casos_especiales_maksurah()` sin definir la función.

No existe una implementación reproducible de esas matrices.

### HAM-014 — `جَاءَ آلَ` no se resuelve con sólo “tashīl o ibdāl”

REL-001 12-A, líneas 278–283, correlaciona tashīl con tres niveles de badal e ibdāl con qaṣr/madd. El legado devuelve únicamente dos etiquetas y una preferencia en las líneas 561–563.

Se pierden duraciones y compatibilidades. Cada wajh deberá incluir todas sus dimensiones.

### HAM-015 — La función de hamz doble no recibe sura, āyah ni token

Casos como `جَاءَ آلَ`, los grupos de dos kasrah y `ءَآلْـَٔانَ` dependen de ocurrencias concretas. La firma sólo recibe dos hamzāt y si están en una o dos palabras, pero consulta después `palabra` y “casos especiales”.

El contrato es insuficiente e internamente inconsistente.

### HAM-016 — `ءَآلْـَٔانَ` no puede ser un retorno opaco

El legado delega en `aplicar_alan_complex()`, pero no define una estructura ejecutable para conservar las cinco situaciones y sus 7/9/13/27/13 awjuh. Las tablas narrativas no bastan para impedir combinaciones inválidas.

La especificación futura representará cada configuración completa mediante:

- Ocurrencia y alcance contextual.
- Tratamiento de hamzat al-waṣl.
- Duración de lām al-badal.
- Badal anterior o posterior.
- Waṣl/waqf.
- Fuente y estado de revisión.

### HAM-017 — La fuente advierte que falta una interacción con ʿāriḍ

REL-001 12-B, línea 149, indica que las situaciones de `ءَآلْـَٔانَ` tienen relación con madd ʿāriḍ, pero que se omitió para no sobrecargar al estudiante. El legado presenta números cerrados como si fueran el espacio completo.

Las matrices no pueden declararse exhaustivas hasta resolver esa nota con fuentes especializadas.

### HAM-018 — Las aproximaciones gráficas de la fuente no son golden text

REL-001 usa hāʾ, yāʾ, wāw, vocales y longitudes para aproximar pronunciaciones transformadas. Algunas notas declaran expresamente ese carácter aproximativo. Copiar esas cadenas como salida esperada modificaría letras y podría confundir explicación con rasm.

Los golden tests verificarán categorías y spans; la validación fonética requerirá audio/revisión experta.

### HAM-019 — La política Unicode de hamzah está ausente

El documento no define cómo relaciona:

- U+0621 hamzah aislada.
- Alif/wāw/yāʾ con hamzah precompuesta.
- Hamzah combinante.
- Convenciones magrebíes del corpus.
- Hamzah facilitada o trasladada como realización, no escritura.

No se normalizará destructivamente. Se necesita una capa analítica que mantenga correspondencia reversible con cada code point fuente.

### HAM-020 — Hamzat al-waṣl es contextual, no una letra que “desaparece” del corpus

La fuente dice que cae en la pronunciación durante waṣl. El motor heredado formula eliminaciones sin separar rasm y recitación. La hamzah/alif escrita permanecerá intacta y la omisión será una anotación fonética condicionada al modo.

### HAM-021 — Yāʾ al-iḍāfah no se implementa en los algoritmos

Las líneas 654–715 del legado añaden una gran sección de yāʾ al-iḍāfah, pero ninguna de las funciones de hamz la procesa. Tampoco existe detector morfológico de yāʾ del hablante, caso gramatical, hamzah siguiente ni excepciones por ocurrencia.

La sección es un inventario, no una lógica ejecutable.

### HAM-022 — Yāʾāt al-zawāʾid requieren una capa de lectura sobre rasm inmutable

REL-001 12-B, líneas 273–345, define esas yāʾāt como añadidas en recitación respecto de los maṣāḥif ʿUthmāniyyah y distingue su estado en waṣl/waqf. La aplicación no puede insertar o borrar letras en el texto fuente para representarlas.

Se modelarán como realizaciones vinculadas a ocurrencias exactas, con posición fonética, modo y fuente.

### HAM-023 — “47 palabras” mezcla ocurrencias y formas

El legado titula su lista “47 palabras”, pero incluye seis ocurrencias de `نُذُرِۦ`, varias repeticiones de `نَكِيرِۦ` y otros lexemas repetidos. REL-001 habla de 47 yāʾāt/posiciones, no necesariamente 47 strings distintos.

La base deberá diferenciar lexema, token, ocurrencia y fenómeno.

### HAM-024 — REL-001 Parte 12-B contiene contaminación editorial no resuelta

Las líneas 254–269 de REL-001 declaran seis palabras en doce lugares, pero incluyen:

- Un ejemplo acompañado de varias alternativas especulativas sobre cuál āyah se pretendía citar.
- Un ejemplo que la propia nota dice no cumplir la condición de alif precedente.
- Un comentario de “corrección” añadido al texto.

Esto no puede utilizarse como fuente normativa. Deben consultarse las páginas físicas, las obras citadas y un especialista. La copia se conserva intacta como evidencia del problema; no se corrige silenciosamente.

### HAM-025 — La lista de once lugares contiene un khilāf no reducible a una fila

REL-001 12-B, líneas 236–251, incluye `وَمَحْيَايَ` entre lugares abiertos, pero después registra khilāf y dice que la lectura aplicada es sukūn con madd de seis. El legado la marca simplemente como “khilāf: sukūn/fatḥ”.

La futura entrada deberá distinguir opciones transmitidas, lectura adoptada, preferencia y efecto sobre madd; no será un booleano abierto/cerrado.

### HAM-026 — Las listas manuales no prueban completitud

Los encabezados “lista completa”, los conteos de palabras/lugares y las sumas de combinaciones pueden contener errores de transcripción o de unidad, como demuestra la propia Parte 12-B. Ningún conteo se aprobará sin reconciliar:

- Página física.
- Corpus versionado.
- Identificadores de ocurrencia.
- Fuentes autorizadas.
- Revisión humana.

### HAM-027 — Las reglas cruzan módulos y necesitan configuración común

Hamz interactúa con badal, madd, naql, idghām, sakt, waṣl/waqf, rawm y morfología. No puede resolverse como módulo aislado que retorna un string.

Las elecciones correlacionadas deberán compartir un perfil de recitación versionado para impedir combinaciones incompatibles entre reglas.

## Modelo mínimo que deberá reemplazarlo

La futura especificación deberá separar:

```text
texto coránico inmutable + ocurrencia/token/span
  + identidad y función de cada hamzah
  + morfología y frontera de palabra
  + movimientos escritos y realización recitada
  + modo: ibtida | wasl | waqf_sukun | waqf_rawm | unknown
  + contexto de madd/naql/idgham/sakt
  + perfil de lectura y elecciones correlacionadas
  → conjunto de awjuh completos
  → realización fonética no destructiva
  → preferencia y autoridad
  → evidencia por dimensión
  → aprobación humana, incluida validación oral de tashil
```

Las yāʾāt se modelarán como un dominio relacionado pero separado, con ocurrencias propias y relación reversible con el rasm.

## Casos que la nueva especificación deberá incluir

- Cada clase de hamz mufrad y sus casos negativos.
- Todas las formas citadas de `الإيواء` con variación gramatical y de rasm.
- `رِدْءًا` para probar prioridad de excepción interna.
- `كِتَابِيَهْ` y `مَالِيَهْ` como configuraciones correlacionadas.
- Inicio sobre lām al-taʿrīf tras naql, con cada duración compatible.
- Las tres ocurrencias citadas de isqāṭ, sin editar el texto fuente.
- Cada patrón de hamz doble dentro de una palabra y entre palabras.
- Hamzat al-istifhām + hamzat al-waṣl antes de reglas genéricas.
- Todos los lugares especiales de dos kasrah.
- `جَاءَ آلَ` con todas sus dimensiones de badal.
- Cada una de las cinco situaciones de `ءَآلْـَٔانَ` y sus configuraciones completas.
- Tashīl validado oralmente, no mediante comparación de letras sustituidas.
- Cada categoría de yāʾ al-iḍāfah y sus excepciones por ocurrencia.
- Las 47 ocurrencias candidatas de yāʾāt al-zawāʾid reconciliadas con corpus y fuente física.
- Waṣl, ibtidāʾ, waqf con sukūn y waqf con rawm.
- Reconstrucción exacta del corpus después de retirar anotaciones.

## Decisión de migración

- Conservar el archivo original como legado y catálogo de investigación.
- No migrar sus algoritmos ni las grafías pedagógicas como texto de salida.
- Verificar físicamente la Parte 12-B antes de usar sus listas de yāʾāt.
- Reescribir hamz en especificaciones pequeñas por fenómeno y ocurrencia.
- Modelar los awjuh como configuraciones correlacionadas y versionadas.
- Exigir validación oral de tashīl por especialista cualificado.
- Mantener toda conclusión religiosa como candidata hasta revisión del especialista.

## Próximo documento

Según el orden aprobado, continúa `PALETA_COLORES_WARSH.md`. Se auditará únicamente como propuesta heredada de presentación, nunca como fuente religiosa.
