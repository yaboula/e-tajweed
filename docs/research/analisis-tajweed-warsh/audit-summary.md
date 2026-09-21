# Decisión consolidada sobre `analisis_tajweed_warsh`

- **Identificador de custodia:** LEGACY-ANALYSIS-001
- **Alcance:** 11 artefactos heredados
- **Estado de la auditoría:** completada
- **Estado para implementación normativa:** bloqueado
- **Decisión global:** conservar intacto como legado; no migrar ninguno de sus algoritmos como motor de e-tajweed.

## Resultado ejecutivo

`analisis_tajweed_warsh` contiene conocimiento útil derivado del libro, pero no constituye una especificación religiosa ni técnica confiable. Sus documentos mezclan afirmaciones respaldadas, interpretación, pseudocódigo, convenciones editoriales, colores, ejemplos no verificados y etiquetas de completitud.

La decisión no es desechar el trabajo anterior. Se conservará íntegramente por su valor histórico y como índice de preguntas. Lo que se rechaza es reutilizarlo directamente como:

- Código o pseudocódigo del motor.
- Árbol normativo de reglas.
- Fuente de excepciones aprobadas.
- Golden tests.
- Política Unicode.
- Paleta visual.
- Mecanismo de resolución de solapamientos.

Cada afirmación recuperable deberá volver a atravesar la cadena:

```text
fuente física identificada
  → página y pasaje
  → especificación candidata
  → ocurrencias verificadas en corpus aprobado
  → pruebas positivas, negativas y fronterizas
  → revisión del especialista
  → aprobación versionada
```

## Qué se conserva intacto

### REL-001 — Libro de trabajo

Las 14 partes bajo custodia se conservan sin edición como fuente primaria de trabajo. Su hash de árbol es:

`5c0a5003126b76056430535faec8b0300045b7849db7369be8406e9870d172b2`

REL-001 todavía no equivale a una autoridad final. Algunas transcripciones, especialmente en la Parte 12-B, contienen notas editoriales y ejemplos problemáticos que obligan a consultar las páginas físicas.

### LEGACY-ANALYSIS-001 — Análisis derivado

Los 11 archivos se conservan byte por byte en la copia privada bajo custodia. Su hash de árbol es:

`e272d53d40834884388ad8d16369462161445a7fc5e769ea64a7595026329a81`

Los originales no fueron corregidos. Todas las conclusiones se escribieron en documentos nuevos.

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

- **Estado:** `rejected`.
- **Puede recuperarse:** definición básica, letras y grados respaldados provisionalmente por las páginas 61–62.
- **Debe crearse de nuevo:** detección de sukūn, contexto waṣl/waqf, modelo de grados y pruebas.
- **Razón principal:** ausencia de vocal tratada como sukūn y rangos Unicode usados como semántica de waqf.

Informe: [qalqalah-audit.md](./qalqalah-audit.md).

### `DECISION_LOGIC_NUUN_TANWEEN.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** clasificación básica, grupos de letras y casos citados en la Parte 7.
- **Debe crearse de nuevo:** modelo de nūn/tanwīn, fronteras, waṣl/waqf, naql y precedencias.
- **Razón principal:** depende de signos que el corpus no usa uniformemente y contiene una rama especial inalcanzable.

Informe: [nuun-tanween-audit.md](./nuun-tanween-audit.md).

### `DECISION_LOGIC_MEEM_SAKINAH.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** las tres categorías y la advertencia de iẓhār ante fāʾ/wāw de las páginas 75–76.
- **Debe crearse de nuevo:** identificación de mīm sākinah, fronteras y contexto de recitación.
- **Razón principal:** falla sobre las convenciones del propio corpus, etiqueta mal un ejemplo entre palabras e implementa una hipótesis no documentada.

Informe: [meem-sakinah-audit.md](./meem-sakinah-audit.md).

### `DECISION_LOGIC_TAFKHIM_TARQIQ.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** inventario amplio de categorías, ejemplos, awjuh y preferencias de la Parte 8.
- **Debe crearse de nuevo:** resolución por ocurrencia, excepciones prioritarias, waqf y configuraciones correlacionadas.
- **Razón principal:** el orden de retornos elimina numerosas excepciones y lecturas permitidas.

