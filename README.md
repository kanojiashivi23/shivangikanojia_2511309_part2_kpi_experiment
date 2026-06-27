# Onboarding & Activation Campaign Evaluation (Part 2)

## 1. Business Problem Statement

### A. Core Decision to be Made
Executive leadership must determine whether to scale and deploy the new user onboarding and activation campaign experience to 100% of all incoming platform registrations, continue running the controlled trial to collect additional data, or reject the treatment and retain the existing baseline onboarding framework.

### B. Impacted Stakeholders
*   **Target Users:** Directly alters the first-time user experience (FTUE) for all future sign-ups, shaping their initial product orientation, activation velocity, and long-term engagement.
*   **Customer Support & Operations:** Affected by changes in support ticket velocity, customer confusion patterns, and immediate processing requests (such as refund loops) resulting from the new onboarding flow.
*   **Product & Growth Marketing Teams:** Impacted regarding future roadmap prioritizations, engineering maintenance, and promotional campaign budget allocations.

### C. Primary Success Metric to Improve
The ultimate objective of this onboarding intervention is to drive a statistically significant increase in the **Paid Conversion Rate (`converted_to_paid`)**, converting a higher percentage of signed-up users into long-term, revenue-generating subscribers.

### D. Operational Risks & Guardrails to Monitor
Optimizing for conversion blindly introduces substantial business risks. The following guardrail metrics must be closely monitored to ensure short-term gains do not degrade overall platform health:
*   **Support Ticket Friction:** Spikes in 30-day support tickets (`support_tickets_30d`) indicating user confusion or technical friction in the new flow.
*   **Financial Reductions:** A significant rise in immediate refund requests (`refund_requested`), which would offset conversion gains and signal low-quality conversions or accidental sign-ups.
*   **Engagement Dilution:** Ensuring that an increase in conversion doesn't pull in low-intent users who drag down overall platform utilization and average product engagement scores (`engagement_score`).

### E. Required Evidence for Recommendation
Before a global rollout recommendation can be finalized, leadership requires the following empirical evidence:
1.  **Statistical Validity:** A rigorous hypothesis test (two-sample proportion test) confirming that the lift in the Paid Conversion Rate is statistically significant, with a $p\text{-value} < 0.05$.
2.  **Guardrail Neutrality or Improvement:** Statistical verification that refund rates and support ticket volumes in the treatment group have not significantly degraded compared to the control group.
3.  **Financial Value Lift:** Empirically higher average 30-day revenue (`revenue_30d`) per user to justify the long-term operational costs of scaling the infrastructure.

## 2. North Star Metric & Measurement Hierarchy

###  Selected North Star Metric: Paid Conversion Rate (`converted_to_paid`)
The primary success metric chosen for this controlled business experiment is the **Paid Conversion Rate**, defined as the percentage of total signed-up users who successfully transition into active, revenue-generating paid subscribers within the observation window.

$$\text{Paid Conversion Rate} = \frac{\text{Total Users Converted to Paid}}{\text{Total Signed-up Users}}$$

---

###  Why This Metric is the Main Success Metric
In a subscription-based digital product company, early operational milestones like opening an app or completing a profile are highly encouraging, but a business cannot achieve long-term viability without monetization. 
* **Customer Validation:** A user transitioning from a free trial to a paid subscription represents the ultimate form of customer validation—it proves that the onboarding campaign successfully demonstrated enough core product value to compel the user to spend their own money.
* **Funnel Efficiency:** It captures the performance of the *entire* onboarding funnel, ensuring that we aren't just moving users through the initial setup steps, but effectively driving them toward the final conversion goal.

---

###  Why Other Metrics are Supporting Metrics Instead
* **`started_trial` and `completed_onboarding` (Upstream Process Indicators):** These are critical behavioral milestones, but they serve as leading metrics rather than final outcomes. A user can complete an onboarding wizard or click "Start Trial" out of curiosity, but if they find no ongoing value, they will drop off before making a payment. Treating them as the North Star can lead to misleading optimization where "completion" spikes but revenue stagnates.
* **`engagement_score` (Internal Proxy):** While high engagement is strongly correlated with customer satisfaction, it is a non-financial proxy. Free-tier users can generate deep engagement patterns without ever generating recurring revenue, which fails to support a commercial subscription growth model.
* **`revenue_30d` (Monetary Scale):** While financial, short-term 30-day revenue can be heavily skewed or distorted by a very small group of high-tier premium buyers. Paid Conversion Rate measures the broad, scalable ability of the onboarding experience to convince the average user to subscribe.

---

###  How This Metric Connects to Business Growth
Optimizing the Paid Conversion Rate directly fuels the core growth engine of a SaaS/subscription business model through a clear economic chain reaction:
1. **Reduces Customer Acquisition Cost (CAC) Payback:** By converting a higher percentage of users from the same incoming traffic volume, the company extracts more value out of its marketing spend, driving down net acquisition costs.
2. **Compounds Monthly Recurring Revenue (MRR):** Higher early conversion expands the broad subscriber baseline, providing more predictable capital to reinvest back into product development.
3. **Maximizes Customer Lifetime Value (LTV):** A strong onboarding experience sets a solid foundation for long-term customer relationships, increasing the total lifetime financial value of each acquired user cohort.

---

###  What Could Go Wrong if Optimized Blindly (The Optimization Trap)
If a team optimizes for the Paid Conversion Rate without reviewing counter-balancing guardrails, it can result in severe structural value destruction:
* **The "Tricked-User" Phenomenon:** The team might implement high-pressure onboarding flows, hidden auto-renewal clauses, or aggressive pop-ups. This artificially forces a spike in short-term conversions, but triggers a massive wave of immediate **refund requests (`refund_requested`)** and customer dissatisfaction.
* **Customer Support Overload:** Confusing or pushy onboarding elements can result in an unmanageable spike in **support tickets (`support_tickets_30d`)**, inflating operational costs and wiping out the profit margins gained from the conversion lift.
* **High Downstream Churn:** Users who are pushed into paying before understanding the core product value will cancel their subscriptions in month two, creating an unsustainable "leaky bucket" business model.

## 3. KPI Tree Architecture

The hierarchical structure below maps out how our operational sub-drivers feed directly into our primary drivers, which ultimately impact the baseline North Star Metric.

```text
               🌟 NORTH STAR METRIC (Tier 0)
         [ Paid Conversion Rate (converted_to_paid) ]
                          │
         ┌────────────────┼────────────────┐
         ▼                                 ▼
   PRIMARY DRIVERS (Tier 1)         🛡️ GUARDRAIL METRICS (Counter-Balancing)
 ├── Onboarding Completion Rate     ├── Avg Support Ticket Volume (support_tickets_30d)
 ├── Trial Activation Rate          ├── Total Refund Requests (refund_requested)
 └── Avg 30-Day Revenue Scale       └── Downstream Post-Trial Unsubscribe Rate
         │
         ▼
   SUB-DRIVERS (Tier 2 Diagnostic Inputs)
   ├── Under Onboarding Completion Rate:
   │    ├── Landing Page Visit Velocity (visited_landing_page)
   │    └── Onboarding Flow Step Retention Rate
   │
   ├── Under Trial Activation Rate:
   │    ├── Feature Adoption Engagement Score (engagement_score)
   │    └── Trial Session Frequency
   │
   └── Under Average 30-Day Revenue Scale:
        ├── Premium Plan Tier Mix Ratio (plan_type splits)
        └── Conversion Velocity Pace (days_to_convert)
  
