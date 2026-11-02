# NOVA Q / EIT — F1 V0.3 G0 Byte-Verification and G-01 Addendum

**Record date:** 2026-11-02  
**Classification:** append-only verification and author-approved methodological clarification  
**Status:** local original Markdown bytes VERIFIED; author G0 decision APPROVED; GitHub anchoring of this addendum PENDING  
**Research architect:** Toni Mladenovski

## 1. Referenced unchanged artifacts

| Artifact | SHA-256 | Status |
|---|---|---|
| `NOVA_Q_EIT_RIEMANN_F1_PROTOCOL_V0_3_CANDIDATE.md` | `118c9457120ae9c8c1e2e99f43d56bec06d51ad4177154058659c9ce18c2fca6` | SHA-256 independently computed from the uploaded bytes, MATCH to Kimi-declared value |
| `F1_G0_AUTHOR_DECISION_RECEIPT_V0_1.md` | `26a4b21a2ab60c4358a51ebe81944f4810a329f5422358e87a5a9b133438ca2e` | Separate original author-authorization record, preserved without edits |
| `NOVA_Q_EIT_RIEMANN_V0_8_2_RC3.zip` | `ea09917e090306bc4a2df58758fe0a29c6a90b7365384981094c5ec847a95414` | Frozen engineering baseline, read-only |

The original V0.3 header states `NOT FROZEN`, and the body states `G0 = PENDING_AUTHOR_APPROVAL`. These accurately describe the document *at its creation* and are not silently edited. The author's later G0 approval is recorded in the separate receipt. The receipt's earlier statement that V0.3 bytes were unavailable is historical; the new matching SHA-256 above supplies the missing byte-identity observation without rewriting the receipt.

**Limit:** this verification covers the original V0.3 Markdown file, not the full 14-file V0.3 ZIP or its internal `SHA256SUMS`. No cryptographic author signature or certified timestamp is asserted. The GitHub commit, if/when created, is an external hosted reference, not an independent attestation of scientific truth.

## 2. Approved G-01 clarification: B8 autonomous development selection

For model selection on development indices **15001–20000**, run **500 nonoverlapping rollouts of horizon 10**:

`origin(j) = 15001 + 10*j`, for integer `j = 0, ..., 499`.

At each origin, the permitted true zero ordinates end at index `origin - 1`. Predict indices `origin` through `origin + 9` without access to true ordinates within that rollout; for later steps, feed back the model's own prior predictions. True ordinates become available for the next rollout only as the protocol allows. For tuning and selection, compute NMAE across the union of all **5,000** development predictions. Choose model hyperparameters solely from this fixed development layout. No hold-out zero (`k > 20000`) may be used for B8 tuning.

This statement is the G-01 detail expressly approved in the G0 author decision. It is incorporated as a **prospective, separately cited interpretive addendum**; it is not claimed to appear in the hashed original protocol. If a reviewer considers this modification material, the combined effective protocol must be versioned and re-reviewed before A1.

## 3. Approved G-02 decision: beacon fail-closed

The author accepts the scheduled `drand quicknet` third-party availability dependency. If the scheduled beacon round cannot be obtained and cryptographically verified within the original protocol's 72-hour period, `B2 = BLOCKED`; selecting a replacement round or network requires a separately reviewed new version and author authorization.

## 4. Scientific and execution boundary

```text
G0_AUTHOR_DECISION       = APPROVED
G0_V0_3_MD_HASH          = VERIFIED
G0_APPEND_ONLY_RECORD    = PREPARED; GITHUB_COMMIT_PENDING
A1                      = NOT_AUTHORIZED
A2                      = NOT_AUTHORIZED
B1                      = NOT_AUTHORIZED
B2                      = NOT_AUTHORIZED
B3                      = NOT_AUTHORIZED
RC3_ENGINEERING_BASELINE= FROZEN
F1                      = NOT_TESTED
GUE_BASELINE            = NOT_BUILT
EIT_ACTIVATION_VALIDATED= NO
RH_PROVEN               = NO
P_VS_NP_PROVEN          = NO
V0_9                    = HOLD
```

Nothing here executes the F1 evaluation, changes original source bytes, proves the Riemann hypothesis, or changes the independent authorization gates.
