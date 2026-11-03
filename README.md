# Senior Leadership Workshop Management Portal

A full-stack web application designed to modernize the management of a **Senior Leadership Workshop (SLW)** by replacing a difficult-to-maintain legacy system with a centralized, role-based platform.

> **Portfolio Notice:** This repository is a project showcase. It does **not** contain production source code, credentials, proprietary business data, or sensitive organizational information.

---

## 📌 Project Overview

The Senior Leadership Workshop Management Portal was developed to replace a legacy application that was difficult to maintain and often required software engineering support for routine updates.

The goal was not simply to redesign the interface. The project involved rebuilding the underlying workflows and data relationships so that program managers could manage the program more independently while participants received a clearer and more structured experience.

The result is a **Python/Django web application** supporting the workshop lifecycle from nomination through participation and alumni status.

---

## 🎯 The Problem

The legacy system presented several operational challenges:

- Program information was difficult to maintain.
- Routine updates frequently required developer assistance.
- Data relationships were limited or inconsistent.
- Nomination and participant management involved manual processes.
- Program managers had limited administrative control.
- Adding or modifying functionality could take significant development effort.
- The system was difficult to scale and maintain over time.

The new application was designed around the actual business workflow rather than simply recreating the legacy system.

---

## 💡 The Solution

I designed and developed a **role-based Django application** that centralizes workshop administration and provides different experiences based on each user's responsibilities.

### Program Managers / Administrators

Administrators can manage:

- Workshops
- Users
- Nominations
- Participants
- Organizations
- Facilitators
- Email templates
- Participant progress
- Program data

### Nominators

Nominators can submit and manage participant nominations through a structured workflow.

### Participants

Participants can:

- Complete required pre-work
- Update profile information
- Provide contact information
- Submit hotel and logistical information
- Complete assigned tasks
- Monitor their progress

### Alumni

Participants can transition into alumni status after completing the program, allowing the system to support the broader participant lifecycle.

---

## ✨ Key Features

### Role-Based Dashboards

Users receive different dashboards, permissions, and functionality depending on their assigned role.

```text
Admin / Program Manager
        │
        ├── Manage Workshops
        ├── Manage Nominations
        ├── Manage Participants
        ├── Manage Organizations
        └── Monitor Progress

Nominator
        │
        └── Submit & Manage Nominations

Participant
        │
        ├── Complete Profile
        ├── Complete Pre-Work
        └── Track Requirements

Alumni
        │
        └── Alumni Access
```

### Nomination Workflow

The application provides a structured nomination process.

```text
Nomination Submitted
        │
        ▼
      Pending
        │
        ▼
Program Manager Review
        │
    ┌───┴───┐
    ▼       ▼
Approved  Rejected
    │
    ▼
Participant Created
```

Program managers can review nominations individually or use bulk administrative actions to streamline the process.

### Participant Pre-Work

Participants complete required information through a guided workflow.

Examples include:

- Contact information
- Profile information
- Hotel information
- Program requirements
- Assigned pre-work
- Required tasks

Progress tracking provides both participants and administrators with visibility into completion status.

### Submit-and-Lock Workflow

Certain tasks can be locked after submission to protect finalized information and prevent accidental changes.

### Organization Management

Organizations are modeled using relational **parent/child relationships** rather than relying on a flat list.

```text
Parent Organization
│
├── Organization A
│   ├── Division A
│   └── Division B
│
└── Organization B
    └── Division C
```

This provides a more flexible structure for managing organizational relationships.

### Facilitator Management

Program administrators can create, update, and manage facilitator information directly through the application.

This reduces the need for developers to make routine content or personnel updates.

### Email Templates

Reusable email templates allow common program communications to be managed consistently without requiring changes to application code.

### Soft Delete & Restore

Important records can be removed from normal workflows without immediately destroying the underlying data.

Authorized administrators can restore records when necessary.

### Data Export

Administrative information can be exported for reporting and operational use.

The application uses `django-import-export` to support structured data export functionality.

---

## 🛠️ Technology Stack

| Area | Technology |
|---|---|
| Backend | Python / Django |
| Architecture | Django MVT |
| Database Access | Django ORM |
| Database Design | Relational |
| Frontend | HTML / CSS / JavaScript |
| Templates | Django Templates |
| Authentication | Django Authentication |
| Authorization | Role-Based Access |
| Import / Export | django-import-export |
| Cloud | Microsoft Azure |
| CI/CD | Azure DevOps |
| Version Control | Git |

---

## 🏗️ Application Architecture

