# RC3 — APPEND-ONLY REGISTRATION ADDENDUM: GitHub Anchor

**Addendum to:** `RC3_ENGINEERING_BASELINE_REGISTRATION_2026-11-02.md` (Tasklet documentary registration)  
**Recorded:** 2026-11-02 (session timestamp 13:44 -07:00)  
**Prepared by:** Kimi (independent verifier), per Order 03 instructions for the registration record  
**Nature:** APPEND-ONLY. This addendum adds an external custody reference. It does not modify RC3, any original freeze document, or the prior registration. No new freeze approval is granted or implied.

## GitHub archival anchor (Order 02 — COMPLETE)

- **Repository:** https://github.com/eit-orbitos/nova-q-eit-riemann
- **Commit:** `91a582b3c2fb1a8abe72fca8943af58ccef9b6b0`
- **Commit message:** "Archive RC3 engineering freeze evidence — 2026-11-02"
- **Commit timestamp:** 2026-11-02T20:42:34Z (server-side committer time; author offset -06:00)
- **Contents:** adds exactly the three original freeze documents, byte-identical in content to the verified originals:
  1. `NOVA_Q_EIT_RIEMANN_V0_8_2_RC3_ENGINEERING_FREEZE_RECEIPT.md`
  2. `NOVA_Q_EIT_RIEMANN_V0_8_2_RC3_FREEZE_STATUS.json`
  3. `NOVA_Q_EIT_RIEMANN_RC3_EXTERNAL_SHA256_ANCHOR.txt`

## Independent verification performed (Kimi, Order 03 step 1–2)

- Commit exists at the stated repository; full SHA matches.
- Repository is public; commit retrieved via the GitHub API and the HTML commit page independently.
- All three archived files carry the same RC3 digest `ea09917e090306bc4a2df58758fe0a29c6a90b7365384981094c5ec847a95414` — **matches the frozen baseline** (and matches the ZIP bytes verified directly in Order 01).
- Archived receipt content is identical to the original freeze receipt (same decision text, exclusions block, authorization form, and custody statements). Archived status JSON is valid JSON with identical research flags.

## Status change: external-anchor limitation

- **Before:** L-1 / external-anchor limitation — the standalone digest file was external to the ZIP but held only in conversation attachments; no user-controlled repository record existed.
- **Now:** the freeze evidence (including the RC3 digest) has a **user-controlled, public, versioned GitHub repository reference** at the commit above. The previous external-anchor limitation is recorded as **MITIGATED — GitHub-hosted reference exists**.
- **Not claimed:** this is not an author-signed archive (the commit's "verified" flag is GitHub's own web-flow key, not the author's personal signature) and not an independently timestamp-certified record (no trusted timestamp authority; the timestamp is GitHub server-side). No archival DOI exists.

## Preserved invariants (unchanged)

```
RC3_ENGINEERING_BASELINE = FROZEN
F1 = NOT_TESTED
F2 = FAIL_FOR_PHI_LOG_X
EIT_ACTIVATION_VALIDATED = NO
RH_PROVEN = NO
V0_9 = HOLD
```

The frozen ZIP itself is not archived in the repository (its exact bytes remain the declared artifact, hash-identified); only the freeze evidence and digest record are. Any future successor requires a new separately named candidate, hash, and review.
