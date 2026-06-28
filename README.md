# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

**Jahnavi Gurram | bitsom_ba_2511092**

---

## Business Context

A subscription-based digital product company launched a new onboarding campaign. Users were randomly split into two groups — Control (existing onboarding) and Treatment (new campaign). Leadership needs a data-driven recommendation on whether to roll out the Treatment to all users.

---

## Dataset Description

| Property | Value |
|---|---|
| File | campaign_experiment_data.xlsx |
| Records | 1,408 (raw) → 1,400 (after dedup) |
| Columns | 16 |
| Groups | Control (693 users), Treatment (715 users) |
| Key fields | experiment_group, visited_landing_page, started_trial, completed_onboarding, converted_to_paid, revenue_30d, support_tickets_30d, refund_requested, engagement_score, days_to_convert |
| Segments | region, device_type, traffic_source, plan_type |

---

## North Star Metric

**Paid Conversion Rate** — the percentage of users who convert to a paid subscription within 30 days.

Selected because it directly drives revenue growth, captures the full activation funnel, and is the metric the campaign was specifically designed to improve. Other metrics (engagement, revenue per user, trial starts) are important supporting metrics but are upstream or downstream of the conversion decision itself.

---

## KPI Tree Summary

The North Star breaks into four primary drivers, each with two sub-drivers, plus four guardrail metrics. See `outputs/kpi_tree.png` for the full diagram.

- **Landing Page Visit Rate** → traffic quality, campaign reach
- **Trial Start Rate** → page speed, CTA clarity
- **Onboarding Completion Rate** → step count, UX friction
- **Revenue Per User** → plan mix, upsell conversion
- **Guardrails:** refund rate, support ticket rate, days to convert, engagement score

---

## Data Cleaning & Preparation

| Check | Finding | Action |
|---|---|---|
| Duplicate user IDs | 8 duplicates | Removed (kept first) |
| Missing device_type | 18 records | Filled as "Unknown" |
| Missing traffic_source | 24 records | Filled as "Unknown" |
| Missing engagement_score | 14 records | Filled with median |
| Missing days_to_convert | 1,336 records | Expected — only converted users have this value |
| Invalid binary values | None | All columns clean |
| Revenue outliers | A few users >₹5,000 | Kept — legitimate high-value plans |
| Group balance | 693 Control, 715 Treatment | Acceptable balance |

---

## Experiment Analysis Approach

1. Cleaned and deduplicated the dataset
2. Calculated 11 comparison metrics for Control vs Treatment
3. Analyzed all metrics by 4 segments (region, device, traffic source, plan type)
4. Performed a two-proportion Z-test on the primary metric
5. Evaluated 4 guardrail metrics for risk assessment
6. Synthesized findings into a launch recommendation

---

## Hypothesis Test Summary

| Parameter | Value |
|---|---|
| Metric | Paid Conversion Rate |
| Test | Two-Proportion Z-Test (one-tailed) |
| α | 0.05 |
| Control rate | 3.17% |
| Treatment rate | 6.99% |
| Z-statistic | 3.264 |
| P-value | 0.00055 |
| Decision | **Reject null hypothesis** — Treatment significantly improves conversion |

---

## Guardrail Metrics

| Metric | Control | Treatment | Verdict |
|---|---|---|---|
| Refund Rate | 0.00% | 0.42% | ⚠️ Minor concern |
| Support Ticket Rate | 14.78% | 24.79% | 🔴 Significant spike |
| Engagement Score | 57.03 | 62.93 | ✅ Improved |
| Days to Convert | 8.86 | 6.40 | ✅ Faster |

Support tickets increased by 68% — this is the primary risk flag. Refunds were introduced but remain small. Engagement and conversion speed both improved.

---

## Final Recommendation

**Launch with guardrails.** The Treatment nearly doubled conversion (p < 0.001), improved engagement and conversion speed, and showed consistent gains across all segments. However, support ticket rates must be addressed before full scale — either through expanded support staffing or UX improvements to reduce confusion in the new flow. Refund rate and revenue quality should be monitored weekly for 60 days post-launch.

---

## Assumptions and Limitations

- The experiment assumes random assignment with no selection bias
- Revenue per converted user dropped significantly (₹1,630 → ₹770), suggesting the campaign converts lower-value users
- Long-term retention is unknown — 30-day data may not capture churn
- Support ticket content was not analyzed qualitatively
- Novelty effect may inflate Treatment metrics temporarily

---

## Screenshots

| File | Shows |
|---|---|
| screenshots/summary_metrics.png | Control vs Treatment comparison table |
| screenshots/hypothesis_test_output.png | Z-test calculation and result |
| screenshots/kpi_tree_preview.png | KPI tree diagram |
