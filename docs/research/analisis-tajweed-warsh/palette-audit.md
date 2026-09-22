# Auditoría de `PALETA_COLORES_WARSH.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `PALETA_COLORES_WARSH.md`
- **SHA-256:** `ae3f00b1481c7bd53f2f6ce4fe32fa3972df8d25047323871d538cac892ff1c9`
- **Estado:** `accepted_product_reference`
- **Decisión vigente:** por decisión del propietario, define las nueve categorías visuales y sus familias de color. No define por sí sola las condiciones religiosas de detección.
- **Referencia visual oficial:** `PAL-001`, imagen de *مصحف التجويد* entregada y verificada por el propietario el 2026-09-22.
- **SHA-256 de PAL-001:** `df83d1e1b7196e0eb0f4cc898071b784528f7b2d57e48ab75d9129ff1667bd4d`.
- **Custodia privada:** `resources/sources/private/PAL-001/mushaf-al-tajwid-official-palette.png`.

## Decisión posterior que prevalece

El objetivo de e-tajweed es la detección exacta y la coloración de las nueve entradas de esta paleta. Sus categorías, familias cromáticas y significado son una referencia válida y obligatoria del producto.

Los HEX del documento heredado se conservan como tonos base. La aplicación puede emplear una paleta derivada con modificaciones ligeras de contraste, luminosidad o saturación para mejorar claridad y accesibilidad. Esas modificaciones no pueden cambiar la identidad, la familia cromática ni el significado de una categoría.

Los hallazgos restantes de este informe se conservan únicamente como advertencias de implementación: accesibilidad, solapamientos, CSS y trazabilidad deberán resolverse sin rechazar ni cambiar el mapeo semántico aprobado.

La paleta no reemplaza al libro ni a los documentos de decisión para detectar una regla. Detección y coloración permanecen separadas internamente, pero ambas son resultados obligatorios de la aplicación.

## Elementos aceptados y controles pendientes

El documento revela algunas intenciones útiles, pero no soluciones aprobadas:

- Diferenciar visualmente tipos de anotación.
- Mostrar duración cuando una regla de madd la incluya.
- Mantener el texto base legible.
- Ofrecer una leyenda.
- Distinguir fenómenos específicos del perfil de Warsh seleccionado.

Estas intenciones complementan las nueve categorías y colores ya aceptados por decisión del propietario. Las advertencias técnicas no autorizan a cambiar ese mapeo.

## Hallazgos históricos de implementación

> **Decisión vigente:** los hallazgos siguientes sirven para mejorar la implementación, la accesibilidad y la validación. No rechazan las nueve entradas ni sus familias oficiales. Los HEX heredados pueden ajustarse ligeramente conforme a la política de `docs/governance/product-scope.md`.

### PAL-HIST-001 — La fuente visual no estaba identificada durante la auditoría inicial

Las líneas 255–260 citaban un “Diagrama circular Tajweed Warsh” sin autor, título completo, edición, institución, URL, imagen bajo custodia, fecha de consulta ni licencia.

Este bloqueo de identidad quedó resuelto para el uso interno del producto cuando el propietario entregó y verificó la imagen oficial `PAL-001`. Siguen pendientes los datos bibliográficos y los derechos de redistribución; por ello la imagen se conserva en custodia privada y no se publicará automáticamente como activo de la aplicación.

### PAL-002 — El documento se declara compatible sin evidencia

La línea 259 afirma compatibilidad con sistemas de marcado de Corán digital, pero no identifica ningún estándar, esquema de datos, formato de anotación ni prueba de interoperabilidad.

Una lista de colores HEX no constituye un estándar. La compatibilidad futura deberá demostrarse con contratos y fixtures concretos.

### PAL-003 — La paleta incorpora reglas religiosas no aprobadas

Las tablas asignan duraciones, obligatoriedad, listas de condiciones y categorías como si ya fueran definitivas. Sin embargo, las auditorías previas han rechazado los documentos lógicos correspondientes como guías de implementación.

