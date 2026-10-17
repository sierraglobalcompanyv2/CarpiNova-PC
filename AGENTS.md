# CarpiNova PC — Agent Instructions

These are durable repository guardrails for ChatGPT, Codex, Copilot, and other agents. They are intentionally compact. Live GitHub state, the approved product direction and canonical `CarpiNova-Knowledge` remain authoritative.

## Authority and recovery

When facts conflict, use this precedence:

1. live GitHub state: exact `main`, branch/PR heads, compare, CI, reviews and open issues;
2. canonical `CarpiNova-Knowledge` bundles/contracts for carpentry facts;
3. the approved CarpiNova visual/mockup direction for UX decisions;
4. these durable `AGENTS.md` rules;
5. the active issue/PR contract or checkpoint;
6. `README.md`, release records and historical documents;
7. memory.

A new chat/session must recover state from the repositories, not from private conversation history: read `AGENTS.md`, `README.md`, fresh `main`, open issues/PRs, exact diffs and exact-head CI.

`CarpiNova-PC` is a consumer. It must never become a second source of truth for carpentry knowledge.

## The four master laws

These four laws apply to every product, code, documentation and design change.

### 1. KISS — smallest correct path

Apply this order:

`CORRECTO -> SIMPLE -> EFICIENTE -> OPTIMIZADO -> EFICAZ -> ESTABLE -> MANTENIBLE -> RAPIDO -> ESCALAR SOLO SI HACE FALTA`

Prefer `A -> B`. Do not add backend, database, auth, plugin systems, parallel renderers, generic UI frameworks, state frameworks, AI/vector infrastructure, extra build systems or abstraction layers for hypothetical future needs.

Use the existing React/Vite/TypeScript stack until a demonstrated requirement cannot be solved cleanly with it.

### 2. Anti-noise — keep only useful product truth

Evaluate changes in this order:

`DELETE? -> SIMPLIFY? -> REUSE? -> MERGE? -> OPTIMIZE? -> EXTEND? -> ADD?`

Do not accumulate duplicate docs, copied Knowledge, temporary workflows, stale branches, verification diaries, one-off UI components or compatibility code without a current consumer.

Deletion requires evidence: check references, tests, workflows, current consumers, rollback and unique forensic value. Git history is the default historical archive.

### 3. Anti-patch — root cause before fix

Use:

`OBSERVE -> REPRODUCE -> ISOLATE -> ROOT CAUSE -> REAL RED -> MINIMAL FIX -> REMOVE OBSOLETE WORKAROUND -> GREEN -> REGRESSION -> REAL CONSUMER`

Do not stack CSS exceptions, source-specific branches, compatibility hacks, duplicated canonical data, fallbacks or test exceptions merely to force green.

If a UI or data problem needs repeated local exceptions, stop and find the shared cause.

### 4. Design law — clear, consistent, accessible, faithful to the approved mockup

Apply this order:

`APPROVED MOCKUP -> DESIGN TOKENS -> HIERARCHY -> COMPONENTS -> STATES -> RESPONSIVE -> ACCESSIBILITY -> POLISH`

A visual improvement does **not** authorize a new architecture.

The approved CarpiNova direction is:

- clear, warm and practical woodworking interface;
- neutral/light surfaces with wood-inspired accenting;
- technical/visual workspace is the protagonist, not dashboard chrome;
- simple navigation and a contextual information panel;
- target workspace concepts include views such as **Vistas**, **Despiece**, **Medidas** and **Instrucciones** when their product capability is actually implemented;
- large, comfortable controls suitable for tablet/touch use;
- avoid ERP/dashboard/KPI aesthetics unless a real feature explicitly requires them;
- never fake CAD/3D, measurements or capabilities that the current product does not yet implement.

The public `nextlevelbuilder/ui-ux-pro-max-skill` project is an advisory design reference. Apply useful principles; do **not** vendor its CLI, datasets, search engine or architecture into CarpiNova.

## UI/UX design rules

Use these rules for every new or modified user-facing surface:

- Reuse design tokens before adding raw colors, radii, shadows, spacing or typography values.
- Keep body copy left-aligned by default; center only short content when the approved composition genuinely calls for it.
- Keep readable body text around a 16 px minimum at normal desktop/mobile zoom and approximately `1.5–1.7` line-height.
- Keep long reading lines roughly in the `45–75ch` range.
- Use a clear heading hierarchy; responsive headings should scale without dominating the workspace.
- Normal text/background contrast must target WCAG AA (`4.5:1`); visible keyboard focus is required.
- Essential touch/click targets should be approximately `44x44 px` or larger, with enough separation to avoid accidental activation.
- Every form control needs a real accessible label; semantic HTML comes before ARIA patches.
- Keyboard access must work for essential actions. Do not remove focus outlines without an equivalent visible focus state.
- Responsive behavior must be checked at approximately `1440`, `768` and `390` px and remain fluid between them; no horizontal overflow in normal content.
- Test long Spanish labels/text, not only short synthetic strings. Wrapping must not break layout or hide actions.
- Prefer CSS/SVG/native controls over decorative icon packages or emoji-based interface icons.
- Avoid decorative motion. If motion is later introduced, it must respect reduced-motion preferences.
- Loading, empty, error, disabled, selected, hover and focus states must remain visually understandable.

