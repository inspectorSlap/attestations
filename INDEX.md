# Attestation INDEX — Rupert email-drafter case study

> Hashes-only, externally timestamped commitments. A hash is a *commitment*, not a disclosure.
> See `METHOD.md` for the exact hashing method and `README.md` for how to verify.

**Two date columns, two epistemic grades** (captured-vs-reconstructed discipline, applied to dates):

- **attested existence-by** — the OpenTimestamps proof. *Proven.* (Filled when `ots stamp` runs.)
- **claimed creation** — earliest private-repo commit touching the object. *Unverified here; checkable under NDA against the historical tree* (METHOD §C). Stated because silence on chronology is more corrosive to the anti-HARKing claim than an explicitly-labeled unverified date.

## ⭐ Primary commitments — check these first

The load-bearing anti-HARKing anchors: content-hashes of exact bytes. **Note the chronology:** `rup-es-prereg-primary` (claimed 2026-07-16) precedes its results `rup-es-postfix-eval-01` (claimed 2026-07-18) — the pre-registration was committed before the result existed, checkable under NDA.

| attested existence-by | claimed creation (NDA-checkable) | object id | object hash (sha256) | what was committed |
|---|---|---|---|---|
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-instrument` | `0d64c804ae65a80b8123ccc4b736522c5aa00d4a4fdc3d09f5e19845398a1358` | the frozen production scoring instrument — the one both Stage-4 arms were scored under (the one-variable claim) — hash only; text held |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-incident-draft` | `ac89e498d332d70e48e4544ce1e32611f5b18c05ba01657e0d5e6f8e3ff56020` | the exact model-emitted client-facing draft at the incident (the failing output under study) — hash only; content held |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-prereg-primary` | `a37fa376de482ecdaeaffe0a410b6da306be039ca898971535084f3342cc36ae` | the primary pre-registration: direction + a hash-anchored target committed BEFORE the fix existed (the load-bearing anti-HARKing anchor) |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-prereg-prospective` | `8bea41ffdccb22eb490f3e66c7b1e76266e1eb94c3c711894636ca3a0d37999c` | prospective-observation pre-registration: predicted a real-time catch on the fixed locus BEFORE the observation window |
| ⏳ set at `ots stamp` | 2026-07-19 | `rup-es-prereg-characterization` | `631f22b913c6718fcfa74221ff4c9774324935aab4cf03d74a234a5bff6c51b6` | email-drafter study · instrument-characterization pre-registration: selection rule, statistics and outcome-meanings committed BEFORE any measurement call — **contemporaneous, not backfill** (predicted direction held) |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-prereg-revision` | `6623e6df9c72447d3ef01460e3aa32ba9244197024293727fb3516990a03fc52` | email-drafter study · apparatus revision · pre-registration: a direction committed before the re-scoring run (the direction itself held) |

## Bundle object seals (secondary — tamper-evidence)

| attested existence-by | claimed creation (NDA-checkable) | object id | object hash (sha256) | contents (mechanism-free) |
|---|---|---|---|---|
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-incident-01` | `e3deb1973aa2260952af1a4457cbde651f723cd250772441d7255d5343692dee` | captured production-incident state: the sealed failing event + its substrate, frozen before any fix |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-retrieval-01` | `1214031077e4123f2d6307e752ec44058ddaa4998e11a8ceba5fc0c6cdb40423` | reconstruction of the retrieval neighbourhood that conditioned the failing output (method disclosed; values reconstructed, second-grade) |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-detection-01` | `7a8c2b27a9b31f983ffeae097fcaf7bd7037e2f3d0def0e1042161833d12731a` | post-incident detection audit: whether the frozen instrument flags the frozen failure |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-prefix-eval-01` | `bc5409ea73c7fe814e38d4457d169b44f8e96704666b6eed593738107adcf360` | pre-fix evaluation results bundle (contains the primary pre-registration, attested separately) |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-prefix-eval-02` | `9243033aedfaee3002843ae0a768da38c09ce4234ad535a8153f4c635027439a` | a further evaluation pass over the frozen pre-fix events |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-migration-01` | `e84233988f107d933acc5671fd08cdaf7aa9e45adcdbe1b375d685ab39e3fbe5` | the fix: the one code change under test, dated AFTER the pre-registration |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-postfix-eval-01` | `363cabb88322337d498be99bf758b5ce3ae716c7d1100ead8b0d036a35457856` | post-fix interventional battery: the confirmation run with one variable changed |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-lockdown-01` | `4243f6b7f7c9b7f34cac6bf47f153eb4ce93e860ca453b63f9eb3af7c17b838a` | regression lock: a fixture that fails the build if the fixed behaviour regresses |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-prospective-01` | `f4cbfef71d32122e87cde518b8559d2922a38b455af8d0031c9f8ec59d29dade` | a prospective observation: a registered prediction, the observed catch, and an honest false-positive |
| ⏳ set at `ots stamp` | 2026-07-18 | `rup-es-harness-01` | `4d881c1cc491e64db45898acf67bf7bcc9fcddb408eaa42a6ceae325daa59f2e` | the evaluation harness scripts (assert the instrument hash before running; reproduce the results) — Tier B: scripts embed held rubric text |
| ⏳ set at `ots stamp` | 2026-07-16 | `rup-es-narrative-01` | `cd1cbb5d540f9d2895485cd6f937572028ede18d018085a66aba6bae57975050` | case-study write-up (living-narrative snapshot at prep date; NOT a frozen anchor) |

_The **claimed creation** dates are unverified in the public chain by construction — the OTS proof only bounds existence-**by** the stamp date. Checkable under NDA against the private repo's commit history (METHOD §C)._

## Apparatus versions (append-only note)

The published apparatus triple (`APPARATUS-SPEC.md`, identified by rubric hash `0d64c804…`) is the instrument both Stage-4 arms ran under, which is all the one-variable claim requires. **Additional instrument versions exist, are attested internally, and publish post-filing.** This chain is append-only, so completing the record later is trivially clean — deferral, not concealment. The evolution across versions is held pending filing; it adds nothing to the one-variable claim.

## Served-model capture (time-bounded limit)

The apparatus triple publishes the judge's served build id (not only the alias). For these sealed runs the served id was captured at the **run** level, so an intra-run reroute is not independently excludable per event (`APPARATUS-SPEC.md`). This is a property of *when* these runs happened: objects attested from here forward carry **per-event** served ids, so the limitation is bounded in time, not permanent.
