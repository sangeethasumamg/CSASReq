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

# 3.2 View/Modify CP Demographics

### User Story 3.2.1: View/Modify CP Demographics
**As a** case worker  
**I want** to edit/modify case and party information on the Case Management page  
**So that** I can manage and track the progress of child support cases accurately and take appropriate action as needed

#### Acceptance Criteria:
1. When a user searches with a case number on the search bar, the user should be taken to a screen that displays detailed information related to the selected case. Application number should not fetch those details.
2. Upon selecting CP Demographics from View/Modify CP in the left navigation, the system should display case-specific information including Case Number, Case Type and SubType, Assistance Status, Intergovernmental Status, Case Status, Family Violence/Domestic Violence indicators, Protective Orders, Good Cause status, Arrears Only indicator.
3. The system should display two columns showing details of CP (Name, Member ID, MDM ID, IRN, SSN, Deceased status, Case Association) and NCP (Name, Member ID, MDM ID, IRN, SSN, Incarceration status, Deceased status, Case Association).
4. The top-right section should show Current Date and Time and User ID of the person currently logged in.
5. The system should display the left-hand menu with Case Information, Member Information (View/Modify CP, CP Demographics, CP Employer Info; View/Modify NCP; View/Modify Child; View/Modify Member Insurance), Federal Case Registry, AOP unmatched searches, Division of vital records, File upload, Supervisory information, Billing suppression, Disbursement hold.
6. The system should display detailed CP information including CP Member ID, Name, SSN/ITIN (masked), Date of Birth, Gender, Race, MDM ID titled Custodial Party Data.
7. Custodial Party SSN History should be accessible via a collapsible section with Cancel, Edit, and Save buttons.
8. The system should display editable CP personal information: Relationship to Child, Family Violence Indicator, Protective Order Indicator, Domestic Violence Indicator, City, Nickname, Pregnancy, Suffix, Deceased, Date of death, User Modified ID, Date Modified.
9. Temporary Cash Assistance (TCA) section: Cash Assistance State, County, Last TCA Check Date, TCA/TANF Applicant Status, Current/Former TCA/TANF Recipient, Cash Assistance Start/End Date, Grant Amount.
10. Medical Assistance section: Medical Assistance State, County, MA Applicant, Current/Former MA Recipient.
11. Communication section: Notification Type, Text/Email Notification Preference, Home/Business/Cell Phone, Email.
12. Custodial Party Alternative Name: First Name, Middle Name, Last Name, Suffix.
13. CP mailing, residential, and service address sections with fields: Bad address, Source, International address, Address validated, Address line 1-2, City, State, County, Zip, Country, Updated date.
14. Custodial party nearest relative and attorney information sections with standard address and contact fields.
15. Cancel and Update buttons at bottom right. Cancel retains old values; Update validates and saves. Submit on confirmation popup displays "CP information successfully updated." Access denied message for unauthorized users: "You do not have access to this page! Please reach out System Administrator!"

---

# 3.3 View/Modify CP Employer Information

### User Story 3.3.1: View/Modify CP Employer Information
**As a** case worker  
**I want** to view detailed case and employment information on the CP Employer Information page  
**So that** I can manage and track case and employment information and take appropriate action as needed

#### Acceptance Criteria:
1. When a user clicks View/Modify CP → CP Demographics in the left pane (accordion expands), then CP Employer Information, the user should be taken to the CP Employer Information page.
2. The system should display case-specific information and two columns showing CP and NCP details (Name, Member ID, MDM ID, IRN, SSN, Deceased status, Incarceration status, Case Association).
3. Employer History section: data under Name, Type, Start Date, End Date, Phone No, Email, Updated System/User Edit; pagination; Add Employer button.
4. Employer Information section: Self employed (Checkbox), Verification Indicator, Employer Name, Employer Type, Employer Phone, Email, Fax, FEIN, SEIN, Employer Sponsored Insurance availability, Occupation, Source, International Address, Address Validated, Address Line 1-2, City, State, County, Zip Code, Country, Start Date, End Date, Updated date, Income, Frequency, Modified date.
5. Income Information section: editable fields under Income Type, Income Source, Income Frequency, Income Amount.
6. Cancel and Update buttons at bottom right. Update validates and saves; Cancel retains old values and discards changes.

