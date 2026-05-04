# email-A-B-testing-analysis-
End-to-end email A/B testing analysis: experiment design,  power analysis, Z-test, T-test, Bayesian testing, and  segment-level insights. Python (scipy, statsmodels) +  Power BI dashboard. Variant B (personalized) won with  97.9% Bayesian confidence and +302% revenue lift.


# 📧 Email Campaign A/B Testing Analysis
### Company A — Personalized vs Generic Subject Line

---

## 🗂 Project Overview

This project demonstrates a complete **A/B testing framework** applied to Company A's email marketing campaign. The test evaluated whether **personalized subject lines** (using the recipient's first name) outperform **generic subject lines** in driving open rates, click-through rates, conversions, and revenue.

The analysis covers the full A/B testing lifecycle:
1. **Experiment Design** — sample size, power analysis, random assignment
2. **Exploratory Data Analysis** — metric distributions, segment breakdowns
3. **Statistical Testing** — Z-test, T-test, and Bayesian A/B test
4. **Business Recommendation** — winner declaration, segment insights, action plan

> **Note:** Company A is an anonymized client. The dataset is simulated to reflect realistic email marketing dynamics including segment-level variation, conversion funnel behavior, and revenue distributions.

---

## 🧪 Experiment Design

| Parameter | Value |
|---|---|
| Test type | A/B Test (two variants) |
| Channel | Email marketing |
| Test element | Subject line |
| Variant A (Control) | Generic subject line |
| Variant B (Treatment) | Personalized subject line with recipient name |
| Total subscribers | 10,000 |
| Split | 50/50 random assignment |
| Test duration | 4 weeks (March 2024) |
| Primary metric | Open Rate |
| Secondary metrics | CTR, Conversion Rate, Revenue per User |
| Significance threshold | α = 0.05 |

---



## 📦 Dataset

### Main Dataset: `email_ab_test_data.csv`

| Field | Description |
|---|---|
| `subscriber_id` | Unique subscriber identifier |
| `variant` | A (Control) or B (Treatment) |
| `send_date` | Date email was sent |
| `age_group` | Subscriber age group |
| `customer_segment` | New, Returning, or VIP |
| `days_since_last_purchase` | Recency metric |
| `opened` | 1 if email was opened, 0 otherwise |
| `clicked` | 1 if link was clicked, 0 otherwise |
| `converted` | 1 if purchase was made, 0 otherwise |
| `revenue` | Revenue generated ($) |

---

## 🔍 Part 1 — Exploratory Data Analysis

**Notebook:** `01_eda_analysis.ipynb`

### Page 1 — Test Overview
<img width="1306" height="741" alt="image" src="https://github.com/user-attachments/assets/c5410511-4617-49d8-af7c-917869dfd50a" />



Key EDA findings:

- **Variant B consistently outperformed Variant A** on open rate every single day of the 4-week test — no crossover observed
- **VIP customers** showed the strongest response to personalization
- **New customers** showed no meaningful lift — generic subject line performs equally well for acquisition
- Revenue distribution for converters: Variant B median (~$50) higher than Variant A (~$33)

### Key Metrics at a Glance

| Metric | Variant A | Variant B | Lift |
|---|---|---|---|
| Open Rate | 21.86% | 26.78% | **+22.5%** |
| CTR | 20.31% | 21.96% | **+8.1%** |
| Conversion Rate | 0.10% | 0.28% | **+180%** |
| Revenue per User | $0.037 | $0.149 | **+302%** |

---

## 📊 Part 2 — Statistical Analysis

**Notebook:** `02_ab_test_analysis.ipynb`

### Page 2 — Statistical Results
 <img width="1308" height="738" alt="image" src="https://github.com/user-attachments/assets/c847765d-2b9c-4288-b46a-4e38b2e2291f" />


### Power Analysis

Before interpreting results, we assessed whether the test had sufficient statistical power:

| Parameter | Value |
|---|---|
| Baseline conversion rate | 0.10% |
| Minimum detectable effect | 20% relative lift |
| Required sample per variant | 392,050 |
| Actual sample per variant | 5,000 |
| Test adequately powered | ⚠️ No — underpowered for conversion |

