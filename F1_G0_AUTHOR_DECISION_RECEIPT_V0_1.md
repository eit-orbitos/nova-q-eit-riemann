# NOVA Q / EIT — F1 V0.3 G0 Author Decision Receipt V0.1

**Disposition:** `G0_AUTHOR_DECISION = APPROVED`  
**Date/time of receipt:** `2026-11-02T14:37:39-07:00`  
**Research Architect:** Mr. Toni Mladenovski  
**Authorization:** explicit chat message `Go aprouve` (not a cryptographic signature)  
**Scope:** methodological G0 author decision only, not Phase A/B execution authorization.

## Exact artifact identity / evidence limitation

- Intended V0.3 protocol: `NOVA_Q_EIT_RIEMANN_F1_PROTOCOL_V0_3_CANDIDATE.md`.
- **SHA-256 as reported by Kimi:** `118c9457120ae9c8c1e2e99f43d56bec06d51ad4177154058659c9ce18c2fca6`.
- The **V0.3 protocol bytes were not supplied in this conversation** when this receipt was prepared. That reported digest is not independently recomputed here.
- Consequently `G0_EXACT_PROTOCOL_BYTE_FREEZE = PENDING`. Upon receipt of the file, verify the hash, check the final text against the approved decisions and create an append-only byte-freeze verification addendum. If the text is amended, assign a new digest and record its relationship to this approval; do not silently relabel the old digest.
- Frozen RC3 baseline SHA-256 (immutable): `ea09917e090306bc4a2df58758fe0a29c6a90b7365384981094c5ec847a95414`.

## G0 decisions — P1 through P8

| ID | Author-approved methodological choice |
|---|---|
| P1 | 5% minimum measured NMAE improvement over the strongest eligible comparator in each window; declared confidence and multiplicity checks apply separately. |
| P2 | Two separate, non-overlapping evaluation windows of 500 zeros each. |
| P3 | Development indices 1–20000; evaluation indices within 20001–59999, exact windows selected according to the final protocol ceremony. |
| P4 | Primary autonomous test: 50 non-overlapping horizon-10 rollouts per window. The 20 × horizon-25 design is diagnostic only. One-step and autonomous mode remain separate. |
| P5 | Drand quicknet with pinned chain parameters, BLS signature verification and fail-closed beacon unavailability. No discretionary fallback. |
| P6 | 16 KiB predictor-package limit, excluding the fixed interface file. |
| P7 | 10,000 paired bootstrap resamples; BCa confidence intervals; one-sided 95% and Holm multiplicity adjustment. |
| P8 | The numeric tolerances of the reviewed V0.3 protocol, subject to checking its exact source text before byte-level freeze. |

### G-01 — required B8 clarification

For B8 autonomous tuning/selection on the development selection range **15001–20000**, use **500 non-overlapping horizon-10 rollouts** with origins `15001 + 10j`, `j = 0,…,499`. At the start of each rollout, true zeros only through index `origin−1` are available. Within the rollout, do not reveal true future zeros; the predictor feeds back its own predictions. Each rollout has ten predictions (origin through origin+9). Select using NMAE across the **5000 predictions**, with no alternative post-hoc layout. This is development-only selection; it is not a hold-out test.

### G-02 — accepted dependency / no fallback

If the required quicknet scheduled beacon round cannot be retrieved and verified under the protocol, **B2 remains BLOCKED**; do not substitute another beacon, network or discretionary round. Any change requires a separately reviewed protocol version. The resulting calendar dependency is explicitly accepted.

### Power / effect-size limitation

The author accepts Kimi's *planning estimates*, not as observed F1 results: a true 5% advantage might yield only about 25% probability of protocol PASS; an effect of roughly 6–9% might be needed for 80% power, and these estimates might not transfer to higher-index windows. An `INCONCLUSIVE` scientific result remains valid.

## Separate gate authorization (fail-closed)

```text
G0_AUTHOR_DECISION       = APPROVED
G0_EXACT_PROTOCOL_FREEZE = PENDING_BYTE_VERIFICATION
A1                      = NOT_AUTHORIZED
A2                      = NOT_AUTHORIZED
B1                      = NOT_AUTHORIZED
B2                      = NOT_AUTHORIZED
B3                      = NOT_AUTHORIZED
RC3_ENGINEERING_BASELINE= FROZEN_IMMUTABLE
F1                      = NOT_TESTED
F2                      = FAIL_FOR_PHI_LOG_X
F3                      = NOT_TESTED
F4                      = NOT_TESTED
F5                      = OPEN
GUE_BASELINE            = NOT_BUILT
EIT_ACTIVATION_VALIDATED= NO
NEXT_ZERO_PREDICTION    = NOT_VALIDATED
RH_PROVEN               = NO
P_VS_NP_PROVEN          = NO
V0_9                    = HOLD
```

## Provenance and next action

This receipt records the author's decision and the scope of the Kimi inline correction-check report. It is not a proof of RH or the EIT mechanism and not an independent source-code audit. The next action is to obtain the *actual* V0.3 `.md` and optionally its ZIP, independently hash them, confirm the text matches P1–P8 and G-01/G-02, and create an **append-only G0 byte-identity attestation**. A1 remains blocked until separately authorized.
