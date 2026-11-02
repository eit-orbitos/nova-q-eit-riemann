# NOVA Q / EIT Riemann F1: next-zero prediction protocol

**Version:** V0.3 CANDIDATE, corrective version after Kimi Order 05, for correction check
**Status:** NOT FROZEN. NOT APPROVED. NOT EXECUTED.
**Authority:** F1 V0.3 corrective protocol request from Toni Mladenovski, Research Architect
**Prepared by:** Claude. Claude built V0.8.1 and audited RC2, and must not evaluate the F1 outcome.
**Rights:** Toni Mladenovski. Documentation license per project convention: CC BY-NC-SA 4.0.

```text
RC3_ENGINEERING_BASELINE = FROZEN (not modified by this protocol)
G0                       = PENDING_AUTHOR_APPROVAL
F1                       = NOT_TESTED
F2                       = FAIL_FOR_PHI_LOG_X
EIT_ACTIVATION_VALIDATED = NO
NEXT_ZERO_PREDICTION     = NOT_VALIDATED
GUE_BASELINE             = NOT_BUILT
RH_PROVEN                = NO
P_VS_NP_PROVEN           = NO
V0_9                     = HOLD
```

## 1. Base references

| Item | Value |
|---|---|
| RC3 package SHA-256 | `ea09917e090306bc4a2df58758fe0a29c6a90b7365384981094c5ec847a95414` |
| Freeze records commit | `91a582b3c2fb1a8abe72fca8943af58ccef9b6b0`, `eit-orbitos/nova-q-eit-riemann` |
| Repository head read for V0.2 | `78dfbe5` |
| Parent candidate, preserved unchanged | `NOVA_Q_EIT_RIEMANN_F1_PROTOCOL_V0_2_CANDIDATE.md`, SHA-256 `a650131f170f96eb5dd2899d4a79cae0ca5366593e6437e95f32656ae51e825b` |
| Review addressed | `KIMI_F1_V02_ADVERSARIAL_REVIEW.md`, verdict `READY_WITH_CORRECTIONS` |

RC3 is read-only. New work goes in a separately named package that references RC3 by SHA-256 and never embeds an edited copy. The ZIP is not in the repository, so anyone using RC3 must hash their copy first.

## 2. Question and limits

**Question:** can one frozen EIT rule predict the k-th zeta zero ordinate better than every baseline using the same or less information, on zeros selected after the rule is frozen?

| A PASS would mean | A PASS would not mean |
|---|---|
| This rule beat the listed baselines in these windows and this mode | RH is proven |
| The rule deserves replication at greater height | EIT is physically or causally validated |
| | F2, F3, F4 or F5 are closed |
| | V0.9 is released. Any release needs a separate author decision |

**What F1 can certify:** prediction by a small frozen rule from declared inputs, under the caveat that the author may have seen the public zeros. It cannot distinguish learned public structure from novel structure.

## 3. Separate authorizations

No authorization is granted by this document. Each gate needs its own recorded author decision. An earlier gate never implies a later one.

| Gate | Allows | Status |
|---|---|---|
| G0 | Freeze this protocol, with provisional values settled | PENDING_AUTHOR_APPROVAL |
| A1 | Build the Phase A package and test it on synthetic data | NOT GRANTED |
| A2 | Compute baseline metrics on the development range | NOT GRANTED |
| B1 | Freeze one EIT rule and publish its hash | NOT GRANTED. No rule exists |
| B2 | Derive the windows and compute their ground truth | NOT GRANTED |
| B3 | Run the scientific evaluation | NOT GRANTED |

## 4. Provisional values

These are the values recommended for G0. They stay provisional until the author approves them at G0. After G0 they cannot change within this version.