La capa visual no puede convertirse en una segunda fuente doctrinal. Recibirá anotaciones semánticas aprobadas; nunca decidirá si existe una regla.

### PAL-004 — Los colores resuelven solapamientos de forma doctrinalmente insegura

Las líneas 247–251 establecen prioridades como:

- Rojo sobre todos los demás.
- Gris sobre ghunnah.
- Tafkhīm sobre qalqalah.

Una prioridad visual no determina qué fenómeno existe ni cuál desaparece. Una misma unidad puede necesitar múltiples explicaciones, y una preferencia de color no puede borrar evidencia religiosa.

El motor devolverá todas las anotaciones compatibles. La interfaz elegirá una representación multicanal sin alterar el resultado semántico.

### PAL-005 — La jerarquía de “importancia” carece de fuente

La línea 227 propone rojo/naranja como “más importante” y gris como neutro. Duración, pronunciación, omisión fonética y claridad no forman una escala doctrinal única de importancia.

Esta jerarquía podría hacer que el estudiante ignore reglas no coloreadas o interprete un color como gravedad religiosa. Debe eliminarse.

### PAL-006 — Se propone tachar texto coránico

Las líneas 212–216 aplican `text-decoration: line-through` a letras no pronunciadas o asimiladas. e-tajweed no tachará letras del Corán.

La información fonética se mostrará mediante anotaciones respetuosas y no destructivas, aprobadas visualmente por el especialista. El rasm permanecerá legible e íntegro.

### PAL-007 — El sistema depende exclusivamente del color

Las líneas 6–173 asignan significado por tono y la guía sólo indica “aplicar el color”. No ofrece simultáneamente:

- Etiqueta textual o símbolo distinguible.
- Patrón o subrayado respetuoso.
- Explicación accesible.
- Nombre programático para lectores de pantalla.
- Modo monocromo o impresión.
- Preferencia del usuario.

WCAG 2.2, criterio 1.4.1, exige que el color no sea el único medio visual para comunicar información: <https://www.w3.org/WAI/WCAG22/Understanding/use-of-color>.

### PAL-008 — Blanco sobre naranja falla el contraste mínimo

El CSS de las líneas 192–195 usa texto blanco sobre `#E85E00`. El contraste calculado según luminancia relativa WCAG es aproximadamente `3,48:1`.

Para texto normal, WCAG 2.2 AA exige al menos `4,5:1`. Esta combinación no es aceptable como valor predeterminado: <https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum>.

### PAL-009 — Blanco sobre gris falla de forma severa

El CSS de las líneas 212–216 usa texto blanco sobre `#A9A9A9`. El contraste es aproximadamente `2,35:1`. Además de fallar accesibilidad, se combina con tachado y reduce aún más la legibilidad de letras y diacríticos.

### PAL-010 — Ocre con blanco también falla

Aunque el documento no incluye una clase CSS para el ocre, su patrón general usa texto blanco sobre fondos oscuros. Blanco sobre `#D4A017` produce aproximadamente `2,38:1`. Cualquier uso futuro necesitaría especificar el color de primer plano y comprobar cada estado real.

### PAL-011 — Los colores aislados no bastan; importan los pares y estados

El documento enumera HEX sin definir:

- Primer plano frente a fondo.
- Modo claro y oscuro.
- Selección, foco, hover y texto visitado.
- Superposición de reglas.
- Fondo de página configurable.
- Impresión y escala de grises.
- Alto contraste del sistema operativo.

La accesibilidad debe comprobar pares adyacentes en el contexto real, no colores individuales.

### PAL-012 — No existe alternativa para deficiencias de visión cromática

Verde, rojo, naranja y azul codifican categorías sin prueba de deuteranopía, protanopía, tritanopía o baja saturación. Aunque dos colores tengan contraste contra el fondo, el usuario puede no distinguirlos entre sí.

Cada anotación necesitará nombre, forma o interacción redundante además del color.

