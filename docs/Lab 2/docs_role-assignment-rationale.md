# Role Assignment Rationale & Governance Model

## 1. Role Assignment Justifications
* **David Chen (Help Desk Technician):** Assigned **Helpdesk Administrator**.
  * *Responsibilities:* First-tier support, resetting end-user passwords, and invalidating refresh tokens.
  * *Why Next Role Up Was Excessive:* Assigning *User Administrator* would allow David to delete users, modify user properties across non-admin staff, and reset passwords for limited administrators—exceeding his help desk scope.
* **Alex Mercer (System Administrator):** Assigned **User Administrator**.
  * *Responsibilities:* Onboarding/offboarding staff, managing user properties, creating groups, and handling general user administration.
  * *Why Next Role Up Was Excessive:* Assigning *Global Administrator* provides unrestricted control over tenant settings, billing, domain registration, and security policy modifications, creating an extreme risk of tenant takeover if compromised.
* **Marcus Vance (IT Manager):** Assigned **Reports Reader**.
  * *Responsibilities:* Oversight, auditing compliance, and reviewing sign-in/audit logs.
  * *Why Next Role Up Was Excessive:* Assigning operational admin roles (*User Administrator* or *Global Administrator*) gives write/mutation access. An oversight role only requires read access to directory data and log telemetry.

## 2. Non-Privileged Staffing Baseline
* **12 Standard Users:** Assigned **No Administrative Role**.
* *Rationale:* These accounts perform daily business functions (sales, accounting, operations). Granting administrative privileges violates the Principle of Least Privilege (PoLP). Every extra admin account expands the tenant's attack surface without operational necessity.

## 3. Key Takeaway from Ticket Exercise
The most surprising discovery was that **"resetting a password" is not a single permission**. Permission level depends heavily on the *target account*. Resetting a standard user requires *Helpdesk Administrator*, resetting a limited admin requires *User Administrator*, and resetting a Global Administrator requires *Privileged Authentication Administrator* or another *Global Administrator*. Because changing credentials is a primary privilege escalation vector, resetting an admin's password effectively allows you to become that admin.

## 4. Enterprise Scaling Considerations (500+ Users)
* **Group-Based Role Assignments:** At 500 users, assigning roles individually creates massive management overhead and privilege drift. Roles should be assigned to **Role-Assignable Groups** (requiring Entra ID P1).
* **Free Tier Constraint:** Group-based role assignment was unavailable during this lab because it requires an active Microsoft Entra ID P1 or P2 license.

## 5. Global Admin & Privileged Role Metrics
* **Pre-Lab Baseline:** 1 Global Administrator (Initial Admin).
* **Post-Lab Count:** 2 Global Administrators (Initial Admin + `emergencyadmin` Break-Glass Account).
* **Privileged Role Assignments:** Only **User Administrator** (Alex Mercer) and **Global Administrator** carry Microsoft's `PRIVILEGED` tag. **Helpdesk Administrator** and **Reports Reader** remain non-privileged administrative roles.
* **Microsoft Baseline Alignment:** Keeps active Global Administrators below Microsoft's recommended maximum of 5, while maintaining full break-glass resilience.