# Architecture — Microsoft Purview Compliance Manager

## High-Level Flow

```mermaid
flowchart TD
    A[Users] --> B[Microsoft 365 Tenant]
    B --> C[Microsoft Purview Compliance Manager]
    C --> D[Assessments]
    D --> E[Improvement Actions]
    E --> F[Regulations]
    F --> G[Microsoft Managed Controls]
    G --> H[Customer Managed Controls]
    H --> I[Compliance Reports]
    I --> J[Compliance Score]

    style A fill:#0078D4,color:#fff
    style B fill:#0078D4,color:#fff
    style C fill:#5C2D91,color:#fff
    style D fill:#107C10,color:#fff
    style E fill:#107C10,color:#fff
    style F fill:#D83B01,color:#fff
    style G fill:#FFB900,color:#000
    style H fill:#FFB900,color:#000
    style I fill:#008272,color:#fff
    style J fill:#008272,color:#fff
```

## Detailed Component Interaction

```mermaid
flowchart LR
    subgraph Identity["Identity Layer"]
        Entra[Microsoft Entra ID]
    end

    subgraph Endpoint["Endpoint Layer"]
        Intune[Microsoft Intune]
    end

    subgraph Protection["Threat Protection Layer"]
        Defender[Microsoft Defender]
    end

    subgraph Data["Data Layer"]
        M365[Exchange / SharePoint / Teams]
    end

    subgraph Purview["Microsoft Purview Compliance Portal"]
        CM[Compliance Manager]
        Assess[Assessments]
        IA[Improvement Actions]
        Reg[Regulations Catalog]
    end

    Entra --> CM
    Intune --> CM
    Defender --> CM
    M365 --> CM

    CM --> Assess
    Assess --> IA
    Assess --> Reg
    IA --> Score[Compliance Score]
    Reg --> Score

    IA -- Launch Now --> Intune
    IA -- Launch Now --> Entra
```

## Shared Responsibility Model

```mermaid
flowchart TB
    subgraph MS["Microsoft Managed"]
        M1[Physical Datacenter Security]
        M2[Platform Encryption at Rest/Transit]
        M3[Network Backbone Segmentation]
        M4[Independent Audits — SOC 2, ISO 27001, FedRAMP]
    end

    subgraph CUST["Customer Managed"]
        C1[Identity & Access — MFA, Conditional Access]
        C2[Device Compliance Policies]
        C3[Data Loss Prevention Rules]
        C4[Information Protection Labels]
    end

    MS --> Score[Blended Compliance Score]
    CUST --> Score
```

## Component Descriptions

| Component | Role |
|---|---|
| **Microsoft Entra ID** | Identity provider; source for MFA, Conditional Access, privileged role, and sign-in risk signals |
| **Microsoft Intune** | Endpoint management; source for device compliance policy state and reporting |
| **Microsoft Defender** | Threat protection; source for antivirus, endpoint detection, and threat-related improvement actions |
| **Microsoft 365 workloads (Exchange, SharePoint, Teams)** | Data layer; source for data protection, DLP, and information governance signal |
| **Compliance Manager** | Central orchestration and scoring engine within the Microsoft Purview compliance portal |
| **Assessments** | Tenant-scoped instances of regulation templates, tracking progress against a defined control set |
| **Improvement Actions** | Individual, ownable, testable tasks that satisfy assessment controls |
| **Regulations Catalog** | The full library of available regulation templates (391 items in this implementation) |
| **Compliance Score** | The point-weighted aggregate measurement combining Microsoft-managed and customer-managed achievement |

## Data Flow Summary

1. Signal originates in the underlying Microsoft 365 services (Entra ID, Intune, Defender, and core workloads)
2. Compliance Manager ingests this signal to automatically test improvement actions where possible (automated testing type) or await manual verification (manual testing type)
3. Test results roll up into assessment progress, scoped to the regulation template each assessment was created from
4. Assessment progress rolls up further into the tenant-wide compliance score, split between Microsoft-managed and customer-managed point achievement
5. Reports can be generated at any level of this hierarchy — a single improvement action's evidence, a full assessment snapshot, or the overall compliance score trend — for audit and governance consumption
