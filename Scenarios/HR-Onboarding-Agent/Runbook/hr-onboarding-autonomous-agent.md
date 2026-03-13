# HR Onboarding Autonomous Agent

## Scenario Overview

**Scenario Type**: Employee Self-Service (HR)  
**Agent Type**: Autonomous Agent (Email-triggered + Knowledge-grounded)  
**Delivery Model**: Cloud Accelerate Factory for Agents (CAF)  
**Primary Tools**: Microsoft Copilot Studio, ServiceNow Copilot Connector, Power Platform

This runbook describes how to build and deploy an HR Onboarding Autonomous Agent that helps new hires find HR-related information such as onboarding processes, policies, and employee benefits. The agent uses authoritative HR knowledge and can autonomously respond to email-based inquiries.

---

## Business Outcomes

- Reduce HR helpdesk workload
- Improve new-hire onboarding experience
- Ensure consistent, policy-aligned HR responses
- Increase employee self-service adoption

---

## In Scope / Out of Scope

### In Scope
- HR policy and onboarding Q&A
- Knowledge-grounded responses using ServiceNow
- Email-triggered autonomous execution
- Deployment to Microsoft 365 Copilot and Teams

### Out of Scope
- HR transactional workflows (payroll, updates)
- Case management systems
- Custom ML model training

---

## Reference Architecture

``

## Architecture

- Logical Architecture
User (Email / Copilot)
   ↓
Autonomous HR Agent (Copilot Studio)
   ├─ Knowledge: ServiceNow Copilot Connector
   ├─ Tool: Office 365 Outlook (Send Email)
   └─ Trigger: New Email Arrives

- Key Components

**ServiceNow Copilot Connector**: HR knowledge grounding
**Power Platform Environment (Developer)**: Agent lifecycle management
**Microsoft 365 Copilot**: End-user access channel


## Prerequisites

### Licensing & Permissions
- Microsoft 365 Copilot license
- Copilot extensibility enabled in tenant
- Permission to create Power Platform environments
- Permission to configure Copilot connectors
- Teams custom app side-loading enabled

### Environment
- Dedicated Power Platform **Developer Environment**
- Dataverse enabled
- Non-default environment recommended

---

## Knowledge Preparation (ServiceNow)

### ServiceNow Copilot Connector
- Create ServiceNow developer tenant
- Configure ServiceNow Copilot Connector
- Verify connector availability in Microsoft 365 Search & Intelligence

### HR Knowledge Content
Create and publish the following articles in ServiceNow Knowledge Base:
- **Employee Handbook** (Category: Policy)
- **Health & Wellness Benefits** (Category: Benefit)

### Indexing
- Run **Full Crawl** on ServiceNow Copilot Connector
- Confirm indexed item count increases before agent testing

---

## Agent Build & Configuration

### Create Custom Agent
- **Name**: `HROnboardingAutoAgent`
- **Description**: HR Onboarding Agent
- **Orchestration**: Generative (default)

### Add Knowledge Source
- Add ServiceNow Copilot Connector
- Disable Web Search to enforce authoritative grounding

### Add Tools
- Tool: **Office 365 Outlook – Send an email (V2)**
- Tool Name: `SendEmail`
- Authentication: Maker credentials

### Configure Trigger
- Trigger: **When a new email arrives (V3)**
- Logic:
  - Extract question from email body
  - Search ServiceNow knowledge
  - Respond to sender via email

---

## Agent Instructions

```text
Capabilities:
This is an HR onboarding agent for new hires.

HR Questions:
- Use ServiceNow knowledge only.
- If no result is found, respond with:
  "I don't know, please reach out to HR."

Email Trigger Logic:
- Question is stored in email body.
- Search ServiceNow knowledge.
- Send response email to sender.
- Email body must be HTML formatted.


## Suggested Starter Prompts

TitlePromptBenefitWhat is wellness benefit programMedical PlanProvide information for the medical plan and display it as a tableTravel ExpenseWhat is the travel expense?Code of ConductWhat is company code of conductOnboardingWhat is the onboarding process?

Validation & Testing
Functional Testing

Test agent responses in Copilot Studio
Verify citations reference ServiceNow articles

Autonomous Testing

Send email from non-maker account
Confirm automated email response
Validate trigger and tool execution in Activity logs


Publish & Deployment
Publish Agent

Publish agent in Copilot Studio
Review embedded credential warnings

Extend to Microsoft 365 Copilot

Enable Teams and M365 Copilot channel
Republish agent after channel addition

Tenant-wide Deployment

Submit agent for admin approval
Approve agent in Integrated Apps
Make agent available org-wide


Success Metrics

HR Agent MAU
HR inquiry deflection rate
Time-to-answer for onboarding questions
Microsoft 365 Copilot usage growth


Known Limitations & Escalation

Transactional HR workflows → Route to ISD / Partner
Knowledge quality issues → Update ServiceNow KB first
Custom workflow requirements → Outside CAF standard scope

