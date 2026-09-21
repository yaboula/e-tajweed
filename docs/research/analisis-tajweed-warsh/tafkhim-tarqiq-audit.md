# Auditoría de `DECISION_LOGIC_TAFKHIM_TARQIQ.md`

- **Artefacto:** LEGACY-ANALYSIS-001 / `DECISION_LOGIC_TAFKHIM_TARQIQ.md`
- **SHA-256 del original antes de editar:** `4c28f82edce393a405cf8c6d5f02a18d18870be04eee0eaecb6d40b08c9facf1`
- **Estado:** `corrected`
- **Decisión:** migrado con el mismo nombre y corregido en el propio documento contra REL-001, páginas 79–88.
- **Fuente local contrastada:** REL-001 / `parte 8.md`.

## Veredicto

El original era una recopilación extensa de la Parte 8 y conservaba muchas listas, ejemplos y preferencias declaradas por el libro. Sin embargo, las transformaba en árboles secuenciales que no mantenían las relaciones entre regla general, excepción, wajh permitido, preferencia y contexto de recitación. Esos defectos quedaron corregidos en `DECISION_LOGIC_TAFKHIM_TARQIQ.md`.

El defecto más grave estaba en rāʾ: varias ramas de `وجهان` y de tafkhīm excepcional eran inalcanzables porque una condición general retornaba antes. La corrección resuelve primero los catálogos especiales, conserva configuraciones correlacionadas con badal y sustituye las cadenas vocalizadas por identificadores de ocurrencia candidatos.

Durante la implementación, el propietario validará manualmente los resultados contra el muṣḥaf coloreado y certificado de Warsh ʿan Nāfiʿ por ṭarīq al-Azraq. La revisión por un profesor, qāriʾ o especialista cualificado se conserva como control final cuando esté disponible.

## Elementos respaldados provisionalmente por REL-001

### Definiciones y clasificación general

REL-001, líneas 11–21, respalda provisionalmente las definiciones de tafkhīm y tarqīq, el uso habitual de `tafkhīm` para rāʾ y `taghlīẓ` para lām, y la división pedagógica en tres grupos. El documento heredado reproduce este núcleo en sus líneas 8–39.

La suma de letras sólo describe esa clasificación; no valida las condiciones posteriores ni su implementación.

### Alif līnah y letras de madd

REL-001, líneas 23–32, define alif līnah y afirma que sigue a la letra precedente en tafkhīm/tarqīq. También incorpora wāw y yāʾ de madd a esa dependencia. El documento recoge la regla general en sus líneas 47–55 y 125–139.

La implementación heredada sólo desarrolla una función para alif. No especifica las dos letras de madd añadidas por la propia fuente.

### Lām de lafẓ al-jalālah

REL-001, líneas 35–48, respalda provisionalmente las condiciones generales de tarqīq y taghlīẓ de la lām en `اللَّه` y `اللَّهُمَّ`, incluido el inicio de lectura. El documento recoge esos grupos en sus líneas 57–67 y 143–167.

Los casos unidos mediante tanwīn o hamzat al-waṣl requieren una representación explícita de waṣl. No pueden reducirse a observar el carácter inmediatamente anterior.

### Otras lāmāt en Warsh

REL-001, líneas 52–105, respalda provisionalmente:

- Las cuatro condiciones generales de taghlīẓ.
- Los tres lexemas, en cinco ocurrencias, con alif separadora y dos awjuh.
- La interacción de `فِصَالًا` con badal.
- Los casos de lām terminal en waqf.
- Los siete lugares relacionados con alif dhāt yāʾ y la restricción de ruʾūs al-āy en once suras.

El documento heredado conserva gran parte de esas listas, pero no modela de forma completa sus combinaciones.

### Rāʾ

REL-001, líneas 109–178, enumera condiciones de tarqīq, tafkhīm, casos con dos awjuh y tres formas de waqf. El documento reproduce la mayoría de esos enunciados y ejemplos en sus líneas 241–342.