---

# 3.4 View/Modify Child Information

### User Story 3.4.1: View/Modify Child Information
**As a** case worker  
**I want** to view and modify child information on the Case Management page  
**So that** I can manage and track the progress of child support cases accurately and take appropriate action as needed

#### Acceptance Criteria:
1. When the user clicks Member Information, the system should display View/Modify CP, View/Modify NCP, and View/Modify Child in the left navigation.
2. Upon clicking View/Modify Child, the system shall display Child Information within the left-hand navigation.
3. The system should display case-specific information and two columns showing CP and NCP details.
4. Child data section: table format with Member ID, Full Name, SSN/ITIN, Date of Birth, Gender, Race, MDM ID, IRN.
5. With appropriate access rights: Cancel, Edit, Save, and Delete buttons shall be visible and enabled. Without edit permissions: Edit, Save, Delete shall be greyed out or hidden.
6. SSN History: expandable historical log of SSN changes (masked), timestamps, change source.
7. Child data editable fields: Relationship to CP, State Conceived, Birth Country/State/City, Suffix, Emancipation Date, Emancipation Notice dates, Deceased Indicator, Family Violence, Protective Order, Domestic Violence, Participation Status, Participation Start Date, Out of Home Indicator/Date, Source, SSI Indicator, School Enrollment Form Verified, Parentage information (Established Through, Date, Establishment Country/State/County, Affidavit fields), Relationship between mother and father.
8. Add Child, Cancel, DVR, and Save buttons at bottom right. Cancel retains old values; Save updates modified information.

---

# 3.5 View/Modify NCP Income and Assets

### User Story 3.5.1: View/Modify NCP Income and Assets
**As a** case worker  
**I want** to verify and manage NCP Income and Assets data within the Case Management module  
**So that** I can ensure accurate tracking of NCP financial and assets information for necessary case processing

#### Acceptance Criteria:
1. When the user navigates to Member Information and clicks View/Modify NCP → NCP Income and Assets, the system should display the financial details.
2. The system should display case-specific information in the top center panel and two columns showing CP and NCP details.
3. Left-hand menu: Case Information, Member Information (View/Modify CP/NCP, NCP Demographics, NCP Employer, NCP Income and Assets, NCP Relative, NCP Address, NCP incarceration suspension summary, Add NCP, View/Modify Child, View/Modify member insurance), Federal Case Registry, DVR, AOP Unmatched search, File Upload, Supervisory Functions, Billing Suppression, Disbursement hold.
4. Income Information section: Add Income Info button; table with Income Type, Income Source, Income Frequency, Income Amount.
5. Union Information section: Is NCP a union member (Radio Yes/No).
6. Non-Custodial Party Assets section: Add Asset button; table with Asset type, Property, Ownership, View Details, Delete; pagination.
7. Cancel and Update buttons. Update saves changes; Cancel discards changes.

---

# 3.6 View/Modify NCP Relative

### User Story 3.6.1: View/Modify NCP Relative
**As a** case worker  
**I want** to verify and manage NCP relative data within the Case Management module  
**So that** I can ensure accurate tracking and management of NCP relative information for effective case processing

#### Acceptance Criteria:
1. When a user clicks NCP Relative under View/Modify NCP in Member Information, the system should navigate to the NCP Relative page and highlight the section in the left-hand menu.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Non-Custodial Party data: Member Id, Name, SSN/ITIN, DOB, Gender, Race, MDM ID; NCP SSN History tab; Cancel, Edit, Save buttons.
4. NCP Address History: table with S.No, Address Verified, Type, Address Line 1, City, State, County, Country, Updated date, Edit; Add New Address button; pagination.
5. Non-Custodial Party Address 1 section: editable fields for address type (Residential, Mail, Service, Other), Source, International Address, Address manually verified, Sequence number, Address Line 1-2, City, State, County, Zip, Country, Date at address, Correct address indicator, Date Verified, End date, Tribe membership.
6. Previous, Cancel, and Next buttons for navigation.

---

