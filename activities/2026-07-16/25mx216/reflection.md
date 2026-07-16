This file captures the critical takeaways from planning an enterprise-grade SDLC, identifying potential friction points, and posing thoughtful future questions.

```markdown
# Mission TCS — Reflection

## 💡 What Surprised Me?

1.  **The Breadth of "Role-Based Access Control" (RBAC):**  
    Initially, authentication feels like a straightforward "login/logout" problem. However, breaking down how an *enterprise* handles user hierarchy (where an Admin of Company A can invite users, but Viewers of Company B must have zero write permissions across multiple micro-services) proved that security is the single most complex architectural pillar of a B2B app.
    
2.  **The Importance of "Fail-Secure" Backends:**  
    It's easy to hide buttons in the UI using simple React state (`role === 'admin'`). The real challenge is designing the backend APIs so that even if a clever user sends a spoofed HTTP request (e.g., via Postman or Curl), the API intercepts it and blocks access at the database level.

3.  **Automated Security Gates in CI/CD:**  
    I realized that security cannot be an afterthought left for a monthly audit. Integrating tools like Snyk and automated dependency checks directly into the PR review process prevents vulnerable code from ever reaching the staging environment.

---

## 🙋 What Would I Ask Claude Next?
If I had Claude on my team for the next sprint, I would ask:
*   *"How can we securely manage multi-tenant database isolation (e.g., Database-per-tenant vs. Shared Database with Row-Level Security) for this enterprise client portal?"*
*   *"Can you help me write the boilerplate for our Express/NestJS backend that handles Gherkin-style RBAC validation middleware?"*
*   *"What is the most robust way to implement the token exchange flow when bridging SAML 2.0 / Okta with our React client side?"*
