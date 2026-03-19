# Design Decisions

Records why the current version is shaped the way it is. Each entry captures the decision, what alternatives were considered, and what evidence drove the choice.

---

## D01: Change Spec as a first-class output mode (not a sub-type of Full Spec)

**Decision**: Change Spec is a separate output mode with its own template, conventions, and review checklist items — not a variant of Full Spec with extra fields.

**Why**: Modifying existing documents has fundamentally different precision requirements than creating new ones. In a new spec, execution quality depends on the output contract (how clearly the deliverable is defined). In a change spec, execution quality depends on anchor precision (how exactly each modification point is located). Treating change specs as "full specs with an extra section" would bury this distinction.

**Evidence**: Seven change specs were executed against four real documents (35+ modifications). Anchor quality was the single biggest factor in execution speed and accuracy. When anchors were precise (two-endpoint), execution was instant. The only friction came from format mismatches (trailing whitespace), not from content ambiguity.

---

## D02: SKILL.md architecture — independent sections + Process references (scheme 3)

**Decision**: Task Decomposition and Change Spec Conventions are independent top-level sections in SKILL.md. Process steps reference them but don't duplicate their content.

**Alternatives considered**:
- Scheme 1 (independent sections only): Conventions exist as standalone sections, Process doesn't mention them. Problem: agent executors read Process sequentially and wouldn't encounter the conventions unless they knew to look.
- Scheme 2 (pure inline): All convention content lives inside Process steps. Problem: Process becomes very long; reviewers can't find or reference specific rules without reading the whole flow.
- Scheme 3 (chosen): Process steps contain the core judgment ("check anchors per §Change Spec Conventions"), independent sections contain the full rules. Both sequential readers and reference-seekers are served.

**Why scheme 3 won**: The primary user is an agent, which reads sequentially — so Process must mention the checkpoints. But conventions will grow over time, and cramming them into Process steps creates a maintenance problem. Independent sections can grow without making Process unreadable.

**Trigger for revisiting**: If SKILL.md exceeds ~300 lines, consider whether the independent sections should move to `references/` with only links in SKILL.md.

---

## D03: INSERT BEFORE / INSERT AFTER instead of bare INSERT

**Decision**: Operation types for change specs require explicit direction. "INSERT" alone is not permitted.

**Why**: During execution of seven change specs, every INSERT operation required the executor to infer direction from the anchor description. When the anchor said "after X, before Y", direction was unambiguous. But when it said "at location X", the executor had to guess whether content goes before or after X. Requiring INSERT BEFORE or INSERT AFTER eliminates this ambiguity at spec-writing time rather than execution time.

**Evidence**: Executor feedback explicitly recommended "统一约定一个方向，或者在每条改动中显式标注前面/后面" (standardize a direction convention or explicitly label before/after in each change).

---

## D04: Complete replacement over incremental patching — structural change as the threshold

**Decision**: When a modification changes the structure of content (list nesting, table columns, paragraph organization), provide the complete final version. When it only adds/changes individual elements within an unchanged structure, incremental instructions are acceptable.

**Alternatives considered**:
- Always use complete replacement: safe but wastes tokens on trivial changes (e.g., appending one row to a 20-row table).
- Always use incremental instructions: compact but error-prone when structure changes (executor must mentally reconstruct the final state).
- Threshold by line count (e.g., "if changing >50% of lines, use complete replacement"): arbitrary and hard to judge.

**Why structural change is the right threshold**: The executor's failure mode is not "too many changes" but "can't see the final shape". Adding one item to a flat list is trivial to imagine. Changing a flat list into a nested list is not — even if only 3 of 20 items changed, the nesting structure affects all items. The distinction is cognitive, not quantitative.

**Evidence**: BP-06 (5-item flat list → 12-item nested list) required complete replacement and worked perfectly. A-05b (append one item to existing list) worked with incremental instruction. D-02 (change 2 rows in a table without structural change) worked with targeted replacement.

---

## D05: Temporary numbering with dedicated renumbering phase

**Decision**: When inserting new sections into a numbered sequence across multiple phases, use temporary identifiers (e.g., §4.4a, §4.4b) during insertion phases. A dedicated renumbering phase replaces all temporary identifiers with final numbers.

**Why**: Guessing final numbers during an insertion phase creates a dependency on all other insertions being complete — which contradicts the goal of independently verifiable phases. Temporary identifiers isolate each phase's changes from numbering decisions.

**Evidence**: Core Spec modification used this pattern (Phase B inserted §4.4a–d and §4.5a–b; Phase C renumbered to §4.5–§4.10). Zero numbering conflicts. Phase C's evaluation checklist ("search for 4.4a, confirm zero matches") provided a clean verification step.

---

## D06: Executor TBD as a supported pattern

**Decision**: Specs can be written with "Executor: TBD". When TBD, write for the most constrained plausible executor (generalist LLM agent with no prior context).

**Why**: In practice, specs are often written before the executor is assigned. Requiring a known executor at writing time either blocks spec creation or forces the author to guess. Writing for the most constrained executor produces the most portable spec — a human can always skip detail that an agent needs, but an agent can't fill in context that was assumed but unstated.

---

## D07: Execution environment warnings in both Process and template

**Decision**: The warning about trailing whitespace and formatting artifacts appears in two places — Process step 10 (reminding the spec author to include it) and the change-spec-template Failure Handling section (where the executor will actually see it).

**Why**: Two different readers need the same information. The spec author needs to remember to include the warning. The spec executor needs to see the warning when they encounter matching failures. Putting it in only one place means one reader misses it.

**Evidence**: During execution of seven change specs, trailing whitespace was the single largest source of debugging friction. It caused the first str_replace attempt on the Blueprint to fail, requiring a fallback to line-based replacement. One sentence of warning would have saved ~30% of debugging time.

---

## D08: Two-window parallel iteration as validation method

**Decision**: The v2.0 iteration was done by two independent instances (Clé A: design side, Clé B: execution side) working from the same feedback, then merging.

**Why this matters for the skill itself**: The convergent conclusions (both instances independently arrived at the same four iteration items) have higher confidence than either instance's conclusions alone. The divergent conclusions (architecture choices, checklist items) revealed genuine design trade-offs that required human judgment to resolve. This pattern — independent iteration then structured merge — is itself a form of the spec discipline being applied to its own evolution.

**What converged** (high confidence): Change Spec as new mode, phase splitting, executor TBD, execution environment warnings, two-endpoint anchors, operation type labeling, cross-file reference timing.

**What diverged** (required judgment): SKILL.md architecture (scheme 1 vs 2 vs 3), checklist item granularity (6 vs 9 items), whether to include a worked example, where to place the "complete replacement" rule.
