---
status: accepted
---

# Separate PR explanation from read-only two-axis review

Source: [Define code review and pull request completion](https://github.com/wienans/humanlayer-agents/issues/10)

`describe-pr` owns the reviewer-facing PR package: PR creation and refresh, Delivery Ticket and Design Artifact navigation, Delivery Ticket deviation analysis, recorded local verification evidence, and an optional walkthrough. A separate, reusable `code-review` workflow reviews a manually selected `<fixed-point>...HEAD` snapshot through isolated Standards and Spec axes, reports prioritized findings only in the session, and neither reruns verification nor changes code or tracker state; only findings explicitly selected by the human return to `implement`. This separation preserves one implementation authority and avoids turning PR narration, review, or automated merge judgment into competing sources of implementation intent.