# 3.7 View/Modify NCP Incarceration Summary

### User Story 3.7.1: View/Modify NCP Incarceration Summary
**As a** case worker  
**I want** to verify and manage NCP incarceration details within the Case Management module  
**So that** I can accurately track incarceration statuses and suspensions of arrears accrual for appropriate case handling

#### Acceptance Criteria:
1. When a user searches with a case number and selects NCP Incarceration under Member Information, the system should display the incarceration page.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Case Information section: Case Status, Case Type, Case Sub-type, Function, Exclude auto suspension, Exclude auto suspension date.
4. NCP Active Incarceration Information: Prisoner Id, Admission date, Original Projected Release date, Last updated date, CP notice sent date, Institution name.
5. Suspension of accrual of Arrears Investigation/Appeal: Investigation reason, Investigation date, Investigation disposition, Investigation disposition date, Appeal File date, Appeal Disposition, Appeal Disposition date.
6. Incarceration history: table with Source, Verified, Admission date, Release date, Updated date, Updated by; pagination.
7. Add or Edit incarceration details button; Cancel button. Cancel discards changes and returns to case management home page.

---

# 3.8 View/Modify Member Insurance

### User Story 3.8.1: View/Modify Member Insurance
**As a** case worker  
**I want** to view and modify member insurance within the Case Management module  
**So that** I can track and update insurance information for members to ensure correct case processing

#### Acceptance Criteria:
1. When the user clicks View/Modify Member Insurance under Member Information in the left navigation, the system navigates to the Member Insurance page.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Left-hand menu: Case Information, Member Information (View/Modify CP/NCP/Child, Child Information, View/Modify Member Insurance), Federal Case Registry, DVR, AOP Unmatched search, File Upload, Supervisory Functions, Billing Suppression, Disbursement hold.
4. Member Insurance section: Add new Insurance button (opens widget); Print button.
5. Table headings: Member ID, Name, SSN, DOB, Gender, Provider Name, Policy Number.
6. Previous button (navigates to Child Information); Next button (navigates to Federal Case Registry).

---

# 3.9 View/Modify NCP Demographics

### User Story 3.9.1: View/Modify NCP Demographics
**As a** case worker  
**I want** to verify the NCP demographics page within the Case Management module  
**So that** I can ensure accurate tracking of NCP details for case processing

#### Acceptance Criteria:
1. When a user searches with a case number and selects NCP Demographics, the system should navigate to the NCP Demographics page.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Non-Custodial Party data: Member ID, Name, SSN/ITIN, DOB, Gender, Race, MDM ID; NCP SSN History tab; Cancel, Edit, Save buttons.
4. NCP personal data: Relationship to child, Family violence, Protective order, Domestic violence, Source, Approx. age, Deceased, Birth city/state, Suffix, Alias, Bad Address, Eye Color, Hair Color, Height, Weight, Identification marks, Driver's license, License plate, Marital status, Educational level, Citizenship status, Cell/Home/Business Phone, Email, Notification type, Email/Text Notification.
5. NCP Military Information: Marital Status, Military branch, Military Service number, Military Entry/Discharge dates.
6. NCP Attorney Information: First/Middle/Last name, Phone, Source, Address fields.
7. NCP Employment Referral Program: Referral date, Referral type, Referral country, Program type, Enrollment date, Completion Date, Not completed.
8. Cancel and Update buttons. Update saves all changes; Cancel discards unsaved changes.

---

# 3.10 View/Modify NCP Employer Information

### User Story 3.10.1: View/Modify NCP Employer Information
**As a** case worker  
**I want** to view employer information within the Case Management module  
**So that** I can accurately manage and update Employer information for proper case processing and tracking