| ID | Item | Recommended for G0 | Why it needs a decision |
|---|---|---|---|
| P1 | Improvement margin | **5% point margin**: measured rule NMAE ≤ 0.95 × best comparator. Separately, the corrected statistical lower bound must exceed 0 | Sets how large a gain counts |
| P2 | Evaluation windows | **Two windows of 500 consecutive zeros** | Sets test size and replication |
| P3 | Index ranges | Development 1 to 20000; evaluation indices 20001 to 59999, with W1 inside 20001 to 40499 and W2 inside 40501 to 59999 | Sets height and cost |
| P4 | Autonomous design | Primary: 50 non-overlapping rollouts of horizon 10 per window. Diagnostic only: 20 rollouts of horizon 25. One-step stays separate | Sets the meaning of autonomous skill |
| P5 | Public randomness | drand quicknet, pinned as in section 8.2, BLS verification, exact scheduled round, 72-hour fail-closed policy | Closes byte grinding, adds an outside dependency |
| P6 | Rule package limit | 16 KiB, excluding the fixed interface file | Limits hidden zero tables |
| P7 | Bootstrap | 10,000 paired resamples, one-sided 95% BCa, Holm | Sets statistical strictness |
| P8 | Numerical tolerances | Unchanged from V0.2, section 10 | Sets what counts as agreement |

Section 15 shows what these values can and cannot detect. Read it before approving P1, P2 and P4.

## 5. Phase separation

| | Phase A: baselines | Phase B: EIT predictor |
|---|---|---|
| Purpose | Build and control the comparison set | Test one frozen rule |
| Needs an EIT rule | No | Yes |
| Data allowed | Synthetic and development zeros only | Development zeros, then windows after B2 |
| Hold-out access | Forbidden | Only after the rule hash is public |
| Result vocabulary | `A_PASS`, `A_FAIL` (engineering) | `PASS`, `FAIL`, `INCONCLUSIVE`, `INVALID` |
| Effect on F1 | **None. F1 stays NOT_TESTED** | F1 can change only after B3 and author recording |
| Effect on `GUE_BASELINE` | May become `BUILT` when A1 and A2 pass | None |

**Wall between phases:** the Phase A package contains no EIT rule, no window derivation result, and no zero above index 20000. It includes a test that refuses any zero file over that index. Phase B imports the Phase A baselines by hash and cannot change them. A baseline error found later requires a new baseline version and invalidates any evaluation that relied on it.

## 6. Information tiers

A rule declares one tier and all its inputs before freezing. It is compared with every baseline in its tier and below, in the same mode.

| Tier | Allowed inputs | Mode dependence |
|---|---|---|
| T0 | Index k, fixed constants and the Riemann-Siegel theta function. No zero ordinates, no primes | Same output in both modes |
| T1 | T0, plus zeros available under the mode | One-step and autonomous differ |
| T2 | T1, plus prime powers up to one fixed declared X | Differs if zeros are used |
| Excluded | Any evaluation of zeta, xi, the Riemann-Siegel Z function or a zero finder; zero tables; network; files; clock; external randomness | Result `INVALID` |

**Theta whitelist:** a rule may evaluate the Riemann-Siegel theta function at T0 and above, for example `mpmath.siegeltheta`. Theta is smooth and is not a zero source. This allowance covers no other function. A rule may solve its own equations numerically only if every term comes from declared allowed inputs. `zetazero`, `nzeros`, `backlunds`, `siegelz`, `zeta`, `altzeta` and all other zero-finding or zeta-evaluating operations stay excluded.

Knowing how many earlier zeros exist is knowing k, so T1 contains T0 and every T1 rule must beat the smooth count.

A rule whose only extra input is a function of x or k, including `Phi = log x`, adds nothing beyond T0. This protocol does not reopen F2.

## 7. Prediction modes

The two modes are separate experiments. Results are never pooled, and a result in one never transfers to the other. The author declares at B1 which mode or modes will count.

Let `m(t) = 2*pi / log(t / (2*pi))`, the local mean spacing.

