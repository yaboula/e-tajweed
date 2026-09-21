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

- **Estado:** `accepted_product_reference`.
- **Se acepta como:** definición obligatoria de las nueve categorías visuales y sus colores.
- **No se usa como:** fuente religiosa para decidir si una regla está presente.
- **Implementación:** puede añadir accesibilidad y metadatos sin cambiar el mapeo de la paleta.

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

El trabajo continuará **verticalmente, una sola regla cada vez**. Qalqalah y nūn/tanwīn están corregidos. La validación manual de sus resultados se realizará durante la implementación, por lo que la siguiente sesión puede continuar con mīm sākinah.

Orden recomendado:

1. Mantener Qalqalah y nūn/tanwīn como documentos corregidos contra el libro.
2. Revisar y corregir `DECISION_LOGIC_MEEM_SAKINAH.md` como próximo documento, sin abrir otros a la vez.
3. Al implementar cada regla, el propietario comprueba los resultados contra el muṣḥaf certificado.

La revisión del especialista se conserva como control final de la aplicación y no como bloqueo de la revisión documental ni del desarrollo.
