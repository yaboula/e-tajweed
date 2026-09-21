# Biblioteca de referencias de e-tajweed

**Estado:** activa  
**Versión:** 1.0.0  
**Fecha:** 2026-09-21  
**Ámbito inicial:** tajwīd según Warsh ʿan Nāfiʿ por ṭarīq al-Azraq, tratamiento digital del texto coránico y aplicación e-tajweed.

## 1. Propósito

Este documento establece las fuentes que deberán consultar las personas y los agentes de IA que trabajen en e-tajweed. Su objetivo es impedir que una decisión religiosa, lingüística o técnica se tome únicamente de memoria, por intuición o a partir del código anterior.

Las referencias técnicas resuelven cuestiones técnicas. No constituyen autoridad sobre la recitación. Las fuentes religiosas documentan la materia de tajwīd y qirāʾāt, pero ninguna implementación se considerará religiosamente aprobada hasta que sea revisada por un profesor, qāriʾ o especialista cualificado.

## 2. Jerarquía de autoridad

Cuando varias fuentes sean aplicables, se utilizará el siguiente orden:

1. Fuentes religiosas aceptadas expresamente por el proyecto para Warsh ʿan Nāfiʿ por ṭarīq al-Azraq.
2. Decisiones documentadas y aprobadas por el especialista religioso responsable.
3. Estándares técnicos normativos, especialmente Unicode y W3C.
4. Documentación oficial de lenguajes, frameworks y herramientas.
5. Decisiones arquitectónicas internas registradas en el repositorio.
6. Código, documentos y resultados del proyecto anterior, exclusivamente como material que debe auditarse.

El proyecto anterior, una respuesta de IA, una librería de software o una visualización existente nunca serán autoridad religiosa por sí mismos.

## 3. Protocolo obligatorio para personas y agentes

Antes de implementar o modificar una regla, se deberá:

1. Determinar si la cuestión es religiosa, lingüística, Unicode, arquitectónica, visual, de pruebas, de seguridad o una combinación de ellas.
2. Consultar las fuentes correspondientes de este documento.
3. Registrar la edición o versión de la fuente, la página o sección exacta y la fecha de consulta.
4. Distinguir explícitamente entre regla general, excepción, wajh permitido, preferencia de lectura y decisión puramente visual.
5. Crear casos positivos, negativos, fronterizos y, cuando corresponda, casos de waṣl y waqf.
6. Someter el resultado religioso y visual a revisión humana cualificada.

Si falta una fuente suficiente, dos fuentes parecen contradecirse, la edición no puede identificarse o el agente no comprende con seguridad el caso, se aplicará este comportamiento:

```text
estado = requiere_revision
motivo = documentado
resultado_religioso = no_inventar
acción = detener_la_decisión_y_escalar
```

La incertidumbre explícita es un resultado válido. Inventar una respuesta o ocultar una duda no lo es.

## 4. Referencias religiosas y lingüísticas

### REL-001 — Libro de trabajo local

- **Título:** *مذكرة في أحكام التجويد برواية ورش عن نافع من طريق الأزرق*
- **Autor:** عبد الكريم بن مخلوف مقيدش
- **Edición identificada:** sexta edición, Argelia, 2014
- **ISBN:** 978-9947-881-44-6
- **Ubicación heredada:** `D:\Users\aboul\Desktop\Mesa de Trabajo\Mesa de Trabajo3\docs\libro`
- **Uso:** fuente principal de trabajo para extraer y contrastar reglas de tajwīd de Warsh por al-Azraq.
- **Estado:** aceptada para estudio; pendiente de catalogación página por página y validación especializada.
- **Restricción:** no copiar ni publicar íntegramente sin revisar los derechos. Las citas deberán limitarse a lo necesario para trazabilidad y revisión.

### REL-002 — دليل القواعد في القراءة السليمة للقرآن الكريم

