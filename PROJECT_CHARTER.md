# e-tajweed — Constitución de integridad y competencias del proyecto

## 1. Propósito del documento

Este documento establece las competencias, responsabilidades y condiciones
innegociables para cualquier persona o agente de IA que trabaje en **e-tajweed**.

El proyecto trata la digitalización, análisis y visualización de reglas de
Tajwīd del Corán, con atención especial a la recitación de **Warsh ʿan Nāfiʿ
por ṭarīq al-Azraq**. Por la naturaleza del proyecto, una implementación que
«funciona casi siempre» no es aceptable.

Ningún modelo de IA, desarrollador o sistema puede atribuirse infalibilidad ni
autoridad religiosa. La ingeniería puede estructurar, implementar, comprobar
y documentar las reglas, pero la aprobación religiosa final requiere la
revisión de una persona cualificada.

Este archivo debe leerse antes de diseñar, migrar, modificar o implementar
cualquier parte del proyecto.

## 2. Conocimiento religioso y lingüístico

La persona o agente responsable debe trabajar con conocimiento suficiente de:

- Tajwīd general.
- Particularidades de Warsh ʿan Nāfiʿ por ṭarīq al-Azraq.
- Árabe coránico.
- Rasm ʿUthmānī.
- Harakāt, signos coránicos, waqf, ibtidāʾ y taḥrīrāt.
- Diferencia entre regla general, excepción, wajh permitido y preferencia de
  lectura.
- Capacidad de citar libro, página y fuente de cada decisión.

El respaldo final de un profesor, qāriʾ o especialista cualificado es
obligatorio para aprobar las interpretaciones religiosas y los resultados que
se presenten como correctos.

## 3. Ingeniería Unicode

La persona o agente responsable debe dominar:

- Code points, unidades de código UTF-16 y grafemas.
- Marcas combinantes.
- Orden de harakāt.
- Formas de normalización Unicode.
- Signos coránicos de los bloques árabes.
- Unión y renderizado de letras.
- Diferencias entre posición visual y posición interna.
- Comparación de textos sin destruir información.

Nunca se asumirá que «un carácter» equivale a una posición de JavaScript.

Toda política de normalización, segmentación, indexación o comparación debe
estar documentada y probada con texto coránico real antes de utilizarse en un
detector.

## 4. Arquitectura de software

La arquitectura deberá garantizar:

- TypeScript estricto.
- Un motor determinista e independiente de la aplicación.
- Modelado formal de reglas y excepciones.
- Separación absoluta entre texto coránico, detección y presentación.
- Versionado de reglas.
- Resultados explicables y trazables.
- Resolución explícita de solapamientos entre reglas.
- Un diseño que permita sustituir la aplicación sin tocar el conocimiento.

La interfaz, los colores y los componentes visuales nunca podrán definir por sí
mismos la lógica de Tajwīd.

## 5. Verificación y pruebas

La cobertura de código no será suficiente. El proyecto necesitará:

- Casos positivos.
- Casos negativos.
- Casos fronterizos.
- Casos de waṣl y waqf.
- Excepciones.
- Casos con varias reglas coincidentes.
- Pruebas sobre todo el Corán.
- Golden tests aprobados manualmente.
- Pruebas de regresión.
- Pruebas de propiedades.
- Mutation testing cuando resulte útil.
- Comparación carácter por carácter.
- Revisión humana de resultados visuales.

Una regla no estará terminada porque el código compile. Estará terminada cuando
exista la trazabilidad completa:

```text
Fuente → página → especificación → caso verificado
       → implementación → resultado → aprobación humana
```

Ninguna afirmación de precisión total podrá realizarse sin evidencia suficiente,
reproducible y documentada.

## 6. Integridad del texto coránico

Las siguientes condiciones son innegociables:

- El texto original será inmutable.
- Se guardarán huellas criptográficas del corpus.
- La coloración será una capa superpuesta y nunca modificará el texto fuente.
- Ningún algoritmo podrá eliminar, sustituir o reordenar letras y marcas.
- La salida deberá reconstruir exactamente la entrada al retirar las
  anotaciones.
- Ante una situación desconocida, el motor no inventará una respuesta:
  devolverá un estado de incertidumbre.
- Cada dataset tendrá procedencia, versión y licencia.
- La IA no modificará silenciosamente texto coránico.

Cualquier operación sobre el texto deberá ser reversible y verificable. Los
errores de integridad deberán bloquear la publicación del resultado.

## 7. Diseño visual y accesibilidad

La implementación visual deberá cuidar:

- RTL auténtico.
- Tipografía coránica adecuada.
- Ligaduras y posicionamiento de diacríticos.
- Colores distinguibles y accesibles.
- Alternativas que no dependan exclusivamente del color.
- Tooltips y explicaciones que no rompan la unión árabe.
- Compatibilidad con móvil, escritorio, zoom y lectores de pantalla.
- Comparación visual con el muṣḥaf de referencia.

La presentación deberá conservar la legibilidad y dignidad del texto coránico
en todos los dispositivos soportados.

## 8. Seguridad y conservación

El proyecto deberá aplicar:

- Dependencias mínimas y auditadas.
- Actualizaciones controladas.
- Integración continua obligatoria.
- Protección de ramas.
- Revisiones antes de integrar cambios.
- Backups y releases reproducibles.
- Registro de decisiones.
- Prohibición de cambios doctrinales ocultos dentro de refactorizaciones.
- Respeto por licencias y derechos de las fuentes.

Los cambios que afecten reglas, excepciones, datos coránicos o resultados
esperados deberán declararse explícitamente y recibir una revisión específica.

## 9. Conducta obligatoria del desarrollador o agente

Quien trabaje en e-tajweed deberá:

- No presentar una inferencia como un hecho.
- No confiar ciegamente en el proyecto anterior.
- No confiar ciegamente en su primera interpretación.
- No migrar contenido sin clasificarlo previamente.
- No implementar una regla antes de comprenderla y documentarla.
- No declarar precisión del 100 % sin evidencia.
- No mezclar decisiones religiosas con decisiones técnicas o visuales.
- Documentar dudas, contradicciones y desacuerdos.
- Solicitar validación humana cuando corresponda.
- Mantener el contexto mediante documentación versionada y registros de
  decisiones, sin depender de la memoria de un chat.

## 10. Principio rector

La fiabilidad de e-tajweed no dependerá de afirmar que una persona o IA es
perfecta. Dependerá de la combinación de:

> Ingeniería rigurosa + fuentes trazables + pruebas exhaustivas + revisión
> humana cualificada + humildad ante la posibilidad de error.

Toda decisión técnica, migración, refactorización o nueva funcionalidad deberá
respetar este principio y las condiciones de este documento.