Lo que queda rechazado es la conversión de esas listas en una cascada de retornos sin precedencia religiosa formal.

## Hallazgos corregidos

Los códigos siguientes conservan el diagnóstico histórico del original identificado por el hash anterior. Su resolución está aplicada y explicada mediante comentarios visibles en el documento corregido.

### TTR-001 — Los casos especiales de rāʾ están situados después de retornos generales

El algoritmo de las líneas 470–551 evalúa primero condiciones generales de tarqīq, después condiciones generales de tafkhīm y sólo al final los casos de `وجهان`. Esto hace inalcanzables numerosas ramas:

- `فِرْقٍ` satisface antes la condición de kasrah original y retorna tarqīq en las líneas 481–482; nunca alcanza las líneas 539–540 que deben conservar dos awjuh.
- `الْقِطْرِ` tiene rāʾ kasrada y retorna en las líneas 478–479; nunca alcanza las líneas 542–543.
- `مِصْرَ` cae en una condición general de tafkhīm antes de las líneas 545–546.
- `حَيْرَانَ` encuentra yāʾ sākinah antes de rāʾ y retorna en las líneas 484–485; nunca alcanza las líneas 533–534.
- Las seis formas `ذِكْرًا`, `سِتْرًا`, `إِمْرًا`, `وِزْرًا`, `حِجْرًا` y `صِهْرًا` pueden retornar por la condición general de sākin + kasrah antes de llegar a las líneas 530–531.

El resultado no es una mera imperfección técnica: elimina lecturas permitidas que el propio documento había inventariado.

### TTR-002 — Varias excepciones de tafkhīm también quedan eclipsadas

El mismo orden invalida condiciones de tafkhīm declaradas por REL-001:

- `قِرْطَاسٍ`, `فِرْقَةٍ` y las formas de `مِرْصَاد` pueden retornar tarqīq por la kasrah original antes de alcanzar la lista de las líneas 512–513.
- Las formas con rāʾ repetida pueden quedar capturadas por una condición anterior antes de las líneas 518–520.
- Ejemplos tras bāʾ o lām de jarr, como `بِرَسُولٍ` y `لِرَبِّكَ`, satisfacen primero una condición superficial de kasrah anterior antes de alcanzar las líneas 525–526.

Una lista correcta al final del algoritmo no corrige una prioridad incorrecta al principio.

### TTR-003 — Los awjuh de `يَسْرِ` y `نُذُرِ` se pierden en ambas funciones

Las líneas 536–537 intentan conservar dos awjuh en waqf, pero la función general puede retornar antes por la vocal de rāʾ. La función específica de waqf de las líneas 559–585 tampoco contiene estas excepciones y devuelve una única clasificación por defecto.

REL-001, línea 148, declara los dos awjuh con tafkhīm preferido. La implementación heredada no puede producir fielmente ese resultado.

### TTR-004 — Las combinaciones con badal se reducen indebidamente a dos etiquetas

REL-001, líneas 75–78 y 141–143, describe conjuntos correlacionados de cinco o seis awjuh cuando coinciden taghlīẓ/tarqīq con extensiones de badal. El documento los menciona en las líneas 204–207 y 300–304, pero sus algoritmos sólo devuelven:

```text
taghlīẓ o tarqīq
```

Esto pierde qué longitudes de badal son compatibles con cada lectura y cuál método admite cinco o seis combinaciones. Los awjuh deberán modelarse como configuraciones compatibles completas, con fuente y preferencia, no como opciones independientes que la aplicación mezcle libremente.

### TTR-005 — La regla de U+06EA sustituye indebidamente una condición religiosa

Las líneas 85, 250 y 494–495 afirman que una rāʾ con U+06EA debajo se tarqīqa automáticamente y que no hace falta comprobar el alif. REL-001, línea 120, formula otra condición: tarqīq cuando el alif posterior a rāʾ recibe imālah.

