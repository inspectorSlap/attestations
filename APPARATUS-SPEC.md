# APPARATUS SPECIFICATION — Tier-A triple

A scoring instrument is under-specified by its rubric hash alone: the same rubric with a different input-scoping, or served by a different model build, is a different lens. The **apparatus** is therefore **(rubric hash, context-scope descriptor, judge model — alias *and* served id — + temperature)**.

This spec discloses **no rubric criteria** — only configuration — so it publishes as **Tier A** (in the clear) while the rubric *text* stays held (Tier B, hash only). Its value: it lets a reader **verify**, rather than take on prose faith, that two evaluation runs executed under an *identical* apparatus. That is exactly what the one-variable claim depends on.

---

## Published — the one-variable apparatus

The Stage-4 confirmation compares pre-fix vs post-fix drafts scored under a single, identical apparatus. It is identified by its rubric hash (not a version label):

```
frozen scoring apparatus (this study):
  rubric:        0d64c804ae65a80b8123ccc4b736522c5aa00d4a4fdc3d09f5e19845398a1358
  context-scope: ticket_status + draft
  judge (alias): claude-haiku-4-5
  judge (served): claude-haiku-4-5-20251001     ← the resolved build; see note
  temperature:   0
```

A reviewer confirms the pre/post scores ran under the same instrument by checking that both Stage-4 arms (`rup-es-postfix-eval-01`) carry this exact triple (same rubric hash, scope, judge, and temperature).

**Why the served id is here, not just the alias — and its honest limit.** `claude-haiku-4-5` is an *alias*; the vendor can reroute an alias to a different build. If it had rerouted *between* the pre-fix and post-fix runs, the apparatus would not have been identical and the one-variable claim would fail — while an alias-only triple stayed constant and showed nothing. That is precisely the silent-reroute failure the light axis exists to catch, and it must not sit unaddressed inside the spec that certifies apparatus constancy. The Stage-4 battery **captured the served id** at run level: `servedJudge = claude-haiku-4-5-20251001` (and `servedDrafter = claude-sonnet-4-5-20250929`), a single value for the run that generated and scored both arms together. **Limit:** served-model was captured at the *run* level, not first-class *per event*, for these runs (the per-event `light.servedModel` capture is a later, still-landing change). So an intra-run reroute cannot be *independently* excluded per event; the run-level served capture is consistent and is the strongest constancy evidence available for these sealed runs. Stated plainly rather than papered over.

_(The surface under test — the drafter — was held constant across arms at alias `claude-sonnet-4-5` / served `claude-sonnet-4-5-20250929`, temperature 1.0, K=3 samples/input/arm. A property of the treated system, not the apparatus; recorded for completeness.)_

---

## Held pending filing — other instrument versions

Other instrument versions exist and are **attested internally**; their apparatus triples **publish post-filing** (the chain is append-only). They are held now because the *comparison across versions* — what differs between them and why one followed another — is held analysis, and the published v2 triple already makes the one-variable claim checkable without it. The others add nothing to that claim, so the caution costs it nothing. **Deferred, not forgone** — the append-only chain completes the record cleanly after filing.
