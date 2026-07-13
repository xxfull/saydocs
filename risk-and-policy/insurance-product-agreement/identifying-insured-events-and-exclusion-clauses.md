---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/KiKbOTrmqLWnXHD7ZyeJ/feng-xian-yu-zheng-ce/bao-xian-chan-pin-xie-yi/bao-xian-shi-jian-ren-ding-yu-mian-ze-tiao-kuan
---

# Identifying Insured Events and Exclusion Clauses

### How the system identifies an insured event

**Zero Loss Insurance** and **Double Profit Insurance** each attach to one **isolated position**. The system decides whether a policy enters `triggered` by combining trigger conditions, close-reason attribution, and the policy state machine. Key points:

* **Only one primary trigger applies to one close event.** The Zero Loss path and Double Profit path are mutually exclusive for the same position close. See [Trigger conditions](../../insurance/trigger-conditions.md).
* **Trigger price interacts with TP and SL.** Zero Loss logic competes with stop-loss logic. Double Profit logic competes with take-profit logic. The closer effective path takes priority under the product rules.
* **No trigger before expiry means no insurance payout.** The policy can move to `expired`. Premium handling then follows [Refund rules](../../insurance/refund-rules.md).

***

### Exclusions and non-guarantees

The following situations commonly fall into exclusion or non-payout discussions. This list is **not exhaustive**. The formal legal agreement controls.

1. **The position closes before the insurance trigger condition is met**\
   This includes manual full close, a regular TP or SL that fills before the insurance price, or a liquidation that does not follow the Zero Loss payout path. These cases usually end in **cancellation or refund**, not payout.
2. **Fraud, money laundering, or violation of service terms**\
   Abuse of vulnerabilities, market manipulation, sanctions violations, or KYC and AML violations can lead to service refusal or settlement restrictions.
3. **Failures in chain infrastructure or external dependencies**\
   Public-chain congestion, chain reorgs, long oracle failures, and similar events can affect outcomes. Responsibility allocation follows the formal terms and risk disclosures.
4. **The user does not accept the required agreement version**\
   If a new version is required and the user bypasses that requirement, the action can be unsupported or treated as invalid underwriting.
5. **Operational switches and funding capacity**\
   A `triggered` status does **not** always mean funds have already arrived on-chain. If payouts are paused or queued, actual execution timing follows the system state and formal terms.

***

### Related pages

* [Trigger conditions](../../insurance/trigger-conditions.md)
* [List of scenarios not covered by insurance](/broken/pages/Ruh3rBS02nYjnFQg40sF)
