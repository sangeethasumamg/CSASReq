# Child Support Management System (CSMS) - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for all modules to enable developers to implement the Child Support Management System. Each requirement includes specific acceptance criteria that must be met for the feature to be considered complete.

---

## Table of Contents
1. [INTAKE MODULE](#1-intake-module)
2. [CASE REGISTRATION MODULE](#2-case-registration-module)
3. [CASE MANAGEMENT MODULE](#3-case-management-module)
4. [LOCATE MODULE](#4-locate-module)
5. [ESTABLISHMENT MODULE](#5-establishment-module)
6. [ENFORCEMENT MODULE](#6-enforcement-module)
7. [FINANCE MODULE](#7-finance-module)

---

# 1. INTAKE MODULE

## 1.1 Menu Items and Navigation

### User Story 1.1.1: Menu Items Display
**As a** intake worker  
**I want** to see menu items on the dashboard  
**So that** I can have access to various modules

#### Acceptance Criteria:
1. The dashboard displays a list of menu items that correspond to different modules, generated dynamically from the database.
2. The top navigation bar should include the following options in a clearly visible and accessible layout:
   - Hamburger Icon: To expand or collapse the side navigation menu
   - Search Case Number Field: A text field for entering a case number
   - Go Button: Executes the case number search when clicked
   - Clear Button: Resets the case number search field
   - Advanced Search (ADV Search)
   - Document Generation
   - SSP: Link to Self-Service Portal
   - DVR: Link to Digital Video Recording
   - File Management: Provides access to file management features
   - Reports: Link to reporting tools and features
   - Alerts: Displays alerts and notifications related to cases or system updates
   - Prompts: Shows prompts or tips for navigating and using the system
   - Contact Support: Option to contact support for assistance
   - Profile name: Name of person who logged in
3. The secondary top navigation should include quick access to the following modules:
   - Dashboard
   - Case Registration
   - Case Management
   - Locate
   - Intergovernmental
   - Establishment
   - Enforcement
   - Financial Management
4. The side navigation should provide access to options such as:
   - Entire Case Load
   - Intake Search
   - Intake
   - Referral Cases
   - Intergovernmental Cases
   - Establishment Cases
   - Enforcement Cases
   - Financial Management Cases
   - Case Management
   - File Upload
   - Mail Processing
   - Notices
5. Each module is accessible through a clickable menu item on the dashboard.
6. Modules are organized logically and visibly, allowing for easy navigation.
7. The menu items and modules load without delay upon accessing the dashboard.
8. Access permissions ensure that users only see the modules relevant to their role, with visibility controlled based on database permissions.
9. Menu items are updated in real time as per database changes, ensuring that newly added or removed modules are reflected without requiring a page reload.

---

## 1.2 Intake Search

### User Story 1.2.1: Intake Search Functionality
**As a** Intake Worker  
**I want** to search for applications using specific fields and filters  
**So that** I can quickly find and view the relevant application details with ease

#### Acceptance Criteria:
1. When user clicks on the "intake search" option, the following fields should appear on the page:
   - Application Number (Numeric - digits only)
   - Application Name (Text - letters only)
   - Application Status (Dropdown with predefined status options)
   - Start Date (Date formatted as MM-DD-YYYY, Calendar picker)
   - End Date (Date formatted as MM-DD-YYYY, Calendar picker)
   - Items per page (Numeric, Dropdown)
2. The Application Status field should be a dropdown, allowing user to select from predefined status options.
3. The page should have a Search button to initiate the search and a Clear button to reset all fields.
4. On click of search button:
   - System should validate all the values
   - The system should pull and display corresponding application details based on the application number/application name which the user gives
5. The latest application should appear first when fetching the results. All applications should be fetched from the database and displayed accordingly.
6. Pagination should be implemented on the page to allow users to navigate through multiple results if the list of applications is long.

---

## 1.3 Paper Application IV-D Entry

### User Story 1.3.1: Create New Application
**As a** Intake Worker  
**I want** to create a new IV-D application  
**So that** I can start processing child support applications

#### Acceptance Criteria:
1. When the user clicks on the "intake" option, the paper application IV-D page should open.
2. Paper application field dropdown and application name field should be present on the paper application IV-D page.
3. The application name field should only contain alphabets/spaces.
4. Paper application dropdown should have the following set of predefined values:
   - Walk-in
   - Mail
   - Electronic
5. By clicking the next button:
   - The system should validate all the fields
   - The system must save all the values in the database
   - The system should generate a 9 digit application number
6. Application numbers must be sequential.
7. Intake screen and application number should be stored in `Intake_Application` table.

---

## 1.4 Custodial Party (CP) Application Entry

### User Story 1.4.1: CP Application Form
**As a** Intake worker  
**I want** to access custodial party paper application page  
**So that** I can fill the form

#### Acceptance Criteria:

##### CP Personal Information:
1. System should capture the following CP personal information fields:
   - First Name (Text - letters only, Mandatory)
   - Middle Name (Text - letters only)
   - Last Name (Text - letters only, Mandatory)
   - Suffix (Dropdown: Jr, Sr, Ms, Mr, Mrs, Dr)
   - Maiden Name (Text - letters only)
   - Nickname (Text - letters only)
   - DOB (Date formatted as MM-DD-YYYY, Calendar picker)
   - SSN/ITIN (Numeric and special characters, format ###-##-####)
   - Gender (Dropdown with predefined status labels)
   - Race (Dropdown with predefined status labels)
   - Relationship to child (Dropdown: Aunt, Brother, Cousin, Father, Foster parent/state, etc.)

2. System should capture CP Alternative Name:
   - First Name (Text)
   - Middle Name (Text)
   - Last Name (Text)
   - Suffix (Dropdown)

3. System should validate all mandatory fields before allowing progression.

##### CP Address Information:
4. Applicant Mailing Address section should capture:
   - Source (Dropdown with predefined status labels)
   - International address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown with predefined status labels)
   - County (Dropdown with predefined status labels)
   - Zip code (Numeric)
   - Country (Dropdown with predefined status labels)

5. Applicant Residential Address section should capture:
   - Option to check that it is the same as the mailing address (Checkbox)
   - Source (Dropdown)
   - International address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown)
   - County (Dropdown)
   - Zip code (Numeric)
   - Country (Dropdown)

##### CP Contact Information:
6. System should capture contact information:
   - Home phone (Numeric)
   - Business phone (Numeric)
   - Cellphone (Numeric)
   - Email (Alphanumeric characters only)

##### CP Nearest Relative Information:
7. System should capture CP nearest relative information:
   - Relation to applicant (Dropdown)
   - First name (Text - letters only)
   - Last name (Text - letters only)
   - Phone (Numeric)
   - Relative Address:
     - Source (Dropdown)
     - International address (Radio button: Yes/No)
     - Address validated (Tooltip)
     - Address line 1 (Alphanumeric characters only)
     - Address line 2 (Alphanumeric characters only)
     - City (Text - letters only)
     - State (Dropdown)
     - County (Dropdown)
     - Zip code (Numeric)
     - Country (Dropdown)

##### CP Employer Information:
8. System should capture employer information:
   - Is the custodial party employed? (Radio button: Yes/No)
   - If employed, employer details should be captured

##### CP Income Information:
9. Custodial Party Income Information section should have:
   - Income type (Dropdown with predefined status labels)
   - Income frequency (Dropdown with predefined status labels)
   - Income amount (Numeric)
   - Clickable "Add" button to add multiple income entries

##### CP Benefit Information:
10. Benefit information section should capture:
    - Current TCA recipient? (Radio button: Yes/No)
    - Former TCA recipient? (Radio button: Yes/No)
    - TCA Applicant? (Radio button: Yes/No)
    - Current MA recipient? (Radio button: Yes/No)
    - Former MA Recipient? (Radio button: Yes/No)
    - MA applicant? (Radio button: Yes/No)
    - Confirm button on the benefit information section

##### CP Attorney Information:
11. Custodial party Attorney information section should capture:
    - First name (Text - letters only)
    - Middle name (Text - letters only)
    - Last name (Text - letters only)
    - Phone (Numeric and special characters, e.g., (530)413-322)
    - Source (Dropdown)
    - International address (Radio button: Yes/No)
    - Address validated (Tooltip)
    - Address line1 (Alphanumeric characters only)
    - Address line2 (Alphanumeric characters only)
    - City (Text - letters only)
    - State (Dropdown)
    - County (Dropdown)
    - Zip code (Numeric)
    - Country (Dropdown)

##### CP Asset Information:
12. Custodial party asset information section should have:
    - Add asset button on custodial party asset information section

##### Family Violence:
13. Family violence (Radio button: Yes/No)

##### Data Storage:
14. Once a user fills the CP application, all information should be pushed to the corresponding data tables:
    - Personal information of CP should be stored in `Person` table
    - Employer information should be stored in the `Person_Employer` table
    - Asset information should be stored in the `Asset` table
    - Attorney information should be stored in the `Attorney` table
    - All income information should be stored in table `Person_Income`
    - Mapping role of a person to CP, NCP and Child must happen in the `Person_Role_Link` table
    - All the tables should be under `portal` schema

##### Navigation:
15. The system should have a clickable clear button and next button at the bottom of the custodial party page.
16. When user clicks on the next button, NCP application screen displays on the same page.

---

## 1.5 Non-Custodial Party (NCP) Application Entry

### User Story 1.5.1: NCP Application Form
**As a** Intake worker  
**I want** to access non-custodial party application page  
**So that** I can fill the NCP form

#### Acceptance Criteria:

##### NCP Personal Information:
1. System should capture the following NCP personal information fields:
   - First Name (Text - letters only)
   - Middle Name (Text - letters only)
   - Last Name (Text - letters only)
   - Suffix (Dropdown: Jr, Sr)
   - Relationship to child (Dropdown)
   - Nick name (Text - letters only)
   - Maiden name (Text - letters only)
   - Approx age (Numeric)
   - Source (Dropdown)
   - DOB (Date, Calendar picker)
   - SSN/ITIN (Numeric and special characters)
   - Gender (Dropdown)
   - Race (Dropdown)
   - Citizenship status (Dropdown)
   - Marital status (Dropdown)
   - Email (Alphanumeric characters only)
   - Home phone (Numeric and special characters)
   - Business phone (Numeric and special characters)
   - Cell phone (Numeric and special characters)
   - Eye colour (Dropdown)
   - Height(ft) (Dropdown - predefined numbers)
   - Height(in) (Dropdown - predefined numbers)
   - Identification mark (Text - letters only)
   - Hair color (Dropdown)
   - Weight (Numeric)
   - Drivers license number (Numeric)
   - Place of birth city (Text - letters only)
   - Place of birth state (Dropdown)

##### NCP Address Information:
2. NCP Address section should capture:
   - Source (Dropdown)
   - International Address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line 1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown)
   - County (Dropdown)
   - Zip code (Numeric and special characters)
   - Country (Dropdown)

##### NCP Alternative Name:
3. System should capture NCP alternative name:
   - First name (Text)
   - Middle name (Text)
   - Last name (Text)
   - Suffix (Dropdown: Jr, Sr)

##### NCP Military Information:
4. Non-custodial party military information section should capture:
   - Has the NCP ever served in military? (Radio button: Yes/No)
   - If yes, capture military details

##### NCP Incarceration Information:
5. Non-custodial party incarceration information section should capture:
   - Has the NCP ever been in jail? (Radio button: Yes/No)
   - If yes, capture incarceration details

##### NCP Nearest Relationship:
6. Non-custodial party nearest relationship section should capture:
   - First name (Text)
   - Middle name (Text)
   - Last name (Text)
   - Relationship to NCP (Dropdown)
   - Phone (Numeric and special characters)
   - Source (Dropdown)
   - International address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line 1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown)
   - County (Dropdown)
   - Zip code (Numeric and special characters)
   - Country (Dropdown)

##### NCP Mother Information:
7. NCP's Mother section should capture:
   - First name (Text)
   - Middle name (Text)
   - Last name (Text)
   - Phone (Numeric and special characters)
   - Source (Dropdown)
   - International address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line 1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown)
   - County (Dropdown)
   - Zip code (Numeric)
   - Country (Dropdown)

##### NCP Father Information:
8. NCP Father section should capture:
   - First name (Text)
   - Middle name (Text)
   - Last name (Text)
   - Phone (Numeric and special characters)
   - Source (Dropdown)
   - International address (Radio button: Yes/No)
   - Address validated (Tooltip)
   - Address line 1 (Alphanumeric characters only)
   - Address line 2 (Alphanumeric characters only)
   - City (Text - letters only)
   - State (Dropdown)
   - County (Dropdown)
   - Zip code (Numeric and special characters)
   - Country (Dropdown)

##### NCP Employer Information:
9. NCP employer information section should capture:
   - Is the NCP employed? (Radio button: Yes/No)
   - If employed, capture employer details

##### NCP Income and Expense Information:
10. NCP income and expense information section should capture:
    - NCP has license or permit to work? (Radio button: Yes/No)
    - Type (Text - Letters)
    - NCP have other child support cases? (Radio button: Yes/No)
    - State (Dropdown)
    - Income type (Dropdown)
    - Income Frequency (Dropdown)
    - Income amount (Numeric)
    - Add button for the NCP income and expense information section

##### NCP Attorney Information:
11. NCP Attorney information section should capture:
    - First name (Text)
    - Middle name (Text)
    - Last name (Text)
    - Phone (Numeric and special characters, e.g., (530)413-322)
    - Source (Dropdown)
    - International address (Radio button: Yes/No)
    - Address validated (Tooltip)
    - Address line1 (Alphanumeric characters only)
    - Address line2 (Alphanumeric characters only)
    - City (Text - letters and space)
    - State (Dropdown)
    - County (Dropdown)
    - Zip code (Numeric)
    - Country (Dropdown)

##### NCP Asset Information:
12. NCP Asset information section should have:
    - Add asset (Clickable button)

##### Data Storage:
13. Once user clicks next button on NCP application screen:
    - The system validates all values
    - All information should be pushed to the corresponding data tables:
      - Personal information of NCP should be stored in `Person` table
      - Employer information should be stored in the `Person_Employer` table
      - Asset information should be stored in the `Asset` table
      - Attorney information should be stored in the `Attorney` table
      - Military information for NCP should be stored in `Military_Information` table
      - All income information should be stored in table `Person_Income`
      - Mapping role of a person to CP, NCP and Child must happen in the `Person_Role_Link` table
      - All the tables should be under `portal` schema
    - System would take user to next screen named 'support'

##### Navigation:
14. The system should have a clickable back button and next button at the bottom of the non-custodial party page.

---

## 1.6 Support and Insurance Screen

### User Story 1.6.1: Support and Insurance Information
**As a** Intake worker  
**I want** to access the child information and insurance sections  
**So that** I can fill the form

#### Acceptance Criteria:

##### Relationship Information:
1. On the support section screen, dropdown for the relationship between CP and NCP should be present with following predefined status:
   - Unknown
   - Never married
   - Separated
   - Currently married
   - Divorced

2. When the user selects 'separated' in the relationship dropdown, following fields should be revealed:
   - Date Married (Date picker)
   - Date separated (Calendar Picker, formatted as MM-DD-YYYY)
   - Country separated (Dropdown)
   - State separated (Dropdown)
   - County separated (Dropdown)
   - Divorce proceedings by attorney/by court action pending (Radio button: Yes/No)
   - Is child support included in this action? (Radio button: Yes/No)

3. When the user selects 'currently married' in the relationship dropdown, following fields should be visible:
   - Date married (Date picker, formatted as MM-DD-YYYY)
   - Country married (Dropdown)
   - State married (Dropdown)
   - County married (Dropdown)

4. When the user selects 'divorced' in the relationship dropdown, following fields should be visible:
   - Date married (Date picker, formatted as MM-DD-YYYY)
   - Date divorced (Date picker, formatted as MM-DD-YYYY)
   - Country divorced (Dropdown)
   - State divorced (Dropdown)
   - County divorced (Dropdown)

##### Child Information:
5. On the child information section, there should be a clickable 'Add Child' button.

6. Upon clicking the 'Add Child' button, the following fields must appear (with data types as specified):
   - First name (Text - letters, Mandatory)
   - Middle name (Text - letters)
   - Last name (Text - letters, Mandatory)
   - Suffix (Dropdown)
   - Race (Dropdown, Mandatory)
   - Relationship to applicant (Dropdown, Mandatory)
   - Conception occurred state (Dropdown)
   - Gender (Dropdown, Mandatory)
   - Birth state (Dropdown)
   - Birth county (Dropdown)
   - Birth city (Text including space)
   - SSN (Numeric and special characters, visibility toggle)
   - Date of Birth (Calendar picker, formatted as MM-DD-YYYY, Mandatory)
   - Was the mother married to father at the time of birth? (Radio Button: Yes/No)
   - Is there an order for child support for this child? (Radio Button: Yes/No)
   - Does the NCP pay the support? (Radio Button: Yes/No)
   - To whom does NCP party pay the support? (Radio Button: To You, To a Child Support Agency, Other)
   - Clickable save button

7. Once user clicks on the save button:
   - The system validates all values
   - Information is displayed in the table and displayed below the 'Add Child' button with columns: First name, Last name, SSN/ITIN, Race, DOB, Gender

8. There should be flexibility for deleting and updating child information.

9. On clicking the 'Update' button:
   - System should validate all values
   - Updated information should be saved

##### Member Insurance Section:
10. On the member insurance section, there should be an 'add insurance' clickable button.

11. All health insurance details must be stored in the `Person_Health_Insurance` table.

##### Service Request Section:
12. On the File Upload feature/screen in the service request section, there should be following checkboxes along with question tooltip:
    - Full service
    - Locate only
    - Paternity only
    - Medical support only
    - Child support only
    - Child and spousal support only

13. On the file upload section, there should be mandatory dropdown for select category and select document type.

14. There should also be a choose file clickable button and scan button in the section.

15. File upload will be a dummy section currently (to be implemented later).

##### Data Storage:
16. On clicking next:
    - Child information is stored in the `Person` table
    - Parent relationships are stored in the `Parent_Relationship` table
    - Navigate to insurance screen

##### Success Screen:
17. Success screen should display: "Your application has been submitted successfully, assigned to [assigned email]"

18. There should also be a navigate to home page clickable button.

##### Navigation:
19. There should be a back and next button on the paper application custodial party page for navigations.

---

## 1.7 Application in Progress/Resume

### User Story 1.7.1: Save and Resume Application
**As a** Intake Worker  
**I want** to log off from the application  
**So that** I can resume the application wherever I left off

#### Acceptance Criteria:
1. When the user saves a CP/NCP application in the middle of the process and logs off from the system, the application state should be preserved.
2. The system should display a "Resume" Application link near the "In Progress" application status on the Intake Search page.
3. When the user clicks on the "Resume" Application link, they should be directed to the Applicant Information page with all their previously saved data pre-populated.

---

# 2. CASE REGISTRATION MODULE

## 2.1 Case Registration Home Page

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

## 2.2 Member Clearance

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

## 2.3 Member Status

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

## 2.4 CP Demographics

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

## 2.5 CP Income and Assets

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

## 2.6 NCP Demographics

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

## 2.7 NCP Address

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

## 2.8 NCP Relative

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

## 2.9 NCP Income and Assets

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

## 2.10 Child Information

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

## 2.11 Member Insurance

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

## 2.12 Case Status

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

## 2.13 Cancel and Resume Application

### User Story 2.13.1: Cancel and Resume Application
**As a** case worker  
**I want** the ability to cancel an application at any stage  
**So that** I can pause my work when necessary and resume the application later without losing progress

#### Acceptance Criteria:
1. A Cancel button should be available on every page from Member Status to Case Status, allowing the user to cancel the application process at any time.
2. Upon cancellation, the application should be saved as a draft and visible on the Case Registration Home Page.
3. The Case Registration Home Page should display a Continue button next to any canceled (draft) application, allowing users to resume and complete the case creation.

---

## 2.14 Auto-Deletion of Inactive Cases

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

*[This document continues with Case Management, Locate, Establishment, Enforcement, and Finance modules. The format follows the same structure with user stories and detailed acceptance criteria for each feature.]*

---

**Document Status**: This is Part 1 of the Developer Requirements document. Parts 2-7 will continue with Case Management, Locate, Establishment, Enforcement, and Finance modules following the same detailed format with acceptance criteria.
