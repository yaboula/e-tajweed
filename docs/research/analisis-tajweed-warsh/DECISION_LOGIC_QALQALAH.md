# Lógica de decisión: القلقلة (Qalqalah)

- **Documento migrado:** `analisis_tajweed_warsh/DECISION_LOGIC_QALQALAH.md`
- **Estado:** corregido contra el libro
- **Fuente contrastada:** REL-001, Parte 6, páginas 61–62
- **Lectura objetivo:** Warsh ʿan Nāfiʿ por ṭarīq al-Azraq
- **Versión del documento:** 2.0.0

Este es el documento heredado corregido. Conserva la regla útil del análisis anterior, elimina sus inferencias técnicas inseguras y registra lo que deberá verificarse manualmente durante el desarrollo contra el muṣḥaf certificado de referencia.

La revisión final por un profesor, qāriʾ o especialista cualificado se realizará antes de considerar definitiva la aplicación. No bloquea la revisión, implementación y comprobación manual durante el desarrollo.

## Definición y fuente

### Definición

- **Lingüística:** movimiento y agitación.
- **Técnica:** perturbación del punto de articulación al pronunciar una letra sākinah hasta que se perciba una pulsación fuerte.
- **Causa indicada por el libro:** reunión de shiddah y jahr.
- **Letras:** `ق ط ب ج د`, reunidas en `قطب جد`.
- **Condición necesaria:** la letra debe estar sākinah.

La definición, la causa y las letras aparecen en la página 61. La división y los grados continúan en la página 62. La versión anterior atribuía todo a la página 62 y queda corregida aquí.

## Clasificación recogida en REL-001

### Qalqalah ṣughrā

El libro la presenta cuando la letra de qalqalah está sākinah dentro de la palabra.

Ejemplos del libro:

- `أطعمه`
- `أفتطمعون`
- `يجعلون`
- `يبكون`
- `يدخلون`

### Qalqalah kubrā

El libro la presenta cuando la letra está sākinah al final de la palabra.

Ejemplos del libro:

- `الفلق`
- `لهب`
- `أحد`
- `الصمد`

### Grados

1. **Más fuerte:** al detenerse sobre una letra de qalqalah con shaddah, como la qāf de `بالحقّ`.
2. **Intermedio:** al detenerse sobre una letra de qalqalah sin shaddah, como la ṭāʾ de `محيط`.
3. **Menor:** letra de qalqalah sākinah dentro de la palabra.

## Datos necesarios para decidir

La decisión no se hará sobre un carácter aislado. Necesita:

```text
letra
posición dentro de la palabra
estado de sukūn y procedencia de esa información
modo de lectura: waṣl | waqf | desconocido
presencia de shaddah
intervalo exacto del texto original
```

Estados permitidos para el sukūn:

- `explicit`: aparece mediante un signo reconocido en el corpus aprobado.
- `corpus_verified`: está confirmado por los datos lingüísticos del corpus aprobado.
- `waqf_induced`: se produce por una pausa efectivamente seleccionada.
- `unknown`: no se puede demostrar con los datos disponibles.

## Árbol de decisión corregido

```text
1. ¿La letra pertenece a ق ط ب ج د?
   no  → no hay qalqalah
   sí  → continuar

2. ¿Puede demostrarse que la letra está sākinah en el modo de lectura actual?
   no       → no hay qalqalah
   unknown  → requiere comprobación manual
   sí       → continuar

3. ¿Está dentro de la palabra?
   sí → qalqalah ṣughrā, grado menor

4. ¿Está al final y se realiza waqf?
   sí + shaddah     → qalqalah kubrā, grado más fuerte
   sí + sin shaddah → qalqalah kubrā, grado intermedio

5. ¿Está sākinah al final pero se realiza waṣl?
   → pendiente de validación manual; REL-001 no describe este caso
     con precisión suficiente para cerrarlo aquí.
```

El estado pendiente del punto 5 no implica que la regla religiosa sea desconocida. Significa únicamente que este documento no la afirmará sin verificarla en la referencia adoptada por el proyecto.

## Correcciones realizadas sobre la versión heredada

### Sukūn

Se elimina la equivalencia:

```text
ausencia de fatḥah/ḍammah/kasrah = sukūn
```

La falta de una vocal visible puede proceder de una vocalización incompleta o de la convención del corpus. En ese caso el resultado es `unknown`, no qalqalah automática.

### Waqf

Waqf no se deduce sólo por estar al final de una palabra, al final de una āyah o junto a una marca. El modo efectivo de lectura se proporciona o se confirma durante la comprobación.

### Unicode

- No se tratará todo U+06D6–U+06ED como “marcas de pausa”; contiene signos con funciones diferentes.
- U+FC00–U+FC18 no son marcadores Unicode estándar de fin de āyah.
- La numeración de āyāt será metadato separado y comprobable.
- Las marcas combinantes se analizarán como parte del grafema sin modificar ni reordenar el texto coránico.

### Color

`#00BFFF` era una elección visual del análisis anterior, no una regla del libro. Puede conservarse como propuesta de interfaz, pero no participa en la detección ni demuestra el tipo o grado de qalqalah.

### Frecuencias

Se eliminan las frecuencias globales de las cinco letras. No medían ocurrencias de qalqalah y no estaban vinculadas a un corpus versionado.

## Punto textual que debe comprobarse

La página 62 conservada en REL-001 contiene esta formulación para el grado menor:

```text
مثل الوقف على القاف في (وخلقناكم)
```

La expresión menciona waqf sobre una qāf situada dentro de `وخلقناكم`, lo que parece incoherente con la propia clasificación del párrafo. No se corrige de memoria ni se convierte en lógica. Debe compararse con la página física y con el muṣḥaf de referencia durante la validación manual.

## Casos para la validación manual del propietario

La persona responsable del proyecto comprobará visualmente y carácter por carácter estos casos contra un muṣḥaf coloreado, certificado y correspondiente a Warsh ʿan Nāfiʿ por ṭarīq al-Azraq:

- Las cinco letras `ق ط ب ج د` con sukūn demostrado.
- Las mismas letras con vocal efectiva, como casos negativos.
- Los cinco ejemplos internos citados por el libro.
- Los cuatro ejemplos finales citados por el libro, tanto en waṣl como en waqf cuando proceda.
- Final con shaddah en waqf: `بالحقّ`.
- Final sin shaddah en waqf: `محيط`.
- Letra sākinah al final de palabra durante waṣl.
- Texto cuya vocalización no permita demostrar el sukūn.

Cada comprobación deberá registrar sura, āyah, palabra, modo de lectura, resultado observado y referencia exacta del muṣḥaf.

## Estado de esta revisión

La comparación y corrección de este documento contra REL-001 está cerrada. Puede pasarse al siguiente documento del orden establecido.

Durante la futura implementación de Qalqalah se deberá:

- comprobar manualmente los casos contra el muṣḥaf certificado;
- mantener explícitas las dudas todavía abiertas;
- demostrar que retirar las anotaciones reconstruye exactamente el texto original.

La aprobación del especialista se mantiene como control final antes de declarar definitiva la aplicación, no como requisito para continuar ahora con el desarrollo controlado.
