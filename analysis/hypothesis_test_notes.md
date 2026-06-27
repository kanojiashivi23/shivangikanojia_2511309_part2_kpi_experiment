# Statistical Hypothesis Testing Framework & Design Notes

## Hypothesis Test 1: The North Star Metric

*   **Metric Being Tested:** Paid Conversion Rate (`converted_to_paid`)
*   **Metric Type:** Discrete Binary / Proportional ($0 = \text{No Paid Conversion}$, $1 = \text{Converted to Paid}$)
*   **Business Context & Decision Connection:** Leadership needs absolute empirical proof that the new onboarding campaign outperforms the old experience in driving paid subscriptions before deploying it globally. This test determines if the observed lift is a true systemic shift or a product of random sampling variation.

###  Statistical Formulations
*   **Null Hypothesis ($H_0$):** The Paid Conversion Rate of the Treatment group is equal to or less than the Paid Conversion Rate of the Control group. Any observed lift is due to random chance.
    $$H_0: p_{\text{treatment}} \le p_{\text{control}}$$
*   **Alternative Hypothesis ($H_1$):** The Paid Conversion Rate of the Treatment group is strictly greater than the Paid Conversion Rate of the Control group. The new onboarding campaign causes a real, positive performance lift.
    $$H_1: p_{\text{treatment}} > p_{\text{control}}$$

###  Test Parameters & Logic
*   **Test Type:** One-Tailed Two-Sample Proportion Test ($Z\text{-Test}$). 
    *   *Reasoning:* The business objective is explicitly directional—we are testing to confirm a positive improvement ($>$) to justify the engineering and implementation costs of a rollout.
*   **Significance Level ($\alpha$):** $0.05$ ($95\%$ Confidence Level).
*   **Interpretation & Decision Logic:**
    *   If $p\text{-value} < 0.05$, we **Reject the Null Hypothesis ($H_0$)**. We conclude with statistical confidence that the new onboarding flow significantly improves conversion.
    *   If $p\text{-value} \ge 0.05$, we **Fail to Reject the Null Hypothesis ($H_0$)**. The results are statistically inconclusive, and a rollout cannot be recommended on conversion merits alone.
 
*   ##  Hypothesis Test 2: The Primary Funnel Driver

*   **Metric Being Tested:** Onboarding Completion Rate (`completed_onboarding`)
*   **Metric Type:** Discrete Binary / Proportional ($0 = \text{Abandoned Onboarding}$, $1 = \text{Completed Onboarding}$)
*   **Business Context & Decision Connection:** To accept *why* the North Star metric moved, we must evaluate the mechanism. The campaign was explicitly designed to improve activation velocity. This test proves whether the interface updates successfully unblocked user friction during setup.

###  Statistical Formulations
*   **Null Hypothesis ($H_0$):** The Onboarding Completion Rate of the Treatment group is equal to or less than the Onboarding Completion Rate of the Control group.
    $$H_0: p_{\text{treatment}} \le p_{\text{control}}$$
*   **Alternative Hypothesis ($H_1$):** The Onboarding Completion Rate of the Treatment group is strictly greater than the Onboarding Completion Rate of the Control group.
    $$H_1: p_{\text{treatment}} > p_{\text{control}}$$

###  Test Parameters & Logic
*   **Test Type:** One-Tailed Two-Sample Proportion Test ($Z\text{-Test}$).
*   **Significance Level ($\alpha$):** $0.05$ ($95\%$ Confidence Level).
*   **Interpretation & Decision Logic:**
    *   If $p\text{-value} < 0.05$, we **Reject $H_0$**. This confirms the new onboarding layout structurally improves user product-orientation and activation rates.
    *   If $p\text{-value} \ge 0.05$, we **Fail to Reject $H_0$**. Any observed completion changes are mathematically minor and likely due to noise.
 

##  Hypothesis Test 3: The Counter-Balancing Guardrail

*   **Metric Being Tested:** Average 30-Day Support Ticket Volume (`support_tickets_30d`)
*   **Metric Type:** Continuous / Count Variable (Integer $\ge 0$)
*   **Business Context & Decision Connection:** A higher conversion rate is fundamentally risky if it forces users into accidental checkouts or creates massive interface confusion. This test acts as a defensive system check to verify that the Treatment group does not introduce a statistically significant operational support burden.

###  Statistical Formulations
*   **Null Hypothesis ($H_0$):** The average number of support tickets raised by users in the Treatment group is equal to the average number of support tickets raised by users in the Control group.
    $$H_0: \mu_{\text{treatment}} = \mu_{\text{control}}$$
*   **Alternative Hypothesis ($H_1$):** The average number of support tickets raised by users in the Treatment group is different from the average number of support tickets raised by users in the Control group.
    $$H_1: \mu_{\text{treatment}} \neq \mu_{\text{control}}$$

###  Test Parameters & Logic
*   **Test Type:** Two-Tailed Two-Sample Independent $t\text{-Test}$ (assuming unequal variances).
    *   *Reasoning:* We use a two-tailed approach because a change in layout could either create mass confusion (increasing tickets) or streamline common questions (decreasing tickets). We must monitor deviations in both directions.
*   **Significance Level ($\alpha$):** $0.05$ ($95\%$ Confidence Level).
*   **Interpretation & Decision Logic:**
    *   If $p\text{-value} < 0.05$, we **Reject $H_0$**. This mathematically confirms that the new onboarding flow structurally alters customer support dependency. If $\mu_{\text{treatment}} > \mu_{\text{control}}$, the campaign creates a severe operational bottleneck that requires engineering fixes before rolling out.
    *   If $p\text{-value} \ge 0.05$, we **Fail to Reject $H_0$**. This confirms support volume remains safe, stable, and completely neutral across both variations.

