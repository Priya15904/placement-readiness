# Enterprise Client Portal — SDLC & Agile Workflow Mapping

This repository contains the SDLC mapping, Agile sprint planning, and release pipeline design for a large-scale **Enterprise Client Portal**. The portal serves as a secure, unified gateway for B2B clients to manage accounts, view billing, share confidential documents, and access support.

---

## 🎯 1. Epic: Unified Enterprise B2B Client Portal
**Description:** 
As an enterprise client, I want a secure, centralized portal so that I can manage my organization's users, view and pay invoices, share sensitive compliance documents, and communicate with support teams in real time.

### User Stories Break Down

#### 1. User Authentication & Role-Based Access Control (RBAC) [CRITICAL]
*   **As an** Enterprise Client Administrator,
*   **I want to** authenticate securely using Single Sign-On (SSO) and assign granular permissions (Admin, Editor, Viewer) to my team members,
*   **So that** we secure our sensitive corporate data and prevent unauthorized actions.
*   *Estimation:* 8 Story Points (High complexity due to SSO/IdP integration and session management).

#### 2. Secure Document Vault (Secure File Upload & Storage)
*   **As an** Enterprise Client User,
*   **I want to** upload, download, and audit sensitive files in an encrypted storage area,
*   **So that** we can share financial and regulatory documents safely with the account team.
*   *Estimation:* 5 Story Points.

#### 3. Real-Time Billing & Invoicing Dashboard
*   **As an** Enterprise Client Finance Manager,
*   **I want to** view active subscriptions, download past invoices, and pay outstanding balances via credit/ACH,
*   **So that** our account remains active without manual back-and-forth emails.
*   *Estimation:* 5 Story Points.

#### 4. Real-Time Support Ticketing & Live Chat
*   **As an** Enterprise Client User,
*   **I want to** open support tickets, track their resolution status, and chat with technical support,
*   **So that** my operational blockers are resolved with minimal downtime.
*   *Estimation:* 3 Story Points.

#### 5. Custom Notification & Alert Settings
*   **As an** Enterprise Client User,
*   **I want to** configure real-time email, SMS, and in-app notifications for billing updates, document uploads, and ticket status changes,
*   **So that** I stay updated on critical account events without constantly logging in.
*   *Estimation:* 2 Story Points.

---

## 🔒 2. Acceptance Criteria (Most Critical Story: Auth & RBAC)

To guarantee enterprise-grade security, **User Story 1** must meet strict cryptographic, session-handling, and identity-provider rules.

### Scenario 1: Multi-Factor Authentication (MFA) Setup on First Login
*   **Given** a newly invited enterprise user is logging into the portal for the first time,
*   **When** they enter their temporary password,
*   **Then** the system must prompt them to reset their password and register a multi-factor authentication (MFA) device (Authenticator App or SMS).
*   **And** the system must not let them access the dashboard until MFA setup is fully validated.

### Scenario 2: Enforcing Granular RBAC Permissions
*   **Given** a user with the **"Viewer"** role is logged into the portal,
*   **When** they attempt to navigate to the Document Vault upload section or click "Delete Document",
*   **Then** the interface must disable or hide those actions.
*   **And** if they attempt to bypass the UI and make a direct API call, the backend must return a `403 Forbidden` error and log the unauthorized attempt.

### Scenario 3: Session Expiry and Automatic Revocation
*   **Given** an enterprise user has been inactive on the portal for 15 minutes,
*   **When** the 15-minute threshold is reached,
*   **Then** the system must display a 60-second warning countdown.
*   **And** if no action is taken, the session must be automatically terminated, local state cleared, and the user redirected to the login screen with a `Session Expired` notice.

---

## 🚀 3. CI/CD Release Pipeline

This flow represents how a developer's code goes from their local computer into our secure production environment using automated gates.

```mermaid
graph TD
    A[Developer Git Push] --> B[GitHub Pull Request]
    B --> C{CI Pipeline: Automated Gates}
    C -->|Run Unit Tests| D[Vitest / Jest Passes?]
    C -->|Static Analysis| E[ESLint & Prettier Passes?]
    C -->|Security Scan| F[Snyk / Dependabot Passes?]
    
    D -->|Yes| G[Merge PR to 'main']
    E -->|Yes| G
    F -->|Yes| G
    
    G --> H[Staging Deployment]
    H --> I[Automated E2E Tests: Playwright]
    I -->|All Tests Pass| J[Manual Product Owner Verification]
    J -->|Approved| K[Production Deployment via Canary Release]
    K --> L[Prometheus & Grafana Active Monitoring]
