# Microsoft Entra ID: Least Privilege & Admin Roles Lab

## Project Overview
This project demonstrates the design, deployment, and testing of a least-privilege Role-Based Access Control (RBAC) architecture for a 16-person organization in Microsoft Entra ID. The environment enforces strict administrative boundaries, establishes emergency break-glass procedures, and audits administrative role assignments.

## Business Scenario
Northwind Services required delegated administrative roles for helpdesk operations, user management, and IT oversight without over-provisioning tenant-wide permissions. The identity strategy enforces the Principle of Least Privilege (PoLP) to minimize the attack surface and limit potential lateral movement or privilege escalation in the event of account compromise.

## Tools Used
* **Identity Platform:** Microsoft Entra ID (Free Tier)
* **Authentication:** Microsoft Authenticator (MFA)
* **Source Control:** Git & GitHub

## What I Built
* **Delegated Role Matrix:** Assigned scoped roles to key personnel (**Helpdesk Administrator** to David Chen, **User Administrator** to Alex Mercer, and **Reports Reader** to Marcus Vance).
* **Non-Privileged Baseline:** Maintained zero administrative roles for 12 standard organizational accounts.
* **Access Boundary Validation:** Tested and verified explicit permission blocks by signing in as a scoped administrator and attempting unauthorized actions.
* **Emergency Access Strategy:** Deployed an emergency Global Administrator account with documented policy exclusion frameworks.
* **Audit Trail Verification:** Validated directory audit logs tracking administrative role changes.

## Documentation Deliverables
* [Ticket Exercise](docs/lab2/ticket-exercise.md)
* [Role Assignment Rationale](docs/lab2/role-assignment-rationale.md)
* [Break-Glass Strategy](docs/lab2/break-glass.md)

## Key Screenshots
* [Boundary Block Error](screenshots/lab2/action-blocked-boundary.png)
* [Audit Log Role Assignments](screenshots/lab2/audit-log-role-assignment.png)
* [Alex Mercer Role Confirmation](screenshots/lab2/role-assignment%201-confirmation.png.png)
* [David Chen Role Confirmation](screenshots/lab2/roles-assignment%202-confirmation.png.png)
* [Marcus Vance Role Confirmation](screenshots/lab2/roles-assignment%203-confirmation.png.png)
* [Privileged Labels View 1](screenshots/lab2/roles-privileged-label%201.png)
* [Privileged Labels View 2](screenshots/lab2/roles-privileged-label%202.png)

## Security Lessons Learned
* **Least Privilege Limits Blast Radius:** Least privilege is not about distrusting employees; it is about limiting how far a single compromised account can go. An assistant with a narrow password-reset role getting phished is an isolated incident. A Global Administrator getting phished is a full tenant takeover, extending across attached cloud infrastructure.
* **Permissions Depend on the Target:** "Resetting a password" is not a monolithic permission—it splits into distinct privilege levels depending on the target account. Resetting a standard user requires *Helpdesk Administrator*, resetting a limited admin requires *User Administrator*, and resetting a Global Admin requires *Privileged Authentication Administrator*. Any permission that allows changing authentication factors represents a direct privilege escalation vector.

## Future Improvements
* **Role-Assignable Groups:** Shift from direct user assignments to group-based role assignments (requires Entra ID P1).
* **Just-In-Time (JIT) Access:** Implement Privileged Identity Management (PIM) so administrative rights are activated on-demand rather than held permanently (requires Entra ID P2).
* **Administrative Units:** Scope regional or department administrators using Administrative Units (requires Entra ID P1).
* **Access Governance:** Conduct automated, periodic access reviews on administrative role holders (requires Entra ID Governance).
* **Phishing-Resistant MFA:** Implement FIDO2 hardware security keys for emergency break-glass accounts.
