# CSMS Module 8: INTERGOVERNMENTAL - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Intergovernmental Module to enable developers to implement interstate child support case processing functionality in the Child Support Management System. The module supports UIFSA (Uniform Interstate Family Support Act) compliance for cases involving multiple states or jurisdictions.

---

## Table of Contents
1. [Intergovernmental Module Overview](#81-intergovernmental-module-overview)
2. [Intergovernmental Case Types](#82-intergovernmental-case-types)
3. [Initiating State Workflow](#83-initiating-state-workflow)
4. [Responding State Workflow](#84-responding-state-workflow)
5. [Case Transmittal Management](#85-case-transmittal-management)
6. [Interstate Establishment](#86-interstate-establishment)
7. [Interstate Locate](#87-interstate-locate)
8. [Interstate Enforcement](#88-interstate-enforcement)
9. [Interstate Financial/Payment Processing](#89-interstate-financialpayment-processing)
10. [UIFSA Compliance and Tracking](#810-uifsa-compliance-and-tracking)

---

# 8.1 Intergovernmental Module Overview

### User Story 8.1.1: Intergovernmental Module Access
**As a** case worker  
**I want** to access the Intergovernmental module  
**So that** I can manage interstate child support cases

#### Acceptance Criteria:
1. There should be an Intergovernmental module tab in the second top navigation (alongside Case Registration, Case Management, Locate, Establishment, Enforcement, Financial Management).
2. Clicking on "Intergovernmental" reveals sub-tabs or left navigation:
   - Intergovernmental Cases (Initiating)
   - Intergovernmental Cases (Responding)
   - Case Transmittal
   - UIFSA Case Search
3. The module should support both **Initiating State** and **Responding State** workflows.
4. Access permissions ensure only authorized users (case workers, intergovernmental specialists) can access the module.

---

# 8.2 Intergovernmental Case Types

### User Story 8.2.1: Interstate Case Type Identification
**As a** case worker  
**I want** to identify and categorize interstate cases  
**So that** I can route them correctly per UIFSA

#### Acceptance Criteria:
1. System should identify UIFSA case types:
   - **Initiating State** – Maryland sends request to another state (NCP or child in another jurisdiction)
   - **Responding State** – Maryland receives request from another state
2. Interstate case status options:
   - Maryland (in-state case)
   - Interstate Initiating
   - Interstate Responding
   - Interstate – Both (complex cases)
3. Case must capture:
   - Initiating State (FIPS code, state name, case number)
   - Responding State (FIPS code, state name, case number)
   - Controlling Order Jurisdiction (when applicable)
4. System should query FCR (Federal Case Registry) to identify interstate involvement and potential duplicate cases before registration.

---

# 8.3 Initiating State Workflow

### User Story 8.3.1: Initiating State Case Processing
**As a** case worker  
**I want** to process cases where Maryland is the initiating state  
**So that** I can request establishment or enforcement from another state

#### Acceptance Criteria:
1. **Pre-Transmittal Checklist:**
   - Verify NCP/child is in another jurisdiction
   - Determine if child support order exists (query FCR)
   - Identify controlling order when multiple orders exist
   - Gather required documentation (application, court order, etc.)
2. **Case Transmittal (within 20 calendar days per federal requirements):**
   - Select responding state central registry/central authority
   - Transmittal date (mandatory)
   - Transmittal method (electronic, mail)
   - Transmittal status (Pending, Sent, Received, Acknowledged)
   - Tracking/reference number
3. **Ongoing Initiating State Duties:**
   - Provide responding agency with sufficient, accurate information
   - Respond to requests for additional information within 30 calendar days
   - Notify responding agency annually of interest on overdue support
   - Receive, distribute, and disburse collections per federal rules
   - Accept payments from responding agency even if initiating case is closed
4. **Data Fields:**
   - Initiating State: Maryland, FIPS code, Case Number
   - Responding State: State, FIPS code, Case Number (when assigned)
   - Request Type: Establishment (Paternity/Support), Enforcement, Modification, Location
   - Transmittal Date, Status, Response Date

---

# 8.4 Responding State Workflow

### User Story 8.4.1: Responding State Case Processing
**As a** case worker  
**I want** to process cases where Maryland is the responding state  
**So that** I can establish or enforce child support on behalf of the initiating state

#### Acceptance Criteria:
1. **Case Receipt:**
   - Receive transmittal from initiating state central registry
   - Record receipt date
   - Create/link Maryland responding case number
   - Acknowledge receipt to initiating state
2. **Case Processing:**
   - Route to appropriate workflow (Establishment, Locate, Enforcement)
   - Perform requested action (paternity establishment, support order, IWO, etc.)
   - Update initiating state on progress
3. **Collection Handling:**
   - Send collections to initiating state per federal IV-D rules
   - Track payment transmission
   - Maintain payment history for both states
4. **Data Fields:**
   - Initiating State: State, FIPS code, Case Number
   - Responding State: Maryland, FIPS code, Case Number
   - Received Date, Acknowledgment Date
   - Response Status, Action Taken, Completion Date

---

# 8.5 Case Transmittal Management

### User Story 8.5.1: Case Transmittal Tracking
**As a** case worker  
**I want** to track case transmittals to and from other states  
**So that** I can ensure timely processing and compliance

#### Acceptance Criteria:
1. Transmittal tracking for both directions (Initiating → Responding, Responding → Initiating).
2. Transmittal record fields:
   - Transmittal ID (unique)
   - Direction (Outbound/Inbound)
   - From State/FIPS/Case Number
   - To State/FIPS/Case Number
   - Transmittal Date
   - Transmittal Status (Pending, Sent, Received, Acknowledged, Rejected, Returned)
   - Request Type
   - Response Date (when applicable)
   - Tracking Number
   - Notes
3. Status workflow and date tracking for each status change.
4. Alerts for transmittals pending beyond 20 days (initiating) or 30 days (response to additional info request).
5. Integration with document management for attached transmittal packages.

---

# 8.6 Interstate Establishment

### User Story 8.6.1: Interstate Paternity and Support Establishment
**As a** case worker  
**I want** to establish paternity or support orders in interstate cases  
**So that** I can create legal obligations across state lines

#### Acceptance Criteria:
1. Link to Establishment module with interstate context.
2. Initiating State: Request establishment from responding state; track request and response.
3. Responding State: Perform establishment (paternity, support order) in Maryland; report outcome to initiating state.
4. Court order information must capture:
   - Establishment state/county/court
   - Controlling order jurisdiction
   - Non-MD case number, Non-MD court order reference
5. UIFSA case type identification (e.g., initial order, modification, registration of foreign order).

---

# 8.7 Interstate Locate

### User Story 8.7.1: Interstate Locate Services
**As a** case worker  
**I want** to locate NCP/CP across state lines  
**So that** I can support establishment and enforcement in interstate cases

#### Acceptance Criteria:
1. Integration with Locate module and FPLS (Federal Parent Locator Service).
2. When NCP is in another state:
   - Initiating State: Request locate from responding state or use FPLS
   - Responding State: Perform locate; return address/employer to initiating state
3. Support for international locate (Country field) when NCP is outside the U.S.
4. Locate request/response tracking for interstate cases.
5. Data fields: Country, State, County for jurisdiction; Non-MD Case Number for cross-reference.

---

# 8.8 Interstate Enforcement

### User Story 8.8.1: Interstate Enforcement Actions
**As a** case worker  
**I want** to enforce child support orders across state lines  
**So that** I can collect support when NCP is in another jurisdiction

#### Acceptance Criteria:
1. Integration with Enforcement module for interstate context.
2. **Initiating State:** Request enforcement from responding state; receive and disburse collections.
3. **Responding State:** Perform enforcement (IWO, license suspension, etc.) in Maryland; send collections to initiating state.
4. IWO and other enforcement actions must reference interstate case numbers.
5. Collection transmission tracking (amount, date sent, date received by initiating state).
6. Support for registration of foreign support order for enforcement.

---

# 8.9 Interstate Financial/Payment Processing

### User Story 8.9.1: Interstate Payment Handling
**As a** case worker / finance worker  
**I want** to process payments in interstate cases  
**So that** I can distribute collections correctly per federal rules

#### Acceptance Criteria:
1. Integration with Finance module for interstate payment flows.
2. **Initiating State:** Receive collections from responding state; distribute per federal allocation rules.
3. **Responding State:** Send collections to initiating state per IV-D regulations; track transmission.
4. Payment must be tagged with initiating/responding state and case numbers for proper allocation.
5. Support for foreign tax offset investigation (Intergovernmental Tax section) when applicable.
6. Interest and penalties tracking for interstate arrears.

---

# 8.10 UIFSA Compliance and Tracking

### User Story 8.10.1: UIFSA Compliance Tracking
**As a** case worker / supervisor  
**I want** to track UIFSA compliance metrics  
**So that** I can ensure timely processing and meet federal requirements

#### Acceptance Criteria:
1. Timeliness tracking:
   - Transmittal within 20 days (initiating)
   - Response to additional info within 30 days
   - Annual interest notification to responding state
2. UIFSA case type and status reporting.
3. Dashboard or report showing:
   - Pending transmittals
   - Overdue responses
   - Active initiating vs. responding case counts
4. Audit trail for all interstate actions (transmittal, receipt, acknowledgment, collection transmission).

---

## Integration Points

| Module | Integration |
|--------|-------------|
| **Case Management** | Intergovernmental status, initiating/responding state fields, case search |
| **Case Registration** | Identify interstate at registration; FCR query before case creation |
| **Locate** | Interstate locate; FPLS; Non-MD case/order reference |
| **Establishment** | Interstate paternity/support establishment; controlling order |
| **Enforcement** | Interstate IWO, collection transmission |
| **Finance** | Interstate payment receipt, distribution, disbursement |
| **FCR** | Interstate case matching, duplicate detection |

---

## Data Storage (Suggested)

- `intergovernmental_case` – Interstate case header (initiating/responding, state info, case numbers)
- `case_transmittal` – Transmittal records (inbound/outbound, dates, status)
- `interstate_payment` – Payment tracking for interstate collection transmission

---

**Document Status:** Complete requirements for Intergovernmental Module workflow.

**Related Documents:**
- CSMS_Developer_Requirements_with_Acceptance_Criteria.md
- CSMS_Module_3_Case_Management_Requirements.md
- CSMS_Module_4_Locate_Requirements.md
- CSMS_Module_5_Establishment_Requirements.md
- CSMS_Module_6_Enforcement_Requirements.md
- CSMS_Module_7_Finance_Requirements.md
- CSMS_Business_Flow_Module_Connections.md