Unicode denomina U+06EA `ARABIC EMPTY CENTRE LOW STOP`. En el corpus heredado aparece en 1.891 āyāt y se adjunta a letras muy diversas; no significa universalmente “tarqīq de rāʾ”. En formas como `نَصَٰر۪ىٰ` puede ser una señal editorial relacionada con la lectura, pero sólo dentro de la convención documentada de ese corpus.

La regla normativa deberá representar la realización de imālah/taqlīl y usar el code point como evidencia corpus-específica, nunca como causa religiosa autónoma.

Referencia técnica: <https://unicode.org/charts/nameslist/n_0600.html>.

### TTR-006 — El ejemplo `قِيلَ` contradice la clasificación interna

Las líneas 25–31 clasifican qāf entre las letras siempre mufakhkhamah. La línea 132 presenta después `قِيلَ` como ejemplo de tarqīq de yāʾ de madd, aunque la propia regla dice que la letra de madd sigue a la precedente.

REL-001, líneas 31–32, no proporciona ese ejemplo. La relación exacta entre el grado de tafkhīm de qāf kasrada y la cualidad de la yāʾ de madd necesita fuente y revisión experta. El ejemplo heredado no puede migrarse como caso aprobado.

### TTR-007 — Wāw y yāʾ de madd se declaran, pero no se implementan

La tabla de la línea 132 y REL-001 incluyen wāw y yāʾ de madd. Sin embargo, `aplicar_regla_alif_linah` de las líneas 364–379 sólo acepta una alif y no existe función equivalente para las otras dos letras.

El supuesto “algoritmo completo” no cubre todo el alcance que el propio documento declara.

### TTR-008 — La identificación Unicode de alif līnah no está especificada

Las condiciones `alif_actual es sakinah` y `letra_anterior tiene fatḥah` no explican cómo reconocer alif ordinaria, alif pequeña, alif maqṣūrah, marcas combinantes o convenciones de rasm ʿUthmānī. Tampoco distinguen letra base, grafema y realización recitada.

La futura especificación deberá definir qué representación lingüística analiza sin modificar la secuencia fuente.

### TTR-009 — Los casos unidos de lafẓ al-jalālah necesitan waṣl explícito

Las líneas 61–67 y 387–417 clasifican el contexto anterior como si fuera una propiedad aislada. El caso de tanwīn sólo existe al unir la lectura; en waqf no se alcanza el lafẓ siguiente. Hamzat al-waṣl y los movimientos auxiliares tampoco equivalen al code point inmediatamente anterior.

La función deberá recibir el modo de recitación, la frontera de palabra y un análisis de la vocal pronunciada. Sin ello puede aplicar tarqīq a una continuidad que no ocurre.

### TTR-010 — La función de lafẓ al-jalālah carece de salida desconocida

`aplicar_regla_lam_allah` termina sin retorno si el contexto no coincide con una etiqueta prevista. No define texto incompleto, modo desconocido, marca no reconocida ni corpus fuera de alcance.

Según la carta del proyecto, la ausencia de evidencia debe producir `unknown` o `requires_review`, no un valor vacío ni una suposición.

### TTR-011 — Palabras, formas y ocurrencias se cuentan de manera inconsistente

REL-001 distingue de hecho lexemas y lugares coránicos. El documento heredado mezcla ambas unidades:

- Las líneas 196–202 contienen tres formas léxicas en cinco ocurrencias; las líneas 594–597 las llaman “5 palabras” pero enumeran tres.
- Las líneas 211–220 contienen ocho ocurrencias de seis formas; las líneas 599–605 hablan de ocho palabras pero enumeran seis.
- Las líneas 224–232 contienen siete lugares de seis formas escritas; las líneas 607–613 hablan de siete palabras pero enumeran seis.

La base futura deberá asignar identificadores separados a regla, lexema, token coránico y ocurrencia `sura:ayah:posición`.

### TTR-012 — `يُصَالِحَا` exige separar rasm y realización