Informe: [tafkhim-tarqiq-audit.md](./tafkhim-tarqiq-audit.md).

### `DECISION_LOGIC_IDGHAM.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** pares transmitidos y rasgos conservados citados en la Parte 9.
- **Debe crearse de nuevo:** alcance de cada módulo, morfología, waṣl/waqf y lām al-taʿrīf.
- **Razón principal:** convierte ejemplos en listas exclusivas, omite idghām kabīr en el algoritmo y devuelve iẓhār fuera de su dominio.

Informe: [idgham-audit.md](./idgham-audit.md).

### `DECISION_LOGIC_FATH_IMALAH.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** categorías, ocurrencias y matrices candidatas de la Parte 10.
- **Debe crearse de nuevo:** morfología, ruʾūs al-āy, iʿrāb, waṣl/waqf y awjuh correlacionados.
- **Razón principal:** evalúa casos especiales e iltiqāʾ al-sākinayn después de retornos definitivos.

Informe: [fath-imalah-audit.md](./fath-imalah-audit.md).

### `DECISION_LOGIC_MUDUD.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** clases, duraciones, excepciones y matrices candidatas de la Parte 11.
- **Debe crearse de nuevo:** análisis por span, causas coincidentes y perfil coherente de duración.
- **Razón principal:** el algoritmo borra excepciones y awjuh, deja layn sin resolución y aplica una única prioridad por palabra.

Informe: [mudud-audit.md](./mudud-audit.md).

### `DECISION_LOGIC_HAMZ.md`

- **Estado:** `rejected`.
- **Puede recuperarse:** catálogo de fenómenos, ocurrencias y combinaciones de las Partes 12-A/12-B, sujeto a verificación.
- **Debe crearse de nuevo:** tashīl oral, morfología, Unicode, matrices completas, yāʾāt y perfiles correlacionados.
- **Razón principal:** ramas inalcanzables, pérdida de awjuh, sustituciones textuales inseguras y fuente 12-B contaminada por correcciones no resueltas.

Informe: [hamz-audit.md](./hamz-audit.md).

### `PALETA_COLORES_WARSH.md`

- **Estado:** `rejected`.
- **Se conserva como:** referencia histórica de una intención visual.
- **Debe crearse de nuevo:** toda la capa visual y accesible.
- **Razón principal:** fuente no verificable, contrastes fallidos, dependencia exclusiva del color, prioridades doctrinales por tono y tachado del texto coránico.

Informe: [palette-audit.md](./palette-audit.md).

## Qué se migrará para revisar

No se migrará lógica ejecutable. Se extraerán, en documentos nuevos y uno por uno:

- Definiciones respaldadas por una página concreta.
- Condiciones generales respaldadas.
- Excepciones y awjuh con ocurrencias identificadas.
- Preferencias de lectura exactamente como las formule la fuente.
- Preguntas abiertas y desacuerdos.
- Casos candidatos para revisión humana.

La extracción nunca copiará una etiqueta como “completo”, “sin excepciones” o “verificación matemática” sin demostrarla de nuevo.

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

### Especialista cualificado

Debe existir una persona responsable —profesor, qāriʾ o especialista cualificado— que pueda aprobar:

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

La siguiente fase segura es **verificación y registro de fuentes**, no desarrollo de la aplicación ni del motor.

Orden recomendado:

1. Identificar y verificar físicamente REL-001, empezando por Parte 12-B.
2. Fijar corpus y muṣḥaf de referencia con licencia y hashes.
3. Confirmar el perfil exacto de riwāyah/ṭarīq/método.
4. Nombrar al especialista responsable de aprobación.
5. Elegir una primera regla pequeña y volver a especificarla desde fuentes.
6. Crear casos candidatos y obtener aprobación humana.
7. Sólo entonces diseñar el contrato del motor alrededor de una regla aprobada.

Hasta completar esos controles, el resultado correcto del proyecto es **decisión documentada, fuentes preservadas y cero lógica religiosa implementada**.
