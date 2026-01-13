# CSMS Module 7: FINANCE - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Finance Module to enable developers to implement financial management functionality in the Child Support Management System.

---

## Table of Contents
1. [Finance Module Overview](#71-finance-module-overview)
2. [Payment Receipt](#72-payment-receipt)
3. [Payment Processing](#73-payment-processing)
4. [Disbursement Management](#74-disbursement-management)
5. [Account Management](#75-account-management)
6. [Financial Reporting](#76-financial-reporting)
7. [Billing and Fee Management](#77-billing-and-fee-management)
8. [Bank Reconciliation](#78-bank-reconciliation)

---

# 7.1 Finance Module Overview

The Finance Module manages all financial transactions, payments, receipts, disbursements, and accounting for child support cases. This module handles payment collection, distribution, account management, and financial reporting.

---

# 7.2 Payment Receipt

### User Story 7.2.1: Payment Receipt Entry
**As a** finance worker / case worker  
**I want** to record payment receipts  
**So that** I can track incoming payments

#### Acceptance Criteria:
1. System should provide payment receipt entry functionality.
2. Payment Source Types:
   - Employer Income Withholding
   - Direct Payment (NCP)
   - Tax Intercept
   - Bank Account Levy
   - Other Sources
3. Payment Recording:
   - Receipt Number (auto-generated, unique, mandatory)
   - Case Number (mandatory)
   - NCP Information (mandatory)
   - Receipt Date (mandatory)
   - Payment Amount (mandatory, numeric, positive)
   - Payment Source (mandatory)
   - Payment Method (Check, EFT, Cash, etc.)
   - Check Number (if applicable)
4. Payment Validation:
   - Amount validation
   - Date validation
   - Duplicate check detection
5. Data Storage:
   - Payment receipts stored in `payment_receipt` table (financial schema)
   - Links to case and NCP

---

# 7.3 Payment Processing

### User Story 7.3.1: Payment Application and Processing
**As a** finance worker  
**I want** to process and apply payments  
**So that** I can allocate payments correctly

#### Acceptance Criteria:
1. System should provide payment processing functionality.
2. Payment Application Logic:
   - Current Support (first priority)
   - Arrears (second priority)
   - Fees (third priority)
   - Medical Support
   - Child Care
3. Payment Allocation Rules:
   - Configurable allocation rules
   - Pro-rata allocation
   - Manual allocation capability
4. Payment Distribution:
   - Automatic distribution calculation
   - Distribution to CP
   - Distribution to state (if applicable)
   - Distribution to federal (if applicable)
5. Applied Amount Tracking:
   - Applied Amount field
   - Distribution tracking
   - Unapplied amount handling
6. Data Storage:
   - Payment application stored in `payment_application` table (financial schema)
   - Links to receipt and accounts

---

# 7.4 Disbursement Management

### User Story 7.4.1: Disbursement Processing
**As a** finance worker  
**I want** to process disbursements  
**So that** I can distribute payments to custodial parties

#### Acceptance Criteria:
1. System should provide disbursement processing functionality.
2. Disbursement Types:
   - Current Support Disbursement
   - Arrears Disbursement
   - Fee Disbursement
3. Disbursement Processing:
   - Disbursement Number (auto-generated, unique, mandatory)
   - Case Number (mandatory)
   - CP Information (mandatory)
   - Related Receipt (if applicable)
   - Disbursement Date (mandatory)
   - Disbursement Amount (mandatory, numeric, positive)
   - Disbursement Method (Check, Direct Deposit, EFT, Card, mandatory)
   - Payee Information (mandatory)
   - Account Information (for direct deposit/EFT)
4. Disbursement Hold Management:
   - Hold Types: Case level, Member level, Receipt level
   - Hold Reasons
   - Hold Dates (Start, End)
   - Release Processing
5. Disbursement Status:
   - Status options: Pending, Processed, Held, Cancelled
   - Status tracking
6. Disbursement History:
   - View all disbursements for a case
   - Disbursement details
   - Status history
7. Data Storage:
   - Disbursements stored in `disbursement` table (financial schema)
   - Disbursement holds stored in `disbursement_hold` table (financial schema)
   - Links to case, CP, and receipts

---

# 7.5 Account Management

### User Story 7.5.1: Account Balance Management
**As a** finance worker  
**I want** to manage account balances  
**So that** I can track financial obligations

#### Acceptance Criteria:
1. System should provide account management functionality.
2. Account Types:
   - Current Support Account
   - Arrears Account
   - Fee Account
3. Account Balance Tracking:
   - Account Balance (calculated, mandatory)
   - Account Status (Active, Closed, etc.)
   - Payment Frequency
   - Last Payment Amount
   - Last Payment Date
4. Account Information Display:
   - Account type
   - Account status
   - Payment/Frequency
   - Account balance
   - Last payment amount
   - Last payment date
5. Payment History:
   - View all payments for an account
   - Payment details
   - Application details
6. Account Updates:
   - Automatic balance updates
   - Manual adjustment capability
   - Adjustment reasons
7. Data Storage:
   - Accounts stored in `account` table (financial schema)
   - Links to case

---

# 7.6 Financial Reporting

### User Story 7.6.1: Financial Reports Generation
**As a** finance worker / supervisor  
**I want** to generate financial reports  
**So that** I can monitor financial activity

#### Acceptance Criteria:
1. System should provide financial reporting functionality.
2. Report Types:
   - Payment Reports
   - Disbursement Reports
   - Arrears Reports
   - Account Balance Reports
   - Collection Reports
   - Financial Summary Reports
   - Federal Reporting (OCSE-34, OCSE-157)
3. Report Parameters:
   - Date ranges
   - Case filters
   - Account type filters
   - Status filters
4. Report Formats:
   - PDF export
   - Excel export
   - On-screen viewing
5. Federal Reporting:
   - OCSE-34 report generation
   - OCSE-157 report generation
   - Data validation
   - Submission tracking

---

# 7.7 Billing and Fee Management

### User Story 7.7.1: Billing Suppression and Fee Management
**As a** finance worker  
**I want** to manage billing and fees  
**So that** I can control billing and collect appropriate fees

#### Acceptance Criteria:
1. System should provide billing suppression functionality.
2. Billing Suppression:
   - Suppression Status (Active, Inactive)
   - Suppression Reason
   - Start Date
   - End Date
   - Other NCP's case billing suppression indicator
   - Last Update Date
3. Billing Suppression History:
   - View suppression history
   - Suppression details
   - Update tracking
4. Fee Management:
   - Application Fee tracking
   - Collection Fee calculation
   - Service Fee tracking
   - Fee Collection
   - Fee Distribution
5. Data Storage:
   - Billing suppression stored in `billing_suppression` table (financial schema)
   - Links to case and court orders

---

# 7.8 Bank Reconciliation

### User Story 7.8.1: Bank Reconciliation
**As a** finance worker  
**I want** to reconcile bank statements  
**So that** I can ensure financial accuracy

#### Acceptance Criteria:
1. System should provide bank reconciliation functionality.
2. Bank Statement Import:
   - Import capability
   - Statement format support
   - Data validation
3. Reconciliation Process:
   - Match payments to bank deposits
   - Match disbursements to bank withdrawals
   - Identify discrepancies
   - Resolution tracking
4. Reconciliation Status:
   - Status tracking per transaction
   - Reconciliation date
   - Reconciled by user
5. Discrepancy Resolution:
   - Discrepancy identification
   - Resolution process
   - Resolution tracking

---

# 7.9 URPA (Undistributed Remittance Payment Account)

### User Story 7.9.1: URPA Management
**As a** finance worker  
**I want** to track URPA  
**So that** I can manage undistributed payments

#### Acceptance Criteria:
1. System should provide URPA tracking functionality.
2. URPA Information:
   - Total URPA amount
   - URPA Update Date
   - AU Number
   - Case Identifier ID
   - Program ID
   - Monthly Grant Amount
   - Source
3. URPA Updates:
   - Update tracking
   - Update history
4. URPA Distribution:
   - Distribution processing
   - Distribution tracking
5. Data Storage:
   - URPA information stored in `urpa` table (financial schema)
   - Links to case

---

**Document Status**: High-level requirements for Finance Module. Detailed user stories and acceptance criteria should be developed based on specific state financial system requirements and business rules.

**Related Documents**: 
- CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Intake and Case Registration)
- CSMS_Module_3_Case_Management_Requirements.md
- CSMS_Module_4_Locate_Requirements.md
- CSMS_Module_5_Establishment_Requirements.md
- CSMS_Module_6_Enforcement_Requirements.md

---

**Note**: Finance Module integrates with:
- Case Management Module (for case information)
- Enforcement Module (for payment collection)
- Establishment Module (for order-based obligations)
- State Financial Systems (for payment processing)
- Federal Systems (for reporting)
