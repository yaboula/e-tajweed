# Decisión consolidada sobre `analisis_tajweed_warsh`

- **Identificador de custodia:** LEGACY-ANALYSIS-001
- **Alcance:** 11 artefactos heredados
- **Estado de la auditoría:** completada
- **Estado del trabajo:** revisión y corrección, un documento cada vez
- **Decisión global:** conservar una copia de custodia y migrar los documentos con su nombre original para compararlos con el libro y corregirlos.

## Resultado ejecutivo

`analisis_tajweed_warsh` contiene conocimiento útil derivado del libro, pero no constituye una especificación religiosa ni técnica confiable. Sus documentos mezclan afirmaciones respaldadas, interpretación, pseudocódigo, convenciones editoriales, colores, ejemplos no verificados y etiquetas de completitud.

La decisión no es desechar el trabajo anterior. Se conservará íntegramente por su valor histórico y como índice de preguntas. Lo que se rechaza es reutilizarlo directamente como:

- Código o pseudocódigo del motor.
- Árbol normativo de reglas.
- Fuente de excepciones aprobadas.
- Golden tests.
- Política Unicode.
- Mecanismo de resolución de solapamientos.

La excepción es `PALETA_COLORES_WARSH.md`: por decisión del propietario, es la referencia válida para las nueve categorías y colores de salida. No se usa como fuente de las condiciones religiosas de detección.

Cada afirmación recuperable deberá atravesar la cadena:

```text
fuente física identificada
  → página y pasaje
  → corrección del documento migrado
  → ocurrencias verificadas en corpus aprobado
  → pruebas positivas, negativas y fronterizas
  → validación manual del propietario contra el muṣḥaf certificado
  → implementación controlada
  → revisión final del especialista antes de la aprobación definitiva
```

## Qué se conserva intacto

### REL-001 — Libro de trabajo

Las 14 partes bajo custodia se conservan sin edición como fuente primaria de trabajo. Su hash de árbol es:

`5c0a5003126b76056430535faec8b0300045b7849db7369be8406e9870d172b2`

REL-001 todavía no equivale a una autoridad final. Algunas transcripciones, especialmente en la Parte 12-B, contienen notas editoriales y ejemplos problemáticos que obligan a consultar las páginas físicas.

### LEGACY-ANALYSIS-001 — Análisis derivado

Los 11 archivos se conservan byte por byte en la copia privada bajo custodia. Su hash de árbol es:

`e272d53d40834884388ad8d16369462161445a7fc5e769ea64a7595026329a81`

Esta copia privada permanece intacta como referencia histórica. En e-tajweed se migra cada documento con el mismo nombre y se corrige directamente; Git registra cada cambio.

## Decisión por artefacto

### `Fahrass.md`

- **Estado:** `source_check`.
- **Se conserva como:** índice provisional de navegación.
- **No se acepta como:** prueba de que cada título, parte y página coincide con la edición física.
- **Acción futura:** reconciliarlo con el ejemplar físico de REL-001.

Informe: [fahrass-audit.md](./fahrass-audit.md).

### `ARBOL_COMPLETO_REGLAS_TAJWEED.md`

- **Estado:** `rejected`.
- **Se conserva como:** mapa histórico de intenciones y preguntas.
- **No se migra como:** árbol completo, especificación, política Unicode ni golden tests.
- **Razón principal:** alcance incompleto, ejemplos mal clasificados, corpus no reproducible y mezcla de regla con presentación.

Informe: [arbol-completo-audit.md](./arbol-completo-audit.md).

### `DECISION_LOGIC_QALQALAH.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado con su nombre original y corregido contra las páginas 61–62.
- **Correcciones principales:** sukūn no inferido por ausencia de vocal, waqf explícito, rangos Unicode corregidos y color separado de la decisión religiosa.
- **Validación prevista:** comprobación manual del propietario contra el muṣḥaf coloreado y certificado durante la implementación.

