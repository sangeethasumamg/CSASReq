# CSMS Module 6: ENFORCEMENT - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Enforcement Module to enable developers to implement enforcement functionality in the Child Support Management System.

---

## Table of Contents
1. [Enforcement Module Overview](#61-enforcement-module-overview)
2. [Income Withholding Order (IWO) Management](#62-income-withholding-order-iwo-management)
3. [National Medical Support Notice (NMSN)](#63-national-medical-support-notice-nmsn)
4. [License Suspension/Revocation](#64-license-suspensionrevocation)
5. [Passport Denial](#65-passport-denial)
6. [Tax Intercept](#66-tax-intercept)
7. [Asset Seizure](#67-asset-seizure)
8. [Arrears Management](#68-arrears-management)
9. [Enforcement Actions Tracking](#69-enforcement-actions-tracking)

---

# 6.1 Enforcement Module Overview

The Enforcement Module manages enforcement actions to collect child support payments and enforce court orders. This includes income withholding, license suspension, tax intercepts, and other enforcement mechanisms.

---

# 6.2 Income Withholding Order (IWO) Management

### User Story 6.2.1: Income Withholding Order Creation and Management
**As a** case worker  
**I want** to create and manage Income Withholding Orders  
**So that** I can enforce child support payments through employer withholding

#### Acceptance Criteria:
1. System should provide IWO creation and management functionality.
2. IWO Creation:
   - IWO Type (Initial, Modification, Termination)
   - Related Court Order Number (mandatory)
   - Employer Information (mandatory):
     - Employer Name
     - Employer Address
     - Employer FEIN/SEIN
   - IWO Number (auto-generated, unique)
   - Notice Type
3. IWO Transmission:
   - Sent Date (mandatory when sent)
   - Transmission Method
   - Tracking Number
4. IWO Status Tracking:
   - Status options: Sent, Received, Acknowledged, Effective, Terminated
   - Received Date
   - Acknowledgment Code
   - Acknowledgment Date
   - Effective Date
5. IWO History:
   - View all IWOs for a case
   - View IWO modifications
   - View termination history
6. Employer Outreach:
   - Employer contact information
   - Employer response tracking
   - IWO Termination notice capability
7. Data Storage:
   - IWO information stored in `income_withholding_order` table (enforcement schema)
   - Links to case, court order, and employer

---

# 6.3 National Medical Support Notice (NMSN)

### User Story 6.3.1: National Medical Support Notice Management
**As a** case worker  
**I want** to create and manage NMSN  
**So that** I can enforce medical support obligations

#### Acceptance Criteria:
1. System should provide NMSN creation and management functionality.
2. NMSN Creation:
   - Related Court Order Number (mandatory)
   - Employer Information (mandatory)
   - NMSN Number (auto-generated, unique)
3. NMSN Transmission:
   - Sent Date (mandatory when sent)
   - Transmission Method
4. NMSN Status Tracking:
   - Status options: Sent, Received, Enrolled, Declined, Terminated
   - Received Date
   - Enrollment Status
   - Insurance Provider Information
   - Enrollment Date
5. Premium Payment Tracking:
   - Premium amount
   - Payment status
   - Payment tracking
6. NMSN History:
   - View all NMSNs for a case
   - View NMSN status changes
7. Data Storage:
   - NMSN information stored in `national_medical_support_notice` table (enforcement schema)
   - Links to case, court order, and employer

---

# 6.4 License Suspension/Revocation

### User Story 6.4.1: License Suspension Management
**As a** case worker  
**I want** to suspend or revoke licenses for non-payment  
**So that** I can enforce child support obligations

#### Acceptance Criteria:
1. System should provide license suspension/revocation functionality.
2. License Types Supported:
   - Driver's License
   - Professional Licenses
   - Recreational Licenses
3. Suspension Request:
   - License Type (mandatory)
   - License Number (mandatory)
   - License State (mandatory)
   - Suspension Reason (mandatory)
   - Request Date
4. Suspension Status Tracking:
   - Status options: Requested, Sent, Suspended, Reinstated
   - Suspension Date
   - Notification Date to NCP
5. Reinstatement Process:
   - Reinstatement Request
   - Reinstatement Date
   - Reinstatement Reason
   - Payment Compliance verification
6. Integration:
   - Integration with DMV systems
   - Automated status updates
7. Data Storage:
   - License suspension information stored in `license_suspension` table (enforcement schema)
   - Links to enforcement action and person

---

# 6.5 Passport Denial

### User Story 6.5.1: Passport Denial Management
**As a** case worker  
**I want** to request passport denial for non-payment  
**So that** I can enforce child support obligations

#### Acceptance Criteria:
1. System should provide passport denial functionality.
2. Passport Denial Request:
   - Request Date
   - Arrears Threshold (minimum arrears amount)
   - Request Status
3. Status Tracking:
   - Status options: Requested, Approved, Denied, Released
   - Approval Date
   - Release Date
   - Release Reason
4. Integration:
   - Integration with federal passport denial system
   - Automated status updates
5. Data Storage:
   - Passport denial information stored in `enforcement_action` table (enforcement schema) with action_type = 'PASSPORT_DENIAL'

---

# 6.6 Tax Intercept

### User Story 6.6.1: Tax Refund Intercept
**As a** case worker  
**I want** to intercept tax refunds for arrears  
**So that** I can collect past-due child support

#### Acceptance Criteria:
1. System should provide tax intercept functionality.
2. Tax Intercept Types:
   - Federal Tax Refund Intercept
   - State Tax Refund Intercept
3. Intercept Request:
   - Intercept Type (mandatory)
   - Request Date
   - Arrears Amount (mandatory, minimum threshold)
   - Request Status
4. Status Tracking:
   - Status options: Requested, Approved, Intercepted, Released
   - Intercept Amount
   - Intercept Date
   - Release Date (if applicable)
5. Payment Processing:
   - Link to payment receipt
   - Application to arrears
6. Integration:
   - Integration with tax intercept systems
   - Automated status updates
7. Data Storage:
   - Tax intercept information stored in `enforcement_action` table with action_type = 'TAX_INTERCEPT'

---

# 6.7 Asset Seizure

### User Story 6.7.1: Asset Seizure Management
**As a** case worker  
**I want** to seize assets for non-payment  
**So that** I can collect past-due child support

#### Acceptance Criteria:
1. System should provide asset seizure functionality.
2. Asset Seizure Types:
   - Bank Account Levy
   - Property Lien
   - Other Asset Seizure
3. Seizure Request:
   - Seizure Type (mandatory)
   - Asset Information (mandatory)
   - Request Date
   - Arrears Amount
4. Status Tracking:
   - Status options: Requested, Approved, Seized, Released
   - Seizure Amount
   - Seizure Date
   - Release Date (if applicable)
5. Payment Processing:
   - Link to payment receipt
   - Application to arrears
6. Data Storage:
   - Asset seizure information stored in `enforcement_action` table with action_type = 'ASSET_SEIZURE' or 'BANK_LEVY' or 'PROPERTY_LIEN'

---

# 6.8 Arrears Management

### User Story 6.8.1: Arrears Calculation and Tracking
**As a** case worker  
**I want** to calculate and track arrears  
**So that** I can monitor past-due amounts

#### Acceptance Criteria:
1. System should provide arrears calculation and tracking.
2. Arrears Calculation:
   - Automatic calculation based on orders and payments
   - Manual adjustment capability
   - Interest calculation (if applicable)
3. Arrears Balance Tracking:
   - Current arrears balance
   - Arrears by obligation type
   - Arrears history
4. Payment Application:
   - Automatic application to arrears
   - Manual application capability
   - Payment allocation rules
5. Arrears Payment Plans:
   - Payment plan creation
   - Payment plan tracking
   - Payment plan modifications
6. Arrears Reduction Strategies:
   - Tracking of reduction methods
   - Effectiveness monitoring

---

# 6.9 Enforcement Actions Tracking

### User Story 6.9.1: Enforcement Action History
**As a** case worker  
**I want** to track all enforcement actions  
**So that** I can monitor enforcement efforts

#### Acceptance Criteria:
1. System should provide comprehensive enforcement action tracking.
2. Action History:
   - All enforcement actions for a case
   - Action types
   - Action dates
   - Action status
   - Outcomes
3. Action Details:
   - Action Type (IWO, NMSN, License Suspension, Tax Intercept, Asset Seizure, Contempt, etc.)
   - Action Status
   - Action Date
   - Action Details (text/notes)
   - Outcome
   - Outcome Date
4. Reporting:
   - Enforcement action reports
   - Effectiveness metrics
   - Collection statistics
5. Data Storage:
   - Enforcement actions stored in `enforcement_action` table (enforcement schema)
   - Links to case and related entities

---

**Document Status**: High-level requirements for Enforcement Module. Detailed user stories and acceptance criteria should be developed based on specific state requirements and enforcement procedures.

**Related Documents**: 
- CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Intake and Case Registration)
- CSMS_Module_3_Case_Management_Requirements.md
- CSMS_Module_4_Locate_Requirements.md
- CSMS_Module_5_Establishment_Requirements.md
