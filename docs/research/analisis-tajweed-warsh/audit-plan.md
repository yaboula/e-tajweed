# Plan de auditoría de `analisis_tajweed_warsh`

- **Identificador:** LEGACY-ANALYSIS-001
- **Estado global:** revisión correctiva en curso; Qalqalah, nūn/tanwīn, mīm sākinah, tafkhīm/tarqīq e idghām corregidos
- **Importancia:** crítica

## Cambio de método

Este plan queda como registro histórico de la auditoría inicial. El trabajo activo continúa verticalmente, una sola regla cada vez: revisar, corregir, validar y sólo después elegir la siguiente.

**Qalqalah**, **nūn/tanwīn**, **mīm sākinah**, **tafkhīm/tarqīq** e **idghām** han sido corregidos en sus documentos migrados. Antes de crear el motor, todas las reglas pasarán conjuntamente por una verificación completa y exhaustiva contra *الدليل الأوفق*. Después, los resultados concretos del motor se validarán manualmente contra el muṣḥaf durante la implementación. El siguiente documento podrá revisarse en la próxima etapa, sin tratar varios a la vez.

## Regla principal

Los documentos heredados son material de trabajo derivado del libro. Se migran con sus nombres originales, se comparan uno por uno con el libro y se corrigen en el propio documento cuando exista un error.

La copia privada y Git conservan el estado original. No se creará una especificación paralela para sustituir cada documento corregido.

## Controles que debe superar cada documento

1. **Integridad:** confirmar el SHA-256 contra el manifiesto de custodia.
2. **Alcance:** enumerar exactamente qué reglas afirma cubrir y qué deja fuera.
3. **Trazabilidad:** vincular cada afirmación normativa con fuente, edición y página concreta.
4. **Exactitud religiosa:** contrastar regla general, excepciones, awjuh, preferencias, waṣl y waqf.
5. **Revisión lingüística:** comprobar terminología árabe, traducción y morfología necesaria.
6. **Modelo algorítmico:** separar observación, condición, contexto, excepción, prioridad y resultado.
7. **Unicode:** verificar code points, grafemas, marcas combinantes, orden y signos específicos del corpus.
8. **Corpus:** probar ejemplos, numeración de āyāt y afirmaciones de frecuencia sobre un corpus identificado y hasheado.
9. **Solapamientos:** demostrar qué ocurre cuando coinciden varias reglas; no resolverlos sólo mediante prioridad de color.
10. **Pruebas:** producir positivos, negativos, fronterizos y golden tests revisados.
11. **Presentación:** separar detección religiosa de color, estilo y accesibilidad.
12. **Validación humana:** durante el desarrollo, el propietario comprobará manualmente los resultados contra un muṣḥaf coloreado y certificado de Warsh ʿan Nāfiʿ por ṭarīq al-Azraq. La revisión del especialista será un control final antes de declarar definitiva la aplicación.

## Estados permitidos

- `unreviewed`: sólo inventariado.
- `structural_review`: estructura y afirmaciones localizadas, sin validar su verdad.
- `source_check`: comparación detallada con fuentes en curso.
- `technical_check`: Unicode, algoritmo, corpus y pruebas en curso.
- `corrected`: errores documentales o técnicos corregidos contra la fuente.
- `owner_validation`: comprobación manual contra el muṣḥaf certificado en curso.
- `development_ready`: validado por el propietario y utilizable para implementación controlada.
- `final_expert_review`: listo para la revisión final del especialista.
- `final_approved`: aprobado para una versión definitiva.
- `accepted_product_reference`: decisión válida del propietario para alcance, categorías o presentación.
- `needs_rework`: contiene errores que todavía deben corregirse.

La implementación controlada puede comenzar en `development_ready`. Sólo `final_approved` permite presentar una regla como definitivamente aprobada por el proyecto.

## Orden de revisión

### Etapa 0 — Mapa y cobertura

- `Fahrass.md`: comprobar que el índice corresponde realmente a las partes y páginas del libro.
- `ARBOL_COMPLETO_REGLAS_TAJWEED.md`: auditar alcance, terminología, ejemplos, corpus y afirmaciones Unicode.

