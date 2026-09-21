# Estructura general del proyecto

- **Estado:** aprobada como estructura inicial
- **Fecha:** 2026-09-21

## Objetivo

La estructura separa de forma visible cuatro responsabilidades que no deben confundirse:

1. La aplicación que presenta información al usuario.
2. El motor determinista que analiza texto sin depender de la interfaz.
3. El conocimiento religioso estructurado y sometido a revisión.
4. Las fuentes y el corpus cuya integridad debe conservarse.

No se crea todavía código de aplicación, configuración de workspace ni contenido migrado. Las carpetas reservan límites que deberán respetarse cuando comience la implementación.

## Árbol inicial

```text
e-tajweed/
├── .github/
│   └── workflows/                 # Integración continua y controles
├── apps/
│   └── web/                       # Aplicación Next.js
│       ├── public/
│       │   └── fonts/             # Fuentes autorizadas para la aplicación
│       └── src/
│           ├── app/               # Rutas y layouts de Next.js App Router
│           ├── components/        # Componentes compartidos de la aplicación
│           ├── features/          # Funcionalidades de interfaz por dominio
│           ├── lib/               # Adaptadores e integración de la aplicación
│           └── styles/            # Estilos globales y tokens visuales
├── packages/
│   └── engine/                    # Motor TypeScript puro y determinista
│       ├── src/
│       │   ├── domain/            # Tipos, contratos e invariantes
│       │   ├── unicode/           # Segmentación y operaciones Unicode seguras
│       │   ├── detection/         # Detección de candidatos de reglas
│       │   ├── resolution/        # Precedencias y solapamientos
│       │   ├── explanation/       # Resultados explicables y trazables
│       │   └── validation/        # Validación técnica de entradas y salidas
│       └── tests/
│           ├── unit/              # Pruebas unitarias del motor
│           └── property/          # Propiedades e invariantes del motor
├── knowledge/                     # Conocimiento versionado, no interfaz
│   ├── rules/                     # Especificaciones de reglas aprobables
│   ├── exceptions/                # Excepciones explícitas
│   ├── evidence/                  # Relación entre reglas, fuentes y páginas
│   ├── reviews/                   # Estados y aprobaciones humanas
│   └── schemas/                   # Esquemas de los artefactos de conocimiento
├── resources/
│   ├── corpus/
│   │   ├── original/              # Corpus fuente inmutable
│   │   ├── manifests/             # Procedencia, versión, licencia y hashes
│   │   └── derived/               # Artefactos reproducibles derivados
│   └── sources/
│       ├── catalog/               # Metadatos bibliográficos
│       ├── citations/             # Citas necesarias y referencias de página
│       ├── licenses/              # Licencias y autorizaciones
│       └── private/               # Material local no publicable
├── tests/                         # Verificación transversal
│   ├── golden/                    # Casos aprobados por revisión humana
│   ├── corpus/                    # Pruebas sobre el corpus completo
│   ├── fixtures/                  # Entradas compartidas de prueba
│   ├── e2e/                       # Flujos de aplicación en navegador
│   └── visual/                    # Evidencia y regresión visual
├── tools/
│   ├── corpus/                    # Importación e inspección del corpus
│   ├── integrity/                 # Hashes y comprobaciones de invariantes
│   └── migration/                 # Herramientas temporales de migración
└── docs/
    ├── architecture/
    │   └── adr/                   # Architecture Decision Records
    ├── governance/                # Políticas, responsabilidades y aprobaciones
    ├── migration/                 # Inventario y decisiones de migración
    ├── research/                  # Investigación aún no aprobada
    └── validation/                # Protocolos e informes de validación
```

## Dirección permitida de dependencias

```text
apps/web ───────→ packages/engine
    │                    ↑
    ├──────────→ knowledge
    └──────────→ resources/corpus

tools ─────────→ knowledge y resources
tests ─────────→ todas las capas que verifica
```

Reglas obligatorias:

- `packages/engine` no puede importar Next.js, React ni componentes visuales.
- `packages/engine` no contendrá colores, JSX, rutas web ni acceso implícito al corpus.
- `knowledge` no contendrá componentes de interfaz ni decisiones de coloración visual.
- `apps/web` no reimplementará reglas religiosas dentro de componentes.
- `resources/corpus/original` será inmutable. Toda transformación irá a `derived` y deberá ser reproducible.
- `resources/sources/private` no se publicará en Git; sólo podrán versionarse sus metadatos, citas permitidas, licencias y decisiones.
- `research` no equivale a conocimiento aprobado. Una conclusión sólo puede pasar a `knowledge` mediante el proceso de revisión.
- Una herramienta de migración nunca se convertirá silenciosamente en parte del motor de producción.

## Decisiones deliberadas

### Un solo motor de aplicación

La arquitectura inicial es TypeScript. No se crea un segundo motor Python. Si en el futuro se necesita Python para investigación o conversión puntual, será una herramienta aislada y no otra implementación normativa de las reglas.

### Next.js limitado a la aplicación

`apps/web/src/app` sigue las convenciones de App Router. Las carpetas `components`, `features`, `lib` y `styles` están fuera del árbol de rutas para mantener clara su finalidad.

### Conocimiento separado del código

Una regla religiosa deberá poder revisarse como conocimiento estructurado, con fuentes y aprobación, sin tener que interpretar un componente React. El motor consume reglas validadas; no inventa su contenido.

### Sin paquete visual compartido por ahora

Sólo existe una aplicación prevista. Los componentes permanecerán en `apps/web` hasta que una segunda aplicación real justifique extraer un paquete de interfaz común.

## Criterio para añadir carpetas nuevas

Una carpeta nueva deberá representar una responsabilidad estable y distinta. No se añadirá por anticipar una tecnología hipotética. Si cambia un límite arquitectónico, primero deberá registrarse la decisión en `docs/architecture/adr`.