Informe: [qalqalah-audit.md](./qalqalah-audit.md).
Documento corregido: [DECISION_LOGIC_QALQALAH.md](./DECISION_LOGIC_QALQALAH.md).

### `DECISION_LOGIC_NUUN_TANWEEN.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado con su nombre original y corregido contra las páginas 67–72.
- **Correcciones principales:** waṣl/waqf explícito, casos `يس`/`ن` alcanzables, Unicode no destructivo, incertidumbre y separación entre decisiones que comparten verde.
- **Coloración:** iẓhār negro; idghām con ghunnah, iqlāb e ikhfāʾ verdes; idghām sin ghunnah gris.

Informe: [nuun-tanween-audit.md](./nuun-tanween-audit.md).
Documento corregido: [DECISION_LOGIC_NUUN_TANWEEN.md](./DECISION_LOGIC_NUUN_TANWEEN.md).

### `DECISION_LOGIC_MEEM_SAKINAH.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado con su nombre original y corregido contra las páginas 75–76.
- **Correcciones principales:** identidad de mīm sākinah no limitada a U+0652, frontera y waṣl/waqf explícitos, ejemplo de Al-Fīl corregido, Unicode no destructivo, incertidumbre para `مْ + م` dentro de palabra y eliminación de la doble detección tras iqlāb.
- **Coloración:** ikhfāʾ e idghām shafawī verdes; iẓhār shafawī negro; la advertencia ante fāʾ/wāw queda como metadato sin alterar la regla ni el color.

Informe: [meem-sakinah-audit.md](./meem-sakinah-audit.md).
Documento corregido: [DECISION_LOGIC_MEEM_SAKINAH.md](./DECISION_LOGIC_MEEM_SAKINAH.md).

### `DECISION_LOGIC_TAFKHIM_TARQIQ.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado con su nombre original y corregido contra las páginas 79–88.
- **Correcciones principales:** excepciones y awjuh antes de reglas generales, perfiles de badal correlacionados, waṣl/waqf explícitos, elegibilidad de ishmām/rawm, U+06EA sólo como señal editorial y ocurrencias separadas de strings vocalizados.
- **Coloración:** tafkhīm/taghlīẓ azul oscuro `#00008B`; tarqīq negro `#000000`; los casos de dos awjuh conservan ambas salidas y su preferencia.

Informe: [tafkhim-tarqiq-audit.md](./tafkhim-tarqiq-audit.md).
Documento corregido: [DECISION_LOGIC_TAFKHIM_TARQIQ.md](./DECISION_LOGIC_TAFKHIM_TARQIQ.md).

### `DECISION_LOGIC_IDGHAM.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado con su nombre original y corregido contra las páginas 91–94.
- **Correcciones principales:** separación kabīr/ṣaghīr, ejemplos no convertidos en listas exclusivas, waṣl/waqf explícitos, pares transmitidos, morfología real para dhāl→tāʾ, awjuh tipados de qāf→kāf y precondición de artículo para lām al-taʿrīf.
- **Coloración:** idghām general y lām shamsiyyah grises; iẓhār qamariyyah y negativos explícitos negros; nūn/mīm con ghunnah —incluidos los casos citados de kabīr— verdes.

Informe: [idgham-audit.md](./idgham-audit.md).
Documento corregido: [DECISION_LOGIC_IDGHAM.md](./DECISION_LOGIC_IDGHAM.md).

### `DECISION_LOGIC_FATH_IMALAH.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado íntegro con el nombre original y corregido contra las páginas 97–101 de la Parte 10.
- **Correcciones principales:** precedencia de excepciones (`ذِكْرَاهَا`, `الْجَارِ`, fawātiḥ), iltiqāʾ resuelto antes de la salida final y sólo sobre el alif suprimido fonéticamente, iʿrāb/morfología/ocurrencia verificados, badal correlacionado y estados de incertidumbre explícitos.
- **Presentación:** la paleta aceptada no asigna color a fatḥ, taqlīl o imālah kubrā; queda una decisión de producto pendiente, sin crear ni remapear colores.

