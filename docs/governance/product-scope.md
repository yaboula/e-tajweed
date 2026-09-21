# Alcance permanente del producto

- **Decisión del propietario:** 2026-09-21
- **Estado:** vigente
- **Aplicación:** todo el proyecto

## Objetivo

e-tajweed detecta con precisión las reglas de tajwīd presentes en el texto coránico y aplica su coloración correspondiente para Warsh ʿan Nāfiʿ por ṭarīq al-Azraq.

La aplicación **no** tiene como objetivo escuchar, evaluar, corregir ni enseñar la pronunciación del usuario. Las descripciones fonéticas del libro sirven únicamente para comprender las condiciones de detección.

## Las nueve reglas de coloración

El alcance consta exactamente de las nueve entradas de la tabla resumen de `PALETA_COLORES_WARSH.md`:

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

## Fuentes con funciones distintas

- El libro y los documentos `DECISION_LOGIC_*` definen las condiciones de detección.
- `PALETA_COLORES_WARSH.md` es la referencia válida y obligatoria para la categoría visual y el color.
- El muṣḥaf coloreado y certificado sirve para la validación manual durante el desarrollo.
- Un especialista cualificado realizará la revisión final cuando esté disponible.

La separación técnica entre motor y presentación evita que el color determine la regla; no elimina la coloración del objetivo del producto.
