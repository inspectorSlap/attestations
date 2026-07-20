# Public attestation chain — Rupert email-drafter case study

This repository publishes a **hashes-only, externally timestamped** evidentiary chain for artifacts that live in a private repository. It converts "we sealed this on date X" from an assertion into a fact a stranger can verify — **without** disclosing the artifacts themselves.

- **What a hash proves:** the artifact existed, byte-for-byte, at the timestamped moment. A hash is a *commitment*, not a disclosure.
- **What this repo does not do:** it does not let anyone read the artifacts. Reproducibility of the *method* is carried by the public synthetic corpus; this chain carries the *ecological validity* of one real production case, attested.

## Layout

```
README.md        ← this file
METHOD.md        ← the exact, frozen hashing method (normative)
APPARATUS-SPEC.md← the Tier-A apparatus triple (config only; no rubric text)
INDEX.md         ← the attested objects: primary commitments first, then bundle seals
objects/
  <id>.hash      ← one line: the 64-char sha256 for that object
  <id>.hash.ots  ← OpenTimestamps proof (added at attestation time)
```

## How to verify (see METHOD.md §D for detail)

1. Obtain the artifact (or its exact byte source) under NDA.
2. Recompute its hash with the method in `METHOD.md` (directory recipe for seals; `shasum -a 256 <bytes>` for primary commitments).
3. Confirm it matches the value in `INDEX.md`.
4. `ots verify objects/<id>.hash.ots` confirms the hash existed at the attested time.

## ⭐ If you only check three things

Check the **primary commitments** at the top of `INDEX.md` — the scoring instruments and the pre-registrations. Those are the load-bearing anti-HARKing anchors (a pre-registration timestamped *before* its result is what rules out fishing). The bundle object seals below them are secondary tamper-evidence.

## Two date grades (read this)

`INDEX.md` carries two dates per object, with two different epistemic strengths — the same captured-vs-reconstructed discipline the case study itself runs on, applied to dates:

- **attested existence-by** — the OpenTimestamps proof. This is *proven*: the artifact existed, byte-for-byte, by that moment. It does **not** prove the artifact's *original creation* date.
- **claimed creation** — the earliest commit touching the object in the private repository. This is *unverified in this public chain*, but **checkable under NDA** against the historical tree (`METHOD.md §C`). It is stated deliberately: silence on chronology is more corrosive to the anti-HARKing claim than an explicitly-labeled unverified date.

These commitments were attested in a single initial pass, so their **existence-by** dates cluster at the first stamp. That is why the **claimed creation** column matters — it is where the pre-registration-precedes-result chronology lives (checkable under NDA). Objects attested from here forward carry a real, forward-looking existence-by timestamp.

The hashes here were **recomputed** under the current method from the private repository; an earlier internal convenience seal used a different method and is not published. This is disclosed deliberately (`METHOD.md §C`).

## When this publishes

This chain's entire value is the timestamp, and every day of delay pushes the existence-by bound later — most importantly for the pre-registrations, which most need an early bound. The chain discloses nothing (hashes; mechanism-free descriptions; config-only apparatus triple), so there is no reason to hold it. It is published ahead of, and independently of, any writeup.

## Timestamping

Each object hash is anchored with [OpenTimestamps](https://opentimestamps.org) (Bitcoin). `ots stamp` sends only a hash to the calendar servers — **no file content leaves the machine**. An un-upgraded `.ots` is a pending claim; `ots upgrade` promotes it to a completed proof once confirmed in a block.
