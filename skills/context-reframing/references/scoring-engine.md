# Scoring Engine Reference

## How Scoring Works

Claude self-scores all 4 dimensions after each user answer.

1. **Re-evaluate from scratch** — Score based on the FULL conversation, not incrementally
2. **Scores can decrease** — Contradictory information lowers affected dimensions
3. **Low temperature (0.1)** — Consistency matters more than creativity in scoring
4. **No gaming** — Never inflate scores to reach the gate faster

## The 5-Point Rubric

Each dimension scored 0.00 to 1.00 (interpolation between anchors allowed).

### Voice Fidelity — Did we capture the literal request?

| Score | Criteria |
|-------|----------|
| 0.00 | Request not captured at all |
| 0.25 | Paraphrased inaccurately — key words lost or distorted |
| 0.50 | Paraphrased accurately — meaning preserved but not exact words |
| 0.75 | Exact words captured — verbatim quote available |
| 1.00 | Exact words + tone, emotion, and non-verbal context captured |

### Need Identification — Did we find the immediate purpose?

| Score | Criteria |
|-------|----------|
| 0.00 | Purpose completely unknown |
| 0.25 | Vague direction only — "something about search" |
| 0.50 | General goal identified — "wants to find products faster" |
| 0.75 | Specific goal with measurable outcome — "reduce search time from 5 min to 1 min" |
| 1.00 | Goal + priority + trade-offs understood — "speed over precision, willing to sacrifice variety" |

### Context Discovery — Did we uncover the real situation/emotion?

| Score | Criteria |
|-------|----------|
| 0.00 | No situational context known |
| 0.25 | Surface context only — "user is shopping" |
| 0.50 | Behavioral context — "user browses 20+ pages before buying" |
| 0.75 | Emotional/environmental context — "feels overwhelmed, shops during commute with limited time" |
| 1.00 | Full context including triggers, constraints, workarounds, and emotional state |

### Reframe Validity — Does reframed solution address Context?

| Score | Criteria |
|-------|----------|
| 0.00 | No reframe attempted or reframe identical to Voice |
| 0.25 | Reframe exists but still addresses Need, not Context |
| 0.50 | Reframe partially addresses Context but misses key aspects |
| 0.75 | Reframe directly addresses Context with concrete alternative |
| 1.00 | Reframe addresses Context AND validated as more effective than Voice-level solution |

## Domain Weight Profiles

| Dimension | Universal | Product | Debug | Prompt |
|-----------|-----------|---------|-------|--------|
| Voice Fidelity | 20% | 15% | 20% | 25% |
| Need Identification | 25% | 25% | 20% | 25% |
| Context Discovery | **35%** | **40%** | 30% | 25% |
| Reframe Validity | 20% | 20% | **30%** | 25% |

**Why these weights?**
- **Product**: Context Discovery highest — user's life situation drives product decisions
- **Debug**: Reframe Validity highest — the fix MUST address root cause, not symptoms
- **Prompt**: Balanced — AI conversations need equal clarity across all dimensions
- **Universal**: Context Discovery slightly emphasized as the most commonly underweighted dimension

## Calculation

```
Surface Risk = 1 - (voice × w_v + need × w_n + context × w_c + reframe × w_r)
```

### Worked Example (Product Domain — Filter Request)

```
Voice Fidelity:      0.95 × 0.15 = 0.143
Need Identification: 0.85 × 0.25 = 0.213
Context Discovery:   0.90 × 0.40 = 0.360
Reframe Validity:    0.80 × 0.20 = 0.160
                                    ------
Depth                             = 0.876
Surface Risk = 1 - 0.876          = 0.124 ≤ 0.2 → PASS
```

## Score Interpretation

| Surface Risk | Meaning | Action |
|-------------|---------|--------|
| 0.0 – 0.1 | Deep understanding | Proceed immediately |
| 0.1 – 0.2 | Clear enough | Proceed (default threshold) |
| 0.2 – 0.4 | Some gaps | Continue questioning |
| 0.4 – 0.6 | Significant gaps | Focus on weakest dimension |
| 0.6 – 0.8 | Very shallow | Consider reframing the reframe |
| 0.8 – 1.0 | Surface level | Early stages, keep digging |
