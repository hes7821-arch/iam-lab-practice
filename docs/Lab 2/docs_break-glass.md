## Emergency Access (Break-Glass) Strategy

To prevent administrative lockout during cloud identity provider outages, MFA service disruptions, or misconfigured Conditional Access policies, an Emergency Access (Break-Glass) account has been established for the tenant.

### 1. Account Naming & Design
* **User Principal Name:** `emergencyadmin@hes7821gmail515.onmicrosoft.com`
* **Account Type:** Cloud-only (never synced from on-premises AD to avoid sync dependencies).
* **Role Assignment:** Permanently assigned the **Global Administrator** role.
* **Credential Storage:** Uses a high-entropy, 32-character passphrase split across two secure physical locations (e.g., physical safe / encrypted vault).

### 2. Policy Exclusions & MFA Rationale
* **Conditional Access Exclusion:** Explicitly excluded from all current and future Conditional Access (CA) policies, including mandatory MFA and location-based blocking.
* **Rationale:** If an external authentication service, telephony provider, or MFA service experiences a critical outage, standard administrators would be locked out of the tenant. Excluding this emergency account ensures system access remains possible under disaster scenarios.

### 3. Monitoring & Incident Response
* **Audit & Sign-in Alerts:** Configured via Microsoft Entra ID Diagnostic Settings and Log Analytics / Sentinel to trigger an immediate High-Severity alert whenever this UPN logs in.
* **Routine Verification:** Credential validity and exclusion group membership are audited on a bi-annual rotation schedule.