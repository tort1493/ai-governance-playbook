# Data Contract Template

**Dataset / Feed Name:**  
**Owner (Team / Person):**  
**Consumers (Teams / Systems):**  
**Contract Version:** v0.1  
**Last Updated:** YYYY-MM-DD  

---

## 1) Purpose & Intended Use
- **What is this data used for?**
  - Example: model training, inference features, monitoring, reporting
- **Primary user / workflow impacted:**
- **Business outcomes supported (KPIs):**
- **Out-of-scope / prohibited uses:**
  - Example: credit decisioning, employment screening, or any regulated use unless explicitly approved

---

## 2) Data Source & Lineage
- **System of record:**
- **Ingestion method:**
  - batch / streaming / API / file drop
- **Update cadence:**
  - real-time / hourly / daily / weekly
- **Upstream dependencies:**
- **Lineage diagram/link:**
- **Backfill policy:**
  - How historical corrections are handled

---

## 3) Interface & Delivery
- **Delivery format:**
  - Parquet / CSV / JSON / DB table / topic
- **Location / endpoint:**
- **Partitioning:**
- **Schema registry / data catalog link (if any):**
- **SLA / availability:**
  - e.g., 99.5% monthly availability, delivery by 8am ET daily
- **Latency requirement (if streaming):**

---

## 4) Schema (Required)
> Define the *contracted* schema. Any change requires a version bump + consumer notification.

### Fields
| Field Name | Type | Required | Allowed Values / Range | Null Policy | Description |
|---|---|---:|---|---|---|
| example_id | string | ✅ | non-empty | never null | Unique identifier |
| event_ts | timestamp | ✅ | valid ISO | never null | Event timestamp |

### Primary keys
- `example_id`

### Important relationships
- Foreign keys / joins:
- Cardinality notes:

---

## 5) Data Quality Requirements (Guardrails)
### Validations (must pass)
- **Schema checks**
  - No missing required fields
  - Types match contract
- **Uniqueness**
  - Primary key uniqueness for partition/day
- **Range checks**
  - Numeric ranges, timestamps not in future (if applicable)
- **Category checks**
  - Allowed enums only
- **Freshness**
  - Data delivered within SLA window

### Thresholds (examples)
- Missing required fields: **≤ 0.1%**
- Duplicate primary keys: **0 allowed**
- Out-of-range values: **≤ 0.5%**
- Late delivery: **≤ 1 occurrence / month**

### Quality monitoring
- Where are checks implemented? (Great Expectations / pandera / dbt tests)
- Where are results stored? (logs, dashboard)
- Alert channel/on-call:

---

## 6) Change Management
### Versioning rules
- **Patch (v0.1 → v0.1.1):** non-breaking metadata or doc updates
- **Minor (v0.1 → v0.2):** additive non-breaking fields (new optional columns)
- **Major (v0.2 → v1.0):** breaking changes (rename/remove fields, type change)

### Notification process
- Minimum notice period:
  - Minor: **7 days**
  - Major: **30 days**
- Communication channels:
- Consumer sign-off required? (Y/N)

### Deprecation policy
- How long old versions are supported:
- Migration plan template link:

---

## 7) Privacy, Security, and Compliance
### Data classification
- Public / Internal / Confidential / Restricted

### Sensitive data
- PII present? (Y/N)  
  - If yes: list fields + masking approach
- PHI present? (Y/N)
- PCI data present? (Y/N)

### Access controls
- Who can read/write:
- Auth method / IAM roles:
- Encryption at rest/in transit:

### Retention & deletion
- Retention duration:
- Deletion process:
- Audit logging requirements:

---

## 8) Model-Specific Notes (if used for ML)
- **Features derived from this source:**
- **Label definition (if applicable):**
- **Training/inference skew risks:**
- **Expected distribution / seasonality:**
- **Known bias risks / representation gaps:**
- **Drift signals to monitor:**
  - PSI/KL divergence, mean/variance shifts, missingness shifts

---

## 9) Incident Response (When Contract Breaks)
### Severity levels
- **SEV1:** inference blocked, critical business impact
- **SEV2:** partial degradation, workarounds exist
- **SEV3:** minor issues, no immediate impact

### Playbook
1. Confirm scope (which partitions/segments affected)
2. Roll back to last good dataset version (if available)
3. Notify consumers + stakeholders
4. Create incident ticket + owner
5. Postmortem: root cause + prevention actions

### Rollback options
- Restore previous snapshot:
- Hotfix pipeline:
- Disable dependent model feature:

---

## 10) Approvals
- Data Owner:
- Security/Compliance (if needed):
- Consumer Lead:
- Date approved:
