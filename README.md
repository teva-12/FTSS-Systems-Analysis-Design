# 🎓 Faculty Tools Store System (FTSS)
> **Systems Analysis & Design — Full Project Report**  
> Based on *Dennis, Wixom & Roth — 6th Edition* · Agile / Scrum Methodology

<div align="center">

![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)
![Methodology](https://img.shields.io/badge/Methodology-Agile%20%2F%20Scrum-blue?style=for-the-badge)
![Sprints](https://img.shields.io/badge/Sprints-4%20×%202%20weeks-orange?style=for-the-badge)
![SDLC](https://img.shields.io/badge/SDLC-Full%20Coverage-purple?style=for-the-badge)
![Diagrams](https://img.shields.io/badge/Diagrams-14%20UML%20%2B%20Wireframes-red?style=for-the-badge)

</div>

---

## 📌 Project Summary

**FTSS** is a full systems analysis and design project for an **online tools supply platform** serving Engineering and Medical college students. The system allows students to browse, search, and order specialized academic tools — and administrators to manage inventory, process orders, and generate reports.

This project demonstrates complete **SDLC coverage** from Planning through Deployment, applying every major methodology tool from the Dennis, Wixom & Roth textbook.

---

## 🎯 Problem Statement

Students in practical colleges (Electrical Engineering & Medicine) must source tools from scattered off-campus vendors, causing:

- ⏱️ **2–3 hour delays** searching for required tools
- 💸 **High costs** due to no centralized negotiation
- ❌ **Frequent unavailability** during exam and lab seasons

**FTSS solves this** by providing a centralized, always-available online store managed by the college.

---

## 🗂️ Project Report Structure

| Chapter | Title | Key Deliverables |
|---------|-------|-----------------|
| 1 | Project Overview | Background, Scope, User Roles, Objectives |
| 2 | Planning Phase | Feasibility Study, Project Charter, Gantt Chart, Sprint Plan, Risk Register |
| 3 | Analysis Phase | FRs, NFRs, Use Cases, DFD L0/L1/L2, Sequence Diagram |
| 4 | Design Phase | 3-Tier Architecture, ERD, Data Dictionary, Class Diagram, State Diagram, Wireframes |
| 5 | Implementation | REST API Design, Module Breakdown, SQL Schema, Test Plan, Deployment |
| 6 | Product Catalog | Engineering tools, Medical tools, Pricing |
| 7 | Conclusions | SDLC mapping, Agile justification, Future work, References |
| A | Appendix A | Interview Questions |
| B | Appendix B | Survey Results (n=120) |

---

## 📐 Diagrams & Artifacts

### UML Diagrams
| Diagram | Description | Book Chapter |
|---------|-------------|-------------|
| **Use Case Diagram** | 12 use cases, 3 actors, «include»/«extend» | Ch.5 |
| **Sequence Diagram** | Place Order (UC-07) — full basic + alt flow | Ch.5 |
| **Class Diagram** | 10 classes with attributes and methods | Ch.10 |
| **State Diagram** | Order lifecycle — 6 states | Ch.5 |
| **Order Flowchart** | Complete decision logic with branches | Ch.6 |

### Data Flow Diagrams (DFD)
| Diagram | Description | Book Chapter |
|---------|-------------|-------------|
| **DFD Level 0** | Context diagram — 4 external entities | Ch.6 |
| **DFD Level 1** | 5 main processes + 4 data stores | Ch.6 |
| **DFD Level 2** | P3 (Order Processing) decomposition | Ch.6 |

### Data & Architecture
| Artifact | Description | Book Chapter |
|---------|-------------|-------------|
| **ERD** | 8 entities, 7 relationships, crow's foot notation | Ch.10 |
| **Data Dictionary** | PRODUCT + ORDER tables (full column specs) | Ch.10 |
| **3-Tier Architecture** | Presentation → Application → Data | Ch.9 |
| **REST API Design** | 17 endpoints with auth requirements | Ch.13 |

### UI Wireframes (Ch.11)
- 🖥️ **Student Catalog Page** — search, filter, product grid
- 📦 **Product Detail Page** — specs, gallery, add-to-cart
- ⚙️ **Admin Dashboard** — metrics, orders table, low-stock alerts

---

## 🔄 Methodology — Agile / Scrum

```
Sprint 1 (W1–W2)  → Foundation & Auth
Sprint 2 (W3–W4)  → Catalog & Search
Sprint 3 (W5–W6)  → Cart, Orders & Email
Sprint 4 (W7–W8)  → Inventory, Reports & UAT
```

| Metric | Value |
|--------|-------|
| Total Sprints | 4 × 2 weeks |
| User Stories | 12 stories |
| Story Points | 71 points |
| Team Size | 4 developers |

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────┐
│         PRESENTATION TIER               │
│   HTML5 · CSS3 · Bootstrap 5 · JS       │
└──────────────────┬──────────────────────┘
                   │ REST / HTTPS
┌──────────────────▼──────────────────────┐
│          APPLICATION TIER               │
│   Node.js · Express.js · JWT · Mailer   │
│                                         │
│  Auth │ Catalog │ Cart │ Orders         │
│  Admin │ Inventory │ Reports │ Email    │
└──────────────────┬──────────────────────┘
                   │ SQL Queries
┌──────────────────▼──────────────────────┐
│            DATA TIER                    │
│   MySQL 8.0 · Stored Procedures         │
│                                         │
│  STUDENT │ PRODUCT │ ORDER │ CATEGORY   │
│  ORDER_ITEM │ INVENTORY_LOG │ COLLEGE   │
└─────────────────────────────────────────┘
```

---

## 🧩 ERD Entities

```
COLLEGE ──< CATEGORY ──< PRODUCT >──< ORDER_ITEM >──< ORDER
                                          │               │
                                   INVENTORY_LOG      STUDENT
```

| Entity | PK | Key Attributes |
|--------|-----|---------------|
| STUDENT | student_id | email, college_id, year_of_study, password_hash |
| COLLEGE | college_id | college_name, college_type |
| CATEGORY | category_id | category_name, college_id FK |
| PRODUCT | product_id | sku_code, price, stock_qty, reorder_level |
| ORDER | order_id | student_id, status ENUM, total_amount |
| ORDER_ITEM | order_item_id | order_id, product_id, quantity, unit_price |
| INVENTORY_LOG | log_id | product_id, change_qty, change_type |

---

## ✅ Requirements Coverage

### Functional Requirements (12 FRs)

| ID | Requirement | Priority |
|----|------------|---------|
| FR-01 | Student registration with college email verification | High |
| FR-02 | Product catalog organized by college → category | High |
| FR-03 | Keyword, SKU, and category-based search | High |
| FR-04 | Persistent shopping cart per student | High |
| FR-05 | Checkout creates order + decrements inventory | High |
| FR-06 | Email confirmation on order placement | Medium |
| FR-07 | Real-time order status tracking | Medium |
| FR-08 | Admin CRUD for products | High |
| FR-09 | Automatic low-stock alerts | High |
| FR-10 | Admin order fulfillment workflow | High |
| FR-11 | Monthly sales + inventory reports | Medium |
| FR-12 | Complete order history per student | Medium |

### Non-Functional Requirements (9 NFRs)

| ID | Category | Requirement | Priority |
|----|----------|------------|---------|
| NFR-01 | Security | HTTPS/TLS enforced on all endpoints | High |
| NFR-02 | Security | Passwords hashed with bcrypt (min. 10 rounds) | High |
| NFR-03 | Security | Input sanitization — SQL injection, XSS, CSRF prevention | High |
| NFR-04 | Performance | Catalog search < 2 s under 200 concurrent users | Medium |
| NFR-05 | Performance | Checkout end-to-end < 5 s including DB + email | Medium |
| NFR-06 | Availability | ≥ 99.5% uptime during academic semesters | High |
| NFR-07 | Usability | Responsive layout — mobile (375px+), tablet, desktop | High |
| NFR-08 | Scalability | Supports 5,000 students without redesign | Medium |
| NFR-09 | Maintainability | Swagger API docs + inline code comments | Low |

---

## 🔐 Role-Based Access Control

| Feature | Student | Admin | Faculty |
|---------|:-------:|:-----:|:-------:|
| Browse Catalog | ✅ | ✅ | ✅ |
| Shopping Cart | ✅ | ❌ | ❌ |
| Place Order | ✅ | ❌ | ❌ |
| Track Order | ✅ | ❌ | ❌ |
| Admin Dashboard | ❌ | ✅ | ❌ |
| Manage Products | ❌ | ✅ | ❌ |
| Process Orders | ❌ | ✅ | ❌ |
| Generate Reports | ❌ | ✅ | ✅ |

---

## 🧪 Test Summary

| Test ID | Module | Test Case | Status |
|---------|--------|-----------|--------|
| UT-01 | Auth | Register with valid college email | ✅ Pass |
| UT-02 | Auth | Login with wrong password → 401 | ✅ Pass |
| UT-03 | Catalog | Search 'oscilloscope' returns EE-003 | ✅ Pass |
| UT-04 | Cart | Add qty > stock → 409 error | ✅ Pass |
| UT-05 | Orders | Place order → verify inventory decrement | ✅ Pass |
| UT-06 | Email | Order placed → email received < 30s | ✅ Pass |
| UT-07 | Inventory | Stock below reorder → admin alert fired | ✅ Pass |
| UT-08 | Reports | Monthly report renders in < 5s | ✅ Pass |

---

## 📦 Product Catalog Sample

### Engineering College — Electronics & Communications

| SKU | Product | Price (EGP) | Stock |
|-----|---------|:-----------:|:-----:|
| EE-001 | Digital Multimeter UT61E | 450 | 85 |
| EE-002 | Arduino Uno R3 | 280 | 120 |
| EE-003 | Oscilloscope 2ch 100MHz | 3,200 | ⚠️ 3 |
| EE-004 | Breadboard 830-point | 45 | 300 |
| EE-005 | Resistor Kit 600pcs | 120 | 200 |
| EE-006 | Soldering Station 60W | 380 | 40 |

### Medical College

| SKU | Product | Price (EGP) | Stock |
|-----|---------|:-----------:|:-----:|
| MD-001 | Stethoscope | 550 | 60 |
| MD-002 | Reflex Hammer Taylor | 85 | 90 |
| MD-003 | Dissection Set 8-piece | 195 | 75 |
| MD-004 | Lab Coat | 150 | 100 |
| MD-005 | Manual Sphygmomanometer | 320 | ⚠️ 4 |

---

## 📋 Data Validation Mechanisms

| Check Type | Applied On | Rule |
|-----------|-----------|------|
| **Format Check** | Registration — Email | Must match university domain `*@college.edu.eg` |
| **Completeness Check** | Checkout | Payment method + pickup location required |
| **Range Check** | Cart — Quantity | Integer > 0 AND ≤ `stock_qty` |
| **Existence Check** | Login — Email | Must exist in Users table |
| **Consistency Check** | Checkout — Total | Server-side total must match `Σ(qty × price)` |

---

## 🚀 Order Status Lifecycle

```
[Student Checkout]
       │
       ▼
  ┌─────────┐   Admin confirms    ┌────────────┐   Packed   ┌───────────────┐
  │ PENDING │ ──────────────────► │ PROCESSING │ ─────────► │ READY PICKUP  │
  └─────────┘                     └────────────┘            └───────────────┘
       │                               │                            │
       │ Cancel                        │ Cancel                     │ Student collects
       ▼                               ▼                            ▼
  ┌───────────┐               ┌─────────────┐               ┌───────────┐
  │ CANCELLED │               │   ON HOLD   │               │ DELIVERED │
  │(stock     │               │(stock issue)│               │  (Final)  │
  │ restored) │               └─────────────┘               └───────────┘
  └───────────┘
```

---

## 📚 References

- Dennis, A., Wixom, B. H., & Roth, R. M. (2015). *Systems Analysis and Design*, 6th ed. John Wiley & Sons.
- Schwaber, K., & Sutherland, J. (2020). *The Scrum Guide*. Scrum.org.
- Pressman, R. S. (2014). *Software Engineering: A Practitioner's Approach*, 8th ed. McGraw-Hill.
- Nielsen, J. (1994). *Usability Engineering*. Morgan Kaufmann.

---

## 📁 Repository Structure

```
📦 FTSS-SA-D-Project
 ┣ 📄 README.md                          ← You are here
 ┣ 📄 FTSS_Final_Report_v2.pdf           ← Full project report (PDF — view in browser)
 ┣ 📄 FTSS_Final_Report_v2.docx          ← Editable Word version
 ┗ 📁 diagrams/
    ┣ 🖼️ use_case_diagram.png
    ┣ 🖼️ dfd_context_diagram.png
    ┣ 🖼️ dfd_level1.png
    ┣ 🖼️ sequence_diagram_place_order.png
    ┣ 🖼️ order_state_diagram.png
    ┗ 🖼️ order_flowchart.png
```

---

## 👤 Author

**SA&D Course Project**  
Faculty of Engineering / College of Practical Sciences  
Based on: *Dennis, Wixom & Roth — Systems Analysis and Design, 6th Edition*

---

<div align="center">

*Made with ❤️ applying every chapter of Dennis, Wixom & Roth*

</div>