REL-001, línea 68, muestra dentro de la cita coránica `يُصْلِحَا` y añade entre paréntesis `يُصَالِحَا`. El legado conserva ambas formas en su fila de las líneas 201–202 sin explicar cuál es texto fuente, cuál es realización de lectura y cómo se relacionan.

Esta diferencia no se resolverá sustituyendo letras del Corán. Debe documentarse mediante una anotación de lectura respaldada, enlazada al token inmutable y aprobada por el especialista.

### TTR-013 — Las coincidencias por cadena vocalizada no son identificadores estables

Las líneas 448, 473, 497, 512, 519, 530 y siguientes comparan `palabra_actual` con cadenas árabes completas. Esto falla ante variación de caso, marcas editoriales y rasm.

La fuente dice, por ejemplo, que `إِبْرَاهِيم` se trata así dondequiera que aparezca. El corpus heredado contiene al menos `إِبْرَٰهِيمَ` y `إِبْرَٰهِيمُ`, con alif pequeña U+0670 y terminaciones distintas. Ninguna coincide literalmente con la cadena heredada `إِبْرَاهِيمَ`.

Las excepciones deberán anclarse a tokens u ocurrencias verificadas, no a igualdad destructiva o frágil de strings.

### TTR-014 — La condición de alif separadora tiene un fallback inseguro

Las líneas 441–460 aceptan alif como separador, buscan tres palabras conocidas y, si no coinciden, terminan devolviendo taghlīẓ general. REL-001 presenta tres formas concretas para el caso de dos awjuh; no autoriza a clasificar cualquier cadena desconocida con alif mediante un fallback silencioso.

Una forma no reconocida deberá producir `unknown` o quedar sometida a la regla formal una vez ésta sea demostrada, nunca saltar de una whitelist fallida a una conclusión normativa.

### TTR-015 — Waqf cambia el estado fonético, no el texto fuente

Las líneas 451–457 y 559–585 mezclan la vocal escrita con el estado resultante de waqf. Una lām o rāʾ puede quedar sākinah en recitación sin que se elimine su marca original del corpus.

La especificación deberá mantener por separado:

- Estado ortográfico de la fuente.
- Estado fonético bajo waṣl.
- Estado fonético bajo cada tipo autorizado de waqf.

### TTR-016 — Ishmām y rawm se aplican sin validar elegibilidad

REL-001, líneas 168–178, limita ishmām a la letra originalmente ḍammah y rawm a kasrah o ḍammah. La función heredada acepta cualquier rāʾ si el llamador pasa esas etiquetas y reenvía directamente a otra función.

La elegibilidad, el estado original y el modo de recitación deberán formar parte de la precondición y de las pruebas negativas.

### TTR-017 — La lista de once suras queda reducida a un booleano opaco

REL-001, línea 105, identifica las once suras cuyos finales de āyah tienen taqlīl obligatorio. El algoritmo sólo usa `NOT رأس_آية` en la línea 456, sin identificar la sura, la āyah, la fuente de numeración ni la regla que determina el final.

Esta excepción necesita metadatos de corpus verificados y una lista versionada. No se deducirá de los glifos U+FCxx usados por el corpus heredado.

### TTR-018 — El algoritmo de waqf borra awjuh y preferencias

Las líneas 559–585 reducen el resultado a una sola categoría. No devuelven el conjunto de lecturas permitidas, la preferida, el método del transmisor ni la evidencia. Además de `يَسْرِ` y `نُذُرِ`, quedan fuera las relaciones con las condiciones especiales ya inventariadas.

Una preferencia como “tafkhīm muqaddam” no significa que el otro wajh desaparezca. El tipo de salida deberá conservar ambos.

### TTR-019 — “Intersecciones: ninguna” no está demostrado

Las líneas 137–139 y 165–167 niegan intersecciones para alif y lafẓ al-jalālah, mientras el documento sí depende de vocales contextuales, hamzat al-waṣl, waṣl/waqf y letras precedentes. La ausencia de una sección específica en REL-001 no demuestra independencia absoluta.

Los solapamientos se validarán mediante una matriz de reglas y configuraciones de lectura, no mediante declaraciones aisladas.

