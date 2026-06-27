# Product Onboarding Experimentation & KPI Optimization Framework

##  1. Business Context
This project evaluates the performance of a newly designed user activation and onboarding campaign versus our legacy configuration. The ultimate objective is to streamline product onboarding velocity, decrease early lifecycle friction, and increase conversion to long-term paid subscriptions.

---

##  2. Dataset Description
The underlying core data represents a 30-day longitudinal user sample containing experimental logs for 1,400 unique customer records following automated data deduplication. Each record monitors top-of-funnel movement, platform engagement score attributes, financial transaction flags, and support desk data points.

---

##  3. North Star Metric Selected
The primary business compass is the **Paid Conversion Rate** (`converted_to_paid`). This metric directly establishes the link between early user activation and core recurring revenue generation.

---

##  4. KPI Tree Summary
Our core performance drivers map out as an interconnected tracking framework:
*   **Level 1 (North Star Metric):** Paid Conversion Rate
*   **Level 2 (Funnel Components):** Landing Page Visit Rate $\rightarrow$ Trial Start Rate $\rightarrow$ Onboarding Completion Rate.
*   **Level 3 (Guardrail Metrics & Quality Filters):** Average Support Tickets (30d), Refund Requested Rate, and Average Engagement Score.

---

##  5. Experiment Analysis Approach
Raw experimental logs were aggregated, cleaned, and evaluated using an analytical structure inside Excel:
*   **Deduplication:** Dropped 8 exact duplicate user rows, retaining a clean 1,400 user profile base.
*   **Imputation:** Missing text variables (`device_type`, `traffic_source`) were categorized as `"Unknown"`. Missing numeric engagement layers were imputed safely using cohort group means.
*   **Segmentation:** Segmented data by region, device type, and acquisition channel to uncover hidden variances.

---

##  6. Hypothesis Test Summary
*   **Metric:** Paid Conversion Rate
*   **Framework:** One-Tailed Two-Sample Proportions $Z\text{-test}$ ($\alpha = 0.05$).
*   **Results:** Control Conversion = 3.17%, Treatment Conversion = 6.99%. 
*   **Statistical Evidence:** Observed $Z\text{-Score} = 3.2519$, One-Tailed $p\text{-value} = 0.000573$.
*   **Outcome:** Reject Null Hypothesis. The absolute performance lift of $+3.82\%$ is highly statistically significant with $>99.9\%$ confidence.

---

##  7. Guardrail Metrics Considered
To ensure platform safety, three defensive metrics were cross-referenced:
*   **Average Support Tickets (30 Days):** Rose from 0.22 to 0.37 (+0.15). *Identified as an operational support queue volume risk (+68.1% relative increase).*
*   **Refund Requested Rate:** Safely hovered at 0.42% for the Treatment variation, passing financial viability checks.
*   **Average Engagement Score:** Expanded significantly from 57.03 to 62.94 (+5.91 points), confirming post-conversion quality.

---

##  8. Final Recommendation
**Launch Globally with Targeted Support Planning.** Route 100% of live traffic to the new onboarding layout immediately due to the massive conversion double and engagement spikes. However, hold back the `Social Media` traffic subset for design adjustments, as it underperformed baseline conversion rules (dropping from 7.75% to 6.06%).

---

##  9. Assumptions and Limitations
*   **Assumptions:** Assumes stable product pricing profiles and no platform server outages during the 30-day testing window.
*   **Limitations:** The experiment uncovered a notable relative increase (+68.1%) in customer support queue velocity, creating an operational bottleneck that must be managed. 

---

##  10. Screenshots Included
The verification artifacts are mapped across the tracking paths below:
*   `screenshots/summary_metrics.png`: Captures the `Guardrail Metrics Analysis` performance sheet dashboard.
*   `screenshots/hypothesis_test_output.png`: Captures the manual calculation validation matrix and final decision rules.
*   `screenshots/kpi_tree_preview.png`: Provides a visual look at our behavioral tree tracking nodes.

