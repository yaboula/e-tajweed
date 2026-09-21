# Plan de auditoría de `analisis_tajweed_warsh`

- **Identificador:** LEGACY-ANALYSIS-001
- **Estado global:** revisión correctiva en curso; Qalqalah corregida
- **Importancia:** crítica

## Cambio de método

Este plan queda como registro histórico de la auditoría inicial. El trabajo activo continúa verticalmente, una sola regla cada vez: revisar, corregir, validar y sólo después elegir la siguiente.

La primera regla, **Qalqalah**, ha sido corregida en [DECISION_LOGIC_QALQALAH.md](./DECISION_LOGIC_QALQALAH.md). La validación manual contra el muṣḥaf se realizará durante la implementación. El siguiente documento podrá revisarse en la próxima etapa, sin tratar varios a la vez.

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

- `PALETA_COLORES_WARSH.md` sólo después de estabilizar las reglas. La paleta será una decisión de presentación accesible, nunca una fuente religiosa ni un mecanismo para resolver solapamientos.

## Registro inicial por documento

- `Fahrass.md` — `source_check`; aceptable sólo como índice provisional de navegación; pendiente de contrastar REL-001 con la edición impresa.
- `ARBOL_COMPLETO_REGLAS_TAJWEED.md` — `rejected`; no puede migrarse como árbol completo, especificación, golden tests ni política Unicode. Se conserva únicamente para extraer afirmaciones que deberán volver a verificarse.
- `DECISION_LOGIC_QALQALAH.md` — `corrected`; migrado y corregido contra las páginas 61–62; sus resultados se comprobarán manualmente durante la implementación.
- `DECISION_LOGIC_NUUN_TANWEEN.md` — `rejected`; el núcleo clasificatorio coincide provisionalmente con la Parte 7, pero el algoritmo no controla waṣl/waqf de forma general, depende de signos Unicode no uniformes y contiene una rama especial inalcanzable.
- `DECISION_LOGIC_MEEM_SAKINAH.md` — `rejected`; el núcleo coincide provisionalmente con las páginas 75–76, pero el algoritmo falla sobre las convenciones del propio corpus, clasifica mal una frontera de palabra e implementa una hipótesis que declara no documentada.
- `DECISION_LOGIC_TAFKHIM_TARQIQ.md` — `rejected`; conserva un inventario amplio de la Parte 8, pero el orden de retornos vuelve inalcanzables múltiples awjuh y excepciones, y sus coincidencias Unicode/textuales no son seguras.
- `DECISION_LOGIC_IDGHAM.md` — `rejected`; recupera pares citados en la Parte 9, pero convierte ejemplos en listas exclusivas, omite waṣl/waqf, no implementa idghām kabīr y extiende iẓhār fuera de su dominio.
- `DECISION_LOGIC_FATH_IMALAH.md` — `rejected`; conserva numerosas categorías de la Parte 10, pero evalúa excepciones e iltiqāʾ al-sākinayn después de retornos definitivos y depende de análisis contextuales no definidos.
- `DECISION_LOGIC_MUDUD.md` — `rejected`; inventaría muchas categorías de la Parte 11, pero su algoritmo borra excepciones y awjuh, deja layn sin resolución y aplica prioridad a palabras en vez de spans concretos.
- `DECISION_LOGIC_HAMZ.md` — `rejected`; conserva un catálogo amplio de las Partes 12-A/12-B, pero contiene ramas inalcanzables, pierde awjuh correlacionados y depende de una sección de fuente con correcciones editoriales no resueltas.
- `PALETA_COLORES_WARSH.md` — `rejected`; carece de fuente verificable, usa color como único canal, falla contrastes y propone tachar texto coránico y resolver solapamientos mediante prioridad visual.

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

### AUD-006 — La paleta carece de fundamento trazable suficiente

`PALETA_COLORES_WARSH.md` cita como fuente visual un “Diagrama circular Tajweed Warsh” sin identificación verificable. Sus prioridades de color mezclan presentación con resolución de reglas coincidentes y no incluyen validación de accesibilidad.

### AUD-007 — Propuesta visual no aceptable

La paleta propone `text-decoration: line-through` para letras no pronunciadas o asimiladas. e-tajweed no aplicará tachado al texto coránico. La información deberá representarse mediante una capa no destructiva, respetuosa y accesible, aprobada visualmente.

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