#### Acceptance Criteria:
1. When a user clicks Member Information → View/Modify NCP → NCP Employer Information, the system navigates to the NCP Employer Information page.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Non-Custodial Party Employer section: Member ID, Name, SSN/ITIN, DOB, Gender, Race, MDM ID; NCP SSN History tab; Cancel, Edit, Save buttons.
4. Employer History: table with Name, Type, Start Date, End Date, Phone number, Email, Updated, System/User, Edit; pagination; Add Employer button.
5. Employer Information fields: Self Employed, Verification Indicator, Employee Search, Employer Name, Employer Type, Employer Phone, Email, Fax, FEIN, SEIN, Employer Sponsored Insurance, Occupation, Source, International Address, Address Validated, Address Line 1-2, City, State, County, Zip, Country, Start/End/Updated Date, Income, Frequency, Employer Wage withholding, Modified Date.
6. Cancel, Print, and Update buttons at bottom. Cancel resets data and returns to case management main page; Update saves when mandatory fields are filled.

---

# 3.11 Federal Case Registry

### User Story 3.11.1: Federal Case Registry
**As a** case worker  
**I want** to view the federal case history transaction status  
**So that** I can accurately manage and update the Federal Case Registry transaction status for proper case processing and tracking

#### Acceptance Criteria:
1. When a user searches with a case number and selects Federal Case Registry from the left pane, the system should navigate to the Federal Case Registry page.
2. The page should have case number search functionality on the top left.
3. The system should display case-specific information in three columns: Case Number, Linked Case, CP Name, CP Member ID, NCP Name, NCP Member ID.
4. Left-hand menu: Case Information, Member Information, Federal Case Registry, DVR, AOP Unmatched search, File Upload, Supervisory Functions, Billing Suppression, Disbursement hold.
5. Federal Case Registry Transaction Status section: FCR Query, NDNH Query, FPLS Request buttons.
6. Table with column headings: Type, Action, Locate info, Member type, Member ID, Date Transmitted, Date Acknowledged, Acknowledgement code, Batch, Transaction number.
7. Pagination with previous/next arrows and current page number.

---

# 3.12 Disbursement Hold

### User Story 3.12.1: Disbursement Hold
**As a** case worker  
**I want** to view the landing page of the disbursement hold  
**So that** I can manage the disbursement hold for proper case processing and tracking

#### Acceptance Criteria:
1. When a user searches with a case number and selects Disbursement Hold from the left pane, the system takes the user to the Disbursement Hold landing page.
2. Type of Disbursement Hold dropdown: Case level, Member level, Receipt level (Mandatory).
3. Search button displayed next to the dropdown.
4. Left-hand menu: Case Information, Member Information, Federal Case Registry, DVR, AOP Unmatched search, File Upload, Supervisory Functions, Billing Suppression, Disbursement hold.

---

# 3.13 Close, Suspend, Re-Open

### User Story 3.13.1: Close, Suspend, Re-Open
**As a** case worker  
**I want** to view the close, suspend, re-open page within the Case Management module  
**So that** I can view case close, suspend and reopen information and ensure proper case processing and tracking

#### Acceptance Criteria:
1. When a user clicks Case Information on the left, the system should navigate to the Close, Suspend and Re-Open page and highlight the Case Information accordion (expanded) in the left accordion.
2. The system should display case-specific information and two columns showing CP and NCP details.
3. Non-Custodial Party Details section.
4. Left-hand menu: Case Information, Member Information, Federal Case Registry, DVR, AOP Unmatched search, File Upload, Supervisory Functions, Billing Suppression, Disbursement hold.
5. Account Information section.
6. Unprocessed payments section: Receipt number, Collection date, Payment source, Unprocessed reason, Unprocessed amount, Last payment date.
7. Undistributed Payments section.
8. Close, Suspend, Re-Open section.
9. Submit button: on click, system validates all values and updates the database.

---

# 3.14 AOP Unmatched Search

### User Story 3.14.1: AOP Unmatched Search
**As a** case worker  
**I want** to search for unmatched AOP records using options like Mother, Father, Child, or Affidavit Number  
**So that** I can manage and track the progress of child support cases accurately and take appropriate action as needed

#### Acceptance Criteria:
1. When a user searches with a case number, the user should be taken to the case screen. Application number should not fetch those details.
2. When the user selects AOP Unmatched Search from the left navigation, the system navigates to the AOP Unmatched Search page.
3. Left-hand menu: Case Information, Member Information, Federal Case Registry, AOP unmatched searches, Division of vital records, File upload, Supervisory information, Billing suppression, Disbursement hold.
4. AOP Unmatched Search page: Search options (Radio: Mother, Father, Child, Affidavit number); Affidavit number text field when that option is selected.
5. Search button triggers search based on selected criteria and input.
6. When user clicks Search, system validates option and values and displays results.
7. Clear button resets input field and displayed results.
8. Results table or display section below the search to show matching unmatched AOP records.

