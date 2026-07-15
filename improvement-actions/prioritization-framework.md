# Improvement Action Prioritization Framework

## Purpose

With 500 improvement actions tracked across this tenant, an unstructured approach to remediation quickly becomes unmanageable. This framework documents the prioritization logic applied throughout this project to convert a flat 500-item list into an ordered, workable remediation program.

## Prioritization Criteria (in order of precedence)

1. **Test status** — `Failed – High Risk` actions are addressed before `Failed – Low/Medium Risk`, which are addressed before `Not Assessed` actions
2. **Ownership type** — Customer-managed actions are prioritized over Microsoft-managed actions, since Microsoft-managed actions require no organizational effort and are typically already complete
3. **Point value** — Among actions of equal test status and ownership type, higher point-value actions are worked first (most technical actions in this tenant carry a +27 point weight)
4. **Category** — Identity and access control actions (MFA, legacy authentication, privileged access) are prioritized ahead of device compliance actions, which are prioritized ahead of data governance actions, reflecting typical attack-path likelihood
5. **Action type** — Technical actions are generally faster to remediate than Operational actions (which often require policy or process change) and are sequenced accordingly within a sprint, though both are tracked in parallel

## Working Backlog Segmentation

| Segment | Filter Criteria | Cadence |
|---|---|---|
| **Sprint Now** | Test status: Failed – High Risk AND Ownership: Customer-managed | Bi-weekly sprint |
| **Sprint Next** | Test status: Failed – Low/Medium Risk AND Ownership: Customer-managed | Following sprint |
| **Assess** | Test status: Not Assessed | Assign owner, schedule testing |
| **Monitor** | Test status: Passed | Periodic reassessment (quarterly) |
| **Verify Only** | Ownership: Microsoft-managed | Spot-check against Microsoft audit reports |

## Sample Prioritized Actions (Observed in This Tenant)

Based on the criteria above, the following actions from the Overview dashboard's "Key improvement actions" table represent the top of the working backlog — all customer-managed, all +27 points, all failing high risk:

1. Protect against potentially unwanted applications
2. Enable multi-factor authentication for admins
3. Control data by restricting access to cloud service providers
4. Deny account elevation requests from standard user accounts
5. Disable basic authentication for remotely managed clients
6. Require additional authentication at startup
7. Detect and remediate risky sign-ins
8. Disable the local storage of passwords and credentials
9. Enable multi-factor authentication for non-administrative users
10. Block legacy authentication

## Anti-Patterns to Avoid

- **Alphabetical or list-order remediation** — working the backlog in default UI order ignores risk weighting entirely and produces slow, low-impact progress
- **Bulk-accepting updates without verification** — inflates the compliance score without a genuine risk-reduction outcome and creates false audit evidence
- **Treating Microsoft-managed actions as work items** — these require no organizational action; time spent reviewing them should be limited to periodic verification, not active remediation effort
- **Ignoring "Not Assessed" actions indefinitely** — an unassessed control is not a passed control; it is unmeasured risk and should be scheduled for testing, not left in permanent limbo

## Measuring Prioritization Effectiveness

Track **customer-managed point velocity** (points gained per sprint from customer-managed actions specifically) as the primary success metric, rather than overall compliance score movement — overall score can mask stagnant customer-managed progress behind Microsoft-managed point growth that requires no organizational effort.
