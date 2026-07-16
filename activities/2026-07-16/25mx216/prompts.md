# Mission TCS — Prompt Log

Here are the primary prompts used to research, refine, and structure this enterprise SDLC map.

## 1. Defining the Epic and Stories
> **Prompt:**  
> "Act as a Lead Principal Product Manager. I am mapping out a large-scale B2B Enterprise Client Portal. I need to break down our primary Epic (Unified B2B Client Portal) into 5 highly specific Agile user stories. Please estimate each story using Fibonacci story points and justify the estimation based on integration risks and technical complexity."

## 2. Writing Enterprise-Grade Gherkin Criteria
> **Prompt:**  
> "Now act as a Lead QA Automation Engineer. Take the 'User Authentication & RBAC' user story and write 3 exhaustive Gherkin syntax (Given-When-Then) scenarios. Focus on edge cases like MFA bypass prevention, API-level authorization bypass, and session timeouts."

## 3. Designing the Release Pipeline
> **Prompt:**  
> "Generate a Mermaid.js flowchart mapping out a secure enterprise CI/CD pipeline. I want the code to travel from Git Push to production. Ensure there are distinct automated testing blocks (Unit, Linter, Security Scan, E2E playbooks) and a manual product sign-off gate before canary deployment."