> **Important note:** The test was underpowered for conversion rate detection. Open rate results (well-powered with 1,093+ opens per variant) are the most statistically reliable finding.

---

### Statistical Tests

#### Z-Test: Open Rate
```
Variant A: 21.86%
Variant B: 26.78%
Absolute lift: +4.92 percentage points
Relative lift: +22.5%
95% CI: [0.0324, 0.0660]
Z-statistic: -5.73
P-value: 0.000000
Significant: ✅ YES — 100% confidence
```

#### Z-Test: Conversion Rate
```
Variant A: 0.10%
Variant B: 0.28%
Relative lift: +180%
95% CI: [0.0001, 0.0035]
Z-statistic: -2.07
P-value: 0.038762
Significant: ✅ YES — 96.1% confidence
```

#### T-Test: Revenue per User
```
Variant A: $0.037
Variant B: $0.149
Relative lift: +302.3%
95% CI: [$0.024, $0.199]
T-statistic: -2.499
P-value: 0.012461
Significant: ✅ YES — 98.8% confidence
```

#### Bayesian A/B Test
```
Prior: Beta(1,1) — uninformative uniform prior
Posterior A: Beta(6, 4996)
Posterior B: Beta(15, 4987)
P(B > A): 97.9%
Recommendation: ✅ Launch Variant B
```

The Bayesian approach confirms: there is a **97.9% probability** that Variant B's true conversion rate exceeds Variant A's — well above the 95% decision threshold.

---

## 💡 Why Both Frequentist and Bayesian?

| | Frequentist (Z/T-Test) | Bayesian |
|---|---|---|
| Question answered | Is this due to chance? | What's P(B beats A)? |
| Output | p-value | Probability |
| Business interpretation | Technical | Intuitive |
| Can stop early | No | Yes |
| Our result | p < 0.05 ✅ | 97.9% ✅ |

Both approaches agree: **Variant B wins.**

---

## 💰 Part 3 — Business Recommendation

### Page 3 — Action Plan
 
<img width="1301" height="736" alt="image" src="https://github.com/user-attachments/assets/855c1df4-449b-43de-bb29-3ab7608e0a74" />

### 🏆 Winner: Variant B — Personalized Subject Line

**Business Impact:**
- Every 10,000 emails sent with Variant B generates **+$1,120 more revenue** than Variant A
- **+9 incremental conversions** per 10,000 sends
- **+4.92 percentage point** improvement in open rate
- Zero additional cost — purely from subject line personalization

### Segment Insights

| Segment | Recommendation |
|---|---|
| VIP | ✅ Switch to Variant B immediately — strongest lift ($0.10 → $0.29 revenue/user) |
| Returning | ✅ Switch to Variant B — solid lift ($0.03 → $0.20 revenue/user) |
| New | ⚠️ Keep Variant A — no significant lift detected |

### Action Plan

| Priority | Action | Segment | Expected Impact |
|---|---|---|---|
| 1 | Roll out Variant B immediately | Returning + VIP | +$1,120/send |
| 2 | Run separate test for New customers | New | TBD |
| 3 | Monitor open rate weekly | All | Detect novelty decay |
| 4 | Re-run full test in 90 days | All | Confirm sustained lift |
| 5 | Extend personalization to SMS | All | Apply learnings |

### Caveats
- ⚠️ Test underpowered for conversion rate — need 392K per variant for definitive result
- ⚠️ New customer segment showed no lift — do not apply Variant B to acquisition campaigns
- ⚠️ Monitor for novelty effect — personalization lift may decay over time
- ⚠️ Consider multivariate test: name + send time + content personalization

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| Python | Primary analysis language |
| pandas / numpy | Data manipulation |
| scipy / statsmodels | Statistical testing |
| matplotlib / seaborn | Data visualization |
| Power BI | Interactive dashboard |

---



## 🔗 Related Projects

👉 [Marketing Mix Modeling with Robyn](https://github.com/azar2020/marketing-mix-modeling-robyn)
👉 [Marketing Performance Dashboard — Power BI](https://github.com/azar2020/marketing-dashboard-powerbi)

---

## 👤 Author

**Azar Taheri**
[LinkedIn](https://linkedin.com/in/azar-taheri) 
