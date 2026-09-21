# Migración de custodia: libro y análisis heredado

**Fecha:** 2026-09-21

## Resultado

Se realizaron dos copias locales no destructivas. No se modificó ni eliminó ningún archivo de `Mesa de Trabajo3`.

### REL-001 — Libro de trabajo

- Clasificación: fuente primaria de trabajo, conservada intacta.
- Origen lógico: `Mesa de Trabajo3/docs/libro`.
- Custodia local: `resources/sources/private/REL-001/libro`.
- Archivos: 14.
- Tamaño total: 232641 bytes.
- Hash del conjunto: `5c0a5003126b76056430535faec8b0300045b7849db7369be8406e9870d172b2`.
- Verificación: los 14 hashes SHA-256 de origen y destino coinciden.
- Publicación: bloqueada hasta revisar derechos.
- Validación pendiente: comprobar que los Markdown representan fielmente la edición impresa identificada. La identidad entre copias no demuestra fidelidad al libro físico.

El inventario verificable está en `resources/sources/catalog/REL-001.manifest.json`.

### LEGACY-ANALYSIS-001 — `analisis_tajweed_warsh`

- Clasificación: conocimiento derivado heredado, migrado exclusivamente para auditoría.
- Origen lógico: `Mesa de Trabajo3/analisis_tajweed_warsh`.
- Custodia local: `resources/sources/private/LEGACY-ANALYSIS-001/analisis_tajweed_warsh`.
- Archivos: 11.
- Tamaño total: 231478 bytes.
- Hash del conjunto: `e272d53d40834884388ad8d16369462161445a7fc5e769ea64a7595026329a81`.
- Verificación: los 11 hashes SHA-256 de origen y destino coinciden.
- Aprobación: ninguna. Los archivos no pertenecen todavía a `knowledge`.

El inventario verificable está en `resources/sources/catalog/LEGACY-ANALYSIS-001.manifest.json`.

## Protección de los originales

Las dos copias se encuentran bajo `resources/sources/private`, cuyo contenido está excluido de Git. Los manifiestos, el plan de auditoría y los resultados de revisión sí son versionables.

Las copias privadas de custodia no se modificarán. Para el trabajo activo, cada documento de `analisis_tajweed_warsh` se migrará con su nombre original a la zona versionada y se corregirá directamente después de compararlo con el libro. Git conservará la trazabilidad de las correcciones. La validación manual contra el muṣḥaf certificado se realizará durante el desarrollo y la revisión del especialista quedará como control final de la aplicación.