```text
┌───────────────────────────────┐
│             Users             │
│                               │
│ Admin │ Nominator │Participant│
│             Alumni            │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│        Django Web App         │
│                               │
│  Authentication              │
│  Authorization               │
│  Business Logic              │
│  Workflow Management         │
│  Administrative Interfaces   │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│          Django ORM           │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      Relational Database      │
│                               │
│  Users                        │
│  Nominations                  │
│  Participants                 │
│  Organizations                │
│  Workshops                    │
│  Tasks                        │
│  Facilitators                 │
└───────────────────────────────┘
```

The application is built around relational models rather than isolated records. This allows information to remain connected across the different stages of the workshop lifecycle.

---

## 🔄 Example Participant Lifecycle

```text
Nominator
    │
    ▼
Submit Nomination
    │
    ▼
Program Manager Review
    │
    ├──── Rejected
    │
    └──── Approved
             │
             ▼
      Participant Created
             │
             ▼
        Account Access
             │
             ▼
       Complete Profile
             │
             ▼
       Complete Pre-Work
             │
             ▼
       Submit Requirements
             │
             ▼
        Attend Workshop
             │
             ▼
            Alumni
```

Automating this lifecycle reduces manual record management and provides a clearer process for both administrators and participants.

---

## 🧩 Engineering Challenges

### Replacing a Legacy Application

One of the biggest challenges was understanding the existing operational process before determining how it should be represented in a modern application.

Instead of reproducing the legacy application exactly, I worked with the program manager to understand how users actually interact with the program.

Those workflows became the foundation of the new application architecture.

### Relational Data Design

A major architectural improvement was establishing meaningful relationships between entities.

```text
User
 │
 ├── Role
 │
 ├── Nomination
 │
 └── Participant
        │
        ├── Organization
        ├── Workshop
        ├── Pre-Work
        └── Tasks
```

This provides a stronger foundation for maintaining existing functionality and introducing future features.

### Designing for Non-Developers

A major project objective was reducing dependency on software developers for routine program management.

Where appropriate, program managers can maintain information through administrative interfaces rather than requesting source-code changes.

This transformed the application from simply being a website into an operational platform that program staff can manage.

### Deployment & CI/CD

The application's deployment process evolved as the project matured.

The deployment workflow was migrated to **Azure DevOps**, providing a structured CI/CD process for deploying the Django application to Microsoft Azure.

Working through deployment challenges strengthened my experience with:

- CI/CD pipelines
- Environment configuration
- Application settings
- Production logging
- Web server configuration
- Deployment troubleshooting
- Cloud application management

---

## 👩‍💻 My Role

I serve as the **primary developer and technical owner** of the application.

My responsibilities have included:

- Requirements gathering
- Application architecture
- Database modeling
- Backend development
- Frontend development
- Authentication and authorization
- Workflow design
- Administrative tooling
- Testing and debugging
- CI/CD configuration
- Azure deployment
- Production troubleshooting
- User feedback
- Feature refinement

I work directly with the program manager to translate operational requirements into technical solutions.

---

## 📚 What I Learned

### Design Around the Workflow

Successful application design starts with understanding how people actually work rather than immediately choosing a technical solution.

### Data Architecture Matters

Well-designed relationships between models make future features significantly easier to implement and maintain.

### Administrative Usability Matters

A system becomes more sustainable when authorized business users can manage routine information without depending on developers.

### Deployment Is Part of Software Engineering

Building an application is only one part of its lifecycle.

CI/CD, configuration, logging, debugging, documentation, security, and maintainability are equally important.

### Documentation Is Critical for Scaling

As the application grows, documentation becomes increasingly important.

One of the next stages of the project is ensuring that future developers can understand, maintain, and extend the application without relying on knowledge held by a single developer.


## 📷 Screenshots

> Screenshots shown in this repository are sanitized and contain no sensitive participant or organizational information.

### Admin Dashboard

![Admin Dashboard](screenshots/admin-dashboard.png)

### Nomination Workflow

![Nomination Workflow](screenshots/nomination-workflow.png)

### Participant Dashboard

![Participant Dashboard](screenshots/participant-dashboard.png)

### Pre-Work Workflow

![Pre-Work Workflow](screenshots/prework-wizard.png)

---

## 🔒 Why Isn't the Source Code Public?

This project was developed as part of my professional work.

For security, confidentiality, and intellectual property reasons, the production source code is **not publicly available**.

This repository instead serves as a technical case study demonstrating:

- The problem being solved
- System architecture
- Application functionality
- Engineering decisions
- Technologies used
- Development challenges
- Lessons learned

No production credentials, source code, participant information, internal URLs, or proprietary organizational data are included.

---

## 📊 Project Status

**Production Application — Actively Maintained**

The platform continues to evolve based on program requirements and user feedback.

---

Production source code, credentials, proprietary information, internal infrastructure details, and sensitive organizational or participant data are intentionally excluded.