| | One-step (O) | Autonomous (A) |
|---|---|---|
| Interface | `predict(k, zeros_1_to_k_minus_1)` | `rollout(origin, horizon, zeros_1_to_origin_minus_1)` |
| Truth inside the prediction span | Revealed after each prediction | None. The rule feeds on its own output |
| Primary predictions per window | 500 | 50 rollouts × 10 = 500 |
| Primary origins | Not applicable | `start + 10*j`, j = 0 to 49 |
| Truth between rollouts | Not applicable | Revealed up to the next origin only |
| Bootstrap unit | Moving blocks of paired losses | Whole rollouts, paired |
| Diagnostic only | None | 20 rollouts × 25 at `start + 25*j`, j = 0 to 19; error at horizons 1, 5, 10, 25; one 500-zero rollout per window |

Log entries for each prediction are written and chained by hash before the harness reveals more truth.

**Dependence between rollouts:** with 500 zeros per window, horizon 25 allows at most 20 non-overlapping rollouts and horizon 10 allows at most 50. V0.3 does not add overlapping origins, because they would make rollouts directly dependent. Non-overlapping rollouts still come from one consecutive sequence and are not proven independent. The report must give the lag-1 correlation of paired rollout losses. That number cannot change a result.

**Diagnostic results** can never produce or rescue a PASS, and no statistical superiority may be claimed from them. More than 20 rollouts at horizon 25 would require a larger window, which means a new protocol version.

### Baselines

`B0(k)` solves `Nbar(T) = k - 1/2`, with `Nbar(T) = T/(2*pi) * (log(T/(2*pi)) - 1) + 7/8`.

| ID | Tier | One-step form | Autonomous form |
|---|---|---|---|
| B0 | T0 | Smooth count | Same |
| B1 | T0 | Solve `theta(T)/pi + 1 = k - 1/2`, with theta the Riemann-Siegel theta function as in RC3. Theta is a smooth function of T and is allowed at T0 | Same |
| B2 | T1 | `g + m(g)`, where g is the last true zero | Same, g is the last predicted zero |
| B3 | T1 | `g + m(g) * q`, q = GUE median | Same, fed by own predictions |
| B4 | T1 | `g + m(g) * (c0 + c1 s1 + c2 s2 + c3 s3)`, GUE-fitted constants, last three normalized spacings, oldest first | Same, fed by own predictions |
| B5 | T1 | Same form, coefficients fitted on development zeros | Same, fed by own predictions |
| B6 | T1 | `B0(k) + m(B0(k)) * e`, where e is an AR(3) of normalized past errors `(gamma_j - B0(j)) / m(gamma_j)`, fitted on development zeros | Same, fed by own predicted errors |
| B8 | T1 | Regularized long-memory form below | Same, fed by own predicted errors |
| B7-X | T2 | Solve `Nbar(T) + S_X(T) = k - 1/2`, with X in {10, 100, 1000} | Same, uses no zeros |

`S_X(T) = -(1/pi) * sum over prime powers p^n ≤ X of sin(n*T*log p) / (n * p^(n/2))`.

**B8, long-memory ridge baseline:** with `e_j` as in B6, predict `e_k = a0 + sum over i=1..L of a_i * e_(k-i)`. The ridge penalty `lambda * sum(a_i^2)` applies to `a_1..a_L`, not `a0`.
- Grid: L in {10, 20, 50}; lambda in {0.0001, 0.001, 0.01, 0.1, 1}.
- Tuning: fit on development zeros up to 15000, select by primary NMAE on 15001 to 20000. One-step and autonomous horizon 10 are tuned separately. Ties go to smaller L, then larger lambda.
- Final fit: selected values, development zeros up to 20000.
- Output: coefficients stored as a hashed file of exact decimal strings. No zero above 20000 may enter at any point.

**B7 root rule:** scan `B0(k) ± 5*m(B0(k))` in steps of `m(B0(k))/100`, take upward crossings by linear interpolation, choose the one closest to `B0(k)`. If none exists, use `B0(k)`.

T2 baselines are always reported, even when the rule is below T2. A PASS at T0 or T1 must be stated together with the T2 gap.

### GUE reduction

