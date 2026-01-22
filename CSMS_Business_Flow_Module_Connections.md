# CSMS Business Flow and Module Connections

## Document Purpose
This document illustrates how all CSMS modules are interconnected in the business flow, with special focus on the Locate module's role and connections with other modules. Each diagram is followed by a **description** explaining what it shows. Section 6 includes **paragraph-style explanations** of the detailed business logic to complement the flowcharts. Section 8 (Page-by-Page Design Ideas) includes a **Business Logic** subsection for each page, describing the rules, workflows, and data flow that apply to that specific screen.

---

## Table of Contents
1. [Overall System Business Flow](#1-overall-system-business-flow)
2. [Locate Module - Business Context and Connections](#2-locate-module---business-context-and-connections)
3. [Module Interdependencies](#3-module-interdependencies)
4. [Data Flow Between Modules](#4-data-flow-between-modules)
5. [Workflow Scenarios](#5-workflow-scenarios)
6. [Detailed Business Logic for Locate Module](#6-detailed-business-logic-for-locate-module)
7. [External System Connections - Detailed](#7-external-system-connections---detailed)
8. [Page-by-Page Design Ideas for Locate Module](#8-page-by-page-design-ideas-for-locate-module)

### Diagram Index
| # | Diagram | Location | Description |
|---|---------|----------|-------------|
| 1 | Overall System Business Flow | §1 | Child support lifecycle from application receipt through Finance |
| 2 | Locate Module Integration Points | §2 | Locate as central hub; connections to Intake, Case Mgmt, Establishment, Enforcement, Finance |
| 3 | Detailed Locate Module Connection Diagram | §2 | Internal Locate structure, Person tables, consumer modules |
| 4 | Locate Module Dependencies (Connection Matrix) | §3 | Inputs to and outputs from Locate |
| 5 | Data Flow - Locate Module | §4 | How data moves across modules over time |
| — | Workflow Scenarios 1–5 | §5 | Intake, Case Mgmt, Enforcement, Establishment, Finance scenarios |
| 6.2 | Search Logic Flow | §6.2 | Internal search → Enterprise Search → Match resolution |
| 6.3 | Data Update Workflow | §6.3 | Validation → Update → Audit → Notify |
| 6.4 | Enterprise Search Workflow | §6.4 | Request → Submit → Process → User selection |
| 6.5 | Address Validation Workflow | §6.5 | Validate → Valid / Invalid / Suggestions |
| 6.6 | Employer Search Logic | §6.6 | Internal → NDNH → Verification |
| 7.1 | NDNH Workflow | §7.1 | NDNH integration from user search to UI display |
| 7.2 | FCR Workflow | §7.2 | FCR query, submission, response processing |
| 7.3 | FPLS Workflow | §7.3 | FPLS authorization, request, response, review |

---

# 1. Overall System Business Flow

## High-Level Business Process Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                    CHILD SUPPORT APPLICATION LIFECYCLE              │
└─────────────────────────────────────────────────────────────────────┘

                    ┌─────────────────┐
                    │   APPLICATION   │
                    │   RECEIVED      │
                    └────────┬────────┘
                             │
                             ▼
        ┌────────────────────────────────────┐
        │     1. INTAKE MODULE               │
        │  • Application Entry               │
        │  • CP/NCP/Child Info Collection    │
        │  • Initial Data Entry              │
        └────────────┬───────────────────────┘
                     │
                     ▼
        ┌────────────────────────────────────┐
        │     2. CASE REGISTRATION           │
        │  • Member Clearance                │
        │  • MDM ID Generation               │
        │  • Case Registration               │
        │  • Work Item Creation              │
        └────────────┬───────────────────────┘
                     │
                     ▼
        ┌────────────────────────────────────┐
        │     3. CASE MANAGEMENT             │
        │  • Case Maintenance                │
        │  • Party Information Updates       │
        │  • Document Management             │
        └───────┬────────────────────┬───────┘
                │                    │
                │                    │
                ▼                    ▼
    ┌──────────────────┐    ┌──────────────────┐
    │   4. LOCATE      │    │  5. ESTABLISHMENT│
    │   • Find NCP/CP  │    │   • Paternity    │
    │   • Update Info  │    │   • Support Order│
    └───────┬──────────┘    └───────┬──────────┘
            │                       │
            │                       │
            ▼                       ▼
    ┌──────────────────────────────────────┐
    │      6. ENFORCEMENT                  │
    │      • IWO                           │
    │      • License Suspension            │
    │      • Collections                   │
    └──────────────┬───────────────────────┘
                   │
                   ▼
    ┌──────────────────────────────────────┐
    │      7. FINANCE                      │
    │      • Payment Receipt               │
    │      • Disbursement                  │
    │      • Financial Reporting           │
    └──────────────────────────────────────┘
```

**Diagram 1 Description — Overall System Business Flow**

This diagram depicts the end-to-end lifecycle of a child support case from application receipt through financial disbursement. A case begins when an application is received and flows sequentially through **Intake** (application entry, CP/NCP/child data collection), then **Case Registration** (member clearance, MDM ID generation, case registration, work item creation). After registration, **Case Management** maintains the case and can branch to **Locate** (finding and updating NCP/CP location) and **Establishment** (paternity, support order, court proceedings). Both Locate and Establishment feed into **Enforcement** (IWO, license suspension, collections), which in turn feeds **Finance** (payment receipt, disbursement, reporting). The flow is predominantly sequential, with Locate and Establishment as parallel paths from Case Management, and Finance as the final stage.

---

# 2. Locate Module - Business Context and Connections

## Locate Module Integration Points

```
                    ┌─────────────────────────────────────────────┐
                    │         LOCATE MODULE - CENTRAL HUB         │
                    │   (Used Throughout Case Lifecycle)          │
                    └──────────────────┬──────────────────────────┘
                                       │
                    ┌──────────────────┼──────────────────┐
                    │                  │                  │
                    ▼                  ▼                  ▼
        ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
        │   INTAKE         │  │  CASE            │  │  ESTABLISHMENT   │
        │   MODULE         │  │  MANAGEMENT      │  │  MODULE          │
        │                  │  │                  │  │                  │
        │ • NCP missing    │  │ • Update NCP     │  │ • Locate NCP for │
        │   information    │  │   address        │  │   paternity      │
        │ • Initial locate │  │ • Verify current │  │ • Service of     │
        │   attempts       │  │   location       │  │   process        │
        └────────┬─────────┘  └────────┬─────────┘  └────────┬─────────┘
                 │                     │                      │
                 │                     │                      │
                 └─────────────────────┼──────────────────────┘
                                       │
                                       ▼
                    ┌─────────────────────────────────────┐
                    │      ENFORCEMENT MODULE             │
                    │  • Locate NCP for enforcement       │
                    │  • Find employer for IWO            │
                    │  • Update address for service       │
                    │  • Verify location for collection   │
                    └──────────────────┬──────────────────┘
                                       │
                                       ▼
                    ┌─────────────────────────────────────┐
                    │      FINANCE MODULE                 │
                    │  • Update address for payments      │
                    │  • Verify location for              │
                    │    disbursements                    │
                    └─────────────────────────────────────┘
```

**Diagram 2 Description — Locate Module Integration Points**

This diagram shows the Locate module as a **central hub** used across the case lifecycle. Locate connects **upstream** to **Intake** (when NCP information is missing or initial locate is needed), **Case Management** (when NCP address or location must be updated or verified), and **Establishment** (when the NCP must be located for paternity or service of process). It connects **downstream** to **Enforcement** (locating NCP for enforcement, finding employer for IWO, updating address for service) and **Finance** (updating address for payments and verifying location for disbursements). The diagram emphasizes that Locate is not a one-time step but a shared service used by multiple modules at different stages.

---

## Detailed Locate Module Connection Diagram

```
┌──────────────────────────────────────────────────────────────────────┐
│                         LOCATE MODULE                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐              │
│  │  Cases Tab   │  │  Demographics│  │   Address    │              │
│  │  (Search)    │  │  Updates     │  │   Updates    │              │
│  └──────────────┘  └──────────────┘  └──────────────┘              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐              │
│  │  Employer    │  │   Contact    │  │  Required    │              │
│  │  Updates     │  │   Updates    │  │  Actions     │              │
│  └──────────────┘  └──────────────┘  └──────────────┘              │
└──────────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼

┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│   INTAKE      │    │ CASE REG.     │    │ CASE MGT      │
│   Uses Locate │    │ Uses Locate   │    │ Uses Locate   │
│   When:       │    │ When:         │    │ When:         │
│               │    │               │    │               │
│ • NCP info    │    │ • Verify MDM  │    │ • NCP moved   │
│   incomplete  │    │   matches     │    │ • Address     │
│ • Need to     │    │ • Enterprise  │    │   changed     │
│   find NCP    │    │   search      │    │ • Employer    │
│ • Initial     │    │ • Member      │    │   update      │
│   locate      │    │   clearance   │    │ • Contact     │
│               │    │               │    │   update      │
└───────┬───────┘    └───────┬───────┘    └───────┬───────┘
        │                     │                     │
        │ Data Updates        │ Data Updates        │ Data Updates
        │                     │                     │
        └─────────────────────┼─────────────────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   Person Tables   │
                    │  • Person         │
                    │  • Person_Address │
                    │  • Person_Employer│
                    │  • Person_Contact │
                    └───────────────────┘
                              │
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼

┌───────────────┐    ┌───────────────┐    ┌───────────────┐
│ESTABLISHMENT  │    │  ENFORCEMENT  │    │   FINANCE     │
│ Uses Locate   │    │  Uses Locate  │    │  Uses Locate  │
│ When:         │    │  When:        │    │  When:        │
│               │    │               │    │               │
│ • Service of  │    │ • Find NCP    │    │ • Payment     │
│   process     │    │   location    │    │   delivery    │
│ • Paternity   │    │ • Employer    │    │ • Address     │
│   establishment│   │   location    │    │   verification│
│ • Court       │    │ • IWO service │    │ • Disbursement│
│   proceedings │    │ • License     │    │   address     │
│               │    │   suspension  │    │               │
└───────────────┘    └───────────────┘    └───────────────┘
```

**Diagram 3 Description — Detailed Locate Module Connection Diagram**

This diagram illustrates the **internal structure** of the Locate module (Cases Tab, Demographics, Address, Employer, Contact, Required Actions) and how it connects to other modules and shared data. **Intake**, **Case Registration**, and **Case Management** use Locate for scenarios such as incomplete NCP info, MDM verification, enterprise search, member clearance, address/employer/contact changes, and contact updates. All Locate updates flow into **Person tables** (Person, Person_Address, Person_Employer, Person_Contact), which act as the single source of truth. **Establishment**, **Enforcement**, and **Finance** then consume locate data from those tables for service of process, court proceedings, NCP/employer location, IWO, license suspension, payment delivery, address verification, and disbursement. The diagram shows both **who uses Locate** and **where locate data is stored and consumed**.

---

# 3. Module Interdependencies

## Detailed Connection Matrix

### Locate Module Dependencies

```
┌──────────────────────────────────────────────────────────────────┐
│                    LOCATE MODULE - CONNECTIONS                   │
├──────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────┐                                             │
│  │  INPUTS FROM   │                                             │
│  ├────────────────┤                                             │
│  │ • Case Number  │ ← Case Registration Module                  │
│  │ • Application  │ ← Intake Module                             │
│  │   Number       │                                             │
│  │ • Person ID    │ ← All Modules                               │
│  │ • MDM ID       │ ← Case Registration Module                  │
│  │ • Search       │ ← Case Management Module                    │
│  │   Criteria     │                                             │
│  └────────────────┘                                             │
│                                                                  │
│  ┌────────────────┐                                             │
│  │  OUTPUTS TO    │                                             │
│  ├────────────────┤                                             │
│  │ • Updated      │ → Case Management Module                    │
│  │   Addresses    │                                             │
│  │ • Updated      │ → Case Management Module                    │
│  │   Employers    │                                             │
│  │ • Updated      │ → Case Management Module                    │
│  │   Contacts     │                                             │
│  │ • Updated      │ → Case Management Module                    │
│  │   Demographics │                                             │
│  │ • Location     │ → Enforcement Module (for service)          │
│  │   Information  │                                             │
│  │ • Employer     │ → Enforcement Module (for IWO)              │
│  │   Information  │                                             │
│  │ • Verified     │ → Finance Module (for disbursement)         │
│  │   Addresses    │                                             │
│  └────────────────┘                                             │
│                                                                  │
└──────────────────────────────────────────────────────────────────┘
```

**Diagram 4 Description — Locate Module Dependencies (Connection Matrix)**

This diagram summarizes **inputs to** and **outputs from** the Locate module. **Inputs** include Case Number and Application Number (from Case Registration and Intake), Person ID (from all modules), MDM ID (from Case Registration), and Search Criteria (from Case Management). **Outputs** include updated Addresses, Employers, Contacts, and Demographics to Case Management; Location Information and Employer Information to Enforcement (for service and IWO); and Verified Addresses to Finance (for disbursement). The matrix clarifies what each module supplies to Locate and what Locate supplies back, supporting integration and data contract design.

---

# 4. Data Flow Between Modules

## Data Flow Diagram

```
┌──────────────────────────────────────────────────────────────────────┐
│                         DATA FLOW - LOCATE MODULE                    │
└──────────────────────────────────────────────────────────────────────┘

INTAKE MODULE
    │
    │ Creates Application
    │ • Person Data (if known)
    │ • Missing NCP Info
    │
    ▼
┌──────────────────────────────────┐
│      LOCATE MODULE               │
│  • Searches for NCP              │
│  • Finds missing information     │
│  • Updates person records        │
└──────────────┬───────────────────┘
               │
               │ Updates Person Tables
               │ • Person_Address
               │ • Person_Employer
               │ • Person_Contact
               │
               ▼
┌──────────────────────────────────┐
│   CASE REGISTRATION MODULE       │
│  • Uses updated locate data      │
│  • Verifies MDM matches          │
│  • Completes member clearance    │
└──────────────┬───────────────────┘
               │
               │ Creates Registered Case
               │
               ▼
┌──────────────────────────────────┐
│   CASE MANAGEMENT MODULE         │
│  • Maintains locate data         │
│  • Updates when changes occur    │
│  • Provides locate search        │
└──────────────┬───────────────────┘
               │
               ├──────────────────────┐
               │                      │
               ▼                      ▼
┌──────────────────────┐   ┌──────────────────────┐
│  ESTABLISHMENT       │   │  ENFORCEMENT         │
│  MODULE              │   │  MODULE              │
│  • Uses locate for   │   │  • Uses locate for   │
│    service of        │   │    IWO employer      │
│    process           │   │  • Uses locate for   │
│  • Verifies          │   │    service           │
│    location for      │   │  • Updates from      │
│    court             │   │    locate            │
└──────────┬───────────┘   └──────────┬───────────┘
           │                          │
           │                          │
           └──────────┬───────────────┘
                      │
                      ▼
           ┌──────────────────────┐
           │   FINANCE MODULE     │
           │  • Uses verified     │
           │    addresses for     │
           │    disbursements     │
           │  • Updates from      │
           │    locate            │
           └──────────────────────┘
```

**Diagram 5 Description — Data Flow (Locate Module)**

This diagram shows **how data moves** across modules over time. Intake creates the application (including person data and missing NCP info) and feeds the Locate module, which searches for the NCP and updates person records. Locate updates **Person_Address**, **Person_Employer**, and **Person_Contact**. Case Registration then uses that updated data for MDM verification and member clearance, and creates the registered case. Case Management maintains locate data and provides locate search; it branches to **Establishment** (service of process, court location) and **Enforcement** (IWO employer, service, updates from Locate). Both Establishment and Enforcement feed **Finance**, which uses verified addresses for disbursements. The diagram emphasizes that locate data flows **forward** through the pipeline and is reused by downstream modules.

---

# 5. Workflow Scenarios

## Scenario 1: Locate During Intake

```
INTake Worker receives application
         │
         │ NCP information incomplete
         │
         ▼
    ┌─────────────┐
    │   INTAKE    │
    │   MODULE    │
    └──────┬──────┘
           │
           │ Triggers Locate Search
           │
           ▼
    ┌─────────────┐
    │   LOCATE    │
    │   MODULE    │
    │             │
    │ • Search    │
    │   databases │
    │ • Find NCP  │
    │ • Update    │
    │   records   │
    └──────┬──────┘
           │
           │ Updates Person Tables
           │
           ▼
    ┌─────────────┐
    │   INTAKE    │
    │   MODULE    │
    │             │
    │ • Completes │
    │   application│
    │ • Creates   │
    │   work item │
    └─────────────┘
```

**Scenario 1 Description:** An intake worker receives an application with incomplete NCP information. The worker triggers a locate search from the Intake module. The Locate module searches internal and external databases, finds the NCP, and updates person records. Those updates are written back to the person tables. The intake worker then completes the application and creates a work item for downstream processing. This scenario shows Locate being invoked **during Intake** before case registration.

---

## Scenario 2: Locate During Case Management

```
Case Worker needs to update NCP address
         │
         ▼
    ┌─────────────────┐
    │ CASE MANAGEMENT │
    │     MODULE      │
    └────────┬────────┘
             │
             │ Accesses Locate Module
             │
             ▼
    ┌─────────────────┐
    │   LOCATE        │
    │   MODULE        │
    │                 │
    │ • Search for    │
    │   NCP           │
    │ • View current  │
    │   address       │
    │ • View address  │
    │   history       │
    │ • Add new       │
    │   address       │
    └────────┬────────┘
             │
             │ Updates Address
             │
             ▼
    ┌─────────────────┐
    │ CASE MANAGEMENT │
    │     MODULE      │
    │                 │
    │ • Address       │
    │   updated       │
    │ • Available for │
    │   other modules │
    └─────────────────┘
```

**Scenario 2 Description:** A case worker needs to update an NCP’s address. The worker opens Case Management and accesses the Locate module (or a locate view within Case Management). Locate is used to search for the NCP, view the current address and history, and add a new address. The address update is saved to the person tables. The updated address is then available to Case Management and to other modules (Establishment, Enforcement, Finance) that rely on current location data. This scenario illustrates Locate as the **primary tool for ongoing address maintenance** during case management.

---

## Scenario 3: Locate for Enforcement

```
Enforcement Worker needs to send IWO
         │
         ▼
    ┌─────────────────┐
    │   ENFORCEMENT   │
    │     MODULE      │
    └────────┬────────┘
             │
             │ Needs current employer
             │
             ▼
    ┌─────────────────┐
    │   LOCATE        │
    │   MODULE        │
    │                 │
    │ • Search        │
    │   employer      │
    │ • Update        │
    │   employer info │
    │ • Verify        │
    │   current       │
    └────────┬────────┘
             │
             │ Returns Employer Info
             │
             ▼
    ┌─────────────────┐
    │   ENFORCEMENT   │
    │     MODULE      │
    │                 │
    │ • Creates IWO   │
    │ • Sends to      │
    │   employer      │
    └─────────────────┘
```

**Scenario 3 Description:** An enforcement worker must send an Income Withholding Order (IWO) to the NCP’s employer. The worker uses the Enforcement module, which requires current employer information. The worker (or the system) calls the Locate module to search for and verify the NCP’s current employer. Locate returns employer details (name, address, FEIN, etc.). The enforcement worker then creates the IWO and sends it to that employer. This scenario shows Locate supporting **Enforcement** by providing accurate, up-to-date employer data for wage withholding.

---

## Scenario 4: Locate for Service of Process

```
Establishment Worker needs to serve NCP
         │
         ▼
    ┌─────────────────┐
    │  ESTABLISHMENT  │
    │     MODULE      │
    └────────┬────────┘
             │
             │ Needs service address
             │
             ▼
    ┌─────────────────┐
    │   LOCATE        │
    │   MODULE        │
    │                 │
    │ • Finds current │
    │   address       │
    │ • Verifies      │
    │   address       │
    │ • Provides      │
    │   service       │
    │   address       │
    └────────┬────────┘
             │
             │ Provides Address
             │
             ▼
    ┌─────────────────┐
    │  ESTABLISHMENT  │
    │     MODULE      │
    │                 │
    │ • Service       │
    │   completed     │
    │ • Proceeds with │
    │   establishment │
    └─────────────────┘
```

**Scenario 4 Description:** An establishment worker must serve the NCP with legal process (e.g., paternity or support order). The worker uses the Establishment module, which requires a valid service address. The worker consults the Locate module to find and verify the NCP’s current address. Locate provides a serviceable address. The establishment worker completes service and proceeds with establishment actions (e.g., paternity, court proceedings). This scenario shows Locate supporting **Establishment** by ensuring **service of process** can be completed successfully.

---

## Scenario 5: Locate for Payment Disbursement

```
Finance Worker needs to disburse payment
         │
         ▼
    ┌─────────────────┐
    │   FINANCE       │
    │     MODULE      │
    └────────┬────────┘
             │
             │ Needs verified address
             │
             ▼
    ┌─────────────────┐
    │   LOCATE        │
    │   MODULE        │
    │                 │
    │ • Verifies CP   │
    │   address       │
    │ • Confirms      │
    │   current       │
    │ • Updates if    │
    │   needed        │
    └────────┬────────┘
             │
             │ Provides Verified Address
             │
             ▼
    ┌─────────────────┐
    │   FINANCE       │
    │     MODULE      │
    │                 │
    │ • Processes     │
    │   disbursement  │
    │ • Sends to      │
    │   correct       │
    │   address       │
    └─────────────────┘
```

**Scenario 5 Description:** A finance worker needs to disburse a child support payment to the CP. The Finance module requires a verified, current address for the CP to ensure payments are sent to the right location. The worker (or the system) uses the Locate module to verify the CP’s address, confirm it is current, and update it if needed. Locate supplies the verified address. The finance worker then processes the disbursement and sends the payment to that address. This scenario shows Locate supporting **Finance** by reducing **undeliverable payments** and ensuring disbursements reach the correct recipient.

---

## Module Connection Summary Table

| Module | Connection to Locate | When Locate is Used | Data Exchanged |
|--------|---------------------|---------------------|----------------|
| **Intake** | One-way (Intake → Locate → Intake) | Initial NCP search when info incomplete | Person data, address, employer |
| **Case Registration** | Two-way | Member clearance, MDM verification | Person data, SSN history, enterprise matches |
| **Case Management** | Two-way (primary user) | Address/employer/contact updates | All person information |
| **Establishment** | One-way (Locate → Establishment) | Service of process, court proceedings | Service addresses |
| **Enforcement** | One-way (Locate → Enforcement) | IWO employer location, service addresses | Employer info, addresses |
| **Finance** | One-way (Locate → Finance) | Payment disbursement address verification | Verified addresses |

---

## Key Business Rules for Locate Module

1. **Locate can be triggered from multiple modules** - Not just from Case Management
2. **Locate updates are propagated** - Changes made in Locate update central person tables
3. **All modules read from same source** - Person tables are the single source of truth
4. **Locate supports the entire lifecycle** - Used from Intake through Finance
5. **Enterprise Search Integration** - Locate connects to external systems for comprehensive searches

---

# 6. Detailed Business Logic for Locate Module

## 6.1 Business Logic Overview

The Locate Module operates on several key business rules:

### Core Business Rules:
1. **Source Priority**: Information from external federal systems (NDNH, FCR, FPLS) takes precedence over manual entries
2. **Data Validation**: All locate information must be validated before updating person records
3. **Change Tracking**: Every change to location data must be logged with source, user, and timestamp
4. **Conflict Resolution**: When multiple sources provide conflicting information, the most recent verified source is used
5. **Auto-Notification**: Updates to critical location information trigger notifications to relevant case workers

**Narrative — Business Logic Overview**

The Locate module’s business logic is built around five core principles. **Source priority** means federal system data (NDNH, FCR, FPLS) overrides manual data when both exist, so that the most authoritative sources drive person records. **Data validation** ensures that every update—whether from internal search, Enterprise Search, or manual entry—meets format and business rules before it is persisted. **Change tracking** records source, user, and timestamp for every change, supporting audit, compliance, and troubleshooting. **Conflict resolution** applies when multiple sources disagree; the system uses the most recent verified source so that workers and downstream modules rely on up-to-date, validated information. **Auto-notification** ensures that when critical location data (e.g., address, employer) changes, Case Management, Enforcement, or Finance are notified so that pending actions (service, IWO, disbursement) can use the new data. Together, these rules keep locate data accurate, traceable, and actionable across the CSMS.

---

## 6.2 Search and Match Business Logic

### Search Logic Flow:
```
User enters search criteria (Case Number, Name, SSN)
    │
    ▼
┌─────────────────────────────────────────┐
│   Internal Database Search              │
│   • Search Person tables                │
│   • Search Case tables                  │
│   • Fuzzy matching for names            │
└──────────────┬──────────────────────────┘
               │
               │ If match found → Display results
               │ If no match or incomplete → 
               │
               ▼
┌─────────────────────────────────────────┐
│   Enterprise Search Trigger             │
│   • NDNH Search                         │
│   • FCR Query                           │
│   • FPLS Request                        │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Match Resolution                      │
│   • Compare results                     │
│   • Identify best match                 │
│   • Present to user for verification    │
└─────────────────────────────────────────┘
```

**Diagram 6.2 Description — Search Logic Flow**

This flowchart shows the path from user-entered search criteria (case number, name, SSN) through internal database search, optional Enterprise Search (NDNH, FCR, FPLS), and match resolution. Internal matches are displayed immediately; when no match or incomplete data exists, external search is triggered. Match resolution compares results, identifies the best match, and presents it to the user for verification.

### Match Scoring Algorithm:
1. **Exact Match** (Score: 100): SSN + Name + DOB match
2. **High Confidence** (Score: 80-99): SSN + Name match, or Name + DOB + Address match
3. **Medium Confidence** (Score: 60-79): Name + DOB match, or Name + Address match
4. **Low Confidence** (Score: 40-59): Name match only
5. **Review Required**: Score < 40 requires manual review

**Narrative — Search and Match Business Logic**

When a user searches for a case or person in the Locate module, the system first queries internal databases (Person, Case, and related tables) using the entered criteria—case number, name, SSN, or combinations thereof. Name searches use fuzzy matching to handle spelling variations and nicknames. If internal search returns a sufficient match, results are displayed immediately. If no match is found or data is incomplete, the system triggers an **Enterprise Search** against external systems (NDNH, FCR, FPLS). External results are compared with internal data, scored using the match algorithm above, and presented to the user. The user selects the best match and confirms; that selection drives updates to person records. Search and match logic ensures locate efforts start with the fastest, lowest-cost source (internal data) and escalate to federal systems only when necessary, while match scoring helps workers distinguish high-confidence hits from those needing manual review.

---

## 6.3 Data Update Business Logic

### Update Workflow:
```
User selects source data to update
    │
    ▼
┌─────────────────────────────────────────┐
│   Validation Check                      │
│   • Required fields present             │
│   • Data format valid                   │
│   • Business rules satisfied            │
└──────────────┬──────────────────────────┘
               │
               │ Valid?
               │
    ┌──────────┴──────────┐
    │                     │
   YES                   NO
    │                     │
    ▼                     ▼
┌──────────┐      ┌──────────────┐
│ Create   │      │ Display      │
│ Change   │      │ Error        │
│ Record   │      │ Message      │
└────┬─────┘      └──────────────┘
     │
     ▼
┌─────────────────────────────────────────┐
│   Update Person Tables                  │
│   • Mark old record as inactive         │
│   • Create new record                   │
│   • Update current record flag          │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Audit Log Entry                       │
│   • Source                              │
│   • Changed by                          │
│   • Change date/time                    │
│   • Old values                          │
│   • New values                          │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Notify Other Modules                  │
│   • Case Management (if case active)    │
│   • Enforcement (if enforcement pending)│
│   • Finance (if payment pending)        │
└─────────────────────────────────────────┘
```

**Diagram 6.3 Description — Data Update Workflow**

This flowchart shows the path from “user selects source data to update” through validation, person-table updates, audit logging, and notification. Valid updates create change records, update Person tables (including soft-delete of old records), write audit log entries, and notify Case Management, Enforcement, or Finance when relevant. Invalid updates result in error messages with no persistence.

**Narrative — Data Update Business Logic**

Whenever a worker chooses to apply locate results (from internal or external sources) to a person record, the system validates that required fields are present, formats are correct, and business rules are satisfied. If validation fails, the user sees clear error messages and no data is changed. If validation succeeds, the system creates a change record, marks the previous address/employer/contact/demographic record as inactive, inserts a new active record, and updates “current” flags. Every change is written to an audit log with source, user, timestamp, and old/new values. The system then checks whether the case is active, has pending enforcement, or has pending payments; if so, it notifies the appropriate modules so workers can act on the updated information. This end-to-end process keeps person data consistent, traceable, and immediately usable across the application.

---

## 6.4 Enterprise Search Business Logic

### Enterprise Search Workflow:
```
User clicks "Enterprise Search" button
    │
    ▼
┌─────────────────────────────────────────┐
│   Build Search Request                  │
│   • Extract search criteria             │
│   • Format according to system specs    │
│   • Include required identifiers        │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Submit to External Systems            │
│   • NDNH (for employment)               │
│   • FCR (for case history)              │
│   • FPLS (for location)                 │
│   • State systems (if applicable)       │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Wait for Response (Async)             │
│   • Track request status                │
│   • Set timeout                         │
│   • Handle errors                       │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Process Response                      │
│   • Parse response data                 │
│   • Validate data format                │
│   • Store in temporary table            │
│   • Display in "From Sources" section   │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   User Selects Match                    │
│   • User reviews results                │
│   • Selects best match                  │
│   • Confirms update                     │
└─────────────────────────────────────────┘
```

**Diagram 6.4 Description — Enterprise Search Workflow**

This flowchart traces the Enterprise Search process from the user clicking “Enterprise Search” through building the request, submitting to NDNH/FCR/FPLS (and state systems), waiting for async responses, processing and storing results, and finally the user selecting a match and confirming the update.

**Narrative — Enterprise Search Business Logic**

Enterprise Search extends locate capability beyond the CSMS database by querying federal and state systems. When the user clicks “Enterprise Search,” the system gathers available identifiers (SSN, name, DOB, etc.) from the current context, formats them per each system’s specifications, and submits requests to NDNH (employment/wages), FCR (case history), and FPLS (location), as well as applicable state systems. Requests are processed asynchronously; the system tracks status, enforces timeouts, and handles errors (e.g., network failure, invalid credentials). When responses arrive, the system parses and validates the data, stores it in a temporary or staging table, and displays it in the “From Sources” sections (Demographics, Address, Employer). The worker reviews the results, chooses the best match, and confirms the update; only then does the system apply changes to person records via the standard data-update workflow. Enterprise Search thus centralizes external locate activity and ensures that federal/state data is always reviewed by a worker before it becomes the system of record.

---

## 6.5 Address Validation Business Logic

### Address Validation Workflow:
```
User enters/updates address
    │
    ▼
┌─────────────────────────────────────────┐
│   Address Validation                    │
│   • USPS validation (if US address)     │
│   • International address check         │
│   • Format standardization              │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Validation Result                     │
│                                         │
│   Valid → Accept and standardize       │
│   Invalid → Flag for manual review      │
│   Suggestions → Present to user         │
└─────────────────────────────────────────┘
```

**Diagram 6.5 Description — Address Validation Workflow**

This flowchart shows that when a user enters or updates an address, the system runs address validation (e.g., USPS for U.S. addresses, checks for international addresses, format standardization). The result may be valid (accept and standardize), invalid (flag for manual review), or include suggestions (present to user for choice).

**Narrative — Address Validation Business Logic**

Address quality directly affects service of process, IWO delivery, and payment disbursement. When a user enters or updates an address in Locate, the system validates it before saving. For U.S. addresses, validation typically uses USPS or a similar service to verify format, correct minor errors, and standardize abbreviations (e.g., “Street” vs “St”). International addresses are checked for required components and format; they may be flagged for manual review rather than fully validated. If validation succeeds, the system stores the standardized address. If it fails, the record is flagged for review and the user is notified. When the validation service suggests corrections (e.g., missing suite number, suggested ZIP+4), the system presents those suggestions to the user, who can accept, reject, or edit. This logic reduces undeliverable mail and ensures that downstream modules receive consistent, reliable address data.

---

## 6.6 Employer Locate Business Logic

### Employer Search Logic:
```
Search for NCP employer
    │
    ▼
┌─────────────────────────────────────────┐
│   Internal Search                       │
│   • Current employer records            │
│   • Historical employer records         │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   NDNH Query                            │
│   • National Directory of New Hires     │
│   • Employment information              │
│   • W-2 data                            │
└──────────────┬──────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────┐
│   Employer Verification                 │
│   • FEIN/SEIN lookup                    │
│   • Business registration check         │
│   • Address validation                  │
└─────────────────────────────────────────┘
```

**Diagram 6.6 Description — Employer Search Logic**

This flowchart shows that employer locate starts with an internal search of current and historical employer records. If needed, an NDNH query is run for employment and W-2 data. Results are then verified via FEIN/SEIN lookup, business registration checks, and address validation.

**Narrative — Employer Locate Business Logic**

Employer information is critical for income withholding (IWO) and enforcement. The Locate module first checks internal employer records (current and historical) for the NCP. If data is missing or outdated, the system queries NDNH, which holds new-hire and wage data reported by employers. NDNH returns employer name, address, FEIN, employment dates, and often wage information. The system then verifies employer identity using FEIN/SEIN lookups and, where possible, business registration and address validation. Verified employer data is stored and displayed in the “Employer from Sources” and “NCP/CP Employer Information” sections. Workers can add or update employers manually or from NDNH results. Employer locate logic ensures that Enforcement has accurate, verified employer details before sending IWOs, reducing rejected or misdirected orders and improving collection outcomes.

---

# 7. External System Connections - Detailed

## 7.1 NDNH (National Directory of New Hires) Integration

### Purpose:
NDNH provides employment and wage information to help locate NCPs and their employers.

### Integration Details:

#### Connection Method:
- **Protocol**: Secure HTTPS/SSL
- **Format**: XML/EDI
- **Frequency**: Real-time queries and batch processing
- **Authentication**: Federal credentials required

#### Data Exchanged:

**Query Request (CSMS → NDNH)**:
- SSN/ITIN
- First Name
- Last Name
- Date of Birth
- Request Type (Employment, Wage, UI)

**Response (NDNH → CSMS)**:
- Employer Name
- Employer Address
- Employer FEIN
- Employment Start Date
- Quarterly Wage Information
- UI Claim Information
- Match Confidence Score

#### Business Rules:
1. **Query Frequency**: Limited to prevent abuse (typically once per day per person)
2. **Data Retention**: NDNH data retained per federal regulations
3. **Privacy**: All SSN data encrypted in transit and at rest
4. **Audit Trail**: All NDNH queries logged for compliance

#### Workflow:
```
User requests NDNH search
    │
    ▼
┌─────────────────────────────────────────┐
│   Check Query Limits                    │
│   • Daily query count                   │
│   • Person query history                │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Format NDNH Request                   │
│   • Build XML request                   │
│   • Add authentication                  │
│   • Encrypt SSN data                    │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Submit to NDNH                        │
│   • Secure connection                   │
│   • Track request ID                    │
│   • Set timeout (30 seconds)            │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Process Response                      │
│   • Parse XML response                  │
│   • Validate data                       │
│   • Store in locate_results table       │
│   • Display in UI                       │
└─────────────────────────────────────────┘
```

**Diagram 7.1 Description — NDNH Workflow**

This flowchart traces the NDNH integration from user-initiated search through query-limit checks, request formatting (XML, authentication, SSN encryption), submission over a secure connection with a 30-second timeout, and response processing. Responses are parsed, validated, stored in `locate_results`, and displayed in the UI. The diagram emphasizes compliance steps (limits, encryption, audit) and the end-to-end path from user action to displayed employer/wage data.

---

## 7.2 FCR (Federal Case Registry) Integration

### Purpose:
FCR provides information about child support cases across all states to identify interstate cases and duplicate registrations.

### Integration Details:

#### Connection Method:
- **Protocol**: Secure Web Service (SOAP/REST)
- **Format**: XML
- **Frequency**: Real-time queries and batch updates
- **Authentication**: OCSE-approved credentials

#### Data Exchanged:

**Query Request (CSMS → FCR)**:
- Case Number
- CP SSN
- NCP SSN
- Child SSN
- Person Type (CP, NCP, Child)
- Query Type (Case, Person, Order)

**Response (FCR → CSMS)**:
- Matching Case Numbers
- Participating States
- Case Status
- Order Information
- Match Date
- Transaction ID

#### Business Rules:
1. **Query Requirements**: Must query FCR for new cases before registration
2. **Update Frequency**: Case updates must be transmitted to FCR within required timeframe
3. **Data Accuracy**: FCR data takes precedence for interstate case matching
4. **Confidentiality**: All data encrypted per federal requirements

#### Workflow:
```
Case Registration/Update
    │
    ▼
┌─────────────────────────────────────────┐
│   Build FCR Query                       │
│   • Extract case identifiers            │
│   • Format according to FCR spec        │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Submit FCR Query                      │
│   • Authenticate                        │
│   • Submit via web service              │
│   • Receive transaction ID              │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Process FCR Response                  │
│   • Identify matches                    │
│   • Flag potential duplicates           │
│   • Link interstate cases               │
│   • Update case status                  │
└─────────────────────────────────────────┘
```

**Diagram 7.2 Description — FCR Workflow**

This flowchart shows the FCR integration starting from case registration or case update. The system builds an FCR query from case identifiers and formats it per FCR specifications, then submits the query via web service with authentication and receives a transaction ID. The response is processed to identify matches, flag potential duplicates, link interstate cases, and update case status. The diagram reflects FCR’s role in case-level matching and interstate coordination rather than person-level locate.

---

## 7.3 FPLS (Federal Parent Locator Service) Integration

### Purpose:
FPLS provides location services to find parents across state lines and access multiple federal and state databases.

### Integration Details:

#### Connection Method:
- **Protocol**: Secure HTTPS
- **Format**: XML/JSON
- **Frequency**: On-demand queries
- **Authentication**: Federal parent locator credentials

#### Data Exchanged:

**Query Request (CSMS → FPLS)**:
- SSN/ITIN
- Name (First, Middle, Last)
- Date of Birth
- Last Known Address
- Search Type (Location, Employment, Asset)
- Case Number

**Response (FPLS → CSMS)**:
- Current Address (if found)
- Address Sources
- Address Dates
- Employment Information
- Asset Information
- Match Confidence
- Data Source Agencies

#### Business Rules:
1. **Search Authorization**: FPLS searches require valid case justification
2. **Result Handling**: FPLS results must be verified before use
3. **Privacy**: Strict confidentiality requirements for FPLS data
4. **Cost**: Some FPLS searches may incur fees

#### Workflow:
```
User initiates FPLS search
    │
    ▼
┌─────────────────────────────────────────┐
│   Validate Search Authorization         │
│   • Active case required                │
│   • Valid case worker credentials       │
│   • Justification documented            │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Build FPLS Request                    │
│   • Compile available identifiers       │
│   • Select search type                  │
│   • Include case context                │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Submit FPLS Request                   │
│   • Secure connection                   │
│   • Authentication                      │
│   • Request tracking                    │
└──────────┬──────────────────────────────┘
           │
           ▼
┌─────────────────────────────────────────┐
│   Process FPLS Response                 │
│   • Parse location data                 │
│   • Verify result quality               │
│   • Store in locate_results             │
│   • Present to user for review          │
└─────────────────────────────────────────┘
```

**Diagram 7.3 Description — FPLS Workflow**

This flowchart depicts the FPLS integration from user-initiated search. The system first validates search authorization (active case, valid credentials, documented justification). It then builds the FPLS request from available identifiers and case context, submits it over a secure connection with authentication, and processes the response by parsing location data, verifying result quality, storing results in `locate_results`, and presenting them to the user for review. The diagram highlights FPLS’s authorization and verification requirements before location data is used in the Locate module.

---

## 7.4 Other External Connections

### State Systems:
- **DMV**: Driver's license and vehicle registration
- **Vital Records**: Birth certificates, paternity records
- **Unemployment Insurance**: UI claims and wage data
- **Corrections**: Incarceration information

### Commercial Data Sources:
- **Credit Bureaus**: Address and employment verification
- **Public Records**: Property ownership, business registrations

---

# 8. Page-by-Page Design Ideas for Locate Module

## 8.1 Locate Module - Main Landing Page

### Design Concept:
**Layout**: Full-width page with tab navigation
**Color Scheme**: Professional blue/gray palette
**Components**:

```
┌─────────────────────────────────────────────────────────────────────┐
│  [Top Navigation Bar]                                               │
│  [Breadcrumb: Home > Locate]                                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │                    LOCATE MODULE                            │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌──────────────┐          ┌──────────────┐                       │
│  │   [CASES]    │          │ [REQUIRED    │                       │
│  │              │          │  ACTION]     │                       │
│  │    [Tab]     │          │    [Tab]     │                       │
│  └──────────────┘          └──────────────┘                       │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Search Panel (Highlighted)                                  │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐                  │  │
│  │  │Case      │  │First Name│  │Last Name │                  │  │
│  │  │Number    │  │(CP/NCP)  │  │(CP/NCP)  │                  │  │
│  │  └──────────┘  └──────────┘  └──────────┘                  │  │
│  │                                                               │  │
│  │  [Search Button] [Clear Button]                              │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Search Results Table                                        │  │
│  │  ┌──────┬──────────┬────────┬──────────┬─────────┐         │  │
│  │  │Case #│CP Name   │NCP Name│Last Update│Actions │         │  │
│  │  ├──────┼──────────┼────────┼──────────┼─────────┤         │  │
│  │  │12345 │Jane Doe  │John Doe│01/15/2024│[View]   │         │  │
│  │  └──────┴──────────┴────────┴──────────┴─────────┘         │  │
│  │                                                               │  │
│  │  [< Previous] [1] [2] [3] [Next >]                          │  │
│  └─────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Search Panel**: Prominent, centered, with icon indicators
- **Input Fields**: Auto-complete suggestions for case numbers
- **Search Button**: Large, prominent, with search icon
- **Results Table**: Sortable columns, row highlighting on hover
- **Pagination**: Bottom center with page numbers and navigation arrows
- **Empty State**: Friendly message when no results found

### Business Logic:
The Main Landing Page is the **entry point** for the Locate module. Users search by **case number** and/or **first name** and **last name** (CP or NCP). The system validates all entered values before executing the search. Search logic queries internal Person and Case tables (with fuzzy matching for names); results are returned as a list of matching cases with CP name, NCP name, and last update. **Clear** resets all search fields. **Pagination** controls limit the number of rows per page and allow navigation through large result sets. The Cases and Required Action tabs determine whether the user works from search results or from a prioritized task list. No locate data is updated on this page—it is purely **search and navigation** to identify the case/person to work on.

---

## 8.2 Cases Tab - Search Results with Accordion

### Design Concept:
**Layout**: Two-column layout with accordion expansion
**Interaction**: Click to expand case details

```
┌─────────────────────────────────────────────────────────────────────┐
│  [Search Results - 5 cases found]                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Case: 12345                    [🔍 I] Intake Case          │  │
│  │  CP: Jane Doe | NCP: John Doe                                │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ ▼ Locate Summary  [Expanded]                        │   │  │
│  │  │ ▼ Demographics                                        │   │  │
│  │  │ ▼ Address                                             │   │  │
│  │  │ ▼ Employer                                            │   │  │
│  │  │ ▼ Contact                                             │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Case: 12346                    [🔴 R] Referral Case        │  │
│  │  CP: Mary Smith | NCP: Bob Smith                             │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ ▶ Locate Summary  [Collapsed]                       │   │  │
│  │  │ ▶ Demographics                                        │   │  │
│  │  │ ▶ Address                                             │   │  │
│  │  │ ▶ Employer                                            │   │  │
│  │  │ ▶ Contact                                             │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Case Indicator**: Color-coded icon (Yellow=I, Red=R) in top-right
- **Accordion Icons**: ▶ collapsed, ▼ expanded
- **Hover Effect**: Entire case row highlights on hover
- **Expand Animation**: Smooth accordion expansion/collapse
- **Quick Actions**: Action buttons visible on hover

### Business Logic:
This page appears **after a user selects a case** from the Main Landing search results. Each result row expands into an accordion with five sections: **Locate Summary**, **Demographics**, **Address**, **Employer**, and **Contact**. The accordion lets the worker **drill down** into a specific locate area without leaving the case context. Case indicators (e.g., Intake vs Referral) drive **visibility and workflow rules**—e.g., certain actions may be restricted for referral cases. Only one case’s accordion is typically expanded at a time; expanding another can optionally collapse the previous. **No data is persisted** on this page; it is a **navigation layer** that routes the user to the detailed pages (Summary, Demographics, Address, etc.) where actual locate updates occur.

---

## 8.3 Locate Summary Page Design

### Design Concept:
**Layout**: Card-based design with expandable sections
**Visual Hierarchy**: Case info at top, sections below

```
┌─────────────────────────────────────────────────────────────────────┐
│  Case Information Card (Fixed Top)                                  │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Case #: 12345 | Type: IV-D | Status: Active                │  │
│  │  CP: Jane Doe | MDM: MDM12345 | SSN: ***-**-1234            │  │
│  │  NCP: John Doe | MDM: MDM67890 | SSN: ***-**-5678           │  │
│  └─────────────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  ▼ Case Information                                         │  │
│  │  [Expanded Section with details]                            │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  ▼ Address Information                                      │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Type    Address                    Status   Source   │   │  │
│  │  │ Mail    123 Main St, Baltimore...  Active   NDNH    │   │  │
│  │  │ Res     456 Oak Ave, Baltimore...  Active   Manual  │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │  [< 1 2 3 >]                                                │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  ▼ Employer Information                                     │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Employer         Address          Status   Start    │   │  │
│  │  │ ABC Corp        789 Biz St...     Active   01/2024  │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  ▼ Change History                                           │  │
│  │  [Table with pagination]                                    │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  [Previous] [Next]                                                  │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Card Design**: Each section in a card with subtle shadow
- **Expandable Sections**: Smooth expand/collapse with icons
- **Table Design**: Clean tables with alternating row colors
- **Source Badges**: Color-coded badges for data sources (NDNH, FCR, Manual, etc.)
- **Status Indicators**: Green (Active), Red (Inactive), Yellow (Pending)

### Business Logic:
The Locate Summary page is **read-only** and provides a **consolidated overview** of all locate-related data for the selected NCP/CP. **Case Information** is fixed at the top and reflects the current case and party identifiers (case #, type, status, CP/NCP names, MDM IDs, SSN masking). **Address Information**, **Employer Information**, and **Change History** are loaded from Person_Address, Person_Employer, and audit tables; each section supports **pagination** when there are multiple records. Source badges (NDNH, FCR, Manual) indicate where each address or employer record originated, supporting **source priority** and **conflict resolution**. Status (Active, Inactive, Pending) drives downstream use—e.g., only active addresses are used for service or disbursement. **Previous/Next** navigation moves between sections or back to the accordion. No updates are performed on this page; it is for **review and context** before making changes on Demographics, Address, or Employer pages.

---

## 8.4 Demographics Page Design

### Design Concept:
**Layout**: Multi-step wizard with tabs/sections
**Visual Flow**: From Sources → Add New → Change History

```
┌─────────────────────────────────────────────────────────────────────┐
│  Case Information (Top Bar)                                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  NCP Demographics from Sources                              │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ [○] Source: NDNH | Received: 01/15/2024            │   │  │
│  │  │ Name: John Doe | DOB: 01/01/1980 | Status: Verified│   │  │
│  │  │                                                       │   │  │
│  │  │ [○] Source: FCR | Received: 01/10/2024              │   │  │
│  │  │ Name: John A. Doe | DOB: 01/01/1980 | Status: Review│   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  [Reset] [Update Selected] [Enterprise Search] [Next →]     │  │
│  │                                                               │  │
│  │  Showing 1-2 of 2 records  [< 1 >]                           │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  NCP SSN from Sources                                        │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ [○] Source: FCR | SSN: ***-**-5678 | Status: Active│   │  │
│  │  │ [○] Source: Manual | SSN: ***-**-5679 | Status: Old│   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  [← Previous] [Reset] [Enterprise Search] [Update] [Next]   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Add New                                                      │  │
│  │  [Add New Button] → Opens modal/drawer                       │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Change History                                              │  │
│  │  [History table with pagination]                             │  │
│  └─────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Radio Buttons**: Clear selection indicators
- **Source Badges**: Distinct colors for each source type
- **Status Colors**: Visual status indicators
- **Button Grouping**: Related actions grouped together
- **Modal/Drawer**: Add New opens side panel or modal
- **Progress Indicator**: Shows current step in multi-step process

### Business Logic:
The Demographics page supports **viewing, comparing, and updating** NCP/CP demographic data (name, DOB, SSN) from multiple sources. **NCP/CP Demographics from Sources** and **SSN from Sources** list records from NDNH, FCR, FPLS, or manual entry; each row is **selectable via radio**. **Reset** clears the current selection. **Update** applies the selected source’s data to the person record using the standard **data-update workflow**: validation → Person table update → audit log → optional notification to other modules. **Enterprise Search** triggers NDNH/FCR/FPLS queries; results appear in the “From Sources” sections for the user to select and update. **Add New** opens a form to enter demographics manually; that data is stored with source = Manual. **Change History** shows who changed what and when, supporting audit and **conflict resolution**. **Previous/Next** move between Demographics, SSN, Add New, and Change History. **Source priority** applies: federal data overrides manual when both exist, unless the user explicitly overwrites after review.

---

## 8.5 Address Page Design

### Design Concept:
**Layout**: Form-based with address validation indicators
**Visual Feedback**: Real-time address validation

```
┌─────────────────────────────────────────────────────────────────────┐
│  Current Address Information                                        │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Address Type: Residential [Active]                         │  │
│  │  456 Oak Avenue, Baltimore, MD 21201                        │  │
│  │  Status: ✓ Validated | Source: NDNH | Updated: 01/15/2024  │  │
│  └─────────────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Address from Sources                                        │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ [○] Source: NDNH | Type: Residential                │   │  │
│  │  │     123 Main St, Baltimore, MD 21201                │   │  │
│  │  │     Status: ✓ Validated | Date: 01/15/2024         │   │  │
│  │  │                                                       │   │  │
│  │  │ [○] Source: FCR | Type: Mailing                      │   │  │
│  │  │     P.O. Box 123, Baltimore, MD 21201               │   │  │
│  │  │     Status: ⚠ Needs Review | Date: 01/10/2024      │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  [Reset Selection] [Save Selected]                           │  │
│  │  [< 1 2 3 >]                                                 │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Add New Address                                             │  │
│  │  [Add New Address Button] → Opens form                       │  │
│  │                                                               │  │
│  │  Form Fields (in modal/drawer):                              │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Address Type: [Dropdown]                            │   │  │
│  │  │ Address Line 1: [_________________]                 │   │  │
│  │  │ Address Line 2: [_________________]                 │   │  │
│  │  │ City: [_________________]                           │   │  │
│  │  │ State: [Dropdown ▼]                                 │   │  │
│  │  │ Zip: [_______]                                      │   │  │
│  │  │ International: [○ Yes] [○ No]                       │   │  │
│  │  │ [Validate Address Button] → Shows validation status │   │  │
│  │  │                                                       │   │  │
│  │  │ Validation Status: ✓ Validated                       │   │  │
│  │  │ Suggested Format: [Shows standardized address]       │   │  │
│  │  │ [Use Suggested Format] [Keep Original]               │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Change History                                              │  │
│  │  [Table with address change history]                         │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  [← Previous]                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Address Validation**: Real-time validation with visual feedback
- **Validation Status Icons**: ✓ (Validated), ⚠ (Needs Review), ✗ (Invalid)
- **Map Integration**: Optional map view for address verification
- **Suggested Format**: Highlighted when address validation suggests changes
- **Source Indicators**: Clear source badges for each address
- **Address Cards**: Each address in a card format for easy scanning

### Business Logic:
The Address page manages **current addresses** and **addresses from sources** for the selected NCP/CP. **Current Address Information** shows the active address(es) from Person_Address used for service, IWO, or disbursement. **Address from Sources** lists addresses from NDNH, FCR, FPLS, or manual entry; the user **selects** one or more and clicks **Save Selected** to apply them via the **data-update workflow**. **Add New Address** opens a form; entered addresses are **validated** (USPS for U.S., format checks for international) before save. **Validate Address** runs real-time validation; **Valid** → accept and standardize, **Invalid** → flag for review, **Suggestions** → present options (e.g., Use Suggested Format vs Keep Original). Validation status (✓ / ⚠ / ✗) is stored and displayed. **Change History** records all address changes with source, user, and timestamp. **Previous** returns to the prior section or accordion. Address updates **propagate** to Case Management, Enforcement, Establishment, and Finance when those modules use locate data.

---

## 8.6 Employer Page Design

### Design Concept:
**Layout**: Table-based with add employer functionality
**Visual Elements**: Employer cards with key information

```
┌─────────────────────────────────────────────────────────────────────┐
│  Current Employer Information                                       │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  ABC Corporation                                             │  │
│  │  789 Business Street, Baltimore, MD 21201                    │  │
│  │  FEIN: **-******* | Status: Active | Start: 01/2024        │  │
│  └─────────────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Employer from Sources                                       │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ [○] Source: NDNH | Employer: ABC Corp              │   │  │
│  │  │     Address: 789 Business St...                    │   │  │
│  │  │     Status: Verified | Start: 01/2024             │   │  │
│  │  │                                                       │   │  │
│  │  │ [○] Source: FCR | Employer: ABC Corporation         │   │  │
│  │  │     Address: 789 Business Street...                │   │  │
│  │  │     Status: Needs Verification | Start: 12/2023   │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  [Reset Selection] [Add Employer]                            │  │
│  │  [< 1 2 3 >]                                                 │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Add New Employer                                            │  │
│  │  [Add Employer Button] → Opens form                          │  │
│  │                                                               │  │
│  │  Employer Search Feature:                                    │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Search by FEIN/SEIN: [_____________] [Search]      │   │  │
│  │  │ Search by Name: [___________________] [Search]      │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  Employer Form:                                              │  │
│  │  • Employer Name (mandatory)                                 │  │
│  │  • FEIN/SEIN (with mask)                                     │  │
│  │  • Address (with validation)                                 │  │
│  │  • Phone, Email                                              │  │
│  │  • Start Date, End Date                                      │  │
│  │  • [← Previous] [Save] [Next →]                             │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Change History                                              │  │
│  │  [Employer change history table]                             │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  [← Previous]                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Employer Cards**: Visual cards for each employer
- **FEIN/SEIN Masking**: Sensitive data masked with reveal toggle
- **Employer Search**: Quick search by FEIN or name
- **Status Badges**: Active, Inactive, Pending verification
- **Employment Timeline**: Visual timeline of employment history

### Business Logic:
The Employer page manages **current employer** data and **employers from sources** (e.g., NDNH) for the selected NCP/CP. **Current Employer Information** displays the active employer(s) from Person_Employer used for IWO and enforcement. **Employer from Sources** lists employers returned from NDNH, FCR, or manual entry; the user **selects** a record and clicks **Add Employer** to add it to the person’s employer history. **Add New Employer** supports **manual entry** or **search by FEIN/SEIN or name**; matched employers can be imported to avoid duplicates. Employer **verification** (FEIN/SEIN lookup, address validation) runs before save; status (Verified, Needs Verification) is stored and shown. **Reset** clears the current selection. **Change History** logs all employer additions and updates. **Previous** navigates back. Employer updates flow to **Enforcement** for IWO issuance; **source priority** and **change tracking** apply as on Demographics and Address.

---

## 8.7 Contact Page Design

### Design Concept:
**Layout**: Contact information cards with add functionality
**Visual Design**: Clean, organized contact information display

```
┌─────────────────────────────────────────────────────────────────────┐
│  Current Contact Information                                        │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Phone: (410) 555-1234 [Primary] | Cell: (410) 555-5678     │  │
│  │  Email: john.doe@email.com                                  │  │
│  │  Notification: Paperless | Text: Yes | Email: Yes           │  │
│  └─────────────────────────────────────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Add New Contact                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Contact Type: [Dropdown: Phone/Email]               │   │  │
│  │  │ Phone/Email: [___________________]                  │   │  │
│  │  │ Primary: [Checkbox]                                 │   │  │
│  │  │ Notification Preferences:                            │   │  │
│  │  │   [○ Paper] [○ Paperless]                           │   │  │
│  │  │   Text Notification: [○ Yes] [○ No]                 │   │  │
│  │  │   Email Notification: [○ Yes] [○ No]                │   │  │
│  │  │                                                       │   │  │
│  │  │ [Save] [Clear]                                       │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Change History                                              │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Date       Type    Old Value    New Value   User   │   │  │
│  │  │ 01/15/2024 Phone   555-1111     555-1234    User1  │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │  [< 1 2 3 >]                                                │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  [← Previous]                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Contact Cards**: Organized contact information in cards
- **Primary Indicator**: Clear indication of primary contact method
- **Quick Actions**: Edit/Delete buttons on hover
- **Notification Toggles**: Easy toggle switches for preferences
- **Validation**: Real-time format validation for phone/email

### Business Logic:
The Contact page manages **phone and email** contact information and **notification preferences** for the selected NCP (or CP when applicable). **Current Contact Information** shows existing phone, email, and preferences (e.g., Paper vs Paperless, Text, Email) from Person_Contact. **Add New Contact** collects contact type (Phone/Email), value, primary flag, and notification settings; the system **validates** format (e.g., phone pattern, valid email) before save. **Save** persists the new contact and **Clear** resets the form. Only **one primary** contact per type is typically allowed; setting a new primary can demote the previous. **Change History** records all contact changes. Contact data supports **locate follow-up** (e.g., outreach) and **notification delivery**; it does not directly drive service or IWO, but it complements address and employer data. **Previous** returns to the prior section or accordion.

---

## 8.8 File Upload Page Design

### Design Concept:
**Layout**: Search panel + file upload area
**Visual Feedback**: Upload progress and file list

```
┌─────────────────────────────────────────────────────────────────────┐
│  File Upload - Locate Module                                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Search Case/Application                                    │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Search By: [○ Case Number] [○ Application Number]  │   │  │
│  │  │ Enter Value: [___________________] [Search]        │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Case Information (Displayed after search)                  │  │
│  │  Case #: 12345 | Application #: APP123456                   │  │
│  │  Member ID: MEM789 | MDM ID: MDM12345                       │  │
│  │  Name: John Doe | DOB: 01/01/1980                           │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  File Upload Section                                         │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ Instructions:                                       │   │  │
│  │  │ "Documents supporting locate information can be     │   │  │
│  │  │  uploaded. Files must be less than 25 MB each,     │   │  │
│  │  │  total not exceeding 250 MB.                        │   │  │
│  │  │  Formats: PDF, Word (.doc, .docx), Images"         │   │  │
│  │  │                                                       │   │  │
│  │  │  Category: [Select Category ▼]                       │   │  │
│  │  │  Document Type: [Select Type ▼]                      │   │  │
│  │  │  Document Subtype: [Select Subtype ▼]                │   │  │
│  │  │                                                       │   │  │
│  │  │  [Choose File] or [Scan]                             │   │  │
│  │  │                                                       │   │  │
│  │  │  Selected Files:                                      │   │  │
│  │  │  ✓ document1.pdf (2.5 MB) [Remove]                   │   │  │
│  │  │  ✓ document2.jpg (1.8 MB) [Remove]                   │   │  │
│  │  │                                                       │   │  │
│  │  │  Total Size: 4.3 MB / 250 MB                          │   │  │
│  │  │                                                       │   │  │
│  │  │  [Upload Files]                                       │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Uploaded Files                                              │  │
│  │  [Table showing previously uploaded files]                   │  │
│  └─────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Drag & Drop**: Optional drag-and-drop file upload area
- **File Preview**: Thumbnail preview for images
- **Progress Bar**: Upload progress indicator
- **File Size Indicator**: Visual indicator of total size
- **File List**: Clear list of selected files with remove option
- **Validation Messages**: Clear error messages for invalid files

### Business Logic:
The File Upload page attaches **supporting documents** to locate cases (e.g., identity documents, court papers, locate reports). The user **searches by Case Number or Application Number**; the system returns case details (Case #, Application #, Member ID, Jurisdiction, SSN/ITIN, Name, DOB, MDM ID, IRN) to confirm context. **Category**, **Document Type**, and **Document Subtype** are required so files are classified correctly for retrieval and reporting. **Business rules**: each file **under 25 MB**, total batch **up to 250 MB**; formats **PDF, .doc, .docx, .jpg, .png, .gif, .bmp** only. **Choose File** or **Scan** adds files to the selection; **Remove** drops one before upload. **Upload** validates size and type, then stores files in document management and links them to the case/member. **Uploaded Files** lists existing documents with pagination. Uploads support **audit** and **locate justification**; they do not update Person_Address, Person_Employer, or demographics directly.

---

## 8.9 Required Action Tab Design

### Design Concept:
**Layout**: Task list with filters and sorting
**Visual Priority**: High-priority actions highlighted

```
┌─────────────────────────────────────────────────────────────────────┐
│  Required Actions - Locate Module                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Filters                                                     │  │
│  │  Priority: [All ▼] | Status: [All ▼] | Date Range: [______]│  │
│  │  [Apply Filters] [Clear]                                    │  │
│  └─────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐  │
│  │  Actions (12 pending)                                        │  │
│  │  ┌─────────────────────────────────────────────────────┐   │  │
│  │  │ [!] High Priority                                    │   │  │
│  │  │ Case #: 12345 | Action: Verify NCP Address          │   │  │
│  │  │ Due: 01/20/2024 | Assigned: Worker1                 │   │  │
│  │  │ [View Case] [Complete]                               │   │  │
│  │  │                                                       │   │  │
│  │  │ [ ] Normal Priority                                   │   │  │
│  │  │ Case #: 12346 | Action: Update Employer Info         │   │  │
│  │  │ Due: 01/25/2024 | Assigned: Worker2                 │   │  │
│  │  │ [View Case] [Complete]                               │   │  │
│  │  └─────────────────────────────────────────────────────┘   │  │
│  │                                                               │  │
│  │  [< 1 2 3 4 5 >]                                            │  │
│  └─────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### UI/UX Elements:
- **Priority Indicators**: Color-coded priority badges (Red=High, Yellow=Medium, Green=Low)
- **Due Date Highlighting**: Overdue actions in red
- **Quick Actions**: View and Complete buttons for each action
- **Sorting**: Sort by priority, due date, case number
- **Filter Panel**: Collapsible filter panel
- **Action Count**: Badge showing number of pending actions

### Business Logic:
The Required Action tab is a **task queue** for locate-related work items. Actions are created by **business rules** (e.g., new locate request from Intake, stale address, employer verification needed, Enterprise Search results to review) or **manually** by supervisors. Each action has **case**, **action type** (e.g., Verify NCP Address, Update Employer Info), **priority**, **due date**, and **assignee**. **Filters** (Priority, Status, Date Range) and **sorting** (priority, due date, case number) let workers focus on high-priority or overdue tasks. **View Case** opens the case in the Cases tab and scrolls to the relevant accordion section (e.g., Address, Employer). **Complete** marks the action done and optionally records a brief outcome; the system may **create follow-up actions** (e.g., “Verify address” → “Update from NDNH”). Overdue actions are **highlighted** to support SLA and workload management. The **action count** badge drives **workload balancing** and reporting. No Person or Case data is updated on this page; it **routes** users to the correct locate pages to perform the work.

---

## 8.10 Design Principles and Best Practices

### Color Scheme:
- **Primary**: Professional blue (#2563EB) for primary actions
- **Secondary**: Gray (#6B7280) for secondary elements
- **Success**: Green (#10B981) for validated/active status
- **Warning**: Yellow (#F59E0B) for needs review
- **Error**: Red (#EF4444) for errors/invalid
- **Info**: Blue (#3B82F6) for informational messages

### Typography:
- **Headings**: Bold, 18-24px
- **Body**: Regular, 14-16px
- **Labels**: Medium weight, 14px
- **Small Text**: Regular, 12px

### Spacing:
- **Section Padding**: 24px
- **Field Spacing**: 16px vertical
- **Button Spacing**: 12px between buttons
- **Card Margin**: 16px

### Responsive Design:
- **Desktop**: Full layout with all columns
- **Tablet**: Condensed layout, collapsible panels
- **Mobile**: Stack layout, full-width elements

### Accessibility:
- **WCAG 2.1 AA Compliance**: Color contrast ratios
- **Keyboard Navigation**: Full keyboard support
- **Screen Reader**: Proper ARIA labels
- **Focus Indicators**: Clear focus states

---

**Document Status**: Complete with detailed business logic, external connections, and page-by-page design ideas for Locate module

**Purpose**: Provides comprehensive information for developers and designers to implement the Locate module with proper business logic, external integrations, and user-friendly design.
