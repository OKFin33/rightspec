# Review checklist — audit a spec (or self-check before handoff)

Pointing rightspec at an existing spec to grade it runs this checklist. The same checklist is the
self-check before you hand off your own spec.

## Partition screen (start here — the rightspec-specific check)

1. Is everything structurable emitted **as structure** (schema / enum / threshold / table), not
   prose? Scan for prose smells: "usually", "about", "good quality", "if needed", "try to".
2. Is the prose limited to the **irreducible judgment core** (goal, taste, un-enumerated cases,
   dilemmas, escalation)? Any *rule* sitting in prose belongs in structure.
3. Did you run the **gate** — is there genuinely an LLM-needing residue, or is this a function that
   should be code / RPC instead?

If the spec is mostly prose, it usually failed to structure what it could — fix that first.

## Zero-context quick screen (five yes/no — any "no" blocks)

1. Can the executor finish without reading any prior conversation?
2. Are all terms a reasonable executor might read differently defined?
3. Are all required inputs listed, with missing-input handling?
4. Is every step driven by the spec, not unstated author intent?
5. Does the spec say what to do when things go wrong, not just the happy path?

## Detailed (mark ✔️ / ⚠️, comment on any ⚠️)

- **Structure & purpose** — title reflects function; purpose states the outcome; executor + tools defined.
- **Boundaries** — scope concrete; non-goals listed.
- **Clarity** — ambiguous terms defined; assumptions explicit.
- **Inputs** — all preconditions listed; missing-input behavior given.
- **Output contract** — deliverable shape exact (fields / format / order / thresholds); facts vs
  interpretation separable.
- **Internal consistency** — non-goals, workflow, assumptions, and output contract tell one coherent
  story; the output contract only asks for what the workflow produces.
- **Failure handling** — all three categories anticipated (external / judgement-dilemma /
  structural), each with recovery guidance.
- **Escalation** — triggers for asking / handing off / returning a partial result.
- **Evaluability** — success criteria checkable without guessing intent.

## Change Spec–specific (only when reviewing a change spec)

- **Anchor precision & uniqueness** — every edit located by two endpoints; duplicate anchor text disambiguated.
- **Operation clarity** — every op directional (INSERT BEFORE / AFTER, REPLACE, APPEND, DELETE).
- **Content completeness** — every REPLACE has full content; structural changes give the complete final block.
- **Dependencies & numbering** — series order explicit; temporary IDs documented with a renumbering phase.
- **Cross-reference integrity** — references use correct (post-change) numbering, or note otherwise.
- **Format awareness** — warns about trailing whitespace / formatting artefacts.
- **Residue check** — no temporary markers, old numbering, or edit notes remain in the final output.
