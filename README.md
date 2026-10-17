# CarpiNova-PC — Knowledge Explorer y aprendizaje guiado

CarpiNova-PC es el consumidor web local de `CarpiNova-Knowledge`. Permite explorar conocimiento canónico trazable sin duplicarlo ni reinterpretarlo, combina búsqueda y dashboard educativo con lecciones guiadas, figuras normalizadas e interacciones source-backed.

## Las cuatro leyes del proyecto

CarpiNova se gobierna por cuatro leyes durables:

1. **KISS** — solución correcta, simple, eficiente y mantenible; preferir `A -> B` y escalar solo cuando sea necesario.
2. **Antirruido** — borrar/simplificar/reutilizar antes de agregar; no arrastrar documentación, ramas, workflows, compatibilidad o UI sin una necesidad vigente.
3. **Antiparches** — reproducir, aislar y corregir la causa raíz; no acumular excepciones CSS, datos duplicados, ramas por fuente o fallbacks para forzar verde.
4. **Diseño** — interfaz clara, consistente, accesible y fiel al mockup aprobado; una mejora visual no autoriza nueva arquitectura ni puede inventar conocimiento técnico.

Las reglas completas para agentes/Codex viven en `AGENTS.md`.

## Dirección visual aprobada

La evolución de CarpiNova debe seguir el mockup aprobado y mantener una identidad clara, cálida y práctica para carpintería:

- superficies claras/neutras con acentos inspirados en madera;
- el contenido técnico/visual es protagonista, no el chrome de un dashboard;
- navegación sencilla y panel/contexto de apoyo;
- los conceptos de workspace objetivo incluyen **Vistas**, **Despiece**, **Medidas** e **Instrucciones** cuando esas capacidades existan realmente;
- controles cómodos para mouse y tablet/touch;
- evitar apariencia de ERP, exceso de tarjetas/KPIs o complejidad visual que no ayude a aprender o construir;
- no simular CAD/3D, medidas o funciones aún no implementadas.

Como referencia externa de diseño se usan principios útiles del proyecto público `nextlevelbuilder/ui-ux-pro-max-skill`: jerarquía, tokens, tipografía, responsive, estados, contraste, foco y accesibilidad. **No** se incorpora su CLI, sus bases de datos ni su arquitectura al producto.

### Reglas visuales mínimas

- cuerpo de texto normalmente alineado a la izquierda;
- lectura alrededor de 16 px mínimo y `line-height` aproximado `1.5–1.7`;
- líneas largas aproximadamente `45–75ch`;
- contraste de texto normal objetivo WCAG AA (`4.5:1`);
- foco de teclado visible;
- controles esenciales de alrededor de `44x44 px` o mayores;
- etiquetas accesibles reales en formularios;
- sin overflow horizontal normal;
- comprobar aproximadamente `1440`, `768` y `390` px y los tamaños intermedios;
- probar textos reales y largos en español, no solo strings cortos.

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

## Modelo de entrega KISS

El flujo normal de PC es:

```text
OBJETIVO / MOCKUP CHECK
-> RED cuando cambia comportamiento
-> GREEN mínimo
-> npm test / typecheck / build
-> REAL KNOWLEDGE PROOF cuando aplique
-> PR / MERGE
-> SMOKE
```

Para cambios rutinarios de figuras/Knowledge no se debe crear un workflow/PR temporal por figura. El repositorio dispone de un **consumer proof permanente** que recibe los SHAs exactos de Knowledge y PC.

El flujo forense extendido se reserva para cambios de arquitectura, contratos nuevos, migraciones, incompatibilidades o fallas no explicadas.

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

La preparación acepta las versiones Knowledge soportadas por el código (`1.0.0`, `1.1.0` y `1.2.0`). El contrato activo desarrollado para las capacidades actuales es Knowledge `1.2.0`. La compatibilidad histórica no debe conservarse indefinidamente sin un consumidor vigente; cualquier eliminación requiere primero demostrar que es segura.

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

Para una comprobación local contra Knowledge real:

```bash
npm run knowledge:prepare -- --knowledge-root "<ruta-real-a-CarpiNova-Knowledge>"
npm test
npm run typecheck
npm run build
npm audit
```

## Consumer proof permanente por SHA exacto

Workflow: `.github/workflows/knowledge-consumer-proof.yml`.

Desde GitHub Actions, ejecuta **Knowledge Consumer Proof** y proporciona:

- `knowledge_sha`: commit exacto de `CarpiNova-Knowledge`;
- `pc_sha`: commit exacto de `CarpiNova-PC`.

El workflow:

1. rechaza referencias que no sean SHAs completos de 40 caracteres;
2. hace checkout inmutable de ambos commits;
3. instala Python/`uv` y Node 22;
4. ejecuta la validación y preparación real de Knowledge;
5. ejecuta `npm test`, `npm run typecheck`, `npm run build` y `npm audit`;
6. verifica que el build de producción contiene exactamente los mismos cuatro archivos de Knowledge generados.

Eso reemplaza el patrón ruidoso de crear una rama, workflow y PR temporal por cada figura rutinaria.

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

Comprobar aproximadamente:

```text
1440 px
768 px
390 px
```

Validar que no haya overflow horizontal, que búsqueda/filtros/lecciones/figuras sean utilizables, que enlaces y acciones esenciales estén visibles y que el foco de teclado sea perceptible.

## Continuidad si termina un chat/sesión

El proyecto debe recuperarse desde GitHub, no desde memoria privada:

1. leer `README.md` y `AGENTS.md` en Knowledge y PC;
2. leer los `main` actuales y sus SHAs exactos;
3. revisar Issues y PRs abiertos;
4. revisar el diff exacto y CI del PR activo;
5. continuar desde el checkpoint vivo del Issue/PR.

El estado activo no se duplica en nuevos handoffs Markdown dentro del repo. GitHub Issues/PRs contienen el trabajo vivo; Git history conserva el historial.

## Política documental antirruido

- `AGENTS.md`: leyes y reglas durables.
- `README.md`: arquitectura, uso, diseño y recuperación estables.
- Issues/PRs: estado actual, SHAs, decisiones y checkpoints.
- Git history: historial rutinario.
- docs dedicados: solo decisiones/releases con valor duradero único.

No duplicar planes, specs o checkpoints entre Knowledge y PC y no convertir cada gate en otro archivo de documentación.

## Gate final antes de declarar un cambio listo

Todos los comandos relevantes al alcance deben haberse ejecutado realmente. Para cambios que consuman Knowledge o afecten lecciones/figuras/interacciones, una suite sintética verde por sí sola no basta: usar el bundle canónico real mediante la preparación local o el consumer proof permanente.

No hardcodees una copia pedagógica de las lecciones, figuras o interacciones dentro de CarpiNova-PC. El contenido, las relaciones y la procedencia proceden de los bundles canónicos.

## Gobernanza

Las reglas durables para agentes y Codex están en `AGENTS.md`.
