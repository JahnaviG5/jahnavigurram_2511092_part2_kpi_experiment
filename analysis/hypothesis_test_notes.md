# Hypothesis Test Notes

## Metric Being Tested

**Paid Conversion Rate** — the percentage of users who converted to a paid subscription within 30 days.

This was chosen because it is the North Star metric for this experiment. The entire campaign was designed to improve user activation and conversion, so this is the most direct measure of whether the treatment worked.

## Hypotheses

**Null Hypothesis (H₀):** There is no difference in paid conversion rate between the Control and Treatment groups. Any observed difference is due to random chance.

**Alternate Hypothesis (H₁):** The Treatment group has a higher paid conversion rate than the Control group. The new campaign experience improves conversion.

## Test Configuration

| Parameter | Value |
|---|---|
| Test type | Two-Proportion Z-Test |
| Tail | One-tailed (right) |
| Significance level (α) | 0.05 |
| Reason for one-tailed | We are specifically testing if Treatment is *better*, not just different |

## Test Inputs

| Input | Control | Treatment |
|---|---|---|
| Users | 693 | 715 |
| Conversions | 22 | 50 |
| Conversion Rate | 3.17% | 6.99% |

## Test Calculation

- Pooled proportion: (22 + 50) / (693 + 715) = 0.0511
- Standard error: √(0.0511 × 0.9489 × (1/693 + 1/715)) = 0.01172
- Z-statistic: (0.0699 − 0.0317) / 0.01172 = **3.264**
- P-value (one-tailed): **0.00055**

## Decision Rule

- If p-value < 0.05 → Reject the null hypothesis
- If p-value ≥ 0.05 → Fail to reject the null hypothesis

## Result

**P-value = 0.00055**, which is well below 0.05.

**Decision: Reject the null hypothesis.**

There is strong statistical evidence that the Treatment group has a significantly higher paid conversion rate than the Control group. The 3.82 percentage point improvement (from 3.17% to 6.99%) is unlikely to have occurred by chance.

## Business Interpretation

The new campaign experience roughly doubles the conversion rate. This is a meaningful business improvement — for every 1000 users who go through the new experience, approximately 38 more users would convert to paid compared to the old onboarding.

However, the test only tells us that conversion improved. It does not guarantee that overall business health improved. The guardrail metrics (support tickets, refund rate, revenue per converted user) must be evaluated separately before making a launch decision.
