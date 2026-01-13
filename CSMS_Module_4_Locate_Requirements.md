# CSMS Module 4: LOCATE - Developer Requirements with Acceptance Criteria

## Document Purpose
This document provides detailed requirements with acceptance criteria for the Locate Module to enable developers to implement locate functionality in the Child Support Management System.

---

## Table of Contents
1. [Locate Module Overview](#41-locate-module-overview)
2. [Cases Tab - Search Functionality](#42-cases-tab---search-functionality)
3. [Locate Summary](#43-locate-summary)
4. [Demographics Section](#44-demographics-section)
5. [Address Section](#45-address-section)
6. [Employer Section](#46-employer-section)
7. [Contact Section](#47-contact-section)
8. [File Upload in Locate](#48-file-upload-in-locate)
9. [Required Action Tab](#49-required-action-tab)

---

# 4.1 Locate Module Overview

### User Story 4.1.1: Locate Module Access
**As a** Intake worker / Case worker  
**I want** to have locate module  
**So that** I can locate NCP/CP

#### Acceptance Criteria:
1. There should be a locate module tab in the second top navigation.
2. Clicking on the "Locate Module" reveals "Cases" and "Required Action" sub-tabs.

---

# 4.2 Cases Tab - Search Functionality

### User Story 4.2.1: Case Search in Locate
**As a** Intake worker / Case worker  
**I want** to search for cases to locate NCP/CP  
**So that** I can find and update location information

#### Acceptance Criteria:
1. When user clicks on "Cases" tab, the following search fields should be present on the page:
   - Case number (Text field)
   - First name (CP/NCP) (Text field)
   - Last name (CP/NCP) (Text field)
   - Clickable Search button
   - Clickable Clear button
   - Pagination controls
2. When user clicks on search button:
   - System validates all values
   - A list of cases matching the specific case number or person names (CP/NCP) is displayed
3. When a user clicks on a case/NCP/CP from the search results, the system displays an accordion structure with the following sections:
   - Locate Summary
   - Demographics
   - Address
   - Employer
   - Contact
4. The system should support pagination for navigating through multiple search results.

---

# 4.3 Locate Summary

### User Story 4.3.1: Locate Summary View
**As a** Case worker  
**I want** to view locate summary information  
**So that** I can see an overview of location data

#### Acceptance Criteria:
1. When user clicks the "Locate Summary" in the NCP/CP accordion, System displays following expandable/collapsible sections:
   - Case Information
   - Address Information
   - NCP/CP Employer Information
   - Change History
2. Case Information section displays:
   - Case number
   - Case type
   - Case status
   - Case sub-type
   - Case sub-type status
   - Domestic violence indicator
   - Family violence indicator
   - Protective order indicator
   - Good cause indicator
   - CP name, CP member ID, CP MDM ID, CP SSN/ITIN, CP deceased indicator, case association
   - NCP name, NCP member ID, NCP MDM ID, NCP SSN/ITIN, NCP deceased indicator, NCP incarceration indicator, case association
3. Address Information section displays:
   - Address type
   - Address
   - International address
   - Status
   - Source
   - Date
4. NCP/CP Employer Information section displays:
   - Employer name
   - Address
   - Status
   - Source
   - Start date
   - Date
5. Change History section displays:
   - Source
   - Type
   - Updated
   - System/User
   - View details
6. The sections must support pagination for navigating multiple records.
7. A 'Previous' button should be available to navigate between sections.

---

# 4.4 Demographics Section

### User Story 4.4.1: Demographics Locate Information
**As a** Case worker  
**I want** to view and update demographics information from locate sources  
**So that** I can maintain accurate demographic data

#### Acceptance Criteria:
1. When the user clicks "Demographics" in the NCP/CP accordion, display following expandable/collapsible sections:
   - Case Information
   - NCP/CP Demographics from Sources
   - SSN from Sources
   - Add New
   - Change History
2. Case Information section displays:
   - Case number, Case type, Case status, Case sub-type
   - Assistance status, Arrears only
   - Domestic violence indicator, Family violence indicator, Protective order indicator, Good cause indicator
   - CP information (name, member ID, MDM ID, SSN/ITIN, deceased indicator, case association)
   - NCP information (name, member ID, MDM ID, SSN/ITIN, deceased indicator, incarceration indicator, case association)
3. NCP/CP Demographics from Sources section:
   - Must have pagination
   - Displays: Select radio button, Source, Received date, First name, Middle name, Last name, DOB, Status
   - Includes buttons: Reset (reset current selection), Update, Enterprise Search, Next
4. NCP/CP SSN from Sources section:
   - Displays: Select radio button, Source, Received date, SSN, Additional SSN, SSN status
   - Includes buttons: Previous, Reset, Enterprise Search, Update, Next
5. Add New section:
   - Includes an "Add New" clickable button
   - Allows adding new demographic information
6. Change History section:
   - Displays: Source, First name, Middle name, Last name, SSN, DOB, Updated, System/User
   - Provides pagination
   - Includes Previous button for navigation

---

# 4.5 Address Section

### User Story 4.5.1: Address Locate Information
**As a** Case worker  
**I want** to view and update address information from locate sources  
**So that** I can maintain current address data

#### Acceptance Criteria:
1. When the user clicks "Address" under the NCP/CP accordion, display expandable/collapsible sections:
   - Case Information
   - Address Information
   - Address from Sources
   - Add New
   - Change History
2. Case Information section displays standard case and party information.
3. Address Information section displays current address data.
4. Address from Sources section:
   - Provides pagination for navigating multiple address records
   - Displays address information from various sources
   - Includes Reset and Save buttons
5. Add New section:
   - Includes an "Add New Address" clickable button
   - Allows adding new address information
6. Change History section:
   - Provides pagination
   - Displays address change history
7. Previous button available for navigation between sections.

---

# 4.6 Employer Section

### User Story 4.6.1: Employer Locate Information
**As a** Case worker  
**I want** to view and update employer information from locate sources  
**So that** I can maintain current employer data

#### Acceptance Criteria:
1. When the user clicks "Employer" under the NCP/CP accordion, display expandable/collapsible sections:
   - Case Information
   - NCP/CP Employer Information
   - Employer from Sources
   - Add New
   - Change History
2. Case Information section displays standard case and party information.
3. NCP/CP Employer Information section displays current employer data.
4. Employer from Sources section:
   - Includes Reset and Add Employer buttons
   - Displays employer information from various sources
5. Add New section:
   - Includes an "Add Employer" clickable button
   - Includes Previous and Next buttons
   - Allows adding new employer information
6. Change History section:
   - Provides pagination
   - Displays employer change history
7. Previous button available for navigation between sections.

---

# 4.7 Contact Section

### User Story 4.7.1: Contact Locate Information
**As a** Case worker  
**I want** to view and update contact information  
**So that** I can maintain current contact data

#### Acceptance Criteria:
1. When the user clicks "Contact" under the NCP/CP accordion, display expandable/collapsible sections:
   - Case Information
   - NCP Contact Information
   - Add New
   - Change History
2. Case Information section displays standard case and party information.
3. NCP Contact Information section displays current contact data.
4. Add New section:
   - Includes Save and Clear buttons
   - Allows adding new contact information
5. Change History section:
   - Provides pagination
   - Displays contact change history
6. Previous button available for navigation between sections.

---

# 4.8 File Upload in Locate

### User Story 4.8.1: File Upload for Locate Cases
**As a** Case worker  
**I want** to upload files related to locate cases  
**So that** I can attach supporting documents

#### Acceptance Criteria:
1. When the user clicks "File Upload" in the Locate module, the file upload page displays.
2. Searching options should be possible either through Case Number or Application Number.
3. When user enters case number in the enter case number field:
   - The user is able to search that particular case number details
   - The system pulls information from the following fields from the database:
     - Case Number
     - Application Number
     - Member ID
     - Jurisdiction
     - SSN
     - ITIN
     - First Name
     - Last Name
     - Date of Birth
     - MDM ID
     - IRN
4. User is able to upload file/Scan file after choosing category, document type and document subtype.
5. Files must be less than 25 MB each, with a total combined size not exceeding 250 MB.
6. Files must be in one of the following formats: PDF, Word documents (.doc, .docx), or image files (.jpg, .png, .gif, .bmp).
7. The system should have pagination for navigating multiple records in the page.

---

# 4.9 Required Action Tab

### User Story 4.9.1: Required Actions in Locate
**As a** Case worker  
**I want** to see required actions in the Locate module  
**So that** I can prioritize locate tasks

#### Acceptance Criteria:
1. The "Required Action" tab displays actions that require case worker attention.
2. Actions are organized and sortable.
3. Each action includes relevant case/party information.
4. Actions can be filtered and searched.
5. Pagination is provided for navigating multiple actions.

---

**Document Status**: Complete requirements for Locate Module with detailed acceptance criteria for developer implementation.

**Related Documents**: 
- CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Intake and Case Registration)
- CSMS_Module_3_Case_Management_Requirements.md
