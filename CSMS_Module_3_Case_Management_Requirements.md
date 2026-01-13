# CSMS Module 3: CASE MANAGEMENT - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Case Management Module to enable developers to implement the Child Support Management System.

---

## Table of Contents
1. [View Case Details / Main Screen](#31-view-case-details--main-screen)
2. [View/Modify CP Demographics](#32-viewmodify-cp-demographics)
3. [View/Modify CP Employer Information](#33-viewmodify-cp-employer-information)
4. [View/Modify Child Information](#34-viewmodify-child-information)
5. [View/Modify NCP Income and Assets](#35-viewmodify-ncp-income-and-assets)
6. [View/Modify NCP Relative](#36-viewmodify-ncp-relative)
7. [View/Modify NCP Incarceration Summary](#37-viewmodify-ncp-incarceration-summary)
8. [View/Modify Member Insurance](#38-viewmodify-member-insurance)
9. [View/Modify NCP Demographics](#39-viewmodify-ncp-demographics)
10. [View/Modify NCP Employer Information](#310-viewmodify-ncp-employer-information)
11. [Federal Case Registry](#311-federal-case-registry)
12. [Disbursement Hold](#312-disbursement-hold)
13. [Close, Suspend, Re-Open](#313-close-suspend-re-open)
14. [AOP Unmatched Search](#314-aop-unmatched-search)
15. [Billing Suppression](#315-billing-suppression)
16. [Division of Vital Records (DVR)](#316-division-of-vital-records-dvr)
17. [File Upload](#317-file-upload)

---

# 3.1 View Case Details / Main Screen

### User Story 3.1.1: View Case Details
**As a** case worker  
**I want** to view detailed case and party information on the Case Management page  
**So that** I can manage and track the progress of child support cases accurately and take appropriate action as needed

#### Acceptance Criteria:
1. When a user searches with a case number on the search bar in the top left navigation, then the user should be taken to a screen that displays detailed information related to a selected case. Application number should not fetch those details.
2. The system should display case-specific information on the top center panel including:
   - Case Number
   - Case Type and SubType
   - Assistance Status
   - Intergovernmental Status
   - Case Status
   - Family Violence / Domestic Violence indicators
   - Protective Orders
   - Good Cause status
   - Arrears Only indicator
3. The system should display two columns showing details of both:
   - **CP (Custodial Party)** including: CP Name, CP Member ID, MDM ID, IRN, SSN, Deceased status, and Case Association
   - **NCP (Non-Custodial Party)** including: NCP Name, NCP Member ID, MDM ID, IRN, SSN, Incarceration status, Deceased status and Case Association
4. The top-right section should show:
   - Current Date and Time
   - User ID of the person currently logged in
5. The system should display the left-hand menu containing options like:
   - Case Information
   - Member Information
   - Federal Case Registry
   - ADP unmatched searches
   - Division of vital records
   - File upload
   - Supervisory information
   - Billing suppression
   - Disbursement hold
6. Under the case information section on the bottom right, a Print button should be available to allow the user to generate a hard copy or PDF of the case details.
7. A Redirect to CSADocGen App button should be provided for transitioning to the Child Support Automated Document Generation application for further documentation tasks.
8. The Case Details section should display the following editable fields:
   - NCP Unknown (Radio Button: Yes/No, Yes - Mandatory)
   - Case Type (Dropdown: IV-D, No - Mandatory)
   - Sub Type (Dropdown: Federal foster care, Medicaid only, Never assistance, Never assistance-Locate only, Spousal/Alimony Only, State Foster care, Temporary cash assistance, No - Mandatory)
   - Case Status (Dropdown: Active, No - Mandatory)
   - Assistance Status (Dropdown: Not Applicable, Former recipient, No - Mandatory)
   - Intergovernmental Status (Dropdown: Maryland, Interstate initiating, No - Mandatory)
   - Application Fee Status (Dropdown: Paid, Exempt, No - Mandatory)
   - IV-D Service Required (Dropdown: Child Support Only, Paternity and Support, No - Mandatory)
   - Application Mode (Dropdown: Online, In Person, walk-in, No - Mandatory)
   - Case Jurisdiction (Dropdown: Howard County, Baltimore city, etc., No - Mandatory)
   - Case Registration Date (Date Picker: mm/dd/yyyy, No - Mandatory)
   - Application Completion Date (Date Picker: mm/dd/yyyy, No - Mandatory)
   - Case Status Date (Date Picker: mm/dd/yyyy, No - Mandatory)
   - Case Worker Name (Text Field, No - Mandatory)
   - Family Violence (Radio Button: Yes/No, Yes - Mandatory)
   - Domestic Violence (Radio Button: Yes/No, Yes - Mandatory)
   - Protective Order (Radio Button: Yes/No, Yes - Mandatory)
   - Good Cause (Radio Button: Yes/No, Yes - Mandatory)
   - Referral type (Text, No - Mandatory)
   - Referral date (Text, date: mm/dd/yyyy, No - Mandatory)
   - Referral ID (Text, number, No - Mandatory)
9. The intergovernmental section should display:
   - Intergovernmental status (Dropdown: Interstate initiating, No - Mandatory)
   - Initiating State (Dropdown: Maryland, No - Mandatory)
   - Initiating FIPS code (Text field, No - Mandatory)
   - Initiating case number (Text field, No - Mandatory)
   - Responding state (Dropdown: Pennsylvania, No - Mandatory)
   - Responding FIPS code (Text field, No - Mandatory)
   - Responding case number (Text field, No - Mandatory)
10. The case function section should be in table format with case function, start date, and end date as column heading with edit button option.
11. The Scheduler section must display the following in a table format:
    - Appointment Date
    - Appointment Time
    - Appointment Type
    - CP Appointment Status
    - NCP Appointment Status
12. The Establishment - Court Order section should include:
    - Court Order Number
    - Court Order Type
    - Obligation Type
    - Court Order Date
    - Effective Date
    - Entered Date
    - Court Order Status
13. The Enforcement section must include the following sub-sections in a table format:
    - **Income Withholding Order Notice**: Court Order Number, Employer, Notice Type, Sent Date, Received Date
    - **National Medical Support Notice**: Court Order Number, Employer, Sent Date, Status
14. The Financial section must present following fields:
    - Receipt Collected Date (Date Picker: mm/dd/yyyy, No - Mandatory)
    - Receipt Amount (Numeric Field, No - Mandatory)
    - Applied Amount (Numeric Field, No - Mandatory)
    - Distributed Date (Date Picker: mm/dd/yyyy, No - Mandatory)
    - Payment Status (Text field, No - Mandatory)
    - Disbursement Method (Text field, No - Mandatory)
    - Bank Reconciliation Status (Text field, No - Mandatory)
    - Disbursed Date (Date Picker: mm/dd/yyyy, No - Mandatory)
    - Disbursed Amount (Text Field, No - Mandatory)
    - Monthly Grant Amount (Text Field, No - Mandatory)
    - AU Number (Text Field: Alphanumeric, No - Mandatory)
    - Case Identifier ID (Text Field: Alphanumeric, No - Mandatory)
    - Program ID (Text Field: Alphanumeric, No - Mandatory)
    - Total URPA (Numeric Field, No - Mandatory)
    - URPA Update Date (Date Picker: mm/dd/yyyy, No - Mandatory)
    - Source (Text field, No - Mandatory)
15. The Good Cause section should include the following fields:
    - Indicator (Radio Button: Yes/No, No - Mandatory)
    - Status (Dropdown: Pending, Approved, Denied, No - Mandatory)
    - Reason (Dropdown: Domestic Violence, Safety Concern, No - Mandatory)
    - Status Date (Date Picker: mm/dd/yy, No - Mandatory)
    - IV-D Cooperation (Dropdown, No - Mandatory)
    - IV-D Coop Date (Date Picker: mm/dd/yyyy, No - Mandatory)
    - Assignment of Rights (Radio Button: Yes/No, No - Mandatory)
16. IV-D Coop history section should include the following in a table format:
    - IV-D cooperation status
    - Updated date
17. Alert IV-A Agency section should have following data fields:
    - NCP living with CP (Radio Button: Yes/No, No - Mandatory)
    - NCP living with CP updated date (Date picker: mm/dd/yyyy, No - Mandatory)
    - CP receiving support (Radio Button: Yes/No, No - Mandatory)
18. There should be a cancel and update button at the bottom right corner of the page.
19. When the user clicks the cancel button, the system would retain old values and discard any new values the user is trying to enter.
20. When the user clicks the update button, the system validates and then updates all the values to a database.
21. Responsive Design: All sections should be clearly organized and visible without overlapping.

---

**Note**: This document is Part 1 of Case Management Module. The remaining user stories (CP Demographics, CP Employer, Child Information, NCP sections, etc.) will be added in subsequent updates. All user stories follow the same detailed format with acceptance criteria for developer implementation.
