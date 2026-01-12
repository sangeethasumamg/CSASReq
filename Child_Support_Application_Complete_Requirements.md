# Child Support Management System (CSMS) - Complete Requirements Document

## Table of Contents
1. [Executive Summary](#executive-summary)
2. [System Overview](#system-overview)
3. [Module Requirements](#module-requirements)
4. [System Architecture](#system-architecture)
5. [Database Design](#database-design)
6. [Technical Specifications](#technical-specifications)
7. [Security and Compliance](#security-and-compliance)
8. [Integration Requirements](#integration-requirements)

---

## 1. Executive Summary

The Child Support Management System (CSMS) is a comprehensive application designed to manage the entire lifecycle of child support cases from intake through enforcement and financial management. This document provides detailed requirements for building a complete child support application covering all functional modules.

### 1.1 Key Modules
- **Intake Module**: Application intake and initial data collection
- **Case Registration Module**: Case registration and member clearance
- **Case Management Module**: Ongoing case management and maintenance
- **Locate Module**: Locating NCP/CP and related information
- **Establishment Module**: Establishing paternity and support orders
- **Enforcement Module**: Enforcement of child support orders
- **Finance Module**: Financial transactions, payments, and disbursements

---

## 2. System Overview

### 2.1 Purpose
The CSMS system enables child support agencies to efficiently manage cases, track payments, enforce orders, and maintain comprehensive records of all parties involved in child support cases.

### 2.2 Key Users
- **Intake Workers**: Process new applications
- **Case Workers**: Manage registered cases
- **Supervisors**: Oversight and supervisory functions
- **Administrators**: System administration

### 2.3 Core Entities
- **Case**: Main case entity
- **Custodial Party (CP)**: Parent/guardian with custody
- **Non-Custodial Party (NCP)**: Parent obligated to pay support
- **Child/Children**: Children covered by support orders
- **Court Orders**: Legal orders establishing obligations
- **Payments**: Financial transactions
- **Employers**: NCP/CP employer information

---

## 3. Module Requirements

## 3.1 INTAKE MODULE

### 3.1.1 Overview
The Intake Module handles the initial application process for child support services. Intake workers collect comprehensive information from applicants and create work items for case registration.

### 3.1.2 Key Features

#### Application Entry
- **Paper Application IV-D Entry**
  - Application Type: Walk-in, Mail, Electronic
  - Application Name (alphabetic characters only)
  - Sequential 9-digit application number generation
  - Application status tracking

#### Custodial Party (CP) Information
- Personal Information (First Name, Middle Name, Last Name, Suffix, DOB, SSN/ITIN, Gender, Race)
- Mailing Address and Residential Address
- Contact Information (Home Phone, Business Phone, Cell Phone, Email)
- Alternative Names
- Nearest Relative Information
- Attorney Information
- Employment Information
- Income Information (Type, Source, Frequency, Amount)
- Asset Information
- Benefit Information (TCA/TANF, Medical Assistance)
- Family Violence Indicators

#### Non-Custodial Party (NCP) Information
- Personal Information (including physical characteristics)
- Address Information (Residential, Mailing)
- Alternative Names
- Military Information
- Nearest Relative Information (Mother, Father, Other Relatives)
- Employment Information
- Income and Expense Information
- Asset Information
- Attorney Information
- Incarceration Information
- Citizenship Status
- Driver's License Information

#### Child Information
- Personal Information (Name, DOB, SSN, Gender, Race)
- Birth Information (State, County, City, Country)
- Conception State
- Relationship to Applicant
- Parentage Information
- Existing Order Information
- Support Payment Information

#### Support and Insurance
- Relationship between CP and NCP (Never Married, Separated, Currently Married, Divorced, Unknown)
- Marriage/Divorce Dates and Locations
- Child Support Order Status
- Member Insurance Information (Provider, Policy Number)

#### Service Requests
- Full Service
- Locate Only
- Paternity Only
- Medical Support Only
- Child Support Only
- Child and Spousal Support Only

#### File Upload
- Document Categories and Types
- File size limits (25 MB per file, 250 MB total)
- Supported formats: PDF, Word (.doc, .docx), Images (.jpg, .png, .gif, .bmp)
- Scan functionality

### 3.1.3 User Stories Summary
1. Menu Items and Navigation
2. Intake Search (Application Number, Name, Status, Date Range)
3. CP and NCP Application Entry
4. Support and Insurance Screen
5. Application in Progress/Resume Functionality

### 3.1.4 Data Storage Requirements
- Applications stored in `Intake_Application` table
- Person information in `Person` table (portal schema)
- Employer information in `Person_Employer` table
- Income information in `Person_Income` table
- Asset information in `Asset` table
- Attorney information in `Attorney` table
- Role mapping in `Person_Role_Link` table
- Military information in `Military_Information` table
- Health insurance in `Person_Health_Insurance` table
- Parent relationships in `Parent_Relationship` table

---

## 3.2 CASE REGISTRATION MODULE

### 3.2.1 Overview
Case Registration module processes applications from intake and creates registered cases. Case workers review applications, perform member clearance, and complete case registration.

### 3.2.2 Key Features

#### Home Page/Work Queue
- Search Panel (Case Number, Days Left, Start Date)
- Clear button for search criteria
- Case listing with color-coded indicators:
  - Yellow circle with "I" for Intake cases
  - Red circle with "R" for Referral cases
- Case information display:
  - **Intake Cases**: Work Item ID, Application No, Application Type, Date Received
  - **Referral Cases**: Work Item ID, Referral No, Referral Type, Request Type, Date Received
- Modify Action Dropdown:
  - View Summary
  - Register Cases
  - Return Application
  - View Document
  - No Action Required
  - Resolved
  - Check for Case Composition
  - Link Case

#### Member Clearance (Progressive Stepper)
- **CP Screen**:
  - CP Details (MDM ID, Member ID, Name, DOB, SSN/ITIN, Gender, Race, Match/Criteria)
  - CP SSN History (Member ID, Name, SSN, SSN Type, Verification Status, Source)
  - Enterprise Search Matches (MDM ID, Name, DOB, SSN/ITIN, Gender, Race, CIS ID, Participation)
  - Generate MDM ID button
- **NCP Screen**: Same structure as CP
- **Child Screen**: Same structure as CP
- Navigation: Progressive flow through CP → NCP → Child → Member Status

#### Member Status
- CP, NCP, and Child status information
- Fields: MDM ID, Member ID, Member Type, SSN/ITIN, Name, DOB, Gender, Race
- Family Violence, Protective Order, Domestic Violence indicators
- Previous/Next navigation

#### CP Demographics
- CP Personal Information (County, Nickname, Pregnancy, Maiden Name, Suffix, Relationship to Child)
- Temporary Cash Assistance (TCA) Information
- Medical Assistance (MA) Information
- Communication Preferences (Notification Type, Text/Email Notification, Phone, Email)
- CP Alternative Name
- Mailing Address
- Residential Address
- CP Attorney Information
- CP Nearest Relative Information
- Previous/Next navigation

#### CP Income and Assets
- Income Information (Type, Source, Frequency, Amount)
- Asset Information
- Previous/Next navigation

#### NCP Demographics
- NCP Personal Data (Relationship to Child, Physical Characteristics, Contact Information)
- NCP Alternative Name
- NCP Military Information
- NCP Attorney Information
- NCP Employment Referral Program Information
- Previous/Next navigation

#### NCP Address
- NCP Residential Address
- NCP Mailing Address
- NCP Incarceration Information (Currently/Previously, Institution Details)
- Previous/Next navigation

#### NCP Relative
- NCP Nearest Relationship
- NCP's Mother Information
- NCP's Father Information
- Previous/Next navigation

#### NCP Income and Assets
- NCP Employer Information
- Income Information
- Union Information
- Education Information
- NCP Assets
- Previous/Next navigation

#### Child Information
- Child Data (Member ID, Name, SSN, DOB, Gender, Race, etc.)
- Parentage Information
- Relationship between Mother and Father
- DVR Button
- Previous/Next navigation

#### Member Insurance
- Insurance Information Table (Member ID, Name, SSN, DOB, Gender, Provider, Policy Number)
- Previous/Next navigation

#### Case Status
- Case Information (Case Type, Sub Type, Status, Jurisdiction, Dates, etc.)
- Service Required (Child Support Only, Collection and Disbursement, Enforcement, Full Service, Locate Only, Medical Support Only)
- Good Cause Section
- Previous/Cancel/Done buttons
- Case Registration Confirmation

### 3.2.3 Additional Features
- **Cancel and Resume**: Save draft applications and resume later
- **Auto-Deletion**: Inactive cases deleted after 90 days (with 7-day warning notification)

### 3.2.4 Data Flow
1. Application from Intake → Case Registration Home
2. Member Clearance (CP → NCP → Child)
3. Member Status
4. CP Demographics → CP Income/Assets
5. NCP Demographics → NCP Address → NCP Relative → NCP Income/Assets
6. Child Information → Member Insurance → Case Status
7. Case Registration Complete

---

## 3.3 CASE MANAGEMENT MODULE

### 3.3.1 Overview
Case Management module provides comprehensive case maintenance, viewing, and modification capabilities for registered cases.

### 3.3.2 Key Features

#### Case Information/Main Screen
- Case Details Display:
  - Case Number, Type, Sub Type, Status
  - Assistance Status, Intergovernmental Status
  - Family Violence, Domestic Violence, Protective Order indicators
  - Good Cause status, Arrears Only indicator
- CP and NCP Summary Information
- Editable Case Information Fields
- Intergovernmental Section
- Case Function Table
- Scheduler Section (Appointments)
- Establishment - Court Order Section
- Enforcement Section (Income Withholding Order, National Medical Support Notice)
- Financial Section
- Good Cause Section
- IV-D Cooperation History
- Alert IV-A Agency Section
- Print and Redirect to CSADocGen App buttons
- Cancel/Update buttons

#### View/Modify CP
- **CP Demographics**:
  - CP Data and SSN History
  - CP Personal Information
  - TCA Information
  - MA Information
  - Communication Preferences
  - Alternative Names
  - Addresses (Mailing, Residential, Service)
  - Nearest Relative Information
  - Attorney Information
  - Cancel/Update buttons
- **CP Employer Info**:
  - Employer History Table
  - Employer Information (Self Employed, Employer Details, Address, Income)
  - Income Information Table
  - Add Employer button
  - Cancel/Update buttons

#### View/Modify NCP
- **NCP Demographics**:
  - NCP Data and SSN History
  - NCP Personal Data
  - NCP Military Information
  - NCP Attorney Information
  - NCP Employment Referral Program Information
  - Cancel/Update buttons
- **NCP Employer Information**:
  - Employer History Table
  - Employer Information (with Employer Search button)
  - Income Information
  - Cancel/Print/Update buttons
- **NCP Income and Assets**:
  - Income Information Table (with Add Income Info button)
  - Union Information
  - NCP Assets Table (with Add Asset button)
  - Cancel/Update buttons
- **NCP Relative**:
  - NCP Data and SSN History
  - NCP Nearest Relationship
  - NCP's Mother Information
  - NCP's Father Information
  - Previous/Cancel/Next buttons
- **NCP Address**:
  - NCP Address History Table
  - NCP Address Details (with Add New Address button)
  - Previous/Cancel/Next buttons
- **NCP Incarceration Suspension Summary**:
  - Case Information
  - NCP Active Incarceration Information
  - Suspension of Accrual of Arrears Investigation/Appeal Information
  - Incarceration History Table
  - Add/Edit Incarceration Details button
  - Cancel button

#### View/Modify Child
- Child Data Table
- SSN History
- Child Information Fields (Relationship to CP, Birth Information, Emancipation, Participation Status, Parentage Information)
- Add Child button
- Cancel/DVR/Save buttons
- Edit/Save/Delete buttons

#### View/Modify Member Insurance
- Member Insurance Information Table
- Add New Insurance button
- Print button
- Previous/Next buttons

#### Federal Case Registry
- FCR Query, NDNH Query, FPLS Request buttons
- Transaction Status Table (Type, Action, Locate Info, Member Type, Member ID, Dates, Acknowledgement Code, Batch, Transaction Number)
- Pagination

#### Division of Vital Records (DVR)
- CP Search/NCP Search option
- Search Fields (First Name, Middle Name, Last Name, SSN/ITIN, DOB, Affidavit Number)
- Search Results Display
- Search/Previous/Clear buttons

#### AOP Unmatched Search
- Search Options (Mother, Father, Child, Affidavit Number)
- Affidavit Number field
- Search Results Table
- Search/Clear buttons

#### Billing Suppression
- Financial Information Display
- Billing Suppression Fields (Status, Reason, Other NCP's Case Billing Suppression, Last Update Date)
- Billing Suppression History Table
- Submit/Close buttons

#### Disbursement Hold
- Type of Disbursement Hold dropdown (Case level, Member level, Receipt level)
- Search functionality

#### Close, Suspend, Re-Open
- NCP Details (Incarcerated, Deceased)
- Account Information Table
- Unprocessed Payments Table
- Undistributed Payments Table
- Close/Suspend/Re-Open Action Selection
- Submit button

#### File Upload
- Search by SSN/ITIN/MDM ID/Application Number/Case Number/Member ID
- Case/Member Information Display
- File Upload Fields (Select Category, Select Document Type, Choose File, Scan)
- File size and format restrictions
- Finish button

#### Supervisory Functions
- Supervisory oversight capabilities
- Access control based on role

### 3.3.3 Navigation Structure
- Case Information
- Member Information (View/Modify CP, View/Modify NCP, View/Modify Child, View/Modify Member Insurance)
- Federal Case Registry
- Division of Vital Records
- AOP Unmatched Search
- File Upload
- Supervisory Functions
- Billing Suppression
- Disbursement Hold

---

## 3.4 LOCATE MODULE

### 3.4.1 Overview
The Locate Module enables case workers to search for and locate NCP/CP information from various sources and update case records.

### 3.4.2 Key Features

#### Cases Tab
- Search Functionality:
  - Case Number
  - First Name (CP/NCP)
  - Last Name (CP/NCP)
  - Search and Clear buttons
  - Pagination

#### Case Results
- Case listing based on search criteria
- Case information display

#### NCP/CP Details (Accordion Structure)

##### Locate Summary
- Case Information
- Address Information
- NCP/CP Employer Information
- Change History
- Pagination support

##### Demographics
- Case Information
- NCP/CP Demographics from Sources (with Reset, Update, Enterprise Search, Next buttons)
- NCP/CP SSN from Sources (with Previous, Reset, Enterprise Search, Update, Next buttons)
- Add New section (with Add New button)
- Change History (with pagination)

##### Address
- Case Information
- Address Information
- Address from Sources (with Reset, Save buttons, pagination)
- Add New section (with Add New Address button)
- Change History (with pagination)

##### Employer
- Case Information
- NCP/CP Employer Information
- Employer from Sources (with Reset, Add Employer buttons)
- Add New section (with Add Employer button, Previous, Next buttons)
- Change History (with pagination)

##### Contact
- Case Information
- NCP Contact Information
- Add New section (with Save, Clear buttons)
- Change History (with pagination)

#### File Upload (within Locate)
- Search by Case Number or Application Number
- Case/Application Information Display
- File Upload functionality
- File size and format restrictions (25 MB per file, 250 MB total, PDF/Word/Images)

### 3.4.3 Required Action Tab
- Actions requiring case worker attention
- Task management

### 3.4.4 Data Fields
- All standard person demographics
- Address details (Type, International, Validation status, Source, Dates)
- Employer details (Name, Address, Status, Source, Dates)
- Contact information
- Change history tracking

---

## 3.5 ESTABLISHMENT MODULE

### 3.5.1 Overview
The Establishment Module handles paternity establishment and child support order establishment processes.

### 3.5.2 Key Features

#### Paternity Establishment
- Paternity Status Tracking
- Affidavit of Paternity (AOP) Management
  - AOP Creation and Recording
  - AOP Verification
  - AOP Rescission/Undeclared Status
  - AOP Number and Date Tracking
- Genetic Testing Management
  - Test Request
  - Test Results
  - Test Status Tracking
- Court Order for Paternity
  - Order Number
  - Order Date
  - Establishment State/County/Court

#### Support Order Establishment
- Order Type Management
  - Initial Order
  - Modification Order
  - Temporary Order
- Order Details
  - Court Order Number
  - Court Information (State, County, Court Name)
  - Order Date
  - Effective Date
  - Entered Date
  - Order Status
- Obligation Details
  - Obligation Type (Current Support, Arrears, Medical Support, Child Care)
  - Amount and Frequency
  - Start Date
  - End Date
  - Arrears Calculation
- Support Calculation
  - Income Information
  - Guidelines Application
  - Deviation Reasons
  - Calculation Worksheets

#### Case Workflow Management
- Establishment Case Queue
- Case Assignment
- Task Management
- Timeline Tracking
- Status Updates

#### Document Generation
- Petitions
- Motions
- Orders
- Notices
- Integration with CSADocGen

#### Hearing Management
- Hearing Scheduling
- Hearing Type (Paternity, Support, Modification)
- Hearing Date/Time
- Hearing Outcomes
- Hearing Notes

#### Intergovernmental Establishment
- Interstate Case Handling
- Initiating State Information
- Responding State Information
- UIFSA Compliance
- Case Transmittal

### 3.5.3 Integration Points
- Case Management Module
- Enforcement Module
- Finance Module
- Court Systems
- Document Generation System

---

## 3.6 ENFORCEMENT MODULE

### 3.6.1 Overview
The Enforcement Module manages enforcement actions to collect child support payments and enforce court orders.

### 3.6.2 Key Features

#### Income Withholding Order (IWO) Management
- IWO Creation and Transmission
- IWO Types (Initial, Modification, Termination)
- Employer Information
- Employer Outreach
- IWO Status Tracking
  - Sent Date
  - Received Date
  - Acknowledgment
  - Effective Date
- Payment Processing Integration

#### National Medical Support Notice (NMSN)
- NMSN Creation and Transmission
- Employer Information
- Insurance Provider Information
- NMSN Status Tracking
- Enrollment Status
- Premium Payment Tracking

#### Enforcement Actions
- **License Suspension/Revocation**:
  - Driver's License
  - Professional Licenses
  - Recreational Licenses
  - License Suspension Status
  - Reinstatement Process
- **Passport Denial**:
  - Passport Denial Request
  - Status Tracking
  - Release Process
- **Credit Bureau Reporting**:
  - Arrears Reporting
  - Status Tracking
- **Tax Intercept**:
  - Federal Tax Refund Intercept
  - State Tax Refund Intercept
  - Request and Status Tracking
- **Asset Seizure**:
  - Bank Account Levy
  - Property Lien
  - Asset Seizure Status
- **Contempt of Court**:
  - Contempt Filing
  - Court Date Tracking
  - Outcomes

#### Arrears Management
- Arrears Calculation
- Arrears Balance Tracking
- Payment Application
- Arrears Payment Plans
- Interest Calculation
- Arrears Reduction Strategies

#### Contempt and Court Actions
- Contempt Petitions
- Court Filings
- Court Dates
- Outcomes and Orders
- Warrant Information

#### Case Workflow
- Enforcement Case Queue
- Case Assignment
- Task Management
- Action Timeline
- Status Updates
- Automatic Enforcement Triggers

#### Reporting and Notifications
- NCP Notifications
- CP Notifications
- Employer Notifications
- Court Notifications
- Automated Notices

#### Enforcement History
- Action History
- Payment History
- Court Action History
- Status Change History

### 3.6.3 Integration Points
- Case Management Module
- Finance Module
- Establishment Module
- Employer Systems
- Court Systems
- Federal Systems (FCR, NDNH, FPLS)

---

## 3.7 FINANCE MODULE

### 3.7.1 Overview
The Finance Module manages all financial transactions, payments, receipts, disbursements, and accounting for child support cases.

### 3.7.2 Key Features

#### Payment Receipt
- Payment Source Types:
  - Employer Income Withholding
  - Direct Payment (NCP)
  - Tax Intercept
  - Bank Account Levy
  - Other Sources
- Payment Recording
  - Receipt Number (Auto-generated)
  - Receipt Date
  - Payment Amount
  - Payment Source
  - Payment Method
  - Check Number (if applicable)
- Payment Validation
- Payment Matching

#### Payment Processing
- Payment Application Logic
  - Current Support
  - Arrears
  - Fees
  - Medical Support
  - Child Care
- Payment Allocation Rules
- Payment Distribution

#### Disbursement Management
- Disbursement Types:
  - Current Support Disbursement
  - Arrears Disbursement
  - Fee Disbursement
- Disbursement Processing
  - Disbursement Date
  - Disbursement Amount
  - Disbursement Method (Check, Direct Deposit, EFT, Card)
  - Payee Information
- Disbursement Hold Management
  - Hold Reasons
  - Hold Dates
  - Release Processing
- Disbursement History

#### Account Management
- Account Types:
  - Current Support Account
  - Arrears Account
  - Fee Account
- Account Balance Tracking
- Account Status
- Payment History
- Transaction History

#### Financial Reporting
- Payment Reports
- Disbursement Reports
- Arrears Reports
- Account Balance Reports
- Collection Reports
- Financial Summary Reports
- Federal Reporting (OCSE-34, OCSE-157)

#### State Share and Federal Share
- State Share Calculation
- Federal Share Calculation
- Distribution Logic
- Reporting Requirements

#### URPA (Undistributed Remittance Payment Account)
- URPA Tracking
- URPA Updates
- URPA Distribution
- URPA Reporting

#### Billing and Invoicing
- Billing Suppression Management
- Billing Generation
- Invoice Creation
- Billing History

#### Bank Reconciliation
- Bank Statement Import
- Reconciliation Process
- Discrepancy Resolution
- Reconciliation Reports

#### Fee Management
- Application Fee
- Collection Fee
- Service Fee
- Fee Calculation
- Fee Collection
- Fee Distribution

#### Financial Controls
- Audit Trails
- Transaction Logging
- Approval Workflows
- Security Controls
- Reconciliation Controls

#### Integration with Financial Systems
- State Financial System
- Federal Financial Systems
- Banking Systems
- Payment Processors

### 3.7.3 Data Requirements
- Payment Records
- Disbursement Records
- Account Balances
- Transaction History
- Financial Reports
- Audit Logs

---

## 4. System Architecture

### 4.1 Architecture Overview

The CSMS follows a **multi-tier architecture** with separation of concerns:

```
┌─────────────────────────────────────────────────────────┐
│                    Presentation Layer                    │
│              (Web Application - Frontend)                │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                   Application Layer                      │
│              (REST API - Backend Services)               │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                    Business Logic Layer                  │
│            (Domain Services & Business Rules)            │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                      Data Access Layer                   │
│              (Repository Pattern & ORM)                  │
└──────────────────────┬──────────────────────────────────┘
                       │
┌──────────────────────▼──────────────────────────────────┐
│                      Database Layer                      │
│          (Relational Database - PostgreSQL)              │
└─────────────────────────────────────────────────────────┘
```

### 4.2 Technology Stack Recommendations

#### Frontend
- **Framework**: React.js or Angular
- **State Management**: Redux (React) or NgRx (Angular)
- **UI Framework**: Material-UI, Ant Design, or PrimeNG
- **Build Tool**: Webpack or Vite
- **Package Manager**: npm or yarn

#### Backend
- **Language**: Java (Spring Boot) or .NET Core or Node.js (Express/NestJS)
- **API Framework**: RESTful APIs
- **Authentication**: OAuth 2.0 / JWT
- **API Documentation**: Swagger/OpenAPI

#### Database
- **Primary Database**: PostgreSQL (recommended) or SQL Server
- **ORM**: Hibernate (Java), Entity Framework (.NET), or Sequelize/TypeORM (Node.js)
- **Database Migration**: Flyway, Liquibase, or Entity Framework Migrations

#### Infrastructure
- **Web Server**: Nginx or IIS
- **Application Server**: Tomcat (Java), IIS (.NET), or Node.js
- **Containerization**: Docker
- **Orchestration**: Kubernetes (for production)
- **CI/CD**: Jenkins, GitLab CI, GitHub Actions, or Azure DevOps
- **Version Control**: Git (GitHub/GitLab)

#### Additional Services
- **File Storage**: AWS S3, Azure Blob Storage, or local file system
- **Caching**: Redis or Memcached
- **Message Queue**: RabbitMQ, Azure Service Bus, or Apache Kafka
- **Search**: Elasticsearch (for advanced search)
- **Logging**: ELK Stack (Elasticsearch, Logstash, Kibana) or Application Insights
- **Monitoring**: Prometheus, Grafana, or Application Insights

### 4.3 Deployment Architecture

#### Development Environment
- Single server deployment
- Local database
- Development tools and debuggers

#### Testing Environment
- Staging server
- Test database
- Automated testing tools

#### Production Environment
- **High Availability Setup**:
  - Load balancer (Nginx/HAProxy)
  - Multiple application servers (horizontal scaling)
  - Database replication (Master-Slave)
  - Backup and disaster recovery
- **Security**:
  - HTTPS/TLS encryption
  - Firewall configuration
  - Intrusion detection
  - Regular security audits

### 4.4 API Architecture

#### RESTful API Design
- **Base URL**: `/api/v1/`
- **Resource-based URLs**: `/api/v1/cases`, `/api/v1/persons`, etc.
- **HTTP Methods**: GET, POST, PUT, PATCH, DELETE
- **Status Codes**: Standard HTTP status codes
- **Response Format**: JSON
- **Pagination**: Query parameters (`page`, `pageSize`)
- **Filtering**: Query parameters
- **Sorting**: Query parameters (`sortBy`, `sortOrder`)

#### API Endpoints Structure
```
/api/v1/
  ├── auth/ (Authentication)
  ├── cases/ (Case Management)
  ├── persons/ (Person/Party Management)
  ├── applications/ (Intake Applications)
  ├── orders/ (Court Orders)
  ├── payments/ (Payment Processing)
  ├── disbursements/ (Disbursement Management)
  ├── enforcement/ (Enforcement Actions)
  ├── locate/ (Locate Services)
  ├── establishment/ (Establishment Processes)
  ├── documents/ (Document Management)
  └── reports/ (Reporting)
```

### 4.5 Security Architecture

#### Authentication
- Single Sign-On (SSO) support
- Multi-factor Authentication (MFA)
- Session management
- Password policies

#### Authorization
- Role-Based Access Control (RBAC)
- Permission-based access
- Resource-level permissions

#### Data Security
- Encryption at rest
- Encryption in transit (TLS/SSL)
- PII data masking
- Audit logging
- Data backup and recovery

---

## 5. Database Design

### 5.1 Database Schema Organization

The database should be organized into multiple schemas for better organization:

- **`portal`**: Intake and application data
- **`case_mgmt`**: Case management data
- **`financial`**: Financial transactions
- **`enforcement`**: Enforcement actions
- **`establishment`**: Establishment processes
- **`locate`**: Locate information
- **`reference`**: Reference/lookup data
- **`audit`**: Audit logs
- **`security`**: Security and user management

### 5.2 Core Entity Relationship Model

```
┌─────────────┐
│    Case     │
└──────┬──────┘
       │
       ├──────────────┬──────────────┐
       │              │              │
┌──────▼──────┐ ┌─────▼─────┐ ┌─────▼─────┐
│     CP      │ │    NCP    │ │   Child   │
│  (Person)   │ │ (Person)  │ │  (Person) │
└──────┬──────┘ └─────┬─────┘ └─────┬─────┘
       │              │              │
       │              │              │
┌──────▼──────────────▼──────────────▼──────┐
│           Person_Role_Link                │
└───────────────────────────────────────────┘
```

### 5.3 Database Tables

#### 5.3.1 Core Tables (portal schema)

##### Case Tables
```sql
-- Case Table
CREATE TABLE portal.case (
    case_id BIGSERIAL PRIMARY KEY,
    case_number VARCHAR(50) UNIQUE NOT NULL,
    case_type VARCHAR(50),
    case_sub_type VARCHAR(50),
    case_status VARCHAR(50),
    case_status_date DATE,
    case_jurisdiction VARCHAR(100),
    assistance_status VARCHAR(50),
    intergovernmental_status VARCHAR(50),
    application_fee_status VARCHAR(50),
    application_completion_date DATE,
    case_registration_date DATE,
    family_violence_indicator BOOLEAN,
    domestic_violence_indicator BOOLEAN,
    protective_order_indicator BOOLEAN,
    good_cause_indicator BOOLEAN,
    good_cause_status VARCHAR(50),
    good_cause_status_date DATE,
    good_cause_reason VARCHAR(255),
    iv_d_cooperation_status VARCHAR(50),
    iv_d_cooperation_date DATE,
    assignment_of_rights BOOLEAN,
    service_required VARCHAR(100),
    application_mode VARCHAR(50),
    ncp_unknown BOOLEAN,
    intent_to_close VARCHAR(50),
    intent_to_close_date DATE,
    automated_closing_eligibility_date DATE,
    arrears_only_indicator BOOLEAN,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Case Function Table
CREATE TABLE portal.case_function (
    case_function_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    function_type VARCHAR(100),
    start_date DATE,
    end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);
```

##### Person Tables
```sql
-- Person Table (Master Person Record)
CREATE TABLE portal.person (
    person_id BIGSERIAL PRIMARY KEY,
    mdm_id VARCHAR(50) UNIQUE,
    member_id VARCHAR(50),
    ssn VARCHAR(11),
    itin VARCHAR(11),
    first_name VARCHAR(100),
    middle_name VARCHAR(100),
    last_name VARCHAR(100),
    suffix VARCHAR(20),
    date_of_birth DATE,
    gender VARCHAR(20),
    race VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person Role Link Table
CREATE TABLE portal.person_role_link (
    person_role_link_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    case_id BIGINT REFERENCES portal.case(case_id),
    role_type VARCHAR(20) NOT NULL, -- CP, NCP, CHILD
    relationship_to_child VARCHAR(100),
    case_association VARCHAR(100),
    start_date DATE,
    end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person SSN History
CREATE TABLE portal.person_ssn_history (
    ssn_history_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    ssn VARCHAR(11),
    ssn_type VARCHAR(20), -- SSN, ITIN
    verification_status VARCHAR(50),
    verification_source VARCHAR(100),
    effective_date DATE,
    end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Person Address
CREATE TABLE portal.person_address (
    address_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    address_type VARCHAR(50), -- MAILING, RESIDENTIAL, SERVICE
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(50),
    county VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100),
    international_address BOOLEAN DEFAULT FALSE,
    address_validated BOOLEAN,
    address_manually_verified BOOLEAN,
    source VARCHAR(100),
    date_at_address DATE,
    verified_date DATE,
    start_date DATE,
    end_date DATE,
    is_current BOOLEAN DEFAULT TRUE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Person Contact
CREATE TABLE portal.person_contact (
    contact_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    contact_type VARCHAR(50), -- HOME_PHONE, BUSINESS_PHONE, CELL_PHONE, EMAIL
    contact_value VARCHAR(255),
    notification_preference VARCHAR(50), -- PAPER, PAPERLESS
    text_notification BOOLEAN,
    email_notification BOOLEAN,
    is_primary BOOLEAN DEFAULT FALSE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person Employer
CREATE TABLE portal.person_employer (
    employer_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    employer_name VARCHAR(255),
    employer_type VARCHAR(100),
    phone VARCHAR(20),
    email VARCHAR(255),
    fax VARCHAR(20),
    fein VARCHAR(50),
    sein VARCHAR(50),
    employer_sponsored_insurance BOOLEAN,
    occupation VARCHAR(100),
    self_employed BOOLEAN DEFAULT FALSE,
    verification_indicator BOOLEAN,
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(50),
    county VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100),
    international_address BOOLEAN DEFAULT FALSE,
    address_validated BOOLEAN,
    start_date DATE,
    end_date DATE,
    income_amount DECIMAL(18,2),
    income_frequency VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person Income
CREATE TABLE portal.person_income (
    income_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    income_type VARCHAR(100),
    income_source VARCHAR(255),
    income_frequency VARCHAR(50),
    income_amount DECIMAL(18,2),
    start_date DATE,
    end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person Asset
CREATE TABLE portal.asset (
    asset_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    asset_type VARCHAR(100),
    asset_description VARCHAR(255),
    asset_value DECIMAL(18,2),
    ownership_percentage DECIMAL(5,2),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Person Health Insurance
CREATE TABLE portal.person_health_insurance (
    insurance_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    provider_name VARCHAR(255),
    policy_number VARCHAR(100),
    group_number VARCHAR(100),
    start_date DATE,
    end_date DATE,
    is_current BOOLEAN DEFAULT TRUE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Attorney
CREATE TABLE portal.attorney (
    attorney_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id), -- CP or NCP
    attorney_type VARCHAR(20), -- CP_ATTORNEY, NCP_ATTORNEY
    first_name VARCHAR(100),
    middle_name VARCHAR(100),
    last_name VARCHAR(100),
    suffix VARCHAR(20),
    phone VARCHAR(20),
    email VARCHAR(255),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(50),
    county VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100),
    international_address BOOLEAN DEFAULT FALSE,
    address_validated BOOLEAN,
    source VARCHAR(100),
    start_date DATE,
    end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Military Information
CREATE TABLE portal.military_information (
    military_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    military_status VARCHAR(50),
    military_branch VARCHAR(100),
    military_service_number VARCHAR(100),
    entry_date DATE,
    discharge_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Person Alternative Name
CREATE TABLE portal.person_alternative_name (
    alternative_name_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    first_name VARCHAR(100),
    middle_name VARCHAR(100),
    last_name VARCHAR(100),
    suffix VARCHAR(20),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Person Relative
CREATE TABLE portal.person_relative (
    relative_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    relative_type VARCHAR(50), -- NEAREST_RELATIVE, MOTHER, FATHER, OTHER
    first_name VARCHAR(100),
    middle_name VARCHAR(100),
    last_name VARCHAR(100),
    relationship VARCHAR(100),
    phone VARCHAR(20),
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(50),
    county VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100),
    international_address BOOLEAN DEFAULT FALSE,
    address_validated BOOLEAN,
    source VARCHAR(100),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Incarceration Information
CREATE TABLE portal.incarceration (
    incarceration_id BIGSERIAL PRIMARY KEY,
    person_id BIGINT REFERENCES portal.person(person_id),
    currently_incarcerated BOOLEAN,
    previously_incarcerated BOOLEAN,
    work_release BOOLEAN,
    verification_indicator BOOLEAN,
    prisoner_id VARCHAR(100),
    institution_type VARCHAR(100),
    institution_name VARCHAR(255),
    admission_date DATE,
    projected_release_date DATE,
    release_date DATE,
    address_line1 VARCHAR(255),
    address_line2 VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(50),
    county VARCHAR(100),
    zip_code VARCHAR(20),
    country VARCHAR(100),
    international_address BOOLEAN DEFAULT FALSE,
    address_validated BOOLEAN,
    source VARCHAR(100),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);
```

##### Intake Tables
```sql
-- Intake Application
CREATE TABLE portal.intake_application (
    application_id BIGSERIAL PRIMARY KEY,
    application_number VARCHAR(50) UNIQUE NOT NULL,
    application_name VARCHAR(255),
    application_type VARCHAR(50), -- WALK_IN, MAIL, ELECTRONIC
    application_status VARCHAR(50),
    date_received DATE,
    service_fee_paid BOOLEAN,
    service_fee_amount DECIMAL(10,2),
    submitted_date TIMESTAMP,
    assigned_to VARCHAR(100),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Application Member Link
CREATE TABLE portal.application_member_link (
    application_member_link_id BIGSERIAL PRIMARY KEY,
    application_id BIGINT REFERENCES portal.intake_application(application_id),
    person_id BIGINT REFERENCES portal.person(person_id),
    member_type VARCHAR(20), -- CP, NCP, CHILD
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Work Item
CREATE TABLE portal.work_item (
    work_item_id BIGSERIAL PRIMARY KEY,
    work_item_number VARCHAR(50) UNIQUE NOT NULL,
    application_id BIGINT REFERENCES portal.intake_application(application_id),
    work_item_type VARCHAR(50), -- INTAKE, REFERRAL
    work_item_status VARCHAR(50),
    date_received DATE,
    days_left INTEGER,
    assigned_to VARCHAR(100),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);
```

##### Child Specific Tables
```sql
-- Child Information
CREATE TABLE portal.child_information (
    child_info_id BIGSERIAL PRIMARY KEY,
    child_person_id BIGINT REFERENCES portal.person(person_id),
    case_id BIGINT REFERENCES portal.case(case_id),
    relationship_to_cp VARCHAR(100),
    state_conceived VARCHAR(50),
    birth_city VARCHAR(100),
    birth_county VARCHAR(100),
    birth_state VARCHAR(50),
    birth_country VARCHAR(100),
    emancipation_date DATE,
    emancipation_notice_sent_to_cp DATE,
    emancipation_notice_sent_to_ncp DATE,
    out_of_home_indicator BOOLEAN,
    out_of_home_date DATE,
    participation_status VARCHAR(50),
    participation_start_date DATE,
    ssi_indicator BOOLEAN,
    school_enrollment_form_verified BOOLEAN,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Parent Relationship
CREATE TABLE portal.parent_relationship (
    parent_relationship_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    cp_person_id BIGINT REFERENCES portal.person(person_id),
    ncp_person_id BIGINT REFERENCES portal.person(person_id),
    relationship_status VARCHAR(50), -- NEVER_MARRIED, SEPARATED, CURRENTLY_MARRIED, DIVORCED, UNKNOWN
    date_married DATE,
    date_separated DATE,
    date_divorced DATE,
    country_married VARCHAR(100),
    state_married VARCHAR(50),
    county_married VARCHAR(100),
    country_separated VARCHAR(100),
    state_separated VARCHAR(50),
    county_separated VARCHAR(100),
    country_divorced VARCHAR(100),
    state_divorced VARCHAR(50),
    county_divorced VARCHAR(100),
    divorce_proceedings_pending BOOLEAN,
    child_support_included BOOLEAN,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Parentage Information
CREATE TABLE portal.parentage_information (
    parentage_id BIGSERIAL PRIMARY KEY,
    child_person_id BIGINT REFERENCES portal.person(person_id),
    case_id BIGINT REFERENCES portal.case(case_id),
    parentage_status VARCHAR(50), -- ESTABLISHED, REQUIRES_ESTABLISHMENT
    established_date DATE,
    establishment_country VARCHAR(100),
    establishment_state VARCHAR(50),
    establishment_county VARCHAR(100),
    establishment_method VARCHAR(100), -- COURT_ORDER, AFFIDAVIT
    affidavit_available BOOLEAN,
    affidavit_number VARCHAR(100),
    affidavit_date DATE,
    affidavit_rescinded BOOLEAN,
    affidavit_undeclared BOOLEAN,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);
```

#### 5.3.2 Financial Tables (financial schema)

```sql
-- Payment Receipt
CREATE TABLE financial.payment_receipt (
    receipt_id BIGSERIAL PRIMARY KEY,
    receipt_number VARCHAR(50) UNIQUE NOT NULL,
    case_id BIGINT REFERENCES portal.case(case_id),
    ncp_person_id BIGINT REFERENCES portal.person(person_id),
    receipt_date DATE NOT NULL,
    payment_amount DECIMAL(18,2) NOT NULL,
    payment_source VARCHAR(100), -- EMPLOYER, DIRECT, TAX_INTERCEPT, BANK_LEVY
    payment_method VARCHAR(50), -- CHECK, EFT, CASH
    check_number VARCHAR(50),
    applied_amount DECIMAL(18,2),
    distributed_amount DECIMAL(18,2),
    distributed_date DATE,
    payment_status VARCHAR(50),
    disbursement_method VARCHAR(50),
    bank_reconciliation_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Disbursement
CREATE TABLE financial.disbursement (
    disbursement_id BIGSERIAL PRIMARY KEY,
    disbursement_number VARCHAR(50) UNIQUE NOT NULL,
    case_id BIGINT REFERENCES portal.case(case_id),
    cp_person_id BIGINT REFERENCES portal.person(person_id),
    receipt_id BIGINT REFERENCES financial.payment_receipt(receipt_id),
    disbursement_type VARCHAR(50), -- CURRENT_SUPPORT, ARREARS, FEE
    disbursement_date DATE NOT NULL,
    disbursement_amount DECIMAL(18,2) NOT NULL,
    disbursement_method VARCHAR(50), -- CHECK, DIRECT_DEPOSIT, EFT, CARD
    payee_name VARCHAR(255),
    payee_address VARCHAR(255),
    account_number VARCHAR(100),
    routing_number VARCHAR(100),
    disbursement_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Account
CREATE TABLE financial.account (
    account_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    account_type VARCHAR(50), -- CURRENT_SUPPORT, ARREARS, FEE
    account_status VARCHAR(50),
    payment_frequency VARCHAR(50),
    account_balance DECIMAL(18,2) DEFAULT 0,
    last_payment_amount DECIMAL(18,2),
    last_payment_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Payment Application
CREATE TABLE financial.payment_application (
    payment_application_id BIGSERIAL PRIMARY KEY,
    receipt_id BIGINT REFERENCES financial.payment_receipt(receipt_id),
    account_id BIGINT REFERENCES financial.account(account_id),
    applied_amount DECIMAL(18,2) NOT NULL,
    application_date DATE NOT NULL,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Disbursement Hold
CREATE TABLE financial.disbursement_hold (
    disbursement_hold_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    person_id BIGINT REFERENCES portal.person(person_id),
    receipt_id BIGINT REFERENCES financial.payment_receipt(receipt_id),
    hold_type VARCHAR(50), -- CASE_LEVEL, MEMBER_LEVEL, RECEIPT_LEVEL
    hold_reason VARCHAR(255),
    hold_start_date DATE,
    hold_end_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Billing Suppression
CREATE TABLE financial.billing_suppression (
    billing_suppression_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    court_order_id BIGINT,
    billing_suppression_status VARCHAR(50),
    reason VARCHAR(255),
    other_ncp_case_billing_suppression BOOLEAN,
    start_date DATE,
    end_date DATE,
    last_update_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- URPA (Undistributed Remittance Payment Account)
CREATE TABLE financial.urpa (
    urpa_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    total_urpa DECIMAL(18,2),
    urpa_update_date DATE,
    au_number VARCHAR(50),
    case_identifier_id VARCHAR(50),
    program_id VARCHAR(50),
    monthly_grant_amount DECIMAL(18,2),
    source VARCHAR(100),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);
```

#### 5.3.3 Establishment Tables (establishment schema)

```sql
-- Court Order
CREATE TABLE establishment.court_order (
    court_order_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    court_order_number VARCHAR(100) UNIQUE NOT NULL,
    court_order_type VARCHAR(100), -- PATERNITY, SUPPORT, MODIFICATION
    obligation_type VARCHAR(100), -- CURRENT_SUPPORT, ARREARS, MEDICAL_SUPPORT
    court_name VARCHAR(255),
    court_state VARCHAR(50),
    court_county VARCHAR(100),
    court_order_date DATE,
    effective_date DATE,
    entered_date DATE,
    court_order_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Obligation
CREATE TABLE establishment.obligation (
    obligation_id BIGSERIAL PRIMARY KEY,
    court_order_id BIGINT REFERENCES establishment.court_order(court_order_id),
    case_id BIGINT REFERENCES portal.case(case_id),
    obligation_type VARCHAR(100),
    obligation_amount DECIMAL(18,2),
    frequency VARCHAR(50), -- WEEKLY, BIWEEKLY, MONTHLY
    start_date DATE,
    end_date DATE,
    arrears_amount DECIMAL(18,2),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Affidavit of Paternity
CREATE TABLE establishment.affidavit_of_paternity (
    affidavit_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    child_person_id BIGINT REFERENCES portal.person(person_id),
    ncp_person_id BIGINT REFERENCES portal.person(person_id),
    cp_person_id BIGINT REFERENCES portal.person(person_id),
    affidavit_number VARCHAR(100) UNIQUE,
    affidavit_date DATE,
    affidavit_status VARCHAR(50), -- ACTIVE, RESCINDED, UNDECLARED
    rescinded_date DATE,
    undeclared_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Genetic Test
CREATE TABLE establishment.genetic_test (
    genetic_test_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    child_person_id BIGINT REFERENCES portal.person(person_id),
    ncp_person_id BIGINT REFERENCES portal.person(person_id),
    test_request_date DATE,
    test_date DATE,
    test_results VARCHAR(50), -- POSITIVE, NEGATIVE, INCONCLUSIVE
    test_status VARCHAR(50),
    lab_name VARCHAR(255),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);

-- Hearing
CREATE TABLE establishment.hearing (
    hearing_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    hearing_type VARCHAR(100), -- PATERNITY, SUPPORT, MODIFICATION
    hearing_date DATE,
    hearing_time TIME,
    court_name VARCHAR(255),
    hearing_outcome VARCHAR(100),
    hearing_notes TEXT,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);
```

#### 5.3.4 Enforcement Tables (enforcement schema)

```sql
-- Income Withholding Order
CREATE TABLE enforcement.income_withholding_order (
    iwo_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    court_order_id BIGINT REFERENCES establishment.court_order(court_order_id),
    employer_id BIGINT REFERENCES portal.person_employer(employer_id),
    iwo_type VARCHAR(50), -- INITIAL, MODIFICATION, TERMINATION
    notice_type VARCHAR(100),
    iwo_number VARCHAR(100),
    sent_date DATE,
    received_date DATE,
    acknowledgment_code VARCHAR(50),
    acknowledgment_date DATE,
    effective_date DATE,
    iwo_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- National Medical Support Notice
CREATE TABLE enforcement.national_medical_support_notice (
    nmsn_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    court_order_id BIGINT REFERENCES establishment.court_order(court_order_id),
    employer_id BIGINT REFERENCES portal.person_employer(employer_id),
    nmsn_number VARCHAR(100),
    sent_date DATE,
    received_date DATE,
    enrollment_status VARCHAR(50),
    nmsn_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Enforcement Action
CREATE TABLE enforcement.enforcement_action (
    enforcement_action_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    action_type VARCHAR(100), -- LICENSE_SUSPENSION, PASSPORT_DENIAL, TAX_INTERCEPT, BANK_LEVY, CONTEMPT
    action_status VARCHAR(50),
    action_date DATE,
    action_details TEXT,
    outcome VARCHAR(255),
    outcome_date DATE,
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- License Suspension
CREATE TABLE enforcement.license_suspension (
    license_suspension_id BIGSERIAL PRIMARY KEY,
    enforcement_action_id BIGINT REFERENCES enforcement.enforcement_action(enforcement_action_id),
    person_id BIGINT REFERENCES portal.person(person_id),
    license_type VARCHAR(100), -- DRIVERS, PROFESSIONAL, RECREATIONAL
    license_number VARCHAR(100),
    license_state VARCHAR(50),
    suspension_date DATE,
    reinstatement_date DATE,
    suspension_status VARCHAR(50),
    created_by VARCHAR(100),
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_by VARCHAR(100),
    updated_date TIMESTAMP
);
```

#### 5.3.5 Document Management Tables

```sql
-- Document
CREATE TABLE portal.document (
    document_id BIGSERIAL PRIMARY KEY,
    case_id BIGINT REFERENCES portal.case(case_id),
    application_id BIGINT REFERENCES portal.intake_application(application_id),
    person_id BIGINT REFERENCES portal.person(person_id),
    document_category VARCHAR(100),
    document_type VARCHAR(100),
    document_subtype VARCHAR(100),
    document_name VARCHAR(255),
    file_path VARCHAR(500),
    file_size BIGINT,
    file_type VARCHAR(50),
    uploaded_by VARCHAR(100),
    uploaded_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);
```

#### 5.3.6 Reference/Lookup Tables (reference schema)

```sql
-- Reference Data Tables
CREATE TABLE reference.case_type (
    case_type_code VARCHAR(50) PRIMARY KEY,
    case_type_name VARCHAR(255),
    description TEXT,
    is_active BOOLEAN DEFAULT TRUE
);

CREATE TABLE reference.case_status (
    case_status_code VARCHAR(50) PRIMARY KEY,
    case_status_name VARCHAR(255),
    description TEXT,
    is_active BOOLEAN DEFAULT TRUE
);

CREATE TABLE reference.state (
    state_code VARCHAR(10) PRIMARY KEY,
    state_name VARCHAR(100),
    is_active BOOLEAN DEFAULT TRUE
);

CREATE TABLE reference.county (
    county_id BIGSERIAL PRIMARY KEY,
    state_code VARCHAR(10) REFERENCES reference.state(state_code),
    county_code VARCHAR(20),
    county_name VARCHAR(100),
    is_active BOOLEAN DEFAULT TRUE
);

-- Add more reference tables as needed
```

#### 5.3.7 Security and Audit Tables (security schema)

```sql
-- User
CREATE TABLE security.app_user (
    user_id BIGSERIAL PRIMARY KEY,
    username VARCHAR(100) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255),
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    is_active BOOLEAN DEFAULT TRUE,
    created_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_date TIMESTAMP
);

-- Role
CREATE TABLE security.role (
    role_id BIGSERIAL PRIMARY KEY,
    role_name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    is_active BOOLEAN DEFAULT TRUE
);

-- User Role
CREATE TABLE security.user_role (
    user_role_id BIGSERIAL PRIMARY KEY,
    user_id BIGINT REFERENCES security.app_user(user_id),
    role_id BIGINT REFERENCES security.role(role_id),
    assigned_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE
);

-- Permission
CREATE TABLE security.permission (
    permission_id BIGSERIAL PRIMARY KEY,
    permission_name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    resource VARCHAR(100),
    action VARCHAR(50)
);

-- Role Permission
CREATE TABLE security.role_permission (
    role_permission_id BIGSERIAL PRIMARY KEY,
    role_id BIGINT REFERENCES security.role(role_id),
    permission_id BIGINT REFERENCES security.permission(permission_id),
    is_active BOOLEAN DEFAULT TRUE
);
```

#### 5.3.8 Audit Tables (audit schema)

```sql
-- Audit Log
CREATE TABLE audit.audit_log (
    audit_log_id BIGSERIAL PRIMARY KEY,
    table_name VARCHAR(100),
    record_id BIGINT,
    action_type VARCHAR(20), -- INSERT, UPDATE, DELETE
    old_values JSONB,
    new_values JSONB,
    changed_by VARCHAR(100),
    changed_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ip_address VARCHAR(50),
    user_agent VARCHAR(255)
);
```

### 5.4 Indexes

Key indexes should be created for performance:

```sql
-- Case indexes
CREATE INDEX idx_case_case_number ON portal.case(case_number);
CREATE INDEX idx_case_case_status ON portal.case(case_status);
CREATE INDEX idx_case_case_type ON portal.case(case_type);

-- Person indexes
CREATE INDEX idx_person_mdm_id ON portal.person(mdm_id);
CREATE INDEX idx_person_ssn ON portal.person(ssn);
CREATE INDEX idx_person_member_id ON portal.person(member_id);
CREATE INDEX idx_person_last_name_first_name ON portal.person(last_name, first_name);

-- Person Role Link indexes
CREATE INDEX idx_person_role_link_case_id ON portal.person_role_link(case_id);
CREATE INDEX idx_person_role_link_person_id ON portal.person_role_link(person_id);
CREATE INDEX idx_person_role_link_role_type ON portal.person_role_link(role_type);

-- Application indexes
CREATE INDEX idx_intake_application_number ON portal.intake_application(application_number);
CREATE INDEX idx_intake_application_status ON portal.intake_application(application_status);

-- Financial indexes
CREATE INDEX idx_payment_receipt_case_id ON financial.payment_receipt(case_id);
CREATE INDEX idx_payment_receipt_receipt_number ON financial.payment_receipt(receipt_number);
CREATE INDEX idx_payment_receipt_receipt_date ON financial.payment_receipt(receipt_date);
CREATE INDEX idx_disbursement_case_id ON financial.disbursement(case_id);
CREATE INDEX idx_account_case_id ON financial.account(case_id);
```

### 5.5 Database Naming Conventions

- Table names: `snake_case`, singular or plural as appropriate
- Column names: `snake_case`
- Primary keys: `{table_name}_id`
- Foreign keys: `{referenced_table}_id`
- Boolean columns: descriptive names ending with indicator/flag (e.g., `is_active`, `family_violence_indicator`)
- Date columns: descriptive names ending with `_date`
- Timestamp columns: `created_date`, `updated_date`, `changed_date`
- User tracking: `created_by`, `updated_by`, `changed_by`

---

## 6. Technical Specifications

### 6.1 Development Standards

#### Code Organization
- **Layered Architecture**: Presentation, Application, Business Logic, Data Access
- **Separation of Concerns**: Each layer handles specific responsibilities
- **SOLID Principles**: Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, Dependency Inversion
- **Design Patterns**: Repository Pattern, Service Pattern, Factory Pattern, Strategy Pattern

#### Coding Standards
- **Naming Conventions**: 
  - Classes: PascalCase
  - Methods/Variables: camelCase
  - Constants: UPPER_SNAKE_CASE
  - Database: snake_case
- **Documentation**: Code comments, API documentation, README files
- **Error Handling**: Comprehensive exception handling, logging
- **Validation**: Input validation at multiple layers
- **Testing**: Unit tests, integration tests, end-to-end tests

### 6.2 API Design Standards

#### RESTful API Guidelines
- Use nouns for resources, not verbs
- Use HTTP methods appropriately (GET, POST, PUT, PATCH, DELETE)
- Use HTTP status codes correctly
- Version APIs (e.g., `/api/v1/`)
- Use consistent response formats
- Implement pagination for list endpoints
- Support filtering and sorting
- Document APIs with Swagger/OpenAPI

#### API Response Format
```json
{
  "success": true,
  "data": {},
  "message": "Operation successful",
  "errors": [],
  "pagination": {
    "page": 1,
    "pageSize": 20,
    "totalPages": 10,
    "totalRecords": 200
  }
}
```

#### Error Response Format
```json
{
  "success": false,
  "data": null,
  "message": "Validation failed",
  "errors": [
    {
      "field": "ssn",
      "message": "SSN is required"
    }
  ]
}
```

### 6.3 Security Requirements

#### Authentication
- JWT (JSON Web Tokens) for API authentication
- Token expiration and refresh mechanisms
- Password policies (minimum length, complexity requirements)
- Account lockout after failed attempts
- Multi-factor authentication (optional but recommended)

#### Authorization
- Role-Based Access Control (RBAC)
- Resource-level permissions
- API endpoint protection
- UI element visibility based on permissions

#### Data Protection
- Encryption of sensitive data at rest
- TLS/SSL for data in transit
- PII data masking in logs and UI
- Secure password storage (hashing with salt)
- SQL injection prevention (parameterized queries)
- XSS prevention (input sanitization)
- CSRF protection

#### Audit and Compliance
- Comprehensive audit logging
- User activity tracking
- Data access logging
- Compliance with state and federal regulations
- Data retention policies

### 6.4 Performance Requirements

#### Response Times
- Page load: < 3 seconds
- API response: < 1 second (95th percentile)
- Search operations: < 2 seconds
- Report generation: < 30 seconds (depending on complexity)

#### Scalability
- Support for 1000+ concurrent users
- Horizontal scaling capability
- Database query optimization
- Caching strategy (Redis/Memcached)
- Database connection pooling

#### Database Performance
- Index optimization
- Query optimization
- Database partitioning (if needed for large tables)
- Regular database maintenance

### 6.5 Testing Requirements

#### Unit Testing
- Code coverage target: 80%+
- Test all business logic
- Mock external dependencies
- Use testing frameworks (JUnit, NUnit, Jest, etc.)

#### Integration Testing
- API endpoint testing
- Database integration testing
- External service integration testing
- End-to-end workflow testing

#### User Acceptance Testing (UAT)
- Test all user stories
- Test all acceptance criteria
- User workflow testing
- Performance testing
- Security testing

### 6.6 Deployment Requirements

#### Environment Setup
- Development environment
- Testing/QA environment
- Staging environment
- Production environment

#### Deployment Process
- Automated builds
- Automated testing
- Automated deployment (CI/CD)
- Rollback procedures
- Deployment documentation

#### Monitoring and Logging
- Application logging
- Error tracking
- Performance monitoring
- User activity monitoring
- Database monitoring
- Server monitoring

---

## 7. Security and Compliance

### 7.1 Data Privacy
- PII (Personally Identifiable Information) protection
- HIPAA compliance (if applicable)
- State and federal data privacy regulations
- Data minimization principles
- Consent management

### 7.2 Access Control
- User authentication
- Role-based access control
- Permission management
- Session management
- Audit trails

### 7.3 Data Security
- Encryption standards
- Secure data transmission
- Secure data storage
- Backup and recovery procedures
- Disaster recovery plan

### 7.4 Compliance
- Federal child support regulations (OCSE)
- State-specific regulations
- Court order compliance
- Reporting requirements
- Audit requirements

---

## 8. Integration Requirements

### 8.1 External Systems

#### Federal Systems
- **FCR (Federal Case Registry)**: Case and order registration
- **NDNH (National Directory of New Hires)**: Employment information
- **FPLS (Federal Parent Locator Service)**: Locate services
- **OCSE Systems**: Federal reporting and compliance

#### State Systems
- **State Financial System**: Payment and disbursement processing
- **Court Systems**: Court order integration
- **Vital Records**: Birth certificate and paternity records
- **DMV**: License suspension/revocation
- **State Tax**: Tax intercept processing

#### Other Systems
- **Employer Systems**: Income withholding
- **Banking Systems**: Payment processing
- **Credit Bureaus**: Credit reporting
- **Document Generation**: CSADocGen integration

### 8.2 Integration Methods
- RESTful APIs
- SOAP Web Services (if required)
- File transfers (SFTP, secure file transfer)
- Database connections (if applicable)
- Message queues

### 8.3 Data Exchange
- Data mapping and transformation
- Error handling and retry logic
- Data validation
- Audit logging of data exchanges
- Real-time vs. batch processing

---

## 9. Implementation Roadmap

### Phase 1: Foundation (Months 1-3)
- Database setup and schema creation
- Authentication and authorization
- Basic UI framework
- Core API structure
- Development environment setup

### Phase 2: Intake Module (Months 4-6)
- Intake application entry
- CP/NCP/Child information capture
- File upload functionality
- Application search and management

### Phase 3: Case Registration (Months 7-9)
- Member clearance workflow
- Case registration process
- Case status management
- Integration with Intake

### Phase 4: Case Management (Months 10-12)
- Case viewing and modification
- CP/NCP/Child management
- Document management
- Basic reporting

### Phase 5: Locate Module (Months 13-14)
- Locate functionality
- Enterprise search integration
- Address and employer updates

### Phase 6: Establishment Module (Months 15-17)
- Paternity establishment
- Support order establishment
- Court order management
- Document generation integration

### Phase 7: Enforcement Module (Months 18-20)
- Income withholding orders
- Enforcement actions
- License suspension
- Tax intercept

### Phase 8: Finance Module (Months 21-24)
- Payment processing
- Disbursement management
- Account management
- Financial reporting
- Integration with state financial systems

### Phase 9: Testing and Deployment (Months 25-27)
- Comprehensive testing
- Performance optimization
- Security audits
- User training
- Production deployment

---

## 10. Appendices

### 10.1 Glossary
- **CP**: Custodial Party
- **NCP**: Non-Custodial Party
- **IV-D**: Title IV-D of the Social Security Act (Child Support Program)
- **MDM ID**: Master Data Management ID
- **IRN**: Individual Reference Number
- **AOP**: Affidavit of Paternity
- **IWO**: Income Withholding Order
- **NMSN**: National Medical Support Notice
- **FCR**: Federal Case Registry
- **NDNH**: National Directory of New Hires
- **FPLS**: Federal Parent Locator Service
- **URPA**: Undistributed Remittance Payment Account
- **TCA/TANF**: Temporary Cash Assistance/Temporary Assistance for Needy Families
- **MA**: Medical Assistance

### 10.2 References
- OCSE (Office of Child Support Enforcement) regulations
- State-specific child support regulations
- Federal Case Registry specifications
- UIFSA (Uniform Interstate Family Support Act)

### 10.3 Change Log
- Document version tracking
- Requirement changes
- Updates and modifications

---

## Document Control

**Version**: 1.0  
**Date**: 2024  
**Status**: Draft  
**Author**: System Requirements Team  
**Reviewers**: [To be assigned]  
**Approvers**: [To be assigned]

---

*This document provides comprehensive requirements for building a complete Child Support Management System. It should be used as a reference throughout the development lifecycle.*