GUE describes spacing statistics. It predicts nothing until reduced to a rule, and B3 and B4 are that reduction.

- Sampling: `H = (A + A*)/2`, where A has independent standard normal real and imaginary parts.
- Size: N ≥ 1000 and at least 2000 samples.
- Unfolding: central half of the spectrum, semicircle density with radius `2*sqrt(N)`.
- Fitted on simulation only. No zeta zero enters.
- Constants are stored as a hashed file with exact decimal strings. Prediction uses those constants and no BLAS, because RC3 showed byte results depending on the OpenBLAS kernel.
- Regenerating the constants is compared numerically, not by byte identity.

## 8. Data

### 8.1 Development range

Zeros 1 to 20000, proposed source: Odlyzko `zeros1`, stated accuracy within 3×10⁻⁹. That file holds 100,000 zeros, so it must be truncated at ingestion and only the truncated file, with its hash, enters the package.

### 8.2 Windows

**Zeros are public, so nothing here is secret.** The protection is commitment, not secrecy: positions depend on bytes fixed after the rule is frozen. A prior look at those ranges cannot be disproved, and the result report must state that.

```text
H        = SHA-256(rule_package_sha256_bytes || protocol_sha256_bytes || beacon_bytes)
n        = H read as a big-endian integer
W1 start = 20001 + (n mod 20000)
W2 start = 40501 + (floor(n / 2^128) mod 19000)
seed     = n mod 2^64
```

W1 and W2 each hold 500 consecutive zeros. Starts are computed only at B2.

**Pinned beacon, proposed P5:**

| Field | Value |
|---|---|
| Network | drand quicknet |
| Chain hash | `52db9ba70e0cc0f6eaf7803dd07447a1f5477735fd3f661792ba94600c84e971` |
| Group public key | `83cf0f2896adee7eb8b5f01fcad3912212c437e0073e911fb90022d3e760183c8c4b450b6a0a6c3ac6a5776a2d1064510d1fec758c921cc22b0e17e63aaf4bcb5ed66304de9cf809bd274ca73bab4af5a6e9c76a4bc09e76eae8991ef5ece45a` |
| Scheme | `bls-unchained-g1-rfc9380` |
| Period, genesis | 3 seconds, 1692803367 |
| DST | `BLS_SIG_BLS12381G1_XMD:SHA-256_SSWU_RO_NUL_` |

**Scheduled round:**
1. The rule hash is committed publicly at B1.
2. A party other than the rule author retrieves that commit and records the UTC time `T_A`.
3. `R = ceil((T_A + 86400 - 1692803367) / 3) + 1`. Round R's time, `1692803367 + 3*(R-1)`, is at least 24 hours after `T_A`.
4. `R` and `T_A` are entered in the attempt register by a commit visible before round R's time. Otherwise `B2 = BLOCKED`.

**Verification, from any relay, because the signature decides authenticity:**
1. The message is `SHA-256(R as 8 big-endian bytes)`.
2. The signature verifies against the pinned key under the pinned scheme.
3. `randomness = SHA-256(signature)`, and `beacon_bytes` is those 32 bytes.

**Fail-closed rule:** if the value for R cannot be retrieved and cryptographically verified within 72 hours after round R's time, `B2 = BLOCKED`. No other round, network or beacon may be chosen. A later attempt needs a recorded author decision and a new rule version, hence a new hash and a new round, and it enters the attempt register. If P5 is rejected at G0, this section must be rewritten before freezing, because a rule author could otherwise try byte variants to select windows.

Check values, for implementers only: round 1000 has signature `b44679b9a59af2ec876b1a6b1ad52ea9b1615fc3982b19576350f93447cb1125e342b73a8dd2bacbe47e4b6b63ed5e39` and randomness `fe290beca10872ef2fb164d2aa4442de4566183ec51c56ff3cd603d930e54fdd`. It must verify, and the same signature must fail for round 1001. For `T_A = 1800000000`, R = 35761012; for `T_A = 1800000001`, R = 35761013.

