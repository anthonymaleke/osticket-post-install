<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket - Post-Install Configuration

This project covers the configuration that turns a freshly installed osTicket instance into a working IT help desk. It is Part 2 of a three-part series and builds on the Windows Server and IIS environment created in Part 1.

## Portfolio Project

**Author:** Anthony Maleke

**Contact:** [Linkedin](https://github.com/anthonymaleke/osticket-prereqs.git)

## Video Demonstration

- [YouTube: osTicket Tutorial (Part 2 of 3) - Post-Install Configuration](https://www.youtube.com/watch?v=REPLACE_ME)

## The Series

| Part | Repository | Topic |
|---|---|---|
| 1 | [osticket-prereqs](https://github.com/anthonymaleke/osticket-prereqs) | Azure VM, IIS, PHP, database, osTicket installation |
| 2 | **post-install-config** (this repo) | Roles, departments, teams, agents, users, SLAs, help topics |
| 3 | [ticket-lifecycle](https://github.com/anthonymaleke/ticket-lifecycle) | A ticket from intake to resolution |

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines)
- Remote Desktop Protocol (RDP)
- Internet Information Services (IIS)
- osTicket Admin Panel and Agent Panel
- Windows Task Scheduler (optional)

## Operating Systems Used

- Windows Server 2022 Datacenter (Azure Edition)

## Goal

A fresh osTicket installation can accept a ticket but has no structure behind it. The goal of this phase is to build that structure so that a ticket submitted through the portal is categorized, prioritized, assigned and tracked against a deadline without any manual sorting.

## What Gets Configured

| Component | Purpose |
|---|---|
| Roles | Control what each type of agent is allowed to do |
| Departments | Organize tickets and limit which agents can see them |
| Teams | Group agents into support tiers for assignment |
| Agents | The support staff who work tickets |
| Users | The people who submit tickets |
| SLA plans | Define how quickly each kind of ticket must be resolved |
| Help topics | Let users describe their issue while the system picks the department, priority, SLA and assignee |

## Lab Design

### Roles

| Role | Purpose |
|---|---|
| Help Desk Admin | Full control |
| Tier 1 Agent | Front-line handling without delete rights |
| Tier 2 Agent | Escalation handling without delete rights |

### Departments and Teams

| Department | Team |
|---|---|
| IT Service Desk | Tier 1 Support |
| Systems Administration | Tier 2 Support |

### SLA Plans

| Plan | Grace period | Schedule |
|---|---|---|
| P1 Critical | 2 hours | 24/7 |
| P2 High | 8 hours | Business hours |
| P3 Normal | 24 hours | Business hours |
| P4 Low | 72 hours | Business hours |

### Help Topic Routing

| Help topic | Department | Priority | SLA | Team |
|---|---|---|---|---|
| Service Outage | Systems Administration | Emergency | P1 Critical | Tier 2 |
| Account Access and Password Reset | IT Service Desk | High | P2 High | Tier 1 |
| Software Issue or Request | IT Service Desk | Normal | P3 Normal | Tier 1 |
| Hardware or Device Issue | IT Service Desk | Normal | P3 Normal | Tier 1 |
| Network or VPN Issue | Systems Administration | High | P2 High | Tier 2 |
| New Equipment Request | IT Service Desk | Low | P4 Low | Tier 1 |

All names, people and email addresses in this lab are fictional sample data.

## Overview

1. Review system settings and confirm the help desk is online.
2. Create roles.
3. Create departments and teams.
4. Add agents and assign them a role, department and team.
5. Create a business hours schedule and the SLA plans.
6. Create help topics that route tickets automatically.
7. Add end users.
8. Verify the portal and each agent login.
9. Optional: understand the email limitation and schedule the maintenance job.

## Outline

### Configure Roles

- Navigate to: Admin Panel, Agents, Roles
- Create Help Desk Admin, Tier 1 Agent and Tier 2 Agent
- Leave the delete permission off for both tiers (least privilege)

### Configure Departments

- Navigate to: Admin Panel, Agents, Departments
- Create IT Service Desk and Systems Administration

### Configure Teams

- Navigate to: Admin Panel, Agents, Teams
- Create Tier 1 Support and Tier 2 Support

### Configure Agents

- Navigate to: Admin Panel, Agents, Agents
- Create Tier 1 and Tier 2 agents and place your admin account in Systems Administration

### Configure SLA Plans

- Navigate to: Admin Panel, Manage, Schedules, then Manage, SLA
- Create a Business Hours schedule and the four SLA plans
- Set P3 Normal as the system default

### Configure Help Topics

- Navigate to: Admin Panel, Manage, Help Topics
- Create the six topics from the routing table

### Configure Users

- Navigate to: Agent Panel, Users, Add New
- Create two sample end users

## Results

After this phase the portal shows six help topics, and each one carries a department, priority, SLA and assignee behind the scenes. Agents see only the tickets their department and role allow.

## Design Decisions

- **Separate roles for each tier.** Permissions follow the job instead of giving every agent full access.
- **Topic-based routing.** Users pick a plain-language issue type and never see internal departments.
- **SLA by business impact.** The shortest deadline applies only to outages and runs 24/7, while routine requests use business hours.
- **Sample data uses example.com.** No real mailbox is involved, so nothing can be sent to a real person by accident.

## Known Limitations

- Outgoing email is not configured in this series, so alerts and replies are not delivered by email. Everything is demonstrated inside the web portals.
- The lab runs over HTTP and should only use test credentials.

## References

- [osTicket Post-Install Setup Guide](https://docs.osticket.com/en/latest/Getting%20Started/Post-Installation.html)
- [osTicket Admin Panel](https://docs.osticket.com/en/latest/Admin%20Panel.html)
- [osTicket Email Settings](https://docs.osticket.com/en/latest/Getting%20Started/Email%20Settings.html)

## Next Step

Continue to [Part 3: ticket-lifecycle](https://github.com/osticket/osticket-lifecycle).
