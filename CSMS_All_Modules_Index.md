# Child Support Management System (CSMS) - All Modules Index

## Overview
This index provides links to all module requirement documents for the Child Support Management System. Each module has been documented separately with detailed user stories and acceptance criteria for developer implementation.

---

## Document Structure

### Main Requirements Documents

1. **CSMS_Developer_Requirements_with_Acceptance_Criteria.md**
   - Contains: **INTAKE MODULE** (Complete) and **CASE REGISTRATION MODULE** (Complete)
   - Format: Detailed user stories with acceptance criteria
   - Status: ✅ Complete with all acceptance criteria

2. **CSMS_Module_3_Case_Management_Requirements.md**
   - Contains: **CASE MANAGEMENT MODULE**
   - Format: User stories with acceptance criteria
   - Status: 🔄 In Progress (Main screen/view case details included)

3. **CSMS_Module_4_Locate_Requirements.md**
   - Contains: **LOCATE MODULE**
   - Format: User stories with acceptance criteria
   - Status: ✅ Complete

4. **CSMS_Module_5_Establishment_Requirements.md**
   - Contains: **ESTABLISHMENT MODULE** (Paternity and Support Order Establishment)
   - Format: User stories with acceptance criteria
   - Status: ✅ High-level requirements complete

5. **CSMS_Module_6_Enforcement_Requirements.md**
   - Contains: **ENFORCEMENT MODULE**
   - Format: User stories with acceptance criteria
   - Status: ✅ High-level requirements complete

6. **CSMS_Module_7_Finance_Requirements.md**
   - Contains: **FINANCE MODULE**
   - Format: User stories with acceptance criteria
   - Status: ✅ High-level requirements complete

7. **Child_Support_Application_Complete_Requirements.md**
   - Contains: Complete system requirements including architecture, database design, and technical specifications
   - Format: Comprehensive requirements document
   - Status: ✅ Complete

---

## Module Summary

### Module 1: INTAKE MODULE
**Document**: CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Section 1)  
**User Stories**: 7 user stories  
**Key Features**:
- Menu items and navigation
- Intake search
- Paper application IV-D entry
- CP application entry
- NCP application entry
- Support and insurance screen
- Application in progress/resume

### Module 2: CASE REGISTRATION MODULE
**Document**: CSMS_Developer_Requirements_with_Acceptance_Criteria.md (Section 2)  
**User Stories**: 14 user stories  
**Key Features**:
- Case registration home page
- Member clearance (CP, NCP, Child)
- Member status
- CP demographics and income/assets
- NCP demographics, address, relative, income/assets
- Child information
- Member insurance
- Case status
- Cancel and resume functionality

### Module 3: CASE MANAGEMENT MODULE
**Document**: CSMS_Module_3_Case_Management_Requirements.md  
**User Stories**: 17+ user stories  
**Key Features**:
- View case details/main screen
- View/Modify CP (Demographics, Employer)
- View/Modify NCP (Demographics, Employer, Income/Assets, Relative, Address, Incarceration)
- View/Modify Child information
- View/Modify Member Insurance
- Federal Case Registry
- AOP Unmatched Search
- Billing Suppression
- DVR (Division of Vital Records)
- File Upload
- Close, Suspend, Re-open
- Disbursement Hold

### Module 4: LOCATE MODULE
**Document**: CSMS_Module_4_Locate_Requirements.md  
**User Stories**: 9 user stories  
**Key Features**:
- Cases tab search functionality
- Locate summary
- Demographics section
- Address section
- Employer section
- Contact section
- File upload in locate
- Required action tab

### Module 5: ESTABLISHMENT MODULE
**Document**: CSMS_Module_5_Establishment_Requirements.md  
**Key Features**:
- Paternity establishment
- Support order establishment
- Court order management
- Hearing management
- Intergovernmental establishment

### Module 6: ENFORCEMENT MODULE
**Document**: CSMS_Module_6_Enforcement_Requirements.md  
**Key Features**:
- Income Withholding Order (IWO) management
- National Medical Support Notice (NMSN)
- License suspension/revocation
- Passport denial
- Tax intercept
- Asset seizure
- Arrears management
- Enforcement actions tracking

### Module 7: FINANCE MODULE
**Document**: CSMS_Module_7_Finance_Requirements.md  
**Key Features**:
- Payment receipt
- Payment processing
- Disbursement management
- Account management
- Financial reporting
- Billing and fee management
- Bank reconciliation
- URPA management

---

## Additional Documents

### Complete Requirements Document
**Child_Support_Application_Complete_Requirements.md**
- System architecture
- Database design (complete schema)
- Technical specifications
- Integration requirements
- Security and compliance
- Implementation roadmap

### Source Files (Reference)
- `Userstory_CSMSIntake.txt` - Original intake user stories
- `CaseRegistrationUserstoryPagebased.txt` - Original case registration user stories
- `UserStoryCaseManagementPageBased.txt` - Original case management user stories

---

## How to Use These Documents

1. **For Developers**: Start with the module-specific documents (CSMS_Module_X_Requirements.md) for detailed acceptance criteria
2. **For Architects**: Refer to Child_Support_Application_Complete_Requirements.md for system design
3. **For Project Managers**: Use all documents to understand scope and requirements
4. **For Testers**: Use acceptance criteria in each module document for test case development

---

## Document Status Legend

- ✅ Complete - All user stories and acceptance criteria documented
- 🔄 In Progress - Partially complete, additional details to be added
- 📋 High-level - Framework provided, detailed acceptance criteria to be developed

---

## Next Steps

1. Review each module document
2. Use acceptance criteria for development sprints
3. Reference source files for additional context
4. Update documents as requirements evolve
5. Use complete requirements document for architecture and database design

---

**Last Updated**: 2024  
**Document Version**: 1.0