Test vector, for checking only. Inputs are `SHA-256("TEST_RULE")`, `SHA-256("TEST_PROTOCOL")`, `SHA-256("TEST_BEACON")`, as raw bytes:

```text
H    = 38f0c50169a8dfb02cc6b27ee52384d21090793898929f21614cc6d31fc42b2d
W1   = 31118
W2   = 55079
seed = 7011197329982368557
```

### 8.3 Ground truth

Window ordinates are computed at B2 with mpmath, confirmed by a sign change and a zero count, then compared with the second source. This is independent control C1.

## 9. Scoring and decision

**Primary metric:** `NMAE = mean(|prediction - gamma_k| / m(gamma_k))`, evaluated separately per window and mode. The scorer alone uses `m(gamma_k)`.

**Report only:** normalized RMSE, largest error, share of predictions nearest the correct zero.

**Comparison:** paired loss differences against each comparator in the rule's tier and below, in the same mode.

**Bootstrap units:** one-step uses 20 fixed non-overlapping blocks of 25. Autonomous uses the 50 primary rollouts. This replaces the moving blocks of V0.2, because BCa acceleration needs a fixed unit for its jackknife.

**Resampling:** 10,000 paired resamples per window and mode, with the same resample indices for all comparators. The generator is Python `random.Random`, seeded by the integer value of `SHA-256("<seed>|<W1 or W2>|<O or A>")`, with seed in decimal.

**Interval:** one-sided BCa, for the mean paired improvement `comparator loss - rule loss`, with acceleration from delete-one-unit jackknife.
- `z0 = Phi^-1(share of resamples below the estimate)`, clipped to `[1/(B+1), B/(B+1)]` before the inverse.
- `g` is the share of resamples at or below 0.
- If `g = 0`, `p = 1/(B+1)`. If `g = 1`, `p = 1`.
- Otherwise `w = Phi^-1(g) - z0` and `p = Phi(w/(1 + a*w) - z0)`.

"Corrected lower bound above 0" means the comparator is rejected by Holm at one-sided 0.05 using these p values.

**Holm family:** all comparators in the tier and below, across all modes declared at B1, separately for each window. No extra correction is applied across W1 and W2, because PASS needs both. T0 modes are not double-counted when the rule is T0.

**Two separate conditions:** the 5% threshold applies to the point estimate. The statistical condition is that the lower bound exceeds 0. The lower bound does not have to exceed 5%.

Results below are decided per mode.

| Result | Condition |
|---|---|
| **PASS** | In both W1 and W2, measured rule NMAE ≤ 0.95 × best comparator NMAE (P1), and the corrected lower bound of improvement is above 0 against every comparator, in the primary design |
| **FAIL** | In W1 or W2, rule NMAE ≥ best comparator NMAE |
| **INCONCLUSIVE** | Neither PASS nor FAIL |
| **INVALID** | A required control or negative test fails, the firewall is broken, or inputs were undeclared. F1 stays NOT_TESTED |

The first matching row in the order INVALID, FAIL, PASS, INCONCLUSIVE applies.

### No rescue

- One rule per version. Any change is a new version with a new hash and new windows.
- Every attempt, including failed, invalid and blocked ones, enters a public append-only attempt register. Repeated attempts on public zeros raise the chance of a lucky success, so the count must be visible.
- **Register custody:** the register is `F1_ATTEMPT_REGISTER.md` in `eit-orbitos/nova-q-eit-riemann`, outside every package. Each update is its own commit. An entry gives rule version and hash, tier, modes, `T_A`, R, windows, status and result. A registration entry must exist before B2, and the result entry follows. Corrections are new entries, never edits. An evaluation without a registration commit is `INVALID`. A commit gives a hosted reference, not an author signature or certified timestamp.
- An INCONCLUSIVE result is not rescued by a new metric, window, or margin.
- Parameters may be tuned on the development range only, and their number is declared at B1.

## 10. Independent controls

These check the comparison itself. They do not depend on who wrote the EIT rule.