- **Autoridad:** Ministerio de Habices y Asuntos Islámicos del Reino de Marruecos.
- **URL:** <https://www.habous.gov.ma/2012-01-24-11-49-11/758-%D9%85%D9%86%D8%B4%D9%88%D8%B1%D8%A7%D8%AA-%D8%A7%D9%84%D8%AA%D8%B9%D9%84%D9%8A%D9%85-%D8%A7%D9%84%D8%B9%D8%AA%D9%8A%D9%82/16756-%D8%AF%D9%84%D9%8A%D9%84-%D8%A7%D9%84%D9%82%D9%88%D8%A7%D8%B9%D8%AF-%D9%81%D9%8A-%D8%A7%D9%84%D9%82%D8%B1%D8%A7%D8%A1%D8%A9-%D8%A7%D9%84%D8%B3%D9%84%D9%8A%D9%85%D8%A9-%D9%84%D9%84%D9%82%D8%B1%D8%A2%D9%86-%D8%A7%D9%84%D9%83%D8%B1%D9%8A%D9%85.html>
- **Uso:** consulta institucional sobre makhārij, ṣifāt, nūn y mīm, idghām, lām, madd, rāʾ, hamz, imāla, yāʾāt, waqf e ibtidāʾ en el contexto de Warsh por al-Azraq.
- **Estado:** referencia institucional; cada aplicación concreta requiere cita exacta y revisión humana.

### REL-003 — الدليل الأوفق إلى رواية ورش عن نافع من طريق الأزرق

- **Autores:** مصطفى البحياوي، عبد الهادي حميتو، عبد العزيز العمراوي
- **Autoridad:** Ministerio de Habices y Asuntos Islámicos del Reino de Marruecos.
- **URL:** <https://www.habous.gov.ma/component/booklibrary/?Itemid=0&catid=79&id=20&task=view>
- **Uso:** consulta especializada sobre Warsh por al-Azraq, incluidos taḥrīrāt, waqf e ibtidāʾ.
- **Estado:** referencia institucional; pendiente de registrar la edición exacta que utilizará el proyecto.

### REL-004 — Recursos de Warsh del Complejo Rey Fahd

- **Autoridad:** King Fahd Glorious Qur'an Printing Complex.
- **URL principal:** <https://qurancomplex.gov.sa/warsh/>
- **Guía técnica:** <https://qurancomplex.gov.sa/wp-content/uploads/isdarat/booklets/complextechguide.pdf>
- **Uso:** contraste de texto, rasm ʿUthmānī, signos, fuentes y presentación del muṣḥaf de Warsh.
- **Estado:** referencia institucional para corpus y presentación; la licencia y las condiciones de redistribución deberán verificarse antes de incorporar datos o fuentes.

### Regla de validación religiosa

Ninguna de estas referencias elimina la obligación de revisión humana. Para considerar terminada una regla deberá existir esta cadena:

```text
fuente religiosa
  → edición y página
  → especificación inequívoca
  → ejemplos y contraejemplos
  → implementación
  → pruebas
  → revisión visual
  → aprobación del especialista
```

## 5. Unicode y procesamiento del árabe

### UNI-001 — Unicode Standard Annex #15: Normalization Forms

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/reports/tr15/>
- **Consultar para:** NFC, NFD, NFKC, NFKD y consecuencias de normalizar texto.
- **Norma del proyecto:** ninguna normalización se aplicará al corpus original de manera implícita. NFKC y NFKD quedan prohibidas sobre el texto coránico fuente salvo estudio, justificación y aprobación explícitos.

### UNI-002 — Unicode Standard Annex #29: Text Segmentation

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/reports/tr29/>
- **Consultar para:** grafemas extendidos, límites de palabra y segmentación.
- **Norma del proyecto:** una posición UTF-16 de JavaScript no se tratará como si fuera necesariamente una letra o un grafema visible.

