# Engagement Model

This section describes how a Cloud Accelerate Factory (CAF) for Agents engagement is structured — from nomination to production handover — including sprint phases, prerequisites, roles and responsibilities, and expected outcomes.

---

## 🔄 Engagement Flow: Sprint Structure

A CAF engagement consists of **four sequential phases**, each with clearly defined goals, activities, and exit criteria.

![Engagement Flow](https://github.com/Seungjin-Ryu/Cloud-Accelerate-Factory-for-Agents-Runbooks/blob/a0df98ca68b6b0a58ee20e11e3f4e9855d63176f/00-program-overview/CAF%20for%20Agents%20Engagement%20Flow.png)


### Phase 0 — Nomination & Validation

**Goal:** Confirm the customer's eligibility and scenario fit before committing engineering resources.

| Item | Details |
|---|---|
| **Duration** | ~1 week (intake within 48 hours of submission) |
| **Trigger** | CSA / ATU submits nomination via https://aka.ms/FactoryNom |
| **Activities** | Intake review, scenario fit check, eligibility validation, routing decision |
| **Exit Criteria** | Scenario confirmed as CAF-fit OR routed to appropriate alternate program (CSU / ISD / FDE / PG / Partner) |

> 📌 If the scenario does not fit CAF's pre-defined patterns, the team will route to the most suitable delivery channel — no customer is left without a path forward.

---

### Phase 1 — Prerequisites & Scoping

**Goal:** Establish technical and organizational readiness before sprint execution begins.

| Item | Details |
|---|---|
| **Duration** | ~1 week |
| **Activities** | Technical assessment, environment access setup, use case scoping, runbook selection, kickoff meeting |
| **Exit Criteria** | All prerequisites confirmed, delivery scope agreed, project kickoff completed |

**Key Prerequisites Checklist:**
- [ ] Required environment access provisioned (tenant, licenses, connectors)
- [ ] Eligible workload milestone confirmed in MSX (Copilot Studio / AI Foundry)
- [ ] Executive sponsor and project owner identified on customer side
- [ ] Scenario aligns with a supported CAF runbook pattern
- [ ] Weekly checkpoint schedule agreed upon

---

### Phase 2 — Execution & Validation

**Goal:** Deliver the agent solution end-to-end using Microsoft runbooks and reference architectures.

| Item | Details |
|---|---|
| **Duration** | 2–4 weeks (core sprint) |
| **Activities** | Agent development, integration with data sources / LOB systems, testing, governance & security review via Agent Landing Zone |
| **Exit Criteria** | Agent fully developed, tested, and validated against success criteria; reference architecture documented |

**Deliverables in this phase:**
- Fully developed and tested agent solution
- Reference architecture and IaC templates
- Agent Landing Zone governance & security configuration
- Weekly status checkpoint reports

---

### Phase 3 — Customer Testing & Production Cutover

**Goal:** Transition ownership to the customer with confidence in security, scalability, and operability.

| Item | Details |
|---|---|
| **Duration** | ~1 week |
| **Activities** | User Acceptance Testing (UAT) support, production deployment, knowledge transfer, handover documentation |
| **Exit Criteria** | Agent live in production, customer team trained, handover package delivered |

**Deliverables in this phase:**
- Production-deployed agent
- UAT sign-off
- Handover documentation and runbook
- Post-deployment support guidance

---

## ✅ Prerequisites

Before a CAF engagement can begin, the following conditions must be met.

### Customer Prerequisites

| # | Prerequisite | Details |
|---|---|---|
| 1 | **Committed use case** | A confirmed, production-ready agent scenario — not in discovery or pre-sales |
| 2 | **Eligible workload milestone** | Active milestone in MSX for Copilot Studio, AI Foundry, or a qualifying workload |
| 3 | **Sales Stage 2+** | Opportunity must be at Sales Stage 2 or later |
| 4 | **ACV threshold** | \$50K ACV or projected \$50K+ consumption from the scenario |
| 5 | **Environment access** | Customer must provide tenant access and complete required configurations |
| 6 | **Executive sponsorship** | Designated project owner and executive sponsor on the customer side |
| 7 | **Deployment readiness** | Team is available and ready for weekly checkpoints, UAT, and change management |

### Nomination Prerequisites

| # | Prerequisite | Details |
|---|---|---|
| 1 | **Nomination submitted** | Via https://aka.ms/FactoryNom |
| 2 | **MSX milestone added** | Note: the nomination tool may take up to **8 hours** to recognize newly added milestones |
| 3 | **Managed customer** | SMB customers are not eligible for CAF |

> 💡 Refer to the nomination best-practice checklist to ensure your customer is nomination-ready before submitting.

---

## 👥 Roles & Responsibilities (RACI)

The following RACI matrix defines accountability across the four engagement phases.

**Legend:** R = Responsible | A = Accountable | C = Consulted | I = Informed

| Activity | Microsoft CSA / CFTL | Vendor Delivery Team | CAF Program Manager | Customer / Partner |
|---|:---:|:---:|:---:|:---:|
| Nomination submission | R / A | — | I | C |
| Eligibility & scenario validation | A | — | R | I |
| Technical scoping & runbook selection | A | C | I | C |
| Environment access & configuration | I | C | I | R / A |
| Agent development & build | C | R / A | I | I |
| Governance & security setup (Agent Landing Zone) | A | R | I | C |
| Weekly checkpoint facilitation | R | R | A | R |
| UAT planning & execution | C | I | I | R / A |
| Production deployment | C | R | I | A |
| Knowledge transfer & handover | A | R | I | C |
| Post-deployment support coordination | C | I | I | R / A |
| Change management & user training | I | — | I | R / A |

### Role Definitions

| Role | Description |
|---|---|
| **Microsoft CSA / CFTL** | Cloud Factory Technical Lead — Microsoft FTE responsible for technical oversight, runbook quality, and customer-facing alignment |
| **Vendor Delivery Team** | Vetted and trained partner vendors who execute agent delivery following Microsoft runbooks; primarily offshore engineering teams |
| **CAF Program Manager** | Manages intake, routing, scheduling, and overall program governance |
| **Customer / Partner** | Owns project coordination, environment access, UAT, communications, training, and change management |

---

## 🌏 Delivery Model

CAF engagements are delivered through a **vendor-driven model** with Microsoft oversight:

- **Offshore Engineering Teams** (primarily India-based) — Execute agent builds following Microsoft runbooks
- **Regional Project Coordinators & Architects** — Ensure regional context and alignment
- **Cloud Factory Technical Leads (CFTL)** — Microsoft CSA FTEs who provide technical leadership and quality assurance

### Regional Language Support

| Region | Supported Languages |
|---|---|
| **Asia** | English, Chinese, Japanese, Korean |
| **EMEA** | English, German, French |
| **Latin America** | English, Spanish, Portuguese |
| **Global** | English (default) |

---

## 🚫 Out of Scope

The following are explicitly **not supported** within CAF engagements:

- Major infrastructure migrations (SAP, AIX, Oracle Exadata, VMware to AVS)
- Analytics platform migrations (e.g., Tableau to Power BI)
- Deep re-architecture or large-scale code rewrites
- Custom consulting, long-term managed services, or post-delivery compliance work
- VDI migrations (RDS / Citrix to AVD)
- Highly custom or non-repeatable agent scenarios *(these are routed to ISD, FDE, or Partner-led programs)*

---

## 📊 Expected Outcomes

### For Customers

- ✅ Faster time to production with deployment clarity
- ✅ Agent built to enterprise governance, security, and scalability standards
- ✅ Access to Microsoft experts at **zero incremental cost**
- ✅ Reference architecture and IaC templates for future reuse
- ✅ Production-ready handover with UAT sign-off

### For Microsoft

- ✅ Increased Agent MAU, AI Foundry ACR, and Copilot credit consumption
- ✅ Consistent delivery quality using best-practice architectures
- ✅ Clear triage and routing to the correct delivery program
- ✅ Scalable, repeatable delivery through evolving runbooks

---

## 📎 Key Links

| Resource | Link |
|---|---|
| Nominate a Customer | https://aka.ms/FactoryNom |
| Nomination Dashboard | https://aka.ms/Factory-Dashboard |
| CAF Contacts | CloudAccelFactory@Microsoft.com |

