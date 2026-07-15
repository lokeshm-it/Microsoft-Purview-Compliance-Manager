# Reports

This directory is the evidence archive for exported Compliance Manager artifacts.

## Purpose

Compliance Manager reports are point-in-time snapshots — a compliance score, an assessment's progress, or a control's test status can change as remediation continues. This directory models how to preserve those snapshots as durable, date-stamped audit evidence rather than relying solely on live portal state.

## Recommended File Naming Convention

```
<assessment-or-report-type>_<YYYY-MM-DD>.<extension>

Examples:
data-protection-baseline_2026-07-15.pdf
ai-baseline_2026-07-15.pdf
device-compliance-report_2026-07-15.csv
iso-iec-27001-2013-controls_2026-07-15.xlsx
compliance-score-trend_2026-Q2.pdf
```

## Report Types Generated in This Project

| Report | Source | Frequency |
|---|---|---|
| Assessment report (Data Protection Baseline) | Compliance Manager → Assessments → Download as report | End of each remediation sprint |
| Assessment report (AI Baseline) | Compliance Manager → Assessments → Download as report | End of each remediation sprint |
| Device compliance report | Microsoft Intune admin center → Reports → Device Compliance | Monthly |
| Improvement actions export | Compliance Manager → Improvement actions → Export actions | Bi-weekly |
| ISO/IEC 27001:2013 controls export | Compliance Manager → Regulations → ISO/IEC 27001:2013 → Export all | Quarterly, or ahead of audit |

## Handling Sensitive Data

Exported reports may contain tenant-identifying information, user data, or configuration detail not appropriate for a public repository. Before committing any real report export to version control:

- Redact tenant name, domain, and user identifiers
- Remove or mask any IP addresses, device identifiers, or internal hostnames
- Confirm the report does not include personal data subject to regulatory protection

This project's public repository intentionally does not include raw report exports — only the documentation describing the reporting workflow. Treat this directory as a template structure for your own private evidence archive.
