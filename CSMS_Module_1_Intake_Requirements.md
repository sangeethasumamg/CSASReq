# CSMS Module 1: INTAKE - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Intake Module to enable developers to implement intake functionality in the Child Support Management System.

---

## Table of Contents
1. [Menu Items and Navigation](#11-menu-items-and-navigation)
2. [Intake Search](#12-intake-search)
3. [Paper Application IV-D Entry](#13-paper-application-iv-d-entry)
4. [Custodial Party (CP) Application Entry](#14-custodial-party-cp-application-entry)
5. [Non-Custodial Party (NCP) Application Entry](#15-non-custodial-party-ncp-application-entry)
6. [Support and Insurance Screen](#16-support-and-insurance-screen)
7. [Application in Progress/Resume](#17-application-in-progressresume)

---

# 1.1 Menu Items and Navigation

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

# 1.2 Intake Search

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

# 1.3 Paper Application IV-D Entry

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

# 1.4 Custodial Party (CP) Application Entry

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

# 1.5 Non-Custodial Party (NCP) Application Entry

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

# 1.6 Support and Insurance Screen

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

# 1.7 Application in Progress/Resume

### User Story 1.7.1: Save and Resume Application
**As a** Intake Worker  
**I want** to log off from the application  
**So that** I can resume the application wherever I left off

#### Acceptance Criteria:
1. When the user saves a CP/NCP application in the middle of the process and logs off from the system, the application state should be preserved.
2. The system should display a "Resume" Application link near the "In Progress" application status on the Intake Search page.
3. When the user clicks on the "Resume" Application link, they should be directed to the Applicant Information page with all their previously saved data pre-populated.

---

**Document Status:** Complete. Source: CSMS_Developer_Requirements_with_Acceptance_Criteria.md, Userstory_CSMSIntake.txt.