### Etapa 1 — Fundamentos y reglas locales

- `DECISION_LOGIC_QALQALAH.md` contra la Parte 6.
- `DECISION_LOGIC_NUUN_TANWEEN.md` contra la Parte 7.
- `DECISION_LOGIC_MEEM_SAKINAH.md` contra la Parte 7.

### Etapa 2 — Reglas contextuales y solapamientos

- `DECISION_LOGIC_TAFKHIM_TARQIQ.md` contra la Parte 8.
- `DECISION_LOGIC_IDGHAM.md` contra la Parte 9.
- `DECISION_LOGIC_FATH_IMALAH.md` contra la Parte 10.

### Etapa 3 — Reglas de mayor complejidad

- `DECISION_LOGIC_MUDUD.md` contra la Parte 11.
- `DECISION_LOGIC_HAMZ.md` contra las Partes 12-A y 12-B.

### Etapa 4 — Presentación

- `PALETA_COLORES_WARSH.md` es la referencia válida del proyecto para las nueve salidas visuales. Se usa desde el inicio como objetivo de coloración; las mejoras técnicas no pueden sustituir sus categorías o colores sin decisión del propietario.

## Registro inicial por documento

- `Fahrass.md` — `source_check`; aceptable sólo como índice provisional de navegación; pendiente de contrastar REL-001 con la edición impresa.
- `ARBOL_COMPLETO_REGLAS_TAJWEED.md` — `rejected`; no puede migrarse como árbol completo, especificación, golden tests ni política Unicode. Se conserva únicamente para extraer afirmaciones que deberán volver a verificarse.
- `DECISION_LOGIC_QALQALAH.md` — `corrected`; migrado y corregido contra las páginas 61–62; sus resultados se comprobarán manualmente durante la implementación.
- `DECISION_LOGIC_NUUN_TANWEEN.md` — `corrected`; migrado y corregido contra las páginas 67–72, con waṣl/waqf, Unicode no destructivo, casos especiales alcanzables y mapeo negro/verde/gris.
- `DECISION_LOGIC_MEEM_SAKINAH.md` — `corrected`; migrado y corregido contra las páginas 75–76, con identidad dependiente del corpus, frontera y waṣl/waqf explícitos, Unicode no destructivo, incertidumbre para el caso interno y mapeo verde/negro.
- `DECISION_LOGIC_TAFKHIM_TARQIQ.md` — `corrected`; migrado y corregido contra las páginas 79–88, con awjuh prioritarios, perfiles correlacionados, waṣl/waqf, Unicode no destructivo, ocurrencias explícitas y mapeo azul oscuro/negro.
- `DECISION_LOGIC_IDGHAM.md` — `corrected`; migrado y corregido contra las páginas 91–94, con idghām kabīr/ṣaghīr separados, pares transmitidos, waṣl/waqf, morfología explícita, awjuh no destructivos, lām al-taʿrīf validada y mapeo gris/negro/verde.
- `DECISION_LOGIC_FATH_IMALAH.md` — `corrected`; migrado intacto antes de editar y corregido contra las páginas 97–101: excepciones antes de reglas generales, iltiqāʾ antes del resultado final, clasificación verificada, awjuh correlacionados y rasm inmutable. Pendiente decidir presentación: la paleta no asigna color propio a fatḥ/imālah.
- `DECISION_LOGIC_MUDUD.md` — `corrected`; migrado intacto antes de editar y corregido contra las páginas 105–114: decisiones por span, causas y excepciones conservadas, awjuh de ʿayn/layn/badal y matrices vinculadas, waṣl/waqf/ibtidāʾ, incertidumbre y rasm inmutable. Algunos casos visuales no tienen asignación expresa en la paleta.
- `DECISION_LOGIC_HAMZ.md` — `corrected`; migrado intacto antes de editar y cotejado además con el PDF de la sexta edición y *الدليل الأوفق*: excepciones antes de patrones generales, pares y triples con awjuh correlacionados, naql/idghām/sakt en perfil, yāʾāt separadas y rasm inmutable. El falso conflicto de Hūd 11:72 y la lista alterada de p. 151 se corrigieron contra las páginas impresas; permanecen pendientes el mapeo al corpus certificado, ʿāriḍ omitido en p. 144 y la validación oral de tashīl.
- `PALETA_COLORES_WARSH.md` — `accepted_product_reference`; junto con la imagen oficial `PAL-001`, define las nueve categorías, sus familias cromáticas y su significado. Los tonos de interfaz pueden recibir ajustes ligeros y documentados de contraste sin remapear la paleta.