### TTR-020 — “Lista completa” y “verificación matemática” exceden la evidencia

Las líneas 590–652 llaman completa a la lista y las líneas 656–669 presentan una suma de 28 letras como verificación. Estas etiquetas no prueban exhaustividad, prioridades, combinaciones ni corrección sobre el Corán completo.

Hasta que las fuentes autorizadas y el especialista confirmen cada entrada, las listas son inventarios provisionales de REL-001.

### TTR-021 — El resultado final trata lo desconocido como error

Las líneas 548–549 devuelven `ERROR: caso no clasificado`. Una forma desconocida puede revelar una limitación del modelo, una convención editorial distinta o contexto insuficiente. No autoriza a declarar error en el texto ni en la lectura.

La salida deberá distinguir `not_applicable`, `unknown`, `unsupported_input` y `requires_review` con evidencia trazable.

## Modelo mínimo aplicado

El documento corregido representa, como mínimo:

```text
token coránico inmutable + identificador de ocurrencia
  + letra o unidad fonética objetivo
  + estado ortográfico del corpus
  + análisis lingüístico y morfológico
  + modo: wasl | waqf_sukun | waqf_ishmam | waqf_rawm | unknown
  + método/ṭarīq y elecciones correlacionadas
  + regla general
  + excepción prioritaria
  → conjunto de awjuh permitidos
  → preferencia, si la fuente la declara
  → evidencia por cada wajh
  → estado de revisión humana
```

Las excepciones no se implementarán mediante strings sueltos. Las combinaciones con badal, fatḥ, taqlīl o imālah deberán ser configuraciones compatibles, no etiquetas independientes.

## Casos para la implementación y las pruebas

- Cada grupo general de letras, con casos positivos y negativos.
- Alif, wāw de madd y yāʾ de madd bajo letras precedentes verificadas.
- La contradicción candidata de `قِيلَ`, pendiente de resolución experta.
- Lafẓ al-jalālah en inicio, waṣl y waqf, con kasrah original y contextual.
- Tanwīn antes de lafẓ al-jalālah con continuidad y con pausa.
- Las cinco ocurrencias de las tres formas con alif separadora.
- `فِصَالًا` con cada combinación de badal aceptada por el método documentado.
- Las ocho ocurrencias de lām terminal, no sólo seis strings.
- Los siete lugares de alif dhāt yāʾ y la exclusión precisa de ruʾūs al-āy.
- Cada condición general de tarqīq y tafkhīm de rāʾ.
- Cada excepción que debe preceder a una regla general.
- Todos los casos de dos awjuh, conservando el preferido sin eliminar el alternativo.
- `يَسْرِ` y las seis ocurrencias de `نُذُرِ` bajo waqf.
- Waqf con sukūn, ishmām y rawm, incluidos casos no elegibles.
- Variación de terminación y rasm de `إِبْرَٰهِيم` y demás lexemas.
- U+06EA en contextos relacionados y no relacionados con rāʾ.
- Reconstrucción exacta del texto después de retirar anotaciones.

## Decisión de migración

- El original permanece intacto en la fuente y en la custodia histórica.
- Se copió el archivo con el mismo nombre y se verificó su SHA-256 antes de editarlo.
- Se corrigieron tablas, árboles y algoritmos en esa copia, dejando comentarios explicativos.
- Los awjuh, preferencias y dependencias se modelan como datos explícitos y correlacionados.
- Las excepciones se resuelven antes de las reglas generales y lo desconocido devuelve `requires_review`.
- Tafkhīm/taghlīẓ se mapea a azul oscuro `#00008B`; tarqīq, a negro `#000000`.
- Las formas se enlazarán a ocurrencias verificadas, no a igualdad de strings vocalizados.
- La validación manual corresponde al desarrollo; la aprobación definitiva conserva la revisión final del especialista.

## Próximo documento

Según el orden aprobado, continúa `DECISION_LOGIC_IDGHAM.md` contra la Parte 9.
