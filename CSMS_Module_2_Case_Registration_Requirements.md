# CSMS Module 2: CASE REGISTRATION - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Case Registration Module to enable developers to implement case registration functionality in the Child Support Management System.

---

## Table of Contents
1. [Case Registration Home Page](#21-case-registration-home-page)
2. [Member Clearance](#22-member-clearance)
3. [Member Status](#23-member-status)
4. [CP Demographics](#24-cp-demographics)
5. [CP Income and Assets](#25-cp-income-and-assets)
6. [NCP Demographics](#26-ncp-demographics)
7. [NCP Address](#27-ncp-address)
8. [NCP Relative](#28-ncp-relative)
9. [NCP Income and Assets](#29-ncp-income-and-assets)
10. [Child Information](#210-child-information)
11. [Member Insurance](#211-member-insurance)
12. [Case Status](#212-case-status)
13. [Cancel and Resume Application](#213-cancel-and-resume-application)
14. [Auto-Deletion of Inactive Cases](#214-auto-deletion-of-inactive-cases)

---

# 2.1 Case Registration Home Page

### User Story 2.1.1: Case Registration Home Page
**As a** case worker  
**I want** to be able to access home page  
**So that** I can access application created by intake worker

#### Acceptance Criteria:
1. When the user clicks case registration, system should have a search panel located at the top right corner, directly below the second top navigation. The search panel should allow users to filter by:
   - Case Number
   - Days Left
   - Start Date
2. A "Clear" button should be provided in the search panel to reset all search criteria and return to the default view.
3. When a user clicks on search, the corresponding case gets listed out.
4. The left navigation panel has following items:
   - Case registration home
   - Create work item
   - Process IV-D application
   - Process referral
   - File upload
   - File management
   - Supervisory functions
   - Non IV-D
   - Referral new application
   - Search
5. On the case registration page, the system should display a table with rows of case data. Each row should start with a clickable chevron icon, indicating the type of case (intake or referral). The chevron icon in each row should be color-coded:
   - Yellow circle with letter I inside for Intake cases
   - Red circle with letter R inside for referral cases
6. For Intake cases, the row should contain the following information:
   - Work Item ID
   - Application No
   - Application Type
   - Date Received
7. For Referral cases, the row should contain the following information:
   - Work Item ID
   - Referral No
   - Referral Type
   - Request Type
   - Date Received
8. Each row should include a Modify Action dropdown on the right-hand side. The dropdown should contain the following options:
   - View Summary
   - Register Cases
   - Return Application
   - View Document
   - No Action Required
   - Resolved
   - Check for Case Composition
   - Link Case
9. On the view summary selection, a summary box pops up. It shows application number, type, service fee paid, submitted date.
10. The middle section of the summary box has three questions displayed:
    - Are you a current TCA applicant or applying for child support services to be eligible to apply for TCA?
    - Are you a current or former TCA recipient?
    - Are you a current MA recipient?
11. The members information section on summary box has CP, NCP and child information sections on the click of those sections. Each section displays Full name, SSN/ITIN, Race, DOB, Gender
12. On the right side of the case data, the system should display the type of case.
13. Pagination should be able to be implemented to display records. Users should be able to navigate through multiple pages of records efficiently using arrow buttons.
14. Once you select the 'Register cases' option in the modify actions dropdown, the system should display the member clearance page of the paper application from left navigation.

---

# 2.2 Member Clearance

### User Story 2.2.1: Member Clearance - CP Screen
**As a** case worker  
**I want** to be able to access member clearance  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria - CP Screen:
1. System should display the CP screen, followed by NCP and children screen in a progressive stepper format. The screen should be divided into three sections within a stepper/wizard format.
2. CP stepper: Displays the primary details of the Custodial Party such as MDM ID, Member ID, Name, DOB, SSN/ITIN, Gender, Race and Match/Criteria are retrieved from the database.
3. CP SSN History: Shows a historical record of the Custodial Party's Social Security Numbers.
   - CP SSN history table has following columns: Member ID, Name, SSN, SSN Type, Verification Status, SSN verification source
   - CP SSN history section should have an edit, cancel and save button.
4. Enterprise Search Matches: Lists relevant search results from the enterprise system based on the MDM ID.
   - Enterprise search match table has following columns: MDM ID, First name, Middle name, Last name, DOB, SSN/ITIN, Gender, Race, CIS ID, Participation
   - If there is no matching MDM ID case, enterprise search match should display "No matching records found"
5. Pagination should be implemented to display records in enterprise search matches. Users should be able to navigate through multiple pages of records efficiently using arrow buttons.
6. The CP screen should include a clearly labeled "Generate MDM ID" button.
7. On click of Generate MDM ID button on CP screen:
   - System Generate MDM ID for CP
   - System shall navigate to the NCP screen under the "Member Clearance" section in the Paper Application left navigation.

---

### User Story 2.2.2: Member Clearance - NCP Screen
**As a** case worker  
**I want** to process NCP member clearance  
**So that** I can verify NCP information

#### Acceptance Criteria - NCP Screen:
1. The NCP stepper should include the following three sections:
   - NCP: Displays the primary details of the Non Custodial Party retrieved from the database
   - NCP SSN History: Shows a historical record of the Non Custodial Party's Social Security Numbers
   - Enterprise Search Matches: Lists relevant search results from the enterprise system based on the MDM ID
2. Users should be able to edit, save and cancel the information in the SSN History section.
3. Pagination should be implemented to display records in enterprise search matches. Users should be able to navigate through multiple pages of records efficiently using arrow buttons.
4. The NCP screen should include a clearly labeled "Generate MDM ID" button.
5. On click of Generate MDM ID button on NCP screen:
   - System Generate MDM ID for NCP
   - System shall navigate to the Children screen.

---

### User Story 2.2.3: Member Clearance - Child Screen
**As a** case worker  
**I want** to process child member clearance  
**So that** I can verify child information

#### Acceptance Criteria - Child Screen:
1. The child stepper should include the following three sections:
   - Child: Displays the primary details of the child retrieved from the database
   - Child SSN History: Shows a historical record of the child's Social Security Numbers
   - Enterprise Search Matches: Lists relevant search results from the enterprise system based on the MDM ID
2. Users should be able to edit, save and cancel the information in the SSN History section.
3. Pagination should be implemented to display records in enterprise search matches. Users should be able to navigate through multiple pages of records efficiently using arrow buttons.
4. The child screen should include a very clearly labeled "Generate MDM ID" button.
5. On click of Generate MDM ID button on Children screen:
   - System Generate MDM ID for Child
   - System shall navigate to the "Member Status" page under Paper Application in the left navigation, retrieving information of CP, NCP, and child.

---

# 2.3 Member Status

### User Story 2.3.1: Member Status Page
**As a** case worker  
**I want** to be able to access member status  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. When the user clicks next on the member clearance page, the system would take it to the member status page and the left navigation would show member clearance as completed with a tick mark.
2. The system will have the following data fields in CP, NCP and child:
   - MDM ID (Text, Number, No - Mandatory)
   - Member ID (Text, Number, No - Mandatory)
   - Member type (Dropdown, No - Mandatory)
   - SSN/ITIN (Number, Toggle view icon, No - Mandatory)
   - First name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - DOB (Date picker, mm/dd/yyyy, No - Mandatory)
   - Gender (Dropdown, No - Mandatory)
   - Race (Dropdown, No - Mandatory)
   - Family violence (Radio button: Yes/No, No - Mandatory)
   - Protective order (Dropdown, No - Mandatory)
   - Domestic Violence (Dropdown, No - Mandatory)
3. System should display a "Previous" and "Next" button on the page.
4. On clicking the previous button, system should navigate to the member clearance page.
5. On click of Next button on Member Status page:
   - System should validate all the values in the fields
   - System shall navigate to the CP Demographics page under Paper Application in the left navigation.

---

# 2.4 CP Demographics

### User Story 2.4.1: CP Demographics Page
**As a** case worker  
**I want** to be able to access CP demographics  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. On the page titled CP demographics, top section shows a table with following columns: MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender, Race
2. CP personal information has following data fields:
   - County (Dropdown, Yes - Mandatory)
   - Nickname (Text, No - Mandatory)
   - Pregnancy (Radio button: Yes/No, No - Mandatory)
   - Maiden name (Text, No - Mandatory)
   - Suffix (Dropdown, No - Mandatory)
   - Relationship to child (Dropdown: Mother, Yes - Mandatory)
3. Temporary cash assistance has following data fields:
   - Cash assistance state (Dropdown, No - Mandatory)
   - Cash assistance county (Dropdown, No - Mandatory)
   - Date of last TCA check (Calendar, No - Mandatory)
   - TCA applicant (Radio button: Yes/No, Yes - Mandatory)
   - Current TCA recipient (Radio button: Yes/No, Yes - Mandatory)
   - Former TCA Recipient (Radio button: Yes/No, Yes - Mandatory)
4. Medical assistance section has following data fields:
   - Medical assistance state (Dropdown, No - Mandatory)
   - Medical assistance county (Dropdown, No - Mandatory)
   - MA applicant (Radio button: Yes/No, Yes - Mandatory)
   - Current MA recipient (Radio button: Yes/No, Yes - Mandatory)
   - Former MA Recipient (Radio button: Yes/No, Yes - Mandatory)
5. Communication section has following data fields:
   - Notification type (Radio button: Paper/Paperless, Yes - Mandatory)
   - Text notification (Radio button: Yes/No, Yes - Mandatory)
   - Email notification (Radio button: Yes/No, Yes - Mandatory)
   - Home phone (Text, No - Mandatory)
   - Business phone (Text, No - Mandatory)
   - Cell phone (Text, No - Mandatory)
   - Email (Text, No - Mandatory)
6. CP alternative name section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Suffix (Dropdown, No - Mandatory)
7. Mailing address section has following data fields:
   - Source (Dropdown: CP, No - Mandatory)
   - International address (Radio button: Yes/No, No - Mandatory)
   - Address manually verified (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown, No - Mandatory)
8. Residential address section has following data fields:
   - Residential address same as mailing address (Check box, No - Mandatory)
   - Source (Dropdown: CP, No - Mandatory)
   - International address (Radio button: Yes/No, No - Mandatory)
   - Address manually verified (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown, No - Mandatory)
9. Custodial party attorney section has following fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Phone (Text, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International address (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
10. CP Nearest relative section has following data fields:
    - First name (Text, No - Mandatory)
    - Middle name (Text, No - Mandatory)
    - Last name (Text, No - Mandatory)
    - Relationship to CP (Dropdown, No - Mandatory)
    - Phone (Text, No - Mandatory)
    - Source (Dropdown, No - Mandatory)
    - International Address (Radio button: Yes/No, No - Mandatory)
    - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
    - Address line1 (Alphanumeric, No - Mandatory)
    - Address line 2 (Alphanumeric, No - Mandatory)
    - City (Text, No - Mandatory)
    - State (Dropdown, No - Mandatory)
    - County (Dropdown, No - Mandatory)
    - Zip code (Text, Numbers, No - Mandatory)
    - Country (Dropdown: USA, No - Mandatory)
11. The bottom of the page has a Previous and Next button.
12. On clicking previous button, system navigates back to member status page.
13. On click of Next button on CP Demographics page:
    - System validates all the values in CP demographics pages
    - System shall navigate to the "CP Income and Assets" page, displaying sections for: CP Income and Assets, CP Assets and Income Information

---

# 2.5 CP Income and Assets

### User Story 2.5.1: CP Income and Assets Page
**As a** case worker  
**I want** to be able to access CP income and assets  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. CP Income and Assets page displays sections for:
   - CP Income and Assets
   - CP Income Information
   - CP Assets
2. CP income and assets table has following columns: MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender, Race
3. Income information table has following columns: Income type, income source, income frequency and income amount
4. CP assets section displays "No asset information is present" if there are no assets for the CP.
5. There should be a previous and next button in the bottom right corner of the page.
6. On click of the previous button, the system navigates back to the CP demographics page.
7. On click of Next button on CP Income & Assets page:
   - The system validates the values in the CP income and assets page
   - The system shall navigate to the "NCP Demographics" page.

---

# 2.6 NCP Demographics

### User Story 2.6.1: NCP Demographics Page
**As a** case worker  
**I want** to be able to access NCP demographics and address  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. The left navigation of NCP Demographics displays a checkmark on all pages preceding the NCP Demographics page, indicating their completion status.
2. The NCP demographics page displays a top section of Non-custodial Party data table with MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender and Race by retrieving it from the database.
3. NCP personal data section has following data fields:
   - Relationship to child (Dropdown: Father, No - Mandatory)
   - Maiden name (Text, No - Mandatory)
   - Suffix (Dropdown, No - Mandatory)
   - Age (Text, No - Mandatory)
   - Birth city (Text, No - Mandatory)
   - Birth state (Dropdown, No - Mandatory)
   - Identification marks (Text, No - Mandatory)
   - Marital status (Dropdown, No - Mandatory)
   - Deceased (Radio button: Yes/No, No - Mandatory)
   - Eyes (Dropdown, No - Mandatory)
   - Hair (Dropdown, No - Mandatory)
   - Height (Dropdown: Feet(ft), No - Mandatory)
   - Height (Dropdown: Inch(In), No - Mandatory)
   - Weight (Text: lbs, No - Mandatory)
   - Drivers' license number (Text, Number, No - Mandatory)
   - Drivers license state (Dropdown, No - Mandatory)
   - Citizenship status (Dropdown, No - Mandatory)
   - Will the NCP willing to submit to the jurisdiction state and can be served in Maryland? (Radio button: Yes/No, No - Mandatory)
   - Notification type (Radio button: Paper/Paperless, No - Mandatory)
   - Text notification (Radio button: Yes/No, No - Mandatory)
   - Email notification (Radio button: Yes/No, No - Mandatory)
   - Cell phone (Text, No - Mandatory)
   - Home phone (Text, No - Mandatory)
   - Business phone (Text, No - Mandatory)
   - Email (Text, No - Mandatory)
4. NCP alternative name section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Suffix (Dropdown, No - Mandatory)
5. NCP military information section has following data fields:
   - Military status (Dropdown, No - Mandatory)
   - Military branch (Dropdown, No - Mandatory)
   - Military service number (Text, Number, No - Mandatory)
   - Military entry date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Military discharge date (Date picker: mm/dd/yyyy, No - Mandatory)
6. NCP attorney information section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Phone (Text, Number, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
7. The NCP demographics page will have the previous and next button in the bottom right corner of the page.
8. On click of the previous button, the system shall navigate to CP income and assets page.
9. On click of Next button on NCP Demographics page:
   - System verifies all the values user enters
   - It shall navigate to the "NCP Address" page.

---

# 2.7 NCP Address

### User Story 2.7.1: NCP Address Page
**As a** Case worker  
**I want** to be able to access NCP address  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. On the NCP address page, NCP address information section displays the following information after retrieving that from the database: MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender, Race.
2. NCP residential address section has following data fields:
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address manually verified (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
   - Does the NCP belong to any of the following tribe (Radio button: Yes/No, No - Mandatory)
   - Name of tribe (Dropdown, No - Mandatory)
3. NCP mailing address section should have following data fields:
   - Residential address same as mailing address (Checkbox, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address manually verified (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
4. NCP incarceration information section should have following data fields:
   - Currently (Radio button: Yes/No, No - Mandatory)
   - Previously (Radio button: Yes/No, No - Mandatory)
   - Work release (Radio button: Yes/No, No - Mandatory)
   - Verification indicator (Radio button: Yes/No, No - Mandatory)
   - Prisoner ID number (Text, Number, No - Mandatory)
   - Institution type (Dropdown, No - Mandatory)
   - Institution name (Text, No - Mandatory)
   - Admission date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Projected release date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Release date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
5. There is the previous and next button on the bottom right corner of the page.
6. On clicking the previous button, the system navigates to the NCP demographics page.
7. On click of Next button on NCP Address page:
   - System validate the values in the page
   - System shall navigate to NCP relative page

---

# 2.8 NCP Relative

### User Story 2.8.1: NCP Relative Page
**As a** case worker  
**I want** to be able to access NCP relative information  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. NCP relative page should have NCP relative data section with MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender, Race.
2. NCP nearest relationship section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Relationship to NCP (Dropdown, No - Mandatory)
   - Phone (Text, Number, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
3. NCP's mother section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Phone (Text, Number, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
4. NCP's father section has following data fields:
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Phone (Text, Number, No - Mandatory)
   - Source (Dropdown, No - Mandatory)
   - International Address? (Radio button: Yes/No, No - Mandatory)
   - Address validated (Radio button, Question tool tip: Yes/No, No - Mandatory)
   - Address line1 (Alphanumeric, No - Mandatory)
   - Address line 2 (Alphanumeric, No - Mandatory)
   - City (Text, No - Mandatory)
   - State (Dropdown, No - Mandatory)
   - County (Dropdown, No - Mandatory)
   - Zip code (Text, Numbers, No - Mandatory)
   - Country (Dropdown: USA, No - Mandatory)
5. There should be a previous and next button on the page.
6. On clicking previous button, system shall navigate back to NCP address page.
7. On click of next:
   - System validates the values on the page
   - The system navigates to the NCP income and assets page.

---

# 2.9 NCP Income and Assets

### User Story 2.9.1: NCP Income and Assets Page
**As a** case worker  
**I want** to be able to access NCP income and assets  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. On NCP income and assets page, system should have following sections: NCP employer, Income information, Union information, Education information and NCP assets. Page is titled NCP employer.
2. NCP income and asset top section should have a table containing MDM ID, Member ID, Name, SSN/ITIN, DOB, Gender and Race.
3. Income information section has table with income type, income source, income frequency and income amount columns
4. Union information section should have following data fields:
   - Is NCP a union member? (Radio button: Yes/No, No - Mandatory)
5. Education information section should have following data fields:
   - Has the NCP completed high school /Equivalent (Radio button: Yes/No, No - Mandatory)
   - Does the NCP have license, certificate, registration, or permit that is necessary to practice or work in a particular business, occupation or profession (Radio button: Yes/No/Other, No - Mandatory)
6. There should be NCP asset section below that. It displays the message "No asset information is present" if there is no asset
7. There is a previous and next button at the bottom right corner of page.
8. On clicking the previous button, the system shall navigate back to NCP relative page.
9. On the click of next button:
   - System validates all values in the page
   - Navigates to child page.

---

# 2.10 Child Information

### User Story 2.10.1: Child Information Page
**As a** case worker  
**I want** to be able to access child information  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. On the page titled child data, top section has the following data fields:
   - Child member ID (Text, Number, No - Mandatory)
   - First name (Text, No - Mandatory)
   - Middle name (Text, No - Mandatory)
   - Last name (Text, No - Mandatory)
   - Suffix (Dropdown, No - Mandatory)
   - SSN (Text, Numbers, Toggle view icon, No - Mandatory)
   - DOB (Date picker: mm/dd/yyyy, No - Mandatory)
   - Emancipation date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Gender (Dropdown: Female, No - Mandatory)
   - Race (Dropdown: White, No - Mandatory)
   - State conceived (Dropdown, No - Mandatory)
   - City of birth (Text, No - Mandatory)
   - Country of birth (Dropdown: USA, No - Mandatory)
   - State of birth (Dropdown, No - Mandatory)
   - County of birth (Dropdown, No - Mandatory)
   - Out of home indicator (Radio button: Yes/No, No - Mandatory)
   - Out of home date (Date Picker: mm/dd/yyyy, No - Mandatory)
   - Relationship to CP (Dropdown: Daughter/Natural child, No - Mandatory)
   - Does the child reside in Maryland due to directives of the defendant? (Radio button: Yes/No, No - Mandatory)
2. Parentage information section and relationship between mother and father section have following data fields:
   - Parentage status (Dropdown: Requires establishment, No - Mandatory)
3. Relationship between mother and father:
   - Dropdown: Never married, No - Mandatory
4. There is DVR button on the page. When a user clicks on a DVR, it navigates to the DVR page.
5. System should also have the previous and next button on the page.
6. On clicking the previous button, the system navigates to NCP income and assets page.
7. On click of next:
   - The system validates the values in the field
   - Navigates to the member insurance page.

---

# 2.11 Member Insurance

### User Story 2.11.1: Member Insurance Page
**As a** case worker  
**I want** to be able to access member insurance information  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. Page titled Member insurance information has a table with following column: Member ID, name, SSN, DOB, Gender, Provider name, Policy number, view
2. There should be a previous and next button on the member insurance page.
3. On clicking previous button, system shall navigate to child page.
4. On clicking the next button, the system navigates to the case status page.

---

# 2.12 Case Status

### User Story 2.12.1: Case Status Page
**As a** case worker  
**I want** to be able to access case status information  
**So that** I can edit the application created by intake worker

#### Acceptance Criteria:
1. User should be able to navigate to the case status page after clicking next on case registration pages and all other pages before that on case registration has a tick mark in left navigation indicating a completion status.
2. The system should show the application number on the top right section of the case status page.
3. The case status page should have a case information section and good cause section.
4. Case information section should have following data fields:
   - Case type (Dropdown: IV-D, No - Mandatory)
   - Case subtype (Dropdown: Never Assistance, No - Mandatory)
   - Case type date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Assistance status (Dropdown: Not applicable, No - Mandatory)
   - Intergovernmental status (Dropdown: Maryland, Yes - Mandatory)
   - Case status date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Application fee status (Dropdown: Paid, No - Mandatory)
   - Application completion date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Case Jurisdiction (Dropdown: Howard county, Yes - Mandatory)
   - Family violence indicator (Radio button: Yes/No, No - Mandatory)
   - Intent to close (Dropdown, No - Mandatory)
   - Intent to close date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Automated closing eligibility date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Service required (Dropdown, Yes - Mandatory)
5. Good cause section has following data fields:
   - Good cause indicator (Radio button: Yes/No, No - Mandatory)
   - Status (Dropdown, No - Mandatory)
   - Status date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Reason (Dropdown, No - Mandatory)
   - IV-D cooperation status (Radio button: Yes/No, No - Mandatory)
   - IV-D cooperation date (Date picker: mm/dd/yyyy, No - Mandatory)
   - Assignment of rights (Radio button: Yes/No, No - Mandatory)
6. On selecting a value from Service Requested dropdown on Case Status page, System should allow the user to select from the following options:
   - Child Support Only
   - Collection and Disbursement
   - Enforcement of Order
   - Full Service
   - Locate Only
   - Medical Support Only
7. Page should have a previous, cancel and done button.
8. On clicking the previous button, the system shall navigate to the member insurance page.
9. On clicking the cancel button, system should navigate to case registration home page.
10. On click of Done button on Case Status page:
    - System shall display a confirmation message box with the message: "Case has been registered with the case ID."
    - System should provide a "Close" button on the confirmation box.

---

# 2.13 Cancel and Resume Application

### User Story 2.13.1: Cancel and Resume Application
**As a** case worker  
**I want** the ability to cancel an application at any stage  
**So that** I can pause my work when necessary and resume the application later without losing progress

#### Acceptance Criteria:
1. A Cancel button should be available on every page from Member Status to Case Status, allowing the user to cancel the application process at any time.
2. Upon cancellation, the application should be saved as a draft and visible on the Case Registration Home Page.
3. The Case Registration Home Page should display a Continue button next to any canceled (draft) application, allowing users to resume and complete the case creation.

---

# 2.14 Auto-Deletion of Inactive Cases

### User Story 2.14.1: Auto-Deletion of Inactive Cases After 90 Days
**As a** case worker  
**I want** cases with no progress to be automatically deleted after 90 days  
**So that** I can focus my efforts on active cases without unnecessary clutter

#### Acceptance Criteria:
1. If no progress or updates are made to an application within 90 calendar days from the last activity date, the case should be automatically deleted from the system.
2. Progress is defined as any change in the application status, updates to case details, or movement to the next workflow step.
3. Before deletion, the system must send a notification to the assigned case worker at least 7 days in advance, warning them about the upcoming deletion.
4. Upon deletion, all associated case information must be removed from the system to maintain data security and compliance.
5. If a case is updated before the 90-day period expires, the 90-day timer should reset from the latest activity date.

---

**Document Status:** Complete. Source: CSMS_Developer_Requirements_with_Acceptance_Criteria.md, CaseRegistrationUserstoryPagebased.txt.