---

# 3.15 Billing Suppression

### User Story 3.15.1: Billing Suppression
**As a** case worker  
**I want** to view and manage billing suppression details for a child support case  
**So that** I can ensure billing is paused during valid periods and resumed appropriately

#### Acceptance Criteria:
1. When a user searches with a case number, the user should be taken to the case screen. Application number should not fetch those details.
2. When the user selects Billing Suppression from the left navigation, the system navigates to the Billing Suppression page.
3. The system should display case-specific information and two columns showing CP and NCP details.
4. Left-hand menu with standard options; Billing Suppression highlighted when selected.
5. Financial information section: Obligation type, SOA Amount/Frequency, Complaint status, Court order number, Court order status, Court order effective date.
6. Billing Suppression fields: Billing suppression (Dropdown: Inactive, etc.), Reason, Other NCP's case billing suppression (Yes/No), Last update date.
7. Billing suppression entries table: CO Number, Billing Suppression Start Date, Billing Suppression End Date, Billing Suppression Reason, Updated By, Updated Date.
8. Pagination and items-per-page control.
9. Submit and Close buttons. Submit verifies values and updates database; Close closes window without changes.

---

# 3.16 Division of Vital Records (DVR)

### User Story 3.16.1: Division of Vital Records
**As a** case worker  
**I want** to search for Custodial or Non-Custodial Parent records using Division of Vital Records data fields  
**So that** I can accurately match individuals and retrieve official documents for child support case verification

#### Acceptance Criteria:
1. When a user searches with a case number, the user should be taken to the case screen. Application number should not fetch those details.
2. When the user selects DVR from the left navigation, the system navigates to the DVR page.
3. Left-hand menu: Case Information, Member Information, Federal Case Registry, AOP unmatched searches, Division of vital records, File upload, Supervisory information, Billing suppression, Disbursement hold.
4. Division of Vital Records section: CP Search/NCP Search (Radio), Firstname, Middle name, Last name, SSN/ITIN (with toggle view), DOB, Affidavit number.
5. Search, Previous, and Clear buttons. Search validates values and displays results in DVR search result section. Clear resets input fields and search results. Previous navigates to Billing Suppression page.

---

# 3.17 File Upload

### User Story 3.17.1: File Upload
**As a** case worker  
**I want** to search for a member and upload supporting documents  
**So that** I can submit required files for their case efficiently

#### Acceptance Criteria:
1. When a user searches with a case number, the user should be taken to the case screen. Application number should not fetch those details.
2. When the user selects File Upload from the left navigation, the system navigates to the File Upload page.
3. Left-hand menu: Case Information, Member Information, Federal Case Registry, AOP unmatched searches, Division of vital records, File upload, Supervisory information, Billing suppression, Disbursement hold.
4. Instructional text: "Documents supporting members, member applications, or member cases can be uploaded by selecting 'Choose File'. Files can also be scanned by selecting 'Scan'. Files must be no larger than 25MB each with all combined files not exceeding 250MB. Acceptable formats: Word, PDF and Image Files (jpg/png/gif/bmp)."
5. User can search by SSN, ITIN, MDM ID, Application number, Case number, or Member ID.
6. When user selects SSN: Enter SSN field and Search button. Search validates SSN and retrieves application number and case number.
7. File Upload section fields: Enter SSN (Mandatory), Application number, Case number, Member ID, Jurisdiction, SSN, ITIN, First name, Last name, DOB, MDM ID, IRN.
8. Select category, Select document type dropdowns; Choose File, Scan, Finish buttons. Choose File selects file from system; Scan allows scanning; Finish displays uploaded files list.

---

**Document Status:** All 17 sections of the Case Management Module are documented with user stories and acceptance criteria. Source: UserStoryCaseManagementPageBased.txt.
