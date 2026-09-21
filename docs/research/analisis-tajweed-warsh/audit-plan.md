# Plan de auditoría de `analisis_tajweed_warsh`

- **Identificador:** LEGACY-ANALYSIS-001
- **Estado global:** bloqueado para implementación; Etapa 0 completada
- **Importancia:** crítica

## Regla principal

Los documentos heredados son hipótesis de trabajo. No son especificaciones aprobadas y no pueden alimentar el motor, los colores ni los golden tests hasta superar todos los controles de este plan.

Los archivos originales se conservarán sin edición. Las correcciones y conclusiones se escribirán como artefactos nuevos y trazables.

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
12. **Aprobación humana:** obtener revisión final del especialista cualificado.

## Estados permitidos

- `unreviewed`: sólo inventariado.
- `structural_review`: estructura y afirmaciones localizadas, sin validar su verdad.
- `source_check`: comparación detallada con fuentes en curso.
- `technical_check`: Unicode, algoritmo, corpus y pruebas en curso.
- `expert_review`: listo para valoración del especialista.
- `approved`: puede originar conocimiento versionado.
- `rejected`: no debe migrarse.
- `superseded`: reemplazado por una especificación aprobada posterior.

Ningún estado anterior a `approved` permite implementar la lógica como normativa.

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
- `DECISION_LOGIC_QALQALAH.md` — `unreviewed`; referencia declarada: Parte 6, páginas 56-64.
- `DECISION_LOGIC_NUUN_TANWEEN.md` — `unreviewed`; referencia declarada: Parte 7.
- `DECISION_LOGIC_MEEM_SAKINAH.md` — `structural_review`; contiene al menos un caso expresamente descrito como no documentado y pendiente de verificar.
- `DECISION_LOGIC_TAFKHIM_TARQIQ.md` — `unreviewed`; referencia declarada: Parte 8, páginas 77-88.
- `DECISION_LOGIC_IDGHAM.md` — `unreviewed`; referencia declarada: Parte 9, páginas 91-94.
- `DECISION_LOGIC_FATH_IMALAH.md` — `unreviewed`; referencia declarada: Parte 10.
- `DECISION_LOGIC_MUDUD.md` — `unreviewed`; referencia declarada: Parte 11.
- `DECISION_LOGIC_HAMZ.md` — `unreviewed`; referencias declaradas: Partes 12-A y 12-B, páginas 117-154.
- `PALETA_COLORES_WARSH.md` — `structural_review`; bloqueada como especificación visual.

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

Cada documento producirá, por separado:

- Un informe de afirmaciones y fuentes.
- Una lista de contradicciones, ambigüedades y preguntas abiertas.
- Una especificación candidata nueva; nunca una edición silenciosa del legado.
- Casos de prueba candidatos con procedencia.
- Una decisión de `approved`, `rejected` o `superseded`.

Sólo las especificaciones aprobadas podrán entrar en `knowledge/rules`, `knowledge/exceptions`, `knowledge/evidence` y `knowledge/reviews`.
