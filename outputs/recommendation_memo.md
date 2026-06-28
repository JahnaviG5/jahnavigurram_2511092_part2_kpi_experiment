# Recommendation Memo — Campaign Experiment

**To:** Leadership Team  
**From:** Jahnavi Gurram, Business Analyst  
**Date:** June 2025  
**Subject:** Decision Recommendation — New Onboarding Campaign

---

## Executive Summary

The new onboarding campaign (Treatment) nearly doubled the paid conversion rate from 3.17% to 6.99%, a statistically significant improvement (p = 0.00055). Engagement scores also improved meaningfully. However, the Treatment group showed a significant spike in support tickets (14.78% → 24.79%) and introduced a small refund rate (0.42%). Revenue per converted user dropped substantially, indicating the campaign is converting more lower-value users.

**Recommendation: Launch with guardrails.** Roll out the new campaign experience to all users, but invest in support infrastructure and monitor refund rates closely for the first 60 days.

---

## Business Problem Statement

The company needs to decide whether to replace the existing onboarding experience with a new campaign-driven flow. This decision impacts all new users signing up for the product. The primary metric that should improve is paid conversion rate. The risks to monitor are support burden, refund rates, and revenue quality. A data-backed recommendation requires statistically significant evidence of improvement in the primary metric without unacceptable degradation in guardrail metrics.

---

## North Star Metric

**Paid Conversion Rate** — the percentage of users who convert from free/trial to a paid subscription within 30 days.

This was selected because:
- It directly ties to revenue growth and business sustainability
- It captures the full activation funnel (visit → trial → onboard → pay)
- It is the most actionable metric the campaign can influence

Other metrics like revenue per user or engagement score are important but secondary — conversion is the gateway metric that everything else depends on.

**Risk of blind optimization:** Pushing conversion at all costs could attract low-intent users who convert but quickly churn or request refunds, which is exactly what the guardrail analysis below investigates.

---

## KPI Tree Summary

The North Star (Paid Conversion Rate) breaks down into four primary drivers:

1. **Landing Page Visit Rate** → driven by traffic source quality and campaign reach
2. **Trial Start Rate** → driven by page load speed and CTA clarity
3. **Onboarding Completion Rate** → driven by onboarding step count and UX friction
4. **Revenue Per User** → driven by plan mix and upsell conversion

Guardrail metrics monitored: refund rate, support ticket rate, days to convert, engagement score.

See `outputs/kpi_tree.png` for the full visual tree.

---

## Experiment Result Summary

| Metric | Control | Treatment | Difference |
|---|---|---|---|
| Users | 693 | 715 | +22 |
| Landing Page Visit Rate | 63.64% | 72.59% | +8.95pp |
| Trial Start Rate | 25.11% | 29.09% | +3.98pp |
| Onboarding Completion Rate | 15.58% | 21.26% | +5.68pp |
| **Paid Conversion Rate** | **3.17%** | **6.99%** | **+3.82pp** |
| Avg Revenue / User | ₹51.75 | ₹53.88 | +₹2.13 |
| Avg Revenue / Converted User | ₹1,630 | ₹770 | -₹860 |
| Refund Rate | 0.00% | 0.42% | +0.42pp |
| Support Ticket Rate | 14.78% | 24.79% | +10.01pp |
| Engagement Score | 57.03 | 62.93 | +5.90 |
| Days to Convert | 8.86 | 6.40 | -2.46 days |

The Treatment improved every funnel metric. Users visited more, tried more, onboarded more, and converted more. They also converted faster (6.4 vs 8.9 days) and engaged more.

---

## Hypothesis Test Interpretation

A two-proportion Z-test was performed on paid conversion rate.

- Z-statistic: 3.264
- P-value: 0.00055 (one-tailed)
- Decision: **Reject the null hypothesis** at α = 0.05

The improvement is statistically significant. The treatment is not a result of random variation.

---

## Guardrail Analysis

| Guardrail Metric | Control | Treatment | Status |
|---|---|---|---|
| Refund Rate | 0.00% | 0.42% | ⚠️ Minor risk — small but non-zero |
| Support Ticket Rate | 14.78% | 24.79% | 🔴 Significant risk — 68% increase |
| Engagement Score | 57.03 | 62.93 | ✅ Improved |
| Days to Convert | 8.86 | 6.40 | ✅ Faster conversion |

**Key concern:** Support tickets nearly doubled in the Treatment group. This is statistically significant (p < 0.001). While conversion improved, users may be encountering confusion or friction points in the new experience that drive them to reach out to support. This must be addressed before scaling.

**Revenue quality concern:** Revenue per converted user dropped from ₹1,630 to ₹770. The campaign is converting more users, but many of them are on lower-value plans. Total revenue per user is still slightly higher (₹53.88 vs ₹51.75) because the volume increase compensates, but this pattern needs monitoring.

**Refund rate:** Small (0.42%) and not alarming on its own, but it was zero in the Control group. Worth watching over a longer window.

---

## Segment-Level Insights

The Treatment showed consistent improvement across most segments, but some variations stood out:

- **Device type:** Mobile users showed the strongest conversion lift, suggesting the new experience is particularly effective on mobile
- **Plan type:** Free-tier users benefited most from the treatment, converting at higher rates — but they also drove the lower average revenue per converted user
- **Region:** Performance was fairly consistent across regions, with no segment showing negative treatment effects

No segment showed a decline in conversion, which supports a full rollout rather than segment-specific deployment.

---

## Final Recommendation

### **Launch with Guardrails**

The new campaign should be rolled out to all users based on the following reasoning:

1. **Primary metric improved significantly** — conversion nearly doubled with p < 0.001
2. **Funnel improvement is consistent** — every stage from landing page to conversion improved
3. **Engagement improved** — users are more active, not just converting passively
4. **Conversion is faster** — 6.4 days vs 8.9 days reduces the risk of drop-off

**However, the following guardrails must be implemented:**

1. **Support team scaling** — the 10pp increase in support ticket rate means roughly 100 additional tickets per 1000 users. Staff or self-service resources must be expanded before full launch.
2. **Refund monitoring** — track refund rates weekly for the first 60 days. If refunds exceed 2%, pause and investigate.
3. **Revenue quality tracking** — monitor average revenue per converted user monthly. If it drops below ₹500, the campaign may be attracting low-value users who churn quickly.

---

## Risks and Limitations

1. The experiment ran for a limited time window — long-term retention effects are unknown
2. The 8 duplicate user IDs suggest minor data quality issues in the tracking system
3. Revenue per converted user was significantly lower in Treatment — if these users churn within 90 days, the net revenue impact could be negative
4. Support ticket analysis does not reveal *why* tickets increased — a qualitative review of ticket content is needed
5. The test does not account for novelty effect — Treatment users may have engaged more simply because the experience was new

---

## Next Steps

1. Conduct a qualitative review of support tickets from Treatment users to identify specific friction points
2. Run a 90-day retention analysis comparing Treatment vs Control cohorts
3. A/B test a revised version of the campaign that addresses the support ticket issue
4. Explore upsell strategies for the Free-tier users the campaign is converting to improve revenue quality
5. Set up automated monitoring dashboards for refund rate and support ticket volume