Informe: [fath-imalah-audit.md](./fath-imalah-audit.md).
Documento corregido: [DECISION_LOGIC_FATH_IMALAH.md](./DECISION_LOGIC_FATH_IMALAH.md).

### `DECISION_LOGIC_MUDUD.md`

- **Estado:** `corrected`.
- **Acción realizada:** migrado íntegro con el nombre original y corregido contra las páginas 105–114 de la Parte 11.
- **Correcciones principales:** detección por span, ramas independientes para `أَنَا`, mīm al-jamʿ, ṣilah, ʿiwaḍ y fawātiḥ; excepciones de badal antes del resultado general; ʿayn 4/6, layn 4/6 y cuatro awjuh correlacionados de `سَوْءَاتٍ` preservados; perfil de lectura, waṣl/waqf/ibtidāʾ e incertidumbre explícitos.
- **Pendiente:** contraste editorial de `سَوْءَاتٍ`, no extrapolar 6/2 de Āl ʿImrān a al-ʿAnkabūt, y decidir presentación de casos no asignados expresamente por la paleta.

Informe: [mudud-audit.md](./mudud-audit.md).
Documento corregido: [DECISION_LOGIC_MUDUD.md](./DECISION_LOGIC_MUDUD.md).

### `DECISION_LOGIC_HAMZ.md`

- **Estado:** `corrected` tras cotejo de los PDF originales; conserva `requires_review` donde falta validación de ocurrencia o de awjuh completos.
- **Acción realizada:** migrado íntegro con el nombre original y corregido contra las Partes 12-A/12-B, pp. 117–154.
- **Correcciones principales:** prioridad de casos especiales y hamzat al-waṣl, naql interno alcanzable, `كِتَابِيَهْ`/`مَالِيَهْ` vinculados, awjuh completos de dos kasrah y `جَاءَ آلَ`, cinco situaciones de `ءَآلْـَٔانَ` con límites, yāʾāt modeladas aparte, Unicode/rasm no destructivos y taḥqīq nunca por defecto.
- **Cotejo posterior:** el PDF impreso ubica `ءَأَلِدُ` (Hūd 11:72) entre las dos hamzāt y equipara `ءَأَلِهَتُنَا` con `ءَأَمِنتُم` en p. 138; p. 151 declara seis lexemas en doce lugares, sin los ejemplos especulativos de la transcripción. Se conserva la numeración impresa y se mapeará al muṣḥaf certificado antes de activar cada ocurrencia. ʿĀriḍ omitido de las matrices de `ءَآلْـَٔانَ` y tashīl oral siguen pendientes de revisión experta.

Informe: [hamz-audit.md](./hamz-audit.md).
Documento corregido: [DECISION_LOGIC_HAMZ.md](./DECISION_LOGIC_HAMZ.md).

### `PALETA_COLORES_WARSH.md`

- **Estado:** `accepted_product_reference`.
- **Se acepta como:** definición obligatoria de las nueve categorías visuales, sus familias cromáticas y su significado, respaldada por la imagen oficial `PAL-001` entregada por el propietario.
- **No se usa como:** fuente religiosa para decidir si una regla está presente.
- **Implementación:** puede crear tonos derivados con ajustes ligeros de contraste, luminosidad o saturación, además de accesibilidad y metadatos, sin cambiar el mapeo semántico de la paleta.

Informe: [palette-audit.md](./palette-audit.md).

## Qué se migrará para revisar

Los documentos se migrarán uno por uno con sus nombres originales. Para cada uno se:

- comparará cada afirmación con el libro;
- corregirán errores religiosos, lógicos, Unicode o de trazabilidad en el propio archivo;
- conservarán las partes correctas;
- registrarán las dudas sin inventar una respuesta;
- prepararán casos concretos para la validación manual del propietario.

Una etiqueta como “completo”, “sin excepciones” o “verificación matemática” sólo se conservará si puede demostrarse.

## Qué se creará desde cero

Cuando se autorice la siguiente fase, deberán crearse de nuevo:

- Registro de fuentes con edición, procedencia, licencia y páginas verificadas.
- Perfil religioso exacto de Warsh ʿan Nāfiʿ por ṭarīq al-Azraq y método adoptado.
- Corpus coránico autorizado, hasheado y con licencia clara.
- Mapa reversible de code points, grafemas, tokens y ocurrencias.
- Esquema formal de regla, excepción, wajh, preferencia y evidencia.
- Configuración explícita de waṣl, waqf, ibtidāʾ y tipos de waqf.
- Modelo de incertidumbre y revisión.
- Resolución de solapamientos basada en conocimiento, no colores ni orden accidental de `if`.
- Golden tests aprobados manualmente.
- Pruebas de integridad y reconstrucción exacta del texto.
- Capa de presentación accesible, multicanal y separada del motor.

## Bloqueos antes de crear especificaciones normativas

### Identidad de las fuentes

Se necesita identificar la edición física de REL-001 y contrastar cada página citada. La Parte 12-B tiene prioridad por sus anomalías editoriales.

### Autoridades complementarias

Cada regla deberá contrastarse con obras autorizadas para Warsh por ṭarīq al-Azraq. `docs/refrences.md` contiene el catálogo inicial, pero todavía deben registrarse edición, página y licencia de cada obra efectivamente usada.

### Revisión humana y especialista cualificado

Durante el desarrollo, el propietario realizará la comprobación manual precisa contra un muṣḥaf coloreado y certificado de Warsh ʿan Nāfiʿ por ṭarīq al-Azraq. Esta validación permite avanzar de forma controlada.

Antes de declarar definitiva la aplicación se buscará el respaldo final de un profesor, qāriʾ o especialista cualificado para revisar:

- Exactitud religiosa.
- Awjuh permitidos y preferencias.
- Tashīl y demás realizaciones orales.
- Casos de waṣl/waqf.
- Golden tests visuales y fonéticos.

### Corpus y muṣḥaf de referencia

El dataset heredado no puede adoptarse todavía como corpus normativo. Usa convenciones editoriales particulares y glifos U+FCxx como números visuales de āyah. Deben resolverse procedencia, licencia, versión, rasm y referencia visual.

## Estado de `knowledge/`

No se ha aprobado ni escrito ninguna regla normativa en `knowledge/rules`, `knowledge/exceptions`, `knowledge/evidence` o `knowledge/reviews`.

Esto es intencional. La auditoría separó evidencia de legado y conocimiento aprobado; no convirtió automáticamente un resumen heredado en verdad del motor.

## Próxima fase recomendada

El trabajo continuará **verticalmente, un documento cada vez**. Los ocho documentos `DECISION_LOGIC_*` ya tienen una copia migrada y una revisión documental en el mismo archivo. El PDF original permitió resolver las falsas contradicciones de hamz en pp. 138 y 151. Las ocurrencias y las combinaciones omitidas con ʿāriḍ deberán resolverse dentro de la verificación exhaustiva contra *الدليل الأوفق*, antes de crear el motor. La paleta sigue siendo referencia aceptada y no necesita ser reescrita para cerrar esta tanda.

Orden recomendado:

1. Mantener los ocho documentos corregidos; activar cada ocurrencia de hamz sólo tras mapearla al muṣḥaf certificado y conservar `requires_review` en las combinaciones no cubiertas con ʿāriḍ.
2. Antes de decidir otro documento, resolver qué entradas pendientes del análisis heredado conviene tratar a continuación; no modificar la paleta aceptada por analogía.
3. Tras superar la puerta documental previa, al implementar cada regla el propietario vuelve a comprobar los resultados del motor contra el muṣḥaf certificado. Esta comprobación operativa no sustituye la verificación exhaustiva anterior.

Antes de crear el motor se efectuará una verificación completa y exhaustiva de las reglas contra *الدليل الأوفق*. No se sustituirá esta puerta por verificaciones parciales. La revisión del especialista se conserva como control final de la aplicación.
