# METHOD — the exact, frozen hashing method

This file is **normative**. Every hash in `INDEX.md` was produced exactly as described here. Do not change this file; if the method ever changes, publish a new dated method file and never re-issue an existing hash under a new method.

There are **two kinds of attested object** in this chain, hashed two different ways. Read both.

---

## A. Object seals — sha256 of a directory (bundle tamper-evidence)

**Object hash = sha256 of a manifest of per-file sha256s, byte-wise sorted.** Run from the object's root:

```bash
cd <object-root>
find . -type f \
     ! -name 'MANIFEST.sha256' \
     ! -name '.DS_Store' \
     ! -path './.git/*' \
     -print0 \
  | LC_ALL=C sort -z \
  | xargs -0 shasum -a 256 \
  > MANIFEST.sha256          # or: sha256sum (GNU)

# the object hash:
shasum -a 256 MANIFEST.sha256 | cut -d' ' -f1
```

Reproducibility rules (all load-bearing):

- `LC_ALL=C` forces byte-order sort. Locale-dependent sorting silently changes the manifest and therefore the object hash.
- `-print0` / `-z` / `-0` handle spaces and unicode in filenames.
- Paths are **relative, prefixed `./`**, produced by running `find` from the object root. Running from anywhere else changes the paths and the hash.
- **Exclusion set (frozen): `MANIFEST.sha256`, `.DS_Store`, `.git/`.** `.DS_Store` is macOS filesystem metadata, not an artifact; it is machine-specific and would break cross-machine verification, so it is excluded by the method (and not present in any object). `MANIFEST.sha256` excludes itself.
- No trailing-newline normalization, no CRLF conversion. Hash the bytes on disk.
- Line format is `shasum -a 256`'s: `<64-hex-lowercase><SPACE><SPACE><./path>` + `\n` per line. GNU `sha256sum` produces the identical format. The manifest file ends with a newline.
- **Object dirs are kept pristine.** The `MANIFEST.sha256` is stored centrally (in the private prep tree), not written into the object dir. Because the method *excludes* `MANIFEST.sha256`, this makes no difference to the hash: a verifier regenerates the manifest in place and compares.

**Two synthetic objects** (`rup-es-harness-01`, `rup-es-narrative-01`) are rooted at the bundle directory over an explicit file allowlist rather than a whole subtree, because their files live at the bundle root alongside other objects. Their allowlists:

- `rup-es-harness-01`: `./stage0-freeze.cjs ./stage0b-reconstruct.cjs ./stage2-eval-prefix.cjs ./stage4-adjudicate.cjs ./stage4-battery.cjs ./stage5-fixture.cjs`
- `rup-es-narrative-01`: `./BEFORE-AFTER.md ./CLIENT-SPECIFICITY.md ./DEPLOYMENT-STATE.md ./README.md ./TICKET-STATE-RUBRIC-SPEC.md`

Everything else about their manifest (sort, format, sha) is identical.

---

## B. Primary commitments — sha256 of exact bytes (the anti-HARKing anchors)

The load-bearing commitments are **not** directory manifests. A directory manifest is tamper-evidence for a bundle; a **content-hash of exact bytes** is what proves a *specific artifact* — a scoring instrument, the frozen incident output, a pre-registration — was fixed before the result it governs existed. These get individual attestation and individual OTS proofs, and they are listed first in `INDEX.md`.

**Three byte-source rules, and the exact source must be pinned — a verifier who hashes the wrong artifact gets a mismatch and wrongly concludes fabrication. The rubric text and the draft content are held; these anchors are verified under NDA, where the exact per-object byte source is given in the private map. The rules and the decoy traps are stated here so the method is auditable.**

### B1. Scoring instruments (rubrics) — the *resolved judge system string*, NOT a file

The hashed object is **the exact UTF-8 bytes of the rubric text as passed to the judge model's `system` parameter** — no documentation header/footer, and **no trailing newline**. It is *not* any `.txt` file as stored on disk.

| id | sha256 | length | byte source |
|---|---|---|---|
| `rup-es-instrument` | `0d64c804…1358` | 1857 | the rubric string fed to the judge's `system` parameter (held; exact location in the private map) |

**Decoy trap (stated because it is the failure this method exists to prevent):** a companion documentation `.txt` wrapper of the rubric hashes *differently* — `sha256(that file)` = `48e0af2c…`, **not** the anchor — because it carries a `# sha256:` / `# FROZEN` footer. Hash the **resolved system string**, not the wrapper. (The judge's own context-scope finding — that the *resolved* prompt determines behavior — is why the resolved text is the correct object.)

### B2. Frozen incident output — the model-emitted draft in the sealed event

| id | sha256 | length | byte source |
|---|---|---|---|
| `rup-es-incident-draft` | `ac89e498…6020` | 135 | `event.json` → `light.rawResponse.content[0].text` (the exact model output as sealed) |

**Decoy trap:** `sha256(output.txt)` = `ef8bc498…` — **not** the anchor. `output.txt` is a wrapped convenience copy; the committed object is the model's raw output string inside the sealed event.

### B3. Pre-registrations — file-as-stored bytes

Pre-registrations are documents, not strings resolved through a system, so the object is the **file bytes exactly as stored**: `sha256(<file>)`.

| id | sha256 | file |
|---|---|---|
| `rup-es-prereg-primary` | `a37fa376…36ae` | the primary pre-registration document |
| `rup-es-prereg-prospective` | `8bea41ff…999c` | the prospective-observation pre-registration document |

_Additional primary commitments tied to later instrument versions are attested internally and publish post-filing (append-only); see `INDEX.md` "Apparatus versions."_

---

## C. Recompute honesty (read before trusting a backfilled hash)

The hashes in this chain were **recomputed** under this method from the private repo. The bundle carried an *earlier, internal* 8-character convenience seal (a hash of a hand-ordered `SHA256SUMS.txt`, produced a different way — e.g. `rup-es-lockdown-01` internal `9fc05891` vs canonical `4243f6b7…`). Those internal seals are **not** published and have **no cryptographic relationship** to these hashes.

This is disclosed so no one can claim the relationship was hidden. The recompute is **checkable in principle under NDA**: the private repository's commit history contains each object at its original commit, and a reviewer under NDA can regenerate the canonical hash against that historical tree and confirm it matches the published value. That converts "recomputed, trust us" into "recomputed, verifiable against history" — at no cost, because the history already exists. (See also the backfill-date limitation in `README.md`.)

---

## D. Verification (for anyone holding an artifact under NDA)

1. `cd` into the artifact's root (for a primary commitment, obtain the exact byte source named in §B).
2. Run the §A recipe (object seals) or `shasum -a 256 <bytes>` (primary commitments).
3. Confirm the result matches the value in `INDEX.md` (and, for primary commitments, the length in §B).
4. Run `ots verify <object>.ots` to confirm the hash existed at the attested time.

All three passing ⇒ the artifact is byte-identical to the one committed at that date.
