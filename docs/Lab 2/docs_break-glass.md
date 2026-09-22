# Emergency Access (Break-Glass) Strategy

To prevent administrative lockout during critical tenant outages or emergency scenarios, a dedicated Emergency Access (Break-Glass) account has been established for the tenant.

## 1. What Was Built
* **User Principal Name:** `bg-admin-01@hes7821gmail515.onmicrosoft.com`
* **Account Type:** Cloud-only account (isolated from any on-premises synchronization dependencies).
* **Role Assignment:** Permanently assigned the **Global Administrator** role.
* **Authentication & Credential Storage:** Uses a high-entropy, 32-character passphrase split across two secure physical locations (e.g., physical safe / encrypted vault). 
* **MFA Enforcement:** Secured using phishing-resistant multi-factor authentication (such as a hardware FIDO2 security key stored in a physical vault).

## 2. Emergency Monitoring & Auditing
* **Audit & Sign-In Alerts:** Directory logs are monitored via Entra ID Diagnostic Settings / Sentinel to fire a High-Severity alert immediately whenever this account initiates a sign-in session.
* **Routine Audits:** Credential validity and account readiness are tested on a scheduled bi-annual rotation.

## 3. Future To-Do List (Requires Entra ID P1 / P2)
* **Conditional Access Policy Exclusions:** Once upgraded to Entra ID P1, explicitly exclude `bg-admin-01` from all broad Conditional Access policies (such as location-based blocks) to prevent lockouts during policy misconfigurations.
* **Hardware FIDO2 Backup Key:** Provision a secondary FIDO2 hardware security key registered as an alternate authentication factor for the break-glass account.
