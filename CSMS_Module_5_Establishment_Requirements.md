# CSMS Module 5: ESTABLISHMENT - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Establishment Module (Paternity and Support Order Establishment) to enable developers to implement establishment functionality in the Child Support Management System.

---

## Table of Contents
1. [Establishment Module Overview](#51-establishment-module-overview)
2. [Paternity Establishment](#52-paternity-establishment)
3. [Support Order Establishment](#53-support-order-establishment)
4. [Court Order Management](#54-court-order-management)
5. [Hearing Management](#55-hearing-management)
6. [Intergovernmental Establishment](#56-intergovernmental-establishment)

---

# 5.1 Establishment Module Overview

The Establishment Module handles the establishment of paternity and child support orders. This module includes workflows for paternity establishment, support order creation, court order management, and hearing coordination.

---

# 5.2 Paternity Establishment

### User Story 5.2.1: Paternity Establishment Workflow
**As a** case worker  
**I want** to establish paternity for a child  
**So that** I can create legal parentage records

#### Acceptance Criteria:
1. System should provide paternity establishment workflow for cases requiring paternity establishment.
2. Paternity status tracking:
   - Status options: Requires Establishment, Established, Not Established
   - Status date tracking
   - Establishment method tracking
3. Affidavit of Paternity (AOP) Management:
   - AOP creation and recording
   - AOP Number (unique identifier)
   - AOP Date
   - AOP Status (Active, Rescinded, Undeclared)
   - Rescission date (if applicable)
   - Undeclared date (if applicable)
   - Parties involved (CP, NCP, Child)
4. Genetic Testing Management:
   - Test request functionality
   - Test date tracking
   - Test results (Positive, Negative, Inconclusive)
   - Test status tracking
   - Lab information
5. Court Order for Paternity:
   - Court order number
   - Court order date
   - Establishment state/county/court
   - Establishment date
6. Data Storage:
   - Paternity information stored in `parentage_information` table
   - AOP information stored in `affidavit_of_paternity` table
   - Genetic test information stored in `genetic_test` table
   - Court order information stored in `court_order` table

---

# 5.3 Support Order Establishment

### User Story 5.3.1: Support Order Establishment
**As a** case worker  
**I want** to establish child support orders  
**So that** I can create legal support obligations

#### Acceptance Criteria:
1. System should provide support order establishment workflow.
2. Order Type Management:
   - Initial Order
   - Modification Order
   - Temporary Order
3. Order Details:
   - Court Order Number (unique identifier, mandatory)
   - Court Information:
     - Court Name
     - Court State (mandatory)
     - Court County (mandatory)
   - Order Date (mandatory)
   - Effective Date (mandatory)
   - Entered Date
   - Order Status (Active, Modified, Terminated, etc.)
4. Obligation Details:
   - Obligation Type (Current Support, Arrears, Medical Support, Child Care)
   - Amount (mandatory for current support)
   - Frequency (Weekly, Biweekly, Monthly, etc., mandatory)
   - Start Date (mandatory)
   - End Date (if applicable)
   - Arrears Calculation
5. Support Calculation:
   - Income Information capture
   - Guidelines Application
   - Deviation Reasons (if applicable)
   - Calculation Worksheets
6. Data Storage:
   - Court order information stored in `court_order` table (establishment schema)
   - Obligation information stored in `obligation` table (establishment schema)
   - Links to case and parties

---

# 5.4 Court Order Management

### User Story 5.4.1: Court Order Management
**As a** case worker  
**I want** to manage court orders  
**So that** I can track and maintain order information

#### Acceptance Criteria:
1. System should provide court order viewing and modification capabilities.
2. Court Order Display:
   - Court Order Number
   - Court Order Type (Paternity, Support, Modification)
   - Obligation Type
   - Court information (Name, State, County)
   - Dates (Order Date, Effective Date, Entered Date)
   - Court Order Status
   - Related obligations
3. Court Order Modification:
   - Ability to update order status
   - Ability to modify obligation amounts
   - History tracking
4. Court Order History:
   - View all orders for a case
   - View order modifications
   - Date tracking for all changes

---

# 5.5 Hearing Management

### User Story 5.5.1: Hearing Scheduling and Management
**As a** case worker  
**I want** to schedule and manage hearings  
**So that** I can coordinate court proceedings

#### Acceptance Criteria:
1. System should provide hearing management functionality.
2. Hearing Scheduling:
   - Hearing Type (Paternity, Support, Modification)
   - Hearing Date (mandatory)
   - Hearing Time (mandatory)
   - Court Name (mandatory)
   - Hearing Status (Scheduled, Completed, Cancelled, Postponed)
3. Hearing Details:
   - Case information
   - Parties involved
   - Hearing Type
   - Court location
4. Hearing Outcomes:
   - Outcome tracking (Ordered, Denied, Continued, etc.)
   - Outcome Date
   - Hearing Notes
   - Related orders created
5. Data Storage:
   - Hearing information stored in `hearing` table (establishment schema)

---

# 5.6 Intergovernmental Establishment

### User Story 5.6.1: Interstate Establishment Cases
**As a** case worker  
**I want** to manage interstate establishment cases  
**So that** I can handle cross-state establishment

#### Acceptance Criteria:
1. System should support intergovernmental establishment cases.
2. Interstate Case Handling:
   - Initiating State Information:
     - State
     - FIPS Code
     - Case Number
   - Responding State Information:
     - State
     - FIPS Code
     - Case Number
3. UIFSA Compliance:
   - UIFSA case type identification
   - Interstate case status tracking
   - Case transmittal tracking
4. Case Transmittal:
   - Transmittal date
   - Transmittal status
   - Response tracking
5. Integration with Case Management:
   - Link to case management module
   - Shared case information
   - Status synchronization

---

**Note**: This module integrates with:
- Case Management Module (for case information)
- Enforcement Module (for order enforcement)
- Finance Module (for payment processing based on orders)

**Document Status**: High-level requirements for Establishment Module. Detailed user stories and acceptance criteria should be developed based on specific state requirements and workflows.

**Related Documents**: 
- CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Intake and Case Registration)
- CSMS_Module_3_Case_Management_Requirements.md
- CSMS_Module_4_Locate_Requirements.md
