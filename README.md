**Author**: Karuranga
**Student ID**: 27541
**PDB Name**: Grp_B_27541_KARURANGA_HelpDeskTrack_db
**Course**: Database Development with PL/SQL (INSY 8311)
**Instructor**: Eric Maniraguha

## 📌 Overview

This project implements a PL/SQL-based IT Helpdesk Ticket Management System to track ticket creation, escalation, and resolution time for an IT department. It supports real-time ticket updates, staff assignment, and audit mechanisms using triggers, procedures, and packages.

## 📘 Phase I: Problem Statement & Goals

**Simple Problem**: IT staff cannot efficiently prioritize and resolve tickets, leading to delayed support.
**Problem**: Manual tracking of ticket escalations and response times results in missed SLAs, reduced efficiency, and poor end-user satisfaction.
**Context**: IT departments in organizations.
**Target Users**: Helpdesk employees, IT technicians, managers.

### 🎯 Goals

* Automate ticket escalation and resolution workflows
* Monitor technician performance
* Enforce SLA timelines
* Enhance data integrity and access control

## 🧭 Phase II: Business Process Modeling (MIS)

**Simple Problem**: Managers have no visibility on technician workload and ticket bottlenecks.

**Actors**: Employee, Technician, Manager, System

### ✅ Swimlane Process:

1. Employee submits a ticket
2. System logs the ticket
3. Technician is assigned
4. If unresolved in X time, escalate
5. Manager monitors escalations
6. System updates ticket status

## 📐 Phase III: Logical Model Design (ERD)

**Simple Problem**: Ticket data is not normalized, making escalations and reports difficult.

**Entities**: Tickets, Users, Roles, Audit\_Log, Escalation\_History, Holidays

**Normalization**: All tables are normalized to 3NF

**Relationships**:

* Users ⟷ Tickets
* Tickets ⟷ Escalation\_History
* Users ⟷ Audit\_Log
* Holidays used in trigger logic

## 🛠 Phase IV: Database Creation

**Simple Problem**: There was no centralized database for managing helpdesk operations.

**Pluggable DB**: `Grp_B_27541_KARURANGA_HelpDeskTrack_db`
**Admin User**: `helpdesk_admin` with password `karuranga`
**OEM**: Configured and screenshots provided for monitoring

**SQL Scripts:**

* `create_pdb.sql`
* `create_users.sql`
* `grant_privileges.sql`

## 📦 Phase V: Table Implementation & Data Insertion

**Simple Problem**: Helpdesk teams needed test data to simulate operations.

### ✅ Tables Created

* Users
* Tickets
* Roles
* History
* Holidays
* Audit\_Log

### 📋 Sample Data Inserted

* Users with roles (Admin, Technician, Manager)
* Tickets for real-world scenarios
* Escalation history to reflect SLA violations
* Holiday dates for restriction triggers

## 🧾 Phase VI: Procedures, Transactions, Packages

**Simple Problem**: Manually querying and updating ticket info caused errors.

### ✅ What was done:

* **Procedures**: To fetch open tickets, update ticket status, and insert escalation records
* **Functions**: To calculate resolution time and escalation count
* **Packages**: Grouped procedures and functions into `ticket_pkg` and `audit_pkg`
* **Cursors**: Used for looping through ticket records
* **Exception Handling**: Implemented to log and handle errors gracefully

## 🔐 Phase VII: Advanced Programming & Auditing

**Simple Problem**: Unauthorized actions were being performed during business hours or holidays.

### 🛡 Security Enhancements

* Trigger to block INSERT/UPDATE/DELETE during weekdays and holidays
* Holiday data checked dynamically
* Restriction trigger with compound logic

### 📊 Auditing

* `audit_log` table stores: user\_id, operation, timestamp, status, message
* `audit_pkg` automates logging
* All sensitive changes are captured
* Here is the **Data Structure and Methodology** section tailored for your *IT Helpdesk Ticket Escalation and Resolution Time Tracker* project. You can include this in your documentation (README, report, or GitHub repo) right after the project overview or before the phase breakdowns.

---

## 🏗️ Data Structure and Methodology

### 📁 **1. Data Structure Design**

The database schema was designed using principles of **relational modeling** and **normalization** up to **3NF** (Third Normal Form). The system consists of the following key entities:

#### 🗃️ Tables and Their Purposes:

| Table Name    | Purpose                                                              |
| ------------- | -------------------------------------------------------------------- |
| `users`       | Stores user information including roles (Technician, Manager, Admin) |
| `tickets`     | Central table for support ticket details                             |
| `escalations` | Tracks escalation records linked to specific tickets                 |
| `audit_log`   | Logs all insert/update/delete operations for auditing                |
| `holidays`    | Stores restricted calendar dates (e.g., public holidays)             |

Each table uses **surrogate keys** (auto-increment `NUMBER` type via `GENERATED BY DEFAULT AS IDENTITY`) and enforces **referential integrity** with `FOREIGN KEY` constraints. Fields are typed appropriately (e.g., `VARCHAR2` for text, `DATE` for timestamps).

**💡 Example Relationship**:

* One `user` can be assigned to many `tickets`
* One `ticket` can be escalated multiple times (`tickets` ⇄ `escalations`)


### ⚙️ **2. Methodology**

The development process followed a **multi-phase, waterfall-inspired approach** aligning with academic PL/SQL development guidelines.

#### 📌 Step-by-Step Methodology:

| Phase         | Activity Description                                                                  |
| ------------- | ------------------------------------------------------------------------------------- |
| **Phase I**   | Defined the problem and project scope in a real-world IT support context              |
| **Phase II**  | Modeled business processes using swimlane diagrams (draw\.io)                         |
| **Phase III** | Built the ERD, normalized tables, and established relationships and constraints       |
| **Phase IV**  | Created a pluggable Oracle database and user schema with proper privileges            |
| **Phase V**   | Implemented physical table structures and inserted representative sample data         |
| **Phase VI**  | Developed modular PL/SQL procedures, functions, and packages for code reuse and logic |
| **Phase VII** | Added advanced features: triggers, auditing, and business-rule enforcement            |

#### 🔄 Tools and Practices Used:

* **Oracle 19c** with SQL\*Plus and SQL Developer
* **PL/SQL Packages** for modular logic and auditing
* **Triggers** to automate compliance (e.g., holiday restrictions)
* **Draw\.io** for ERD and business process diagrams
* **Auditing Logs** for traceability of user actions

---

### 🔐 Security & Access Control

* Role-based access ensures only authorized users (e.g., Managers/Admins) can escalate tickets or update during restricted times.
* PL/SQL triggers block operations by Technicians on holidays or weekdays and log every action in `audit_log`.