## Hallazgos preliminares bloqueantes

Estos hallazgos proceden de la revisión estructural inicial. Todavía no constituyen la auditoría religiosa completa.

### AUD-001 — El alcance declarado no coincide con el título

`ARBOL_COMPLETO_REGLAS_TAJWEED.md` se presenta como árbol completo, pero declara estar basado en la Parte 7, un CSV Unicode y datos de Al-Baqarah; al final indica que sólo las primeras 100 āyāt fueron analizadas en detalle. No puede utilizarse como árbol completo del proyecto.

### AUD-002 — Ejemplos incompatibles con la clasificación

Dentro de la sección de ikhfāʾ aparecen, entre otros, `لَا رَيْبَ فِيهِ` descrito mediante `ب + ف` aunque no hay nūn sākinah ni tanwīn que active esa regla, y `عَذَابٌ عَظِيم` aunque `ع` aparece en el mismo documento entre las letras de iẓhār. También se describe `أَنفُسَهُمْ` como ikhfāʾ “antes de أ”, cuando el contexto relevante de la nūn es la `ف` siguiente. Estos casos demuestran que los ejemplos no pueden migrarse como golden tests.

### AUD-003 — Estadísticas y corpus sin procedencia suficiente

El árbol usa cifras estimadas, frecuencias Unicode y resultados de `warshData_v2-1.sql` sin que esos datasets estén todavía bajo custodia, versión, licencia y hash en e-tajweed. Todas esas cifras quedan sin validar.

### AUD-004 — Regla religiosa mezclada con convención tipográfica

El documento infiere reglas a partir de la presencia o ausencia visual de sukūn y otros signos. Una convención de un muṣḥaf puede servir como señal del corpus concreto, pero no sustituye la regla religiosa y no es necesariamente portable a otro corpus.

### AUD-005 — Caso reconocido como no documentado

`DECISION_LOGIC_MEEM_SAKINAH.md` incluye en su pseudocódigo un resultado descrito como “caso no documentado en libro - verificar”. Esta rama queda prohibida para implementación hasta localizar una fuente aceptada y obtener revisión.

### AUD-006 — Función de la paleta aclarada por el propietario

`PALETA_COLORES_WARSH.md` ha sido declarada referencia válida del producto para las nueve categorías visuales. No sustituye al libro como fuente de las condiciones religiosas, pero sus asociaciones de categoría y color son obligatorias.

### AUD-007 — Implementación visual pendiente de validación

Los detalles de CSS, contraste y canales complementarios se comprobarán durante el desarrollo contra el muṣḥaf de referencia. Toda representación será una capa no destructiva y no alterará los caracteres coránicos.

### AUD-008 — Etiquetas de completitud sin evidencia suficiente

Expresiones como “algoritmo completo”, “lista completa” o “verificación matemática” no equivalen a validación. Deberán reemplazarse por evidencia reproducible: corpus fijado, casos comprobados, cobertura de excepciones y aprobación humana.

## Salidas de la auditoría

La decisión consolidada y el estado de cada artefacto se encuentran en [audit-summary.md](./audit-summary.md).

Cada documento producirá, por separado:

- Un informe de afirmaciones y fuentes.
- Una lista de contradicciones, ambigüedades y preguntas abiertas.
- El propio documento migrado y corregido, manteniendo su nombre original.
- Casos de prueba candidatos con procedencia.
- Un estado claro dentro del flujo de revisión y validación.

Los documentos en `development_ready` podrán orientar una implementación controlada. La promoción definitiva se reservará para los resultados con validación final.