### UNI-003 — Unicode Standard Annex #9: Bidirectional Algorithm

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/reports/tr9/>
- **Consultar para:** dirección RTL, texto bidireccional, números, puntuación y mezcla de árabe con otros sistemas de escritura.

### UNI-004 — Unicode Standard Annex #53: Unicode Arabic Mark Rendering

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/reports/tr53/>
- **Consultar para:** orden y renderizado de marcas árabes combinantes.
- **Norma del proyecto:** distinguir siempre entre el orden interno de code points y la posición visual resultante.

### UNI-005 — Unicode Core Specification, Chapter 9: Middle East-I

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/versions/Unicode18.0.0/core-spec/chapter-9/>
- **Consultar para:** escritura árabe, unión, marcas, signos y comportamiento general de renderizado.
- **Versión fijada inicialmente:** Unicode 18.0.0. Cualquier actualización deberá evaluarse y registrarse.

### UNI-006 — Tablas oficiales de caracteres árabes

- **Arabic:** <https://unicode.org/charts/nameslist/n_0600.html>
- **Arabic Extended-A:** <https://www.unicode.org/charts/nameslist/n_08A0.html>
- **Consultar para:** nombre oficial, code point y bloque de cada letra, haraka o signo coránico.

### UNI-007 — Unicode Standard Annex #14: Line Breaking Algorithm

- **Autoridad:** Unicode Consortium.
- **URL:** <https://www.unicode.org/reports/tr14/>
- **Consultar para:** saltos de línea y comportamiento de maquetación sin romper secuencias indebidamente.

## 6. Arquitectura y TypeScript

### TS-001 — TypeScript Handbook

- **Autoridad:** TypeScript, Microsoft.
- **URL:** <https://www.typescriptlang.org/docs/handbook/>
- **Consultar para:** sistema de tipos y patrones oficiales del lenguaje.

### TS-002 — TSConfig `strict`

- **Autoridad:** TypeScript, Microsoft.
- **URL:** <https://www.typescriptlang.org/tsconfig/strict>
- **Consultar para:** familia de comprobaciones estrictas.
- **Norma del proyecto:** el motor deberá compilar con TypeScript estricto. Las excepciones deberán justificarse individualmente.

### TS-003 — Referencia de TSConfig

- **Autoridad:** TypeScript, Microsoft.
- **URL:** <https://www.typescriptlang.org/tsconfig/>
- **Consultar para:** significado y efectos de cada opción del compilador.

### TS-004 — Narrowing y exhaustividad

- **Autoridad:** TypeScript, Microsoft.
- **URL:** <https://www.typescriptlang.org/docs/handbook/2/narrowing>
- **Consultar para:** uniones discriminadas, narrowing y comprobaciones exhaustivas mediante `never`.

### WEB-001 — Next.js App Router

- **Autoridad:** documentación oficial de Next.js.
- **URL:** <https://nextjs.org/docs/app>
- **Política de soporte:** <https://nextjs.org/support-policy>
- **Consultar para:** aplicación web, convenciones del framework y versiones mantenidas.
- **Límite de autoridad:** Next.js no define el modelo del conocimiento religioso ni será una dependencia del núcleo determinista.

### Normas arquitectónicas internas pendientes

Los estándares externos no definen por sí solos nuestra arquitectura. El repositorio deberá documentar mediante ADR sus decisiones sobre:

- Separación entre corpus, detección, anotaciones y presentación.
- Modelo de reglas, excepciones, awjuh y preferencias.
- Resolución explícita de solapamientos.
- Versionado de reglas y datasets.
- Explicabilidad y trazabilidad de cada resultado.
- API estable del motor independiente de la aplicación.

## 7. Pruebas y verificación

### TEST-001 — Vitest

- **Autoridad:** documentación oficial de Vitest.
- **URL:** <https://vitest.dev/guide/>
- **Consultar para:** pruebas unitarias, integración, regresión, aserciones y snapshots controlados.
- **Nota:** la ejecución de Vitest no sustituye la comprobación de tipos; la CI deberá ejecutar también el compilador TypeScript.

