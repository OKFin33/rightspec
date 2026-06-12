# Worked examples

## Example 1 — a partitioned spec (Spec mode)

Task: "Have an agent review a PR diff and post the top issues as a summary."

**Partition.** The inputs (the diff, the repo) and the output's shape are structurable; "what
counts as a *top* issue" is the judgment core.

Structured envelope:

```yaml
executor: generalist coding agent; tools: [read_files, git_diff]
inputs:
  diff: required          # the PR diff
  repo_path: required
  if_missing: halt and report
output:
  type: list
  max_items: 5
  item: { issue: string, severity: enum[blocker, major, minor], file: string, line: int }
  format: markdown table, sorted by severity
scope: correctness and clear bugs
non_goals: style nits, formatting, architecture opinions
```

Judgment core (prose — the only part that needs an LLM):

> A "top issue" is something that would break behavior or mislead a reader, not a preference.
> **Good:** "null deref when `config` is absent (auth.py:42)" — concrete, breaks behavior.
> **Bad:** "this function feels long" — preference, no consequence. If two issues tie on severity,
> prefer the one affecting more call sites. If the diff is too large to review fully, review the
> highest-churn files and say so rather than guessing.

Everything mechanical is a contract; the LLM is asked only to judge "is this a real issue."

## Example 2 — a structured change spec (Change Spec mode)

Task: add a governance subsection and replace a mapping list in `Design_Guidelines.md`.

```yaml
- id: DG-01
  location: "§3.4 Layer Interactions, after §3.4.6"
  anchor:
    after: "#### 3.4.6 System roles can override runtime logic but must not absorb identity"
    before: "---"          # the separator before §3.5
  op: INSERT AFTER
  content: |
    #### 3.4.7 Document governance constrains all layers' self-modification

    When an agent modifies its own documents at runtime, it must follow the update rules in
    GOVERNANCE.md ...

- id: DG-02
  location: "§3.6 How layers map to files"
  anchor:
    after: "## 3.6 How layers map to files"
    before: "## 3.7"
  op: REPLACE              # structural change → complete final block, not incremental edits
  content: |
    - **Constitutional layer** maps to `SOUL.md`
    - **Runtime layer** maps to multiple files:
      - `AGENTS.md`: launcher
      - `GOVERNANCE.md`: document update governance (read on demand)
    - **Experience layer** maps to `MEMORY.md + memory/`
```

Prose residue (thin): "DG-02 changes the list structure, so the complete final list is given, not
edits." Failure handling: anchor-not-found → mark and skip; format mismatch → match the target's
bullet style.

## Example 3 — the gate fires (no spec at all)

Request: "Write a spec for an agent to rename every `.jpeg` to `.jpg` in a folder and patch the
references in `index.md`."

Partition: inputs → structure, operation → deterministic, output → checkable. Catalog B is
**empty** — no open-ended judgment anywhere. The right output is **not a spec**: "this is a
function — write a ten-line script, call it deterministically, don't put an LLM in the loop." See
`partition.md` → "the gate".