| ID | Control | Required outcome |
|---|---|---|
| C1 | Two ground truth sources | Max difference ≤ 1×10⁻⁸ over each window and over development samples |
| C2 | Second baseline implementation written from this text by a party other than the builder, with no shared code, submitted with an ambiguity log | All baseline predictions agree within 1×10⁻⁷ in NMAE units, and the log is present |
| C3 | Replay against frozen RC3 values on zeros 101 to 600, within 1×10⁻⁹ | B0 0.20829871921; B1 0.20829827759; one-step B2 0.30328596764; autonomous B2 from zeros 1 to 100 0.42508031629; RC3 one-step AR(3), coefficients fitted on zeros 1 to 100, 0.27658375340 |
| C4 | GUE simulation checks | Mean within 0.002 of 1; variance in 0.175 to 0.185; N versus 2N agreement of median and AR(3) constants within declared Monte Carlo error |
| C5 | Surrogate sequences: synthetic GUE and Poisson spectra, seeded, unrelated to zeta | Harness and baselines run. Results are report-only, showing whether a rule's gain is specific to zeta zeros |
| C6 | Two-environment replay | Predictions agree within 1×10⁻⁹ in NMAE units. Environments recorded in full, including OpenBLAS kernel if used |
| C7 | Oracle through the scorer | NMAE below 1×10⁻¹², showing the scorer can recognize a perfect answer |

C3 uses the frozen RC3 result files by hash and leaves them unchanged. Tolerances are P8.

**C2 ambiguity log:** before seeing the builder's output, the second implementer lists each sentence that allowed more than one reading, the reading chosen and why, or states that none was found. The log is hashed with the submission. Agreement cannot rule out a shared misreading of the same text, which is why the log is required. A real ambiguity is resolved by a new protocol version, not by editing the code to agree.

## 11. Negative tests

Each deliberately bad input must produce the stated outcome. If any does not, the harness is not accepted.

| ID | Input | Required outcome |
|---|---|---|
| N1 | Rule that reads a future zero through any route | Refused or `INVALID` |
| N2 | Changing zeros at index k or later, then rerunning | Prediction for k unchanged, in both modes |
| N3 | Autonomous rule attempting to read truth inside its rollout | Refused; truth not present in its process |
| N4 | Imports of `mpmath.zeta`, `zetazero`, `nzeros`, `backlunds`, `siegelz`, `altzeta`, `scipy.special.zeta`, `socket`, `subprocess`, `urllib`, plus dynamic import and `eval` | Refused by static allowlist. A rule that uses only `siegeltheta` and declared inputs is not refused |
| N5 | Package over P6 or a large embedded numeric table | Refused, or flagged for reviewer before B2 |
| N6 | Non-deterministic rule | `INVALID` |
| N7 | Seeded random spacing rule | Does not PASS |
| N8 | Correct predictions scored against truth shifted by one index | Does not PASS |
| N9 | Altered prediction log after hashing | Detected, `INVALID` |
| N10 | Synthetic rule at 4% gain | `INCONCLUSIVE`, confirming P1 is enforced |
| N11 | Synthetic rule passing W1 and worse than the best comparator in W2 | `FAIL` |
| N12 | T2 rule declared as T1 | Caught at reviewer input audit before B2, `INVALID` |
| N13 | Copy of a baseline submitted as the rule | Not PASS |
| N14 | Zero above index 20000 loaded into Phase A | Refused |
| N15 | Attempted change to RC3 files or the Phase A hash | Detected, run stops |
| N16 | Synthetic paired losses with a known large gain, no gain, and three-comparator Holm cases | Expected rejections occur, including step-down stopping |
| N17 | Forged signature, wrong round, or wrong chain for the beacon | Refused, B2 does not proceed |
| N18 | Beacon value unavailable for 72 hours | `B2 = BLOCKED`, no alternative round, network or beacon accepted |
| N19 | Round R or `T_A` registered after round R's time | `B2 = BLOCKED` |
| N20 | Evaluation with no registration commit | `INVALID` |
| N21 | C2 submission without an ambiguity log | C2 not accepted |
| N22 | Rule that succeeds at the 20 × 25 diagnostic and fails the primary design | Not PASS |
| N23 | B8 tuned with data above index 20000 | Refused |