### TEST-002 — fast-check

- **Autoridad:** documentación oficial de fast-check.
- **URL:** <https://fast-check.dev/docs/introduction/getting-started/>
- **Consultar para:** property-based testing, generación reproducible de entradas y reducción de casos fallidos.
- **Propiedades mínimas candidatas:** retirar anotaciones reconstruye exactamente la entrada; el motor no cambia el orden ni el valor de los code points; una misma entrada y versión producen el mismo resultado.

### TEST-003 — StrykerJS

- **Autoridad:** documentación oficial de Stryker Mutator.
- **URL:** <https://stryker-mutator.io/docs/stryker-js/introduction/>
- **Consultar para:** mutation testing de JavaScript y TypeScript.
- **Uso:** evaluar si las pruebas detectan modificaciones incorrectas de la lógica, especialmente en límites, excepciones y precedencias.

### TEST-004 — Playwright

- **Autoridad:** documentación oficial de Playwright.
- **Accesibilidad:** <https://playwright.dev/docs/accessibility-testing>
- **ARIA snapshots:** <https://playwright.dev/docs/aria-snapshots>
- **Consultar para:** navegador real, flujos de interfaz y comprobaciones automatizadas de accesibilidad.
- **Límite:** las pruebas automáticas no sustituyen la inspección humana de ligaduras, diacríticos, coloración o correspondencia con el muṣḥaf.

### Golden tests religiosos

Los golden tests serán un corpus interno aprobado, no una verdad generada por la herramienta. Cada caso deberá registrar:

```text
case_id
rule_id
riwaya
tariq
source_id
source_edition
source_page_or_section
input_code_points
expected_annotations
expected_explanation
reviewer
review_status
review_date
```

## 8. Integridad del texto coránico

### INT-001 — NIST FIPS 180-4, Secure Hash Standard

- **Autoridad:** National Institute of Standards and Technology.
- **URL:** <https://csrc.nist.gov/pubs/fips/180-4/upd1/final>
- **Consultar para:** algoritmos de hash SHA-2.
- **Norma inicial:** guardar al menos SHA-256 de cada archivo original del corpus y verificarlo en CI.
- **Límite:** un hash demuestra estabilidad de bytes, no corrección religiosa del contenido.

### Registro obligatorio de cada corpus

Todo dataset coránico deberá incluir:

- Identificador y versión inmutables.
- Procedencia y URL o custodio.
- Fecha de obtención.
- Licencia o autorización de uso.
- Codificación y formato.
- Hash criptográfico del archivo original.
- Recuentos de control definidos para ese corpus.
- Transformaciones realizadas y hashes resultantes.
- Estado y responsable de validación.

La coloración y las explicaciones serán anotaciones externas. Al retirar las anotaciones deberá recuperarse exactamente la entrada original, byte por byte cuando el formato lo permita y siempre code point por code point.

## 9. Diseño árabe, RTL y accesibilidad

### UX-001 — Arabic and Persian Layout Requirements

- **Autoridad:** World Wide Web Consortium.
- **URL:** <https://www.w3.org/TR/alreq/>
- **Consultar para:** RTL, composición, dirección, saltos, puntuación y necesidades de presentación árabe.

### A11Y-001 — Web Content Accessibility Guidelines 2.2

- **Autoridad:** World Wide Web Consortium.
- **URL:** <https://www.w3.org/TR/WCAG22/>
- **Consultar para:** uso del color, contraste, reflujo, zoom, teclado, estructura semántica y compatibilidad con tecnologías de asistencia.
- **Norma del proyecto:** ninguna regla dependerá exclusivamente del color; deberá existir una alternativa textual, semántica o visual adicional.

### Revisión visual humana

La aceptación visual incluirá, como mínimo:

