# Assessment Guide — Data Protection Baseline for Microsoft 365

## Overview

The Data Protection Baseline for Microsoft 365 is a built-in, no-additional-license Compliance Manager assessment covering foundational identity, device, and data protection controls for a Microsoft 365 tenant. It is the recommended starting assessment for any organization beginning a Compliance Manager implementation.

## Observed Configuration

| Metric | Value |
|---|---|
| Status | In progress |
| Overall progress | 61% |
| Total points achieved | 13,262.39 / 21,759 |
| Your (customer-managed) improvement actions completed | 36 of 489 |
| Your points achieved | 937 / 9,301 |
| Microsoft actions completed | 729 of 734 |
| Microsoft managed points achieved | 12,345 / 12,438 |
| Assigned Group | Default Group |
| Service | Microsoft 365 |

## Assessment Structure

The assessment detail page is organized into four tabs:

1. **Progress** — narrative summary of completion percentage and points achieved, plus a breakdown of key improvement actions by test status (Passed, Failed – Low Risk, Failed – Medium Risk, Failed – High Risk, Not Assessed)
2. **Controls** — the regulatory controls this assessment maps to, each traceable back to the underlying improvement actions that satisfy it
3. **Your improvement actions** — the 489 customer-managed actions requiring organizational configuration
4. **Microsoft actions** — the 734 Microsoft-managed actions, of which 729 are already completed

## Representative Improvement Actions Observed

| Action | Point Impact | Test Status |
|---|---|---|
| Govern global administrative roles | +27 | Not assessed |
| Turn on email scanning for antivirus solution | +27 | Failed – high risk |
| Use boundary protection to limit access to services based on the... | +27 | Not assessed |
| Enable SMB client to communicate with an SMB server that performs... | +27 | Failed – high risk |
| Enable software installation policies on macOS devices | +27 | Not assessed |

## Working This Assessment

1. Start with the **Progress** tab to understand the current risk distribution across test statuses
2. Filter **Your improvement actions** to `Test status: Failed – high risk` and work these first
3. Cross-reference each action against the **Controls** tab to understand which regulatory requirement it satisfies — this becomes the audit trail
4. Use **Microsoft actions** to confirm shared-responsibility coverage; only 5 of 734 Microsoft actions remain incomplete in this tenant, so effort should be concentrated on the customer-managed side
5. Export the assessment as a report (**Download as report**) at the end of each remediation cycle to preserve a dated progress snapshot

## Why This Assessment Matters

The Data Protection Baseline is intentionally broad — it is not tied to a single regulatory body but instead reflects a general-purpose data protection posture aligned with widely recognized security best practices. Because it requires no additional licensing, it is the fastest path to establishing a measurable compliance score and is typically the assessment referenced first when demonstrating program maturity to leadership.