### PAL-013 — “Negro/crema” mezcla ausencia de marcado con reglas reales

Las líneas 131–153 asignan el mismo aspecto a pronunciación normal, iẓhār, tarqīq, madd al-ʿiwaḍ y madd ṭabīʿī. El usuario no puede saber si una regla fue detectada, si no se marca deliberadamente o si el motor no la reconoció.

La interfaz deberá distinguir semánticamente:

- Regla detectada pero sin resaltado principal.
- Sin regla aplicable.
- Análisis pendiente o desconocido.
- Texto todavía no analizado.

### PAL-014 — Una categoría de color agrupa fenómenos incompatibles

El gris agrupa asimilación, hamzat al-waṣl, alif no pronunciada y casos ortográficos generales. El verde agrupa ghunnah de fenómenos distintos. El rojo mezcla varias causas de madd.

La agrupación visual puede ser útil, pero no debe destruir la identidad de la regla, su causa, duración, contexto ni evidencia. El usuario debe poder inspeccionar el fenómeno exacto.

### PAL-015 — “Letra no pronunciada” no significa necesariamente “gris” ni “invisible”

Una letra puede no pronunciarse sólo en waṣl, en un wajh concreto o debido a una realización determinada. El color no recibe modo de recitación ni perfil de lectura y puede mostrar una afirmación falsa fuera de ese contexto.

La presentación deberá vincularse a un resultado contextual del motor y cambiar de forma explicable al seleccionar waṣl, waqf o un wajh.

### PAL-016 — La segmentación visual puede romper el árabe

Colorear fragmentos mediante spans por code unit puede separar letra base y marcas combinantes, afectar ligaduras, bidi, unión cursiva o posicionamiento de diacríticos. El documento no define límites seguros de anotación ni prueba fuentes coránicas.

La implementación deberá usar spans anclados a grafemas/intervalos aprobados, conservar el orden de code points y verificar visualmente cada fuente y navegador.

### PAL-017 — No existe especificación de RTL ni navegación

La propuesta no cubre:

- Orden RTL y mezcla con números/etiquetas LTR.
- Selección de texto.
- Copia sin estilos ni pérdida de signos.
- Navegación por teclado.
- Lectura mediante tecnología asistiva.
- Tooltips que no rompan la unión árabe.
- Zoom, reflow y dispositivos móviles.

No puede considerarse un sistema visual completo.

### PAL-018 — Las cifras de “reglas” no tienen semántica estable

La línea 171 cuenta 34 reglas principales, pero mezcla reglas, subtipos, duraciones, efectos y categorías de presentación. El total no demuestra cobertura del conocimiento ni de la interfaz.

El diseño futuro partirá de IDs semánticos versionados del motor, no de un conteo manual de filas.

### PAL-019 — Las comparaciones Warsh/Hafs no tienen trazabilidad

Las líneas 231–245 comparan duraciones y cantidades de condiciones sin citar fuentes específicas para ambas riwāyāt ni aclarar ṭuruq, métodos o alcance. Esas comparaciones no son necesarias para la primera versión de e-tajweed y podrían inducir generalizaciones incorrectas.

Se eliminarán hasta disponer de una necesidad pedagógica, fuentes aprobadas y revisión experta.

### PAL-020 — Los nombres de tokens visuales están acoplados a decisiones religiosas

Clases como `.mad-lazim`, `.ghunna` o `.silent-letter` mezclan semántica de dominio con valores CSS directos. Si la paleta cambia, si hay temas o si una regla requiere dos canales, el acoplamiento se vuelve rígido.

La futura arquitectura separará:

```text
rule annotation ID
  → presentation role
  → theme token
  → concrete style per mode
```

### PAL-021 — No existe prueba con muṣḥaf de referencia

La paleta no incluye capturas, páginas de comparación, fuente tipográfica, tamaños, densidad de marcas ni aprobación visual humana. Tampoco demuestra que los diacríticos permanezcan legibles sobre cada fondo.

