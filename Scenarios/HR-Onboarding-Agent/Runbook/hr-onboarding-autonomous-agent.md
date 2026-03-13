# HR Onboarding Autonomous Agent

**Scenario Type**: Employee Self-Service (HR)
**Agent Type**: Autonomous Agent (Email-triggered + Knowledge-grounded)
**Primary Tooling**: Microsoft Copilot Studio, ServiceNow Copilot Connector, Power Platform

## 1. Runbook Overview
### 1.1 Scenario Summary
New hires often struggle to find accurate and timely information related to HR policies, onboarding steps, and employee benefits.
This runbook describes how to deploy an HR Onboarding Autonomous Agent that answers HR-related questions using authoritative HR knowledge and can proactively respond to email-based requests.

### 1.2 Business Outcomes
- Reduced HR ticket volume
- Faster onboarding experience for new hires
- Consistent, policy-aligned HR responses
- Improved employee self-service adoption

### 1.3 In-Scope
- HR policy and onboarding Q&A
- Knowledge-grounded responses (ServiceNow Knowledge)
- Email-triggered autonomous responses
- Deployment to Microsoft 365 Copilot and Teams

### 1.4 Out-of-Scope
- HR case management workflows
- Payroll or transactional HR system updates
- Custom ML model training

## 2. Architecture

2.1 Logical Architecture
User (Email / Copilot)
   ↓
Autonomous HR Agent (Copilot Studio)
   ├─ Knowledge: ServiceNow Copilot Connector
   ├─ Tool: Office 365 Outlook (Send Email)
   └─ Trigger: New Email Arrives

2.2 Key Components

**ServiceNow Copilot Connector**: HR knowledge grounding
**Power Platform Environment (Developer)**: Agent lifecycle management
**Microsoft 365 Copilot**: End-user access channel


## 3. Prerequisites & Readiness

### 3.1 Licensing & Access

- Microsoft 365 Copilot license
- Copilot extensibility enabled in tenant
- Permission to create Power Platform environments
- Permission to create Copilot connectors
- Teams custom app side-loading enabled

3.2 Environment Preparation

- Dedicated Power Platform Developer Environment
- Dataverse enabled
- Non-default environment recommended for isolation

