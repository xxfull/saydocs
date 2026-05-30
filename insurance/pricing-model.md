---
description: This page summarizes the economic model behind YesFi insurance.
metaLinks:
  alternates:
    - https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/bao-xian/ding-jia-mo-xing
---

# Pricing model

* **Engine**: A Monte Carlo model estimates risk over the coverage period.
* **Starting price**: The model starts from the current mark price.
* **Ending price**: The model uses the insurance trigger price as the target boundary. The trigger price depends on `trigger_percent`, side, margin, leverage, and related inputs.
* **Payout base**: The payout base depends on the selected payout ratio. The total premium adds relevant fees on top of that base.

***

### Related pages

* [**Products**](products.md)
* [**Policy life cycle**](policy-life-cycle.md)
* [**Trigger conditions**](trigger-conditions.md)
* [**Refund rules**](refund-rules.md)
