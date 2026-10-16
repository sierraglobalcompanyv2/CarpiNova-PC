# CarpiNova-PC — Knowledge Explorer y aprendizaje guiado

CarpiNova-PC es el consumidor web local de `CarpiNova-Knowledge`. Permite explorar conocimiento canónico trazable sin duplicarlo ni reinterpretarlo, combina búsqueda y dashboard educativo con lecciones guiadas, figuras normalizadas e interacciones source-backed.

## Alcance actual

- React + Vite + TypeScript.
- Ejecución local mediante `localhost`.
- Dashboard educativo con **Empieza aquí**, **Aprende paso a paso** y **Explora todo**, reutilizando categorías y lecciones reales del Knowledge.
- Búsqueda determinística y filtros por `content_type`.
- `learning_text` como explicación principal, con fallback explícito a `normalized_text` y después `source_transcription`.
- Procedencia visible por página/fuente.
- Lecciones guiadas resueltas por `lesson_id`, con pasos en el orden canónico y navegación segura entre lección y contenido.
- Figuras de apoyo que declaran `reconstruction.render_contract = normalized-2d-v1`, renderizadas desde sus entidades, capas y anotaciones canónicas.
- Interacciones source-backed actualmente soportadas: `highlight`, `highlight_measurements`, `identify_parts` y `guided_sequence`.
- Validación fail-closed para Knowledge, referencias, figuras e interacciones requeridas.

No incluye backend, base de datos, Docker, cuentas, progreso persistente, favoritos, IA, embeddings, búsqueda vectorial, CAD/3D, Furniture Engine ni reglas automáticas de fabricación.

## Requisitos

- Windows para la aceptación local objetivo del producto.
- Node.js 22 y npm. CI usa Node 22.
- El repositorio `CarpiNova-Knowledge` disponible localmente.
- Python 3.12 y `uv` configurados como exige `CarpiNova-Knowledge`, porque la preparación ejecuta su validador y generador canónico.

La disposición local recomendada es:

```text
<carpeta-de-trabajo>/
├── CarpiNova-PC/
└── CarpiNova-Knowledge/
```

Con esa estructura no hace falta indicar la ruta de Knowledge manualmente.

## 1. Instalar dependencias

La resolución de dependencias está fijada en `package-lock.json`:

```bash
npm ci
```

## 2. Preparar Knowledge

Con `CarpiNova-Knowledge` como repositorio hermano:

```bash
npm run knowledge:prepare
```

O indicando explícitamente su ruta:

```bash
npm run knowledge:prepare -- --knowledge-root "C:\ruta\a\CarpiNova-Knowledge"
```

El comando:

1. valida el repositorio Knowledge;
2. genera la distribución `BOOK` canónica;
3. valida manifest y SHA-256 de los bundles requeridos;
4. reemplaza `generated/knowledge/` solo cuando todas las comprobaciones pasan.

La preparación acepta las versiones Knowledge soportadas por el código (`1.0.0`, `1.1.0` y `1.2.0`). El contrato activo desarrollado para las capacidades actuales es Knowledge `1.2.0`.

El origen esperado permanece:

```text
book_id = cpnc-2025
scope = BOOK
source_manifest_sha256 = 318ceb94569608bfe062e3e50c7032edee79febf06102f7eec760769a6dfd90c
```

Y deben existir con hashes válidos:

```text
knowledge.bundle.json
figures.bundle.json
lessons.bundle.json
```

`generated/` es reproducible y está ignorado por Git. No copies ni edites manualmente Knowledge dentro de CarpiNova-PC.

## 3. Ejecutar en desarrollo

```bash
npm run dev
```

Abre la dirección `localhost` que muestre Vite.

Si Knowledge no puede cargarse o una referencia requerida viola el contrato, la aplicación debe fallar cerrada. Después de corregir/preparar Knowledge basta recargar la página; el producto no depende de acceso remoto a GitHub en runtime.

## 4. Verificaciones automáticas

```bash
npm ci
npm test
npm run typecheck
npm run build
```

Para un gate de consumidor contra Knowledge real:

```bash
npm run knowledge:prepare -- --knowledge-root "<ruta-real-a-CarpiNova-Knowledge>"
npm test
npm run typecheck
npm run build
npm audit
```

## 5. Preview de producción

```bash
npm run build
npm run preview
```

En preview comprobar al menos estos flujos:

```text
buscar -> filtrar -> abrir ficha -> leer explicación/fallback -> comprobar procedencia

Home -> Aprende paso a paso -> abrir lección -> recorrer pasos -> Ver contenido -> comprobar procedencia -> volver a la lección

lección con figura normalizada -> comprobar diagrama -> ejecutar interacción disponible -> verificar comportamiento fail-closed ante referencias inválidas
```

También comprobar aproximadamente estos anchos:

```text
1440 px
768 px
390 px
```

Validar que no haya overflow horizontal, que búsqueda/filtros/lecciones/figuras sean utilizables, que enlaces y acciones esenciales estén visibles y que el foco de teclado sea perceptible.

## Gate final antes de declarar un cambio listo

Todos los comandos relevantes al alcance deben haberse ejecutado realmente. Para cambios que consuman Knowledge o afecten lecciones/figuras/interacciones, una suite sintética verde por sí sola no es suficiente: preparar y probar el bundle canónico real.

No hardcodees una copia pedagógica de las lecciones, figuras o interacciones dentro de CarpiNova-PC. El contenido, las relaciones y la procedencia proceden de los bundles canónicos.

## Gobernanza

Las reglas durables para agentes y Codex están en `AGENTS.md`.
