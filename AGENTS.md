# CarpiNova PC — Agent Instructions

These instructions are durable repository guardrails. They do not replace live GitHub state, exact-head CI, `CarpiNova-Knowledge`, or a current handoff snapshot.

## Authority

Use this precedence when facts conflict:

1. live GitHub state, exact HEAD files, and exact-head CI;
2. canonical `CarpiNova-Knowledge` bundles/contracts;
3. published agent/Codex delta;
4. current handoff/audit documents;
5. historical documents or memory.

`CarpiNova-PC` is a consumer. It must not become a second source of truth for carpentry knowledge.

## Master laws

### KISS

Apply this order:

`CORRECTO -> SIMPLE -> EFICIENTE -> OPTIMIZADO -> EFICAZ -> ESTABLE -> MANTENIBLE -> RAPIDO -> ESCALABLE SOLO SI HACE FALTA`

Prefer the smallest correct solution. Do not add backend, database, auth, plugin systems, parallel renderers, generic frameworks, AI/vector infrastructure, or other architecture for hypothetical future needs.

### Anti-noise

Evaluate changes in this order:

`DELETE? -> SIMPLIFY? -> REUSE? -> MERGE? -> OPTIMIZE? -> EXTEND? -> ADD?`

Deletion requires evidence. Before deleting, check references, consumers, tests, workflows, provenance/reproducibility implications, rollback, and forensic value. If safety is not demonstrated, prefer `REVIEW` over `DELETE`.

### Anti-patch

Fix root causes, not symptoms. Do not stack compatibility hacks, UI special cases, duplicated canonical data, or test exceptions to force a green result.

## Consumer boundaries

- Consume generated Knowledge; do not copy canonical carpentry content into PC source code.
- `generated/knowledge/` is reproducible output and must not be hand-edited or committed as source truth.
- Prepare Knowledge through `npm run knowledge:prepare` (optionally with `-- --knowledge-root <path>`).
- Keep loading and reference validation fail-closed. Missing/invalid required records must not be silently fabricated.
- Preserve source provenance visible to the user where the current product exposes it.

## Figures and interactions

- Render only figures that explicitly opt into `reconstruction.render_contract = normalized-2d-v1`.
- The current renderer contract supports the existing normalized primitives (`rect`, `line`, `polyline`) and canonical annotations/layers.
- Do not add a second renderer or new primitive merely to make one source figure fit.
- New renderer/schema capability requires an explicit Knowledge source/contract gate before PC implementation.
- Supported source-backed lesson interactions include `highlight`, `highlight_measurements`, `identify_parts`, and `guided_sequence` when their references validate.
- Invalid interaction targets must fail closed rather than producing guessed UI behavior.

## Change discipline

Before mutating:

1. read fresh `main`;
2. inspect the exact branch/PR head and compare against `main`;
3. check for overlapping published work;
4. freeze one micro-objective;
5. keep one PR to one cause.

Do not combine product work with README/governance cleanup in the same PR. Do not treat handoff SHAs, synthetic merge SHAs, or stale branch names as merge leases.

## Required verification

For normal PC changes run:

```bash
npm ci
npm test
npm run typecheck
npm run build
```

When Knowledge consumption, figures, lessons, or interactions are affected, also prepare the intended real Knowledge repository before the final consumer proof:

```bash
npm run knowledge:prepare -- --knowledge-root "<path-to-CarpiNova-Knowledge>"
npm test
npm run typecheck
npm run build
npm audit
```

Use the actual canonical Knowledge bundle for the gate; synthetic fixtures alone are not sufficient consumer proof.

## Stop conditions

Stop and re-audit instead of improvising when any of these is true:

- the requested behavior would duplicate or reinterpret canonical Knowledge;
- source-faithful support requires a new Knowledge schema/render contract;
- required Knowledge references do not validate;
- exact-head CI is red for a product reason;
- `main` moved after the branch was based;
- overlapping agent/Codex work cannot be reconciled;
- a merge would rely on stale or synthetic evidence.

No merge is authorized merely because a branch looks correct. Re-read exact HEAD, compare, CI, scope, and mergeability at the merge gate.