**Limit:** static checks can be evaded by determined code, so reviewer reading of the rule package is required. This limit must appear in the report.

## 12. Phase B rule requirements

The rule package must contain: one deterministic predictor, declared tier and modes, every input, parameter count and origin, development range use, and a statement of the EIT definition it implements. The hash is committed publicly before B2. Whoever writes the rule cannot evaluate it.

A rule cannot be supplied by this protocol. If none is frozen, Phase B does not run and F1 stays NOT_TESTED.

## 13. Roles

| Step | Party |
|---|---|
| Adversarial review of this candidate | Kimi |
| Provisional values, rule, freezes, authorizations | Toni Mladenovski |
| Phase A build from this text | Tasklet, after A1 |
| C2 second implementation, replay, ground truth check | Kimi, after the relevant gate |
| Final reading of results against this protocol | A reviewer who neither wrote the rule nor built the harness |

Agreement among AI systems is not evidence of truth. Hashes prove byte identity only.

## 14. Known contamination and limits

- Zeros 1 to 600 were visible when this design was made. The V0.1 prototype on zeros 101 to 600 influenced the baseline list, including B7 and its X values, and the view that GUE is a weak bar. Those numbers are not F1 results, and the proposed 5% margin was also set after seeing them.
- All windows are publicly computable. See 8.2. Public zero tables cover the whole evaluation range. The package firewall can stop a smuggled table, but it cannot stop an author from having learned public zeros. The consequence for a PASS is stated in section 2.
- Accuracy of B7 and others at index 20000 and above is unknown and must not be inferred from the prototype.
- Internal hash chains do not stop a consistent rewrite (L-1). Each new package digest needs its own record outside the package. A GitHub commit gives a hosted reference, not an author signature or certified timestamp.
- Passing F1 is limited to prediction under these inputs. A strong rule may still be a rediscovery of known structure, which is why the T2 gap is mandatory.
- The section 15 planning figures use zeros 101 to 600 and were seen before the values were recommended.
- The drand network may later be retired or interrupted. V0.3 handles this by blocking, which may delay F1, rather than by a fallback.

## 15. Minimum detectable effect, planning only

Full figures and method are in `F1_MDE_ANALYSIS_V0_3.md`. They come from RC3 zeros 101 to 600 with a normal approximation, and may not hold at index 20000 and above. They are not baseline results, and they are not F1 results. The comparator is B0 at NMAE 0.2083.

| Design | Paired standard error, correlation 0.5 | True gain for an 80% chance of PASS in both windows, correlation 0.3 to 0.9 |
|---|---|---|
| One-step, 20 blocks × 25 | 0.0038 | 6.0% to 8.0% |
| Autonomous primary, 50 × 10 | 0.0041 | 6.1% to 8.6% |
| Autonomous diagnostic, 20 × 25 | 0.0038 | Not a decision design |

What this means:
- A rule with a true gain of exactly 5% has only about a 25% chance of PASS, or lower. The 5% threshold applies to a noisy estimate, in two windows.
- Moving from 20 × 25 to 50 × 10 does not add power against B0. The total is 500 predictions either way, and B0 does not depend on horizon. The gain is more bootstrap units for BCa and a shorter autonomous task.
- Only more zeros per window would reduce the standard error materially, and that would change P2.

## 16. Changes from V0.2

See `F1_PROTOCOL_V0_3_CHANGELOG.md` and `KIMI_FINDINGS_CORRECTION_MAP_V0_3.md`. V0.2 is preserved unchanged.

## 17. Requested next

See `KIMI_CORRECTION_CHECK_REQUEST_F1_V0_3.md`. A check does not freeze, approve, build or execute anything. G0 and A1 remain author decisions.
