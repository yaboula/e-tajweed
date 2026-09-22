# Alcance permanente del producto

- **Decisión inicial del propietario:** 2026-09-21
- **Aclaración sobre la paleta oficial:** 2026-09-22
- **Estado:** vigente
- **Aplicación:** todo el proyecto

## Objetivo

e-tajweed detecta con precisión las reglas de tajwīd presentes en el texto coránico y aplica su coloración correspondiente para Warsh ʿan Nāfiʿ por ṭarīq al-Azraq.

La aplicación **no** tiene como objetivo escuchar, evaluar, corregir ni enseñar la pronunciación del usuario. Las descripciones fonéticas del libro sirven únicamente para comprender las condiciones de detección.

## Las nueve entradas de coloración

El alcance consta exactamente de las nueve entradas semánticas registradas en `PALETA_COLORES_WARSH.md`. La imagen oficial de referencia entregada y verificada por el propietario se conserva como `PAL-001`:

1. Rojo magenta `#D9004C` — madd obligatorio.
2. Naranja oscuro `#E85E00` — madd variable de Warsh.
3. Amarillo ocre `#D4A017` — madd natural especial.
4. Gris medio `#A9A9A9` — letras no pronunciadas o asimilación completa.
5. Verde oscuro `#006400` — ghunnah y reglas nasales.
6. Azul oscuro `#00008B` — tafkhīm.
7. Azul claro `#00BFFF` — qalqalah.
8. Negro `#000000` — iẓhār, lectura normal y madd ṭabīʿī sin marcado especial.
9. Crema `#F5F5DC` — fondo de texto definido por la paleta.

Estas nueve entradas agrupan subreglas. Las subreglas se estudian para lograr una detección exacta, pero no amplían por sí solas el número de salidas visuales del producto.

Los valores HEX anteriores son los tonos base heredados, no una obligación de reproducción fotométrica exacta. La aplicación puede crear una paleta derivada con ajustes **ligeros** de luminosidad, saturación o contraste cuando sean necesarios para que el texto coránico, sus signos y la distinción entre categorías permanezcan claros.

Un ajuste visual será válido únicamente si:

- conserva la familia y el significado de cada color oficial;
- no mueve una regla a otra categoría;
- queda documentado y versionado como token de presentación;
- supera las comprobaciones de contraste y deficiencias de visión cromática;
- se revisa sobre texto coránico real, con diacríticos, en temas y tamaños admitidos;
- no altera el texto fuente ni la decisión semántica del motor.

## Unidad exacta de coloración

La coloración no se aplica necesariamente a una palabra, una letra completa ni un grafema completo. Según la regla y la notación del muṣḥaf de referencia, el objetivo visual puede ser:

- únicamente la letra base;
- únicamente una harakah o signo coránico concreto;
- la letra base y una o varias de sus marcas;
- varios componentes relacionados, cada uno con su propio intervalo de anotación.

La presencia de una regla no autoriza a colorear automáticamente todos los code points del grafema. Cada resultado deberá identificar de forma explícita qué componentes reciben la anotación y cuáles conservan su presentación normal.

El motor y la interfaz deberán distinguir entre letra base, harakāt, shaddah, sukūn, tanwīn y demás signos coránicos sin separarlos, eliminarlos ni reordenarlos en el texto fuente. La retirada de todas las anotaciones deberá reconstruir exactamente la entrada original.

La selección exacta de los componentes coloreados para cada regla se fijará durante la verificación exhaustiva previa al motor mediante comparación con la paleta oficial, *الدليل الأوفق* y el muṣḥaf certificado.

## Fuentes con funciones distintas

- El libro y los documentos `DECISION_LOGIC_*` definen las condiciones de detección.
- `PAL-001` y `PALETA_COLORES_WARSH.md` fijan las familias visuales y su significado. Los tonos concretos de la interfaz pueden adaptarse ligeramente conforme a la política anterior.
- El muṣḥaf coloreado y certificado sirve para la validación manual durante el desarrollo.
- Un especialista cualificado realizará la revisión final cuando esté disponible.

## Puerta obligatoria antes del motor

Antes de comenzar la implementación del motor de detección se realizará una revisión completa y exhaustiva de todas las reglas, excepciones, awjuh y ocurrencias pertinentes contra *الدليل الأوفق إلى رواية ورش عن نافع من طريق الأزرق*.

No se considera suficiente una sucesión de verificaciones parciales. La revisión completa será una fase separada y deberá quedar cerrada antes de traducir las decisiones religiosas a código.

La separación técnica entre motor y presentación evita que el color determine la regla; no elimina la coloración del objetivo del producto.
