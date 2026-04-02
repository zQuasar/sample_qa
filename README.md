# QA/QE Work Guidelines

## Overview

This document outlines the QA/QE engagement model, scope definitions, tier responsibilities, and requirements for requesting testing support. **Anyone requesting testing — developers, teams, or stakeholders — is considered a customer and must meet the requirements defined below before QE engagement begins.**

---

## Customer Requirements (Pre-Engagement)

The following must be satisfied by the requesting team prior to any QA/QE engagement. These are non-negotiable gates.

### Access & Enablement
- Provision all necessary access: environment URLs, credentials, VPN, API keys, platform tools
- Confirm prerequisites are met (stable environment, CI/CD access, tooling setup)
- Provide onboarding documentation or a runbook for QE ramp-up

### Test Cases & Test Plans
- Provide or collaborate on test cases covering expected behavior, edge cases, and regression scope
- A completed test plan (see [Sample Test Plan Template](#sample-test-plan-template)) must accompany the request

### Acceptance Criteria & Goals
- Acceptance criteria documented per feature/ticket in Jira, Confluence, or an agreed-upon MD page
- Clear definition of done (DoD) and exit criteria established before testing begins
- Success metrics defined and aligned with stakeholders

### KT Sessions & Handoffs
- Knowledge transfer (KT) session scheduled before testing begins
- Architectural overview, flow diagrams, or sequence documentation provided
- A designated point of contact from the requesting team identified for the duration of the testing cycle

---

## Scope 1: Dev + QA

> **Applies when:** QE owns or contributes to development work required to enable or support testing.

This scope covers scenarios where QE is an active contributor to the development lifecycle — building automation, creating self-service tooling, or embedding directly into dev workflows.

---

### Tier 1 — Test Automation (QE-Owned)

**Description:** QE designs, builds, and maintains automated test suites integrated into the development pipeline.

| | |
|---|---|
| **Ownership** | QE |
| **Trigger** | Feature complete or dev-ready signal from engineering |
| **Deliverable** | Automated test suite (unit, integration, E2E) |
| **Handoff In** | Stable build, test environment, acceptance criteria, test data |
| **Handoff Out** | Test results, pass/fail report, coverage metrics, defect log |

**Dev Requirements:**
- Stable, deployable build available in a test environment
- Test data setup or seed scripts provided
- API contracts or schema documentation shared
- PR or branch details scoped to the feature under test

---

### Tier 2 — Manual Test Execution (QE-Assisted Dev)

**Description:** QE executes manual tests alongside dev cycles — exploratory, regression, or sprint-based.

| | |
|---|---|
| **Ownership** | QE (with Dev collaboration) |
| **Trigger** | Sprint milestone, feature flag enabled, or UAT gate |
| **Deliverable** | Executed test cases, bug reports, go/no-go recommendation |
| **Handoff In** | Deployment confirmation, test plan, known issues list |
| **Handoff Out** | Test execution report, Jira defect tickets, sign-off or escalation |

**Dev Requirements:**
- Confirmed deployment to test environment before QE engagement
- List of impacted areas and regression scope documented
- Known limitations or in-progress items explicitly noted

---

### Tier 3 — Self-Service Automation (QE-Built Tooling for Dev)

**Description:** QE builds scripts, pipelines, or automation utilities that allow developers to self-serve testing without direct QE involvement.

| | |
|---|---|
| **Ownership** | QE (builds) / Dev (operates) |
| **Trigger** | Recurring dev testing need or repetitive manual testing pattern identified |
| **Deliverable** | Reusable scripts, CI pipeline steps, or test harness with runbook |
| **Handoff In** | Use case definition, target environments, input/output expectations |
| **Handoff Out** | Documented tooling, runbook, onboarding session, maintenance plan |

**Dev Requirements:**
- Clear, scoped use case provided before QE begins building
- Access to target environments and CI/CD pipelines granted
- Feedback loop established for iteration and validation

---

## Scope 2: QA/QE (Validation & Testing)

> **Applies when:** QE operates strictly in a validation and testing capacity from the customer/end-user perspective.

This scope covers structured QE-led testing across three tiers.

---

### Tier 1 — Infrastructure Testing

**Description:** Validation of the underlying infrastructure — environments, networking, configurations, and platform reliability.

| | |
|---|---|
| **Ownership** | QE (validation) / Infra & DevOps (remediation) |
| **Trigger** | New environment provisioning, infrastructure changes, or pre-release gates |
| **Deliverable** | Environment health report, configuration validation, readiness sign-off |
| **Handoff In** | Environment URLs, configs, runbooks, credentials, and access |
| **Handoff Out** | Readiness report, open issues list, go/no-go for Tier 2 |

**Dev/Infra Requirements:**
- Environment must be provisioned and stable before QE engagement
- Network, DNS, and service dependencies documented
- Infrastructure-as-code (IaC) or configuration documentation provided

---

### Tier 2 — Application Testing

**Description:** Functional, regression, integration, and exploratory testing of the application from an end-user perspective.

| | |
|---|---|
| **Ownership** | QE |
| **Trigger** | Feature complete, sprint end, or release candidate |
| **Deliverable** | Full test execution report, defect log, regression coverage summary |
| **Handoff In** | Release notes, test plan, acceptance criteria, build details |
| **Handoff Out** | Signed-off test report, Jira defect tickets, regression baseline update |

**Dev Requirements:**
- Feature-complete build deployed to QE environment
- Release notes or changelog provided
- Acceptance criteria documented per story/ticket in Jira or Confluence
- Regression scope defined — what changed, what is at risk

---

### Tier 3 — App Deployment Testing

**Description:** Validation of the application through the deployment process — smoke tests, rollout verification, and post-deploy health checks.

| | |
|---|---|
| **Ownership** | QE (validation) / DevOps & Engineering (deployment) |
| **Trigger** | Production or staging deployment event |
| **Deliverable** | Deployment validation report, smoke test results, rollback recommendation if applicable |
| **Handoff In** | Deployment plan, target environment details, rollback procedure, monitoring links |
| **Handoff Out** | Go/no-go signal, deployment health summary, post-deploy issue log |

**Dev/DevOps Requirements:**
- Deployment plan and timeline shared in advance with QE
- Rollback procedure documented and verified
- Monitoring and alerting configured (dashboards, logs, alerts) prior to deployment
- Smoke test criteria or checklist agreed upon before deployment begins

---

## Appendix

### Sample Test Plan Template

```
Test Plan: [Feature / Project Name]
Created By: [QE Name]
Date: [Date]
Version: v1.0

─────────────────────────────────────────
1. Scope
   In Scope:   [Features/components being tested]
   Out of Scope: [Explicit exclusions]

2. Objectives
   - [Goal 1]
   - [Goal 2]

3. Acceptance Criteria
   - [Pulled from Jira/Confluence ticket]

4. Test Environment
   Environment URL:
   Branch / Build:
   Test Data:

5. Test Types
   [ ] Functional
   [ ] Regression
   [ ] Integration
   [ ] Exploratory
   [ ] Smoke

6. Entry Criteria  (must be met before testing begins)
   [ ] Build deployed to test environment
   [ ] Access provisioned for QE
   [ ] Test data available
   [ ] KT session completed

7. Exit Criteria  (must be met before sign-off)
   [ ] All critical test cases executed
   [ ] No P1 / P2 defects open
   [ ] Test execution report delivered

8. Defect Management
   Tool: Jira
   Severity: P1 Blocker | P2 Critical | P3 Major | P4 Minor

9. Risks & Assumptions
   - [Risk]
   - [Assumption]

10. Sign-Off
    QE Lead:
    Dev Lead:
    Product Owner:
─────────────────────────────────────────
```

---

*Last Updated: April 2026 | Maintained by: QA/QE Team*
