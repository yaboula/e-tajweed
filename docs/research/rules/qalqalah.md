# Qalqalah — especificación candidata corregida

- **Versión:** 0.1.0
- **Estado:** `requires_expert_review`
- **Ámbito:** Warsh ʿan Nāfiʿ por ṭarīq al-Azraq
- **Fuente de trabajo:** REL-001, Parte 6, páginas 61–62
- **Legado sustituido:** `DECISION_LOGIC_QALQALAH.md`

Esta candidata reemplaza la lógica heredada, pero todavía no es una regla religiosa aprobada ni código del motor.

## Núcleo respaldado provisionalmente

- Qalqalah sólo afecta a las cinco letras de `قطب جد`: `ق ط ب ج د`.
- Requiere que la letra esté sākinah.
- REL-001 distingue qalqalah ṣughrā y kubrā.
- REL-001 presenta tres grados:
  - Más fuerte: letra detenida con shaddah.
  - Intermedio: letra detenida sin shaddah.
  - Menor: letra sākinah en posición interna.

## Entrada mínima del detector

El detector no leerá caracteres aislados. Recibirá:

```text
letra objetivo
posición dentro de la palabra
estado de sukun demostrado
modo de recitación: wasl | waqf | unknown
presencia de shaddah
referencia al intervalo original del texto
```

El estado de sukūn tendrá procedencia explícita:

- `explicit`: signo reconocido en el corpus aprobado.
- `lexical`: confirmado por datos lingüísticos aprobados.
- `waqf_induced`: producido por una pausa seleccionada.
- `unknown`: no puede demostrarse.

## Decisión corregida

1. Si la letra no pertenece a `ق ط ب ج د`, el resultado es `not_applicable`.
2. Si el sukūn es `unknown`, el resultado es `unknown`.
3. Si la letra está vocalizada y no queda sākinah por el modo seleccionado, no hay qalqalah.
4. Si la letra está sākinah dentro de la palabra, la candidata es:
   - categoría: `sughra`;
   - grado: `lowest`.
5. Si la letra queda sākinah al final de palabra por waqf y lleva shaddah, la candidata es:
   - categoría: `kubra`;
   - grado: `strongest`.
6. Si la letra queda sākinah al final de palabra por waqf y no lleva shaddah, la candidata es:
   - categoría: `kubra`;
   - grado: `intermediate`.
7. Una letra final sākinah cuando la lectura continúa en waṣl queda `requires_expert_review`; REL-001 no resuelve este caso con precisión suficiente.

## Salida mínima

```text
ruleId: qalqalah
status: candidate | not_applicable | unknown | requires_expert_review
category: sughra | kubra | null
degree: lowest | intermediate | strongest | null
sourceSpan: intervalo sin modificar
recitationMode: wasl | waqf | unknown
sukunEvidence: explicit | lexical | waqf_induced | unknown
evidence: fuente + página
```

La salida no contiene colores ni texto coránico transformado.

## Inferencias prohibidas

- Ausencia de vocal visible ⇒ sukūn.
- Cualquier signo entre U+06D6 y U+06ED ⇒ waqf.
- Un glifo U+FCxx ⇒ final de āyah.
- Posición final de palabra ⇒ el lector necesariamente se detiene.
- Color o intensidad visual ⇒ categoría religiosa.

## Casos candidatos de verificación

- `أَطْعَمَهُ`: ṭāʾ interna sākinah → candidata ṣughrā/menor.
- `يَبْكُونَ`: bāʾ interna sākinah → candidata ṣughrā/menor.
- Waqf sobre `بِالْحَقِّ`: qāf final con shaddah → candidata kubrā/más fuerte.
- Waqf sobre `مُحِيط`: ṭāʾ final sin shaddah → candidata kubrā/intermedia.
- Cualquiera de las cinco letras con vocal efectiva → resultado negativo.
- Texto insuficientemente vocalizado → `unknown`.
- Letra final sākinah en waṣl → `requires_expert_review`.

Estos ejemplos aún no son golden tests.

## Preguntas pendientes para el especialista

1. Confirmar la relación exacta entre las dos categorías y los tres grados.
2. Resolver la letra de qalqalah sākinah al final de palabra cuando hay waṣl.
3. Verificar la frase problemática de la página 62 sobre `وخلقناكم`.
4. Confirmar ejemplos, terminología y pronunciación para Warsh por ṭarīq al-Azraq.

## Condición para aprobar

Qalqalah sólo podrá pasar a `knowledge/rules` cuando:

- Las páginas físicas 61–62 hayan sido verificadas.
- Las preguntas anteriores tengan respuesta citada.
- El especialista haya aprobado la especificación.
- Los casos se hayan comprobado en el corpus autorizado.
- Existan casos positivos, negativos, waṣl, waqf e incertidumbre.
- Se demuestre que retirar anotaciones reconstruye exactamente el texto original.

Hasta entonces, el motor no implementará esta regla como normativa.
