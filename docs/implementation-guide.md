# Implementation Guide — Microsoft Purview Compliance Manager

This guide documents the end-to-end deployment and operational configuration of Microsoft Purview Compliance Manager, from prerequisites through validation, as implemented in this project.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Licensing](#licensing)
- [Required Roles](#required-roles)
- [Navigation](#navigation)
- [Configuration](#configuration)
- [Creating Assessments](#creating-assessments)
- [Using Built-in Templates](#using-built-in-templates)
- [Reviewing Compliance Score](#reviewing-compliance-score)
- [Monitoring Improvement Actions](#monitoring-improvement-actions)
- [Viewing Regulations](#viewing-regulations)
- [ISO/IEC 27001 Assessment](#isoiec-27001-assessment)
- [Downloading Reports](#downloading-reports)
- [Reviewing Microsoft Actions](#reviewing-microsoft-actions)
- [Validation](#validation)
- [Verification](#verification)
- [Expected Results](#expected-results)

---

## Prerequisites

- An active Microsoft 365 tenant with Microsoft Purview compliance portal access
- A Microsoft 365 E3/E5, Microsoft 365 A3/A5, or equivalent license that includes baseline Compliance Manager capability (Data Protection Baseline is included at no additional cost)
- Microsoft Intune enrollment for device compliance reporting scenarios
- Microsoft Entra ID as the tenant's identity provider (Conditional Access, MFA, and sign-in risk actions depend on Entra ID)
- Network and browser access to `compliance.microsoft.com` (Microsoft Purview compliance portal)

## Licensing

Compliance Manager's **Data Protection Baseline** and **AI Baseline** assessments are included with qualifying Microsoft 365 licensing at no additional cost. Additional regulatory templates ("Premium templates" and "Premium AI templates") require **regulation licenses**, tracked on the Regulations page as:

- **Free regulation licenses used** — no-cost allotment, if applicable to the tenant's licensing agreement
- **Purchased regulation licenses used** — licenses procured specifically to activate premium regulation templates (this tenant has 3 purchased licenses available)

Review current license consumption before activating any new premium regulation to avoid unexpected procurement needs.

## Required Roles

Compliance Manager uses Microsoft Purview role-based access control (RBAC). At minimum, the following roles are required depending on the activity:

| Activity | Minimum Role |
|---|---|
| View Compliance Manager dashboards | Compliance Manager Reader |
| Create/edit assessments | Compliance Manager Assessor or Compliance Manager Administrator |
| Assign improvement actions | Compliance Manager Contributor |
| Activate regulations / manage licenses | Compliance Manager Administrator |
| Access linked admin centers (Intune, Entra) for evidence generation | Role appropriate to that admin center (e.g., Intune Administrator) |

Assign roles through **Microsoft Purview compliance portal → Permissions**, following least-privilege principles — most control owners only need Contributor-level access to update their assigned improvement actions.

## Navigation

Compliance Manager is accessed from the Microsoft Purview compliance portal left-hand navigation:

```
Microsoft Purview → Compliance Manager
    ├── Overview
    ├── Improvement actions
    ├── Solutions
    ├── Assessments
    ├── Regulations
    ├── Policies
    ├── Alerts
    └── Reports
```

## Configuration

1. Sign in to the Microsoft Purview compliance portal with an account holding the Compliance Manager Administrator role
2. Navigate to **Compliance Manager**
3. Review the **Overview** page to confirm the tenant's starting compliance score and baseline data (in this implementation: 59% overall)
4. Configure **Groups** if the organization needs to scope assessments by business unit or subsidiary (this implementation uses the tenant's Default Group)

## Creating Assessments

1. Navigate to **Compliance Manager → Assessments**
2. Select **+ Add assessment**
3. Choose a regulation template from the catalog (e.g., Data Protection Baseline, AI Baseline, or any activated premium template)
4. Assign the assessment to a Group and confirm the applicable Service (Microsoft 365, Azure, or both)
5. Confirm creation — the assessment populates automatically with the improvement actions and Microsoft actions defined by the template

## Using Built-in Templates

This implementation used two built-in, no-additional-cost templates:

- **Data Protection Baseline for Microsoft 365** — a broad baseline covering identity, device, and data protection controls
- **AI Baseline** — a template addressing responsible AI governance controls relevant to AI-powered Microsoft 365 features

Built-in templates require no regulation license and are the recommended starting point before activating premium regulations.

## Reviewing Compliance Score

1. Navigate to **Compliance Manager → Overview**
2. Review the **Overall compliance score** gauge and the **Your points achieved** / **Microsoft managed points achieved** breakdown
3. Use the **Key improvement actions** table to identify the highest-impact unresolved actions
4. Drill into an individual assessment (**Assessments → [assessment name]**) for a scoped progress view

## Monitoring Improvement Actions

1. Navigate to **Compliance Manager → Improvement actions**
2. Apply filters: **Regulations, Solutions, Groups, Test Status, Categories, Testing type, Service, Role type, Service Instances**
3. Sort by **Point value** (descending) to prioritize high-impact actions
4. Open an individual action to review **Details, Evidence,** and **Related controls** tabs
5. Update **Owner** and **Implementation status**; attach evidence before marking an action complete
6. Use **Export actions** to produce a point-in-time CSV/Excel export for offline tracking or GRC platform ingestion

## Viewing Regulations

1. Navigate to **Compliance Manager → Regulations**
2. Browse or search the catalog (391 items in this implementation), grouped by **Sub-Service Compliance Readiness, Included templates, Premium AI templates,** and **Premium templates**
3. Select a regulation to view its **All actions** and **All controls** detail
4. Use **Create new template** to build a custom assessment template if no built-in regulation matches an internal policy requirement

## ISO/IEC 27001 Assessment

1. From **Regulations**, select **ISO/IEC 27001:2013**
2. Review **All controls** (233 items), grouped by **Control Family** (e.g., Access Control)
3. Review **All actions → Your actions** for organization-owned remediation items
4. Review **All actions → Microsoft actions** (347 items) for Microsoft/Azure Control Framework actions already satisfied
5. If not already active, create a dedicated assessment against this regulation from the **Assessments** page to begin tracking implementation and test status against each control

## Downloading Reports

1. From within an assessment, select **Download as report** (top-right of the assessment detail page)
2. For device compliance-specific evidence, use the **Launch Now** link on the relevant improvement action to open **Microsoft Intune admin center → Reports → Device Compliance**, then select **Generate report**
3. Store exported reports in a version-controlled evidence archive (see this repository's `reports/` directory) with a clear date-stamped filename convention, e.g., `data-protection-baseline_2026-07-15.pdf`

## Reviewing Microsoft Actions

1. Within any assessment or regulation, select the **Microsoft actions** tab
2. Review completion status — Microsoft actions are typically already completed and require no organizational effort, but should still be periodically spot-checked against Microsoft's published audit reports
3. Cross-reference Microsoft actions against their paired customer actions to confirm no control gap exists at the shared-responsibility boundary

## Validation

- Confirm the Overview dashboard compliance score matches the sum of active assessment progress, weighted by points
- Confirm every high-priority improvement action has an assigned **Owner**
- Confirm evidence is attached to any improvement action marked **Implemented**

## Verification

- Spot-check a sample of "Passed" test status actions against their attached evidence to confirm the test status is substantiated, not self-attested without proof
- Verify regulation license consumption matches expected procurement (e.g., 0/3 purchased licenses used, confirming headroom for future activations)
- Verify RBAC role assignments align with the least-privilege model defined in [Required Roles](#required-roles)

## Expected Results

Upon completing this implementation, the tenant should reflect:

- An active, measurable **compliance score** visible on the Overview dashboard
- At least one active **assessment** (Data Protection Baseline recommended as the starting point) with a defined progress percentage
- A filterable, exportable **improvement actions** register with assigned owners and current test statuses
- A reviewed **Regulations** catalog with license consumption understood and premium templates activated only where relevant
- For organizations pursuing ISO/IEC 27001 certification: a fully reviewed control and Microsoft action mapping under the ISO/IEC 27001:2013 regulation entry
- At least one exported **compliance report** stored as audit-ready evidence