La aprobación requerirá revisión lado a lado con el muṣḥaf de referencia y casos densos de múltiples reglas.

### PAL-022 — No existe licencia ni versión reproducible

La fecha de creación no sustituye un historial de decisiones. Faltan autoría, licencia, versión de WCAG, algoritmo de contraste, fuente, navegador y criterios de aceptación.

La futura especificación visual será versionada, auditable y acompañada de pruebas automáticas y capturas revisadas.

## Medición reproducible de contraste

Usando la fórmula de luminancia relativa de WCAG para los pares sugeridos o implícitos:

- Blanco sobre `#D9004C`: aproximadamente `5,18:1`.
- Blanco sobre `#E85E00`: aproximadamente `3,48:1` — falla AA para texto normal.
- Blanco sobre `#D4A017`: aproximadamente `2,38:1` — falla AA.
- Blanco sobre `#A9A9A9`: aproximadamente `2,35:1` — falla AA.
- Blanco sobre `#006400`: aproximadamente `7,44:1`.
- Blanco sobre `#00008B`: aproximadamente `15,30:1`.
- Negro sobre `#00BFFF`: aproximadamente `9,90:1`.
- Negro sobre `#F5F5DC`: aproximadamente `18,98:1`.

Que un par supere contraste no valida el sistema completo ni permite usar color como único canal.

## Requisitos mínimos para implementar la paleta válida

La futura capa de presentación deberá:

- Consumir anotaciones aprobadas; no detectar reglas.
- Mostrar múltiples fenómenos sin eliminar ninguno.
- No modificar, tachar, reordenar ni ocultar texto coránico.
- Ofrecer etiqueta o símbolo además de color.
- Permitir temas claro, oscuro, alto contraste y monocromo.
- Cumplir contraste en todos los estados interactivos.
- Mantener letras y marcas combinantes dentro de spans seguros.
- Proporcionar explicación accesible y nombre programático.
- Respetar RTL, unión árabe, ligaduras y diacríticos.
- Permitir copiar el texto fuente exactamente.
- Verificarse en móvil, escritorio, zoom e impresión.
- Compararse visualmente con el muṣḥaf de referencia.
- Obtener aprobación humana del especialista y revisión de accesibilidad.

## Casos de prueba visual necesarios

- Una sola regla sobre una letra con múltiples marcas.
- Dos o más reglas válidas sobre el mismo span.
- Regla que cambia entre waṣl y waqf.
- Varios awjuh seleccionables sin modificar el texto.
- Líneas con alta densidad de anotaciones.
- Fuente coránica principal y fallback controlado.
- Escalas de zoom altas y pantallas pequeñas.
- Temas claro, oscuro, alto contraste y escala de grises.
- Simulación de deficiencias de visión cromática.
- Lectura por teclado y lector de pantalla.
- Copia/pegado y reconstrucción exacta del texto.
- Comparación visual humana con páginas de referencia.

## Decisión de migración vigente

- Migrar `PALETA_COLORES_WARSH.md` con su nombre original cuando corresponda en el orden de trabajo.
- Adoptar sus nueve categorías, familias cromáticas y significado como referencia obligatoria del producto.
- Conservar los HEX heredados como tonos base y permitir sólo ajustes ligeros, documentados y comprobados de contraste y claridad.
- Tratar sus ejemplos CSS y prioridades como detalles de implementación que deberán probarse, no como permiso para cambiar la paleta.
- No usar el color como evidencia para detectar una regla ni como único mecanismo para resolver solapamientos.
- Aplicar la coloración mediante anotaciones que no alteren el texto coránico.
- Verificar visualmente el resultado contra el muṣḥaf certificado durante el desarrollo.

## Cierre del orden de auditoría

Este informe queda como historial técnico. La decisión posterior del propietario fija como objetivo la detección exacta y la coloración de las nueve entradas de la paleta oficial `PAL-001`. Antes de crear el motor habrá una verificación completa y exhaustiva contra *الدليل الأوفق*. La revisión del especialista se mantiene como control final.