Do not refactor stable existing UI merely to satisfy stylistic purity. Improve touched surfaces and shared root causes incrementally.

## Consumer boundaries

- Consume generated Knowledge; do not copy canonical carpentry content into PC source code.
- `generated/knowledge/` is reproducible output and must not be hand-edited or committed as source truth.
- Prepare Knowledge through `npm run knowledge:prepare`.
- Keep loading and references fail-closed. Missing/invalid required records must not be silently fabricated.
- Preserve source provenance wherever the current product exposes it.
- Render only figures that explicitly opt into `reconstruction.render_contract = normalized-2d-v1`.
- Current normalized primitives are `rect`, `line` and `polyline` plus canonical annotations/layers.
- Do not add a second renderer or new primitive merely for one figure. New renderer/schema capability belongs first in Knowledge.

## Default delivery flow

Routine PC work follows:

`OBJECTIVE/MOCKUP CHECK -> RED WHEN BEHAVIOR CHANGES -> MINIMAL GREEN -> PC QA -> REAL KNOWLEDGE PROOF IF RELEVANT -> PR/MERGE -> SMOKE`

Routine Knowledge consumer verification uses the permanent `.github/workflows/knowledge-consumer-proof.yml` workflow with **exact commit SHAs** for both repositories. Do not create a temporary workflow/branch/PR per figure unless the permanent path cannot prove a genuinely new architectural condition.

One PR means one cohesive cause. Do not mix unrelated product, governance and cleanup changes.

## Ten-pass audit

Before implementation/merge, run these ten passes and record only material findings:

1. **Identity** — repo, exact `main`, branch/PR head and intended Knowledge SHA.
2. **Objective** — one cohesive user/product cause.
3. **Canonical input** — Knowledge version, source identity and references.
4. **Contract fit** — existing consumer/render/interaction contract or explicit need to extend Knowledge first.
5. **KISS** — smallest component/state/data path; no unnecessary dependency/architecture.
6. **Anti-noise** — no duplicate truth, temporary residue or unrelated files.
7. **Anti-patch** — root cause rather than CSS/data/test exception stacking.
8. **Design** — approved mockup direction, tokens, hierarchy, states, responsive and accessibility.
9. **QA/consumer** — tests, typecheck, build, audit when relevant, exact real-bundle proof.
10. **Governance/continuity** — fresh compare/CI/reviews/mergeability, exact merge state and recoverable live checkpoint.

## Required verification

For normal PC changes:

```bash
npm ci
npm test
npm run typecheck
npm run build
```

For changes affected by Knowledge consumption, figures, lessons or interactions, also prove the intended exact Knowledge + PC commits through the permanent consumer-proof workflow. That proof prepares the real bundle, runs PC QA/audit and verifies that Vite's production build contains the exact generated bundle.

Synthetic fixtures alone are insufficient for the final real-Knowledge gate; page-specific duplicate consumer assertions are also unnecessary when canonical Knowledge tests already own those semantics.

## Documentation and continuity without noise

Use each surface for one purpose:

- `AGENTS.md`: durable laws and operating/design rules.
- `README.md`: stable architecture, commands, product direction and recovery path.
- GitHub issue/PR: current work, exact SHAs, decisions, checkpoint and blockers.
- Git history: routine historical execution.
- dedicated docs: only unique long-lived product/release decisions.

Do not copy the same spec/plan/checkpoint into both Knowledge and PC. Do not commit chat handoffs or local verification diaries as routine state.

If a chat ends, the next session must be able to recover the current state from live GitHub alone.

## Branch and compatibility hygiene

- Keep only active branches plus branches with demonstrated rollback/forensic value.
- After merge/closure, audit obsolete branches and delete only when their work is safely represented by `main`/Git history.
- Compatibility with old Knowledge versions must have a current reason. Before removing compatibility, prove that no supported consumer still requires it; before keeping it indefinitely, document the active need.
- Never force `main`.

## Stop conditions

Stop and re-audit rather than improvising when:

- the requested behavior would duplicate or reinterpret canonical Knowledge;
- source-faithful support requires a new Knowledge schema/render contract;
- required Knowledge references do not validate;
- the approved mockup and requested UI behavior materially conflict;
- a design fix would require repeated local exceptions instead of a shared root fix;
- exact-head CI is red for an unexplained product reason;
- `main` moved and the relevant delta is unknown;
- overlapping agent/Codex work cannot be reconciled;
- a merge would rely on stale/synthetic evidence;
- compatibility removal or a new dependency lacks explicit evidence.

Evidence controls execution. Complexity is never a substitute for certainty.