- Comparación con el muṣḥaf de referencia aceptado.
- Inspección de ligaduras y posición de diacríticos.
- Pruebas RTL con números, traducciones y explicaciones.
- Pruebas en móvil, escritorio y distintos niveles de zoom.
- Revisión de cada combinación de fuente, navegador y sistema operativo declarada como compatible.

## 10. Seguridad, cadena de suministro y conservación

### SEC-001 — OWASP Application Security Verification Standard

- **Autoridad:** OWASP Foundation.
- **URL:** <https://owasp.org/projects/asvs>
- **Versión inicial de referencia:** ASVS 5.0.0.
- **Consultar para:** requisitos verificables de seguridad de la aplicación.

### SEC-002 — GitHub Protected Branches

- **Autoridad:** documentación oficial de GitHub.
- **URL:** <https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches>
- **Consultar para:** revisiones obligatorias, comprobaciones de estado y protección de ramas.

### SEC-003 — GitHub Dependency Review

- **Autoridad:** documentación oficial de GitHub.
- **URL:** <https://docs.github.com/en/code-security/how-tos/secure-your-supply-chain/manage-your-dependency-security/configure-dependency-review-action>
- **Consultar para:** detectar nuevas dependencias vulnerables o incompatibles antes de integrarlas.

### SEC-004 — GitHub Actions: uso seguro

- **Autoridad:** documentación oficial de GitHub.
- **URL:** <https://docs.github.com/en/actions/reference/security/secure-use>
- **Consultar para:** permisos mínimos, secretos, dependencias de workflows y riesgos de código no confiable.

### SEC-005 — GitHub Artifact Attestations

- **Autoridad:** documentación oficial de GitHub.
- **URL:** <https://docs.github.com/en/actions/concepts/security/artifact-attestations>
- **Consultar para:** procedencia verificable de artefactos y releases.

### LEGAL-001 — WIPO Copyright FAQ

- **Autoridad:** World Intellectual Property Organization.
- **URL:** <https://www.wipo.int/en/web/copyright/faq-copyright>
- **Consultar para:** principios generales de derechos de autor.
- **Límite:** no sustituye asesoramiento jurídico ni resuelve por sí sola la licencia concreta de un libro, fuente tipográfica o corpus.

## 11. Registro de decisiones derivadas de fuentes

Cada decisión religiosa o técnica relevante deberá tener un registro con esta estructura mínima:

```yaml
decision_id: DEC-0000
status: proposed | requires_review | approved | rejected | superseded
domain: religious | linguistic | unicode | architecture | visual | security
question: ""
sources:
  - source_id: REL-000
    edition_or_version: ""
    page_or_section: ""
interpretation: ""
alternatives_considered: []
implementation_impact: ""
tests: []
religious_reviewer: null
technical_reviewer: null
approved_at: null
```

Una refactorización no podrá alterar una decisión religiosa aprobada sin crear una nueva decisión que cite y explique expresamente el cambio.

## 12. Mantenimiento de esta biblioteca

- Las referencias religiosas deberán fijar edición; una página genérica sin edición no es suficiente para aprobar una regla.
- Los estándares técnicos deberán fijar versión cuando un cambio pueda alterar el comportamiento.
- Los enlaces se comprobarán periódicamente, sin sustituir silenciosamente una fuente desaparecida.
- Los documentos con restricciones de copyright se catalogarán mediante metadatos y citas necesarias; no se copiarán íntegramente al repositorio sin autorización.
- Toda nueva referencia deberá indicar autoridad, alcance, versión, estado, licencia conocida y situaciones en las que debe consultarse.
- Cuando una fuente sea reemplazada, permanecerá registrada como histórica para poder reproducir decisiones anteriores.

## 13. Principio final

```text
No recordar cuando se puede consultar.
No suponer cuando se puede verificar.
No implementar una duda religiosa como si fuera certeza.
No modificar el texto coránico para facilitar el software.
```
