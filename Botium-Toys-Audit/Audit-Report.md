# Botium Toys — Security Audit

> This audit was completed as a hands-on activity for the Google Cybersecurity Professional Certificate (Course 2: Play It Safe — Manage Security Risks, Module 2). Botium Toys is a fictional company used for training purposes; this is not a real client engagement.

**Scope:** Entire security program at Botium Toys, including employee equipment, internal network, systems, and physical assets.

**Goal:** Assess existing controls and compliance posture to identify gaps and improve Botium Toys' security posture.

**Risk score:** 8/10 (high) — driven by missing controls and incomplete compliance adherence.

---

## Controls Assessment Checklist

| Control | In Place? | Explanation |
|---|---|---|
| Least Privilege | No | All employees can access customer data; access needs to be restricted by role. |
| Disaster recovery plans | No | None exist; needed to ensure business continuity after an incident. |
| Password policies | Yes | A policy exists, but requirements are too weak to meet current standards. |
| Separation of duties | No | Not implemented, raising fraud and insider-risk exposure. |
| Firewall | Yes | Filters traffic based on defined security rules. |
| Intrusion detection system (IDS) | No | Not in place; needed to detect intrusions in progress. |
| Backups | No | No backups of critical data exist. |
| Antivirus software | Yes | Installed and monitored regularly. |
| Manual monitoring for legacy systems | Yes | Systems are monitored, but with no fixed schedule or clear intervention process. |
| Encryption | No | Not used; sensitive data is stored/transmitted unprotected. |
| Password management system | No | No centralized system to enforce password requirements. |
| Locks (offices, storefront, warehouse) | Yes | Physical locations are adequately secured. |
| CCTV surveillance | Yes | Installed and functioning. |
| Fire detection/prevention | Yes | Functioning fire alarm and prevention systems in place. |

---

## Compliance Checklist

### PCI DSS
| Best Practice | Adhered To? | Explanation |
|---|---|---|
| Only authorized users access credit card data | No | All employees currently have access. |
| Credit card data stored/processed securely | No | No encryption; broad internal access. |
| Data encryption procedures implemented | No | Not currently used. |
| Secure password management adopted | No | Password policy is weak and unmanaged. |

### GDPR
| Best Practice | Adhered To? | Explanation |
|---|---|---|
| E.U. customer data kept private/secure | No | Lack of encryption undermines this. |
| 72-hour breach notification plan | Yes | Plan exists for notifying E.U. customers. |
| Data properly classified and inventoried | No | Assets are listed but not classified. |
| Privacy policies enforced | Yes | Developed and enforced across the team. |

### SOC (Type 1 / Type 2)
| Best Practice | Adhered To? | Explanation |
|---|---|---|
| User access policies established | No | No least privilege or separation of duties. |
| PII/SPII kept confidential | No | No encryption in place. |
| Data integrity ensured | Yes | Data is consistent, accurate, and validated. |
| Data available to authorized individuals | Yes | Available, though not properly restricted by role. |

---

## Recommendations

Prioritize four gaps with the highest combined risk and compliance exposure: implement encryption for stored and transmitted cardholder data (closes a PCI DSS gap), enforce least privilege and separation of duties (addresses SOC and GDPR access-control gaps), deploy a centralized password management system with a stronger password policy, and establish disaster recovery plans with regular backups. Addressing these would resolve most open gaps and meaningfully lower the current risk score from 8/10.
