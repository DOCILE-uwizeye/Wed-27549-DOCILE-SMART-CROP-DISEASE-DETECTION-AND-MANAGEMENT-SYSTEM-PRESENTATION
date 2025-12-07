# Phase II: Business Process Modeling
## Project: Smart Crop Disease Detection & Management System



## 1. Scope Definition
### **Business Process Covered:**  
The process models how a farmer uploads a crop image, how the system analyzes it, detects disease, stores the scan, and generates recommendations.

### **Objectives**
- Detect crop diseases using automated image analysis.
- Provide farmers with treatment and prevention.
- Store historical scans for future tracking.
- Support decision-making using MIS functions.

### **Expected Outcomes**
- Faster and accurate disease detection.
- Better crop health monitoring.
- Increased agricultural productivity.
- Structured data for analytics.

---

## 2. Key Entities & Actors
### **Users**
- Farmers (upload images, view results)
- System admin (manages disease profiles)
- System engine (AI detection logic)

### **Departments / Systems**
- Image Processing Component
- Disease Knowledge Base
- Recommendations Engine
- Database Storage
- Notification/Results System

### **Roles & Responsibilities**
| Actor | Responsibility |
|------|----------------|
| Farmer | Uploads crop image, views diagnosis |
| System Engine | Analyzes image, detects disease |
| Database | Stores users, scans, diseases, history |
| Admin | Updates disease profiles & recommendations |


## 3. Business Process (Swimlane Description)
### **Swimlanes**
- Farmer
- Detection System
- Database
- Recommendation Engine

### **Process Flow (Text Description of Diagram)**
1. **Farmer uploads leaf image.**
2. System receives image → preprocesses it.
3. AI model analyzes leaf → detects disease.
4. System retrieves disease details from the database.
5. System generates treatment & prevention recommendations.
6. System stores scan + results in database.
7. Farmer receives disease report and recommendation.



## 4. BPMN/UML Notations Used
- **Start Event:** Upload image  
- **Tasks:** Analyze image, fetch disease info, store scan, generate recommendation  
- **Decision Point:** Is a disease detected?  
- **End Event:** Results displayed  
- **Data Stores:** Users, disease_profiles, scans, recommendations  



## 5. Logical Flow Validation
- Fully linear from image upload → analysis → results.
- Decision paths clear (diseased or healthy).
- No missing dependencies.
- All actors have defined responsibilities.



## 6. Documentation Summary
### Key MIS Functions Supported
- Data storage & management  
- Automated decision support  
- Real-time processing  
- Analytical insights through history tracking  

### Organizational Impact
- Reduces crop losses  
- Helps farmers make faster decisions  
- Supports digital agriculture adoption  

### BI Opportunities
- Disease trend analysis  
- Crop health forecasting  
- Region-based disease heatmaps  



## Deliverables
- BPMN Diagram (PNG/JPG)
- This documentation file
DRAW I.O
  (./<img width="1275" height="582" alt="DDI1" src="https://github.com/user-attachments/assets/95f7173b-6643-45ff-ad1c-08192e193208" />
)


# PHASE III: Logical Data Model (ERD + 3NF + Data Dictionary)



## 1. ER Diagram Components (Entities & Attributes)

### **users**
- **user_id** (PK)  
- name  
- email  
- password  
- role  

### **disease_profiles**
- **disease_id** (PK)  
- disease_name  
- symptoms  
- causes  
- treatment  
- prevention  

### **scans**
- **scan_id** (PK)  
- **user_id** (FK → users.user_id)  
- image_path  
- **detected_disease** (FK → disease_profiles.disease_id)  
- confidence_score  
- scan_date  

### **recommendations**
- **rec_id** (PK)  
- **disease_id** (FK → disease_profiles.disease_id)  
- recommendation  

### **crop_types**
- **crop_id** (PK)  
- crop_name  



## 2. Normalization Summary (Up to 3NF)

| Normal Form | Description |
|------------|-------------|
| **1NF** | All tables contain atomic values. Each record is unique. |
| **2NF** | All non-key attributes fully depend on the primary key. No partial dependencies exist. |
| **3NF** | No transitive dependencies. All attributes depend only on the table's primary key. |



## 3. Data Dictionary

| Table | Column | Type | Constraints | Description |
|-------|--------|------|-------------|-------------|
| users | user_id | INT | PK | Unique user ID |
| users | name | VARCHAR | NOT NULL | User full name |
| users | email | VARCHAR | UNIQUE, NOT NULL | Login email |
| users | password | VARCHAR | NOT NULL | Hashed password |
| users | role | VARCHAR | NOT NULL | Role (user/admin) |
| disease_profiles | disease_id | INT | PK | Disease identifier |
| disease_profiles | disease_name | VARCHAR | NOT NULL | Name of disease |
| disease_profiles | symptoms | TEXT | NOT NULL | Symptoms description |
| disease_profiles | causes | TEXT | NOT NULL | Causes of the disease |
| disease_profiles | treatment | TEXT | NOT NULL | Treatment methods |
| disease_profiles | prevention | TEXT | NOT NULL | Prevention methods |
| scans | scan_id | INT | PK | Scan record ID |
| scans | user_id | INT | FK → users.user_id | User who uploaded scan |
| scans | image_path | VARCHAR | NOT NULL | Path to uploaded image |
| scans | detected_disease | INT | FK → disease_profiles.disease_id | Disease detected |
| scans | confidence_score | FLOAT | NOT NULL | Accuracy percentage |
| scans | scan_date | DATE | NOT NULL | Date of scan |
| recommendations | rec_id | INT | PK | Recommendation ID |
| recommendations | disease_id | INT | FK → disease_profiles.disease_id | Related disease |
| recommendations | recommendation | TEXT | NOT NULL | Advice or solution |
| crop_types | crop_id | INT | PK | Crop type ID |
| crop_types | crop_name | VARCHAR | UNIQUE | Name of crop |



## 4. BI Considerations

| Aspect | Notes |
|--------|------|
| Fact Table Candidate | **scans** |
| Dimension Tables | users, disease_profiles, crop_types |
| Slowly Changing Dimensions (SCD) | Disease treatments may change over time |
| Audit Trail | Recommended: log table for user actions, scan attempts |



## 5. Assumptions

1. Each scan is linked to exactly one user.  
2. Each scan detects only one disease at a time.  
3. Recommendations are tied to diseases.  
4. Crop types may be linked later for future expansion.  
5. Users, scans, and recommendations are maintained in a consistent format to ensure data integrity.  



## 6. ERD Relationships (Summary)

| Table | Relationship | Reference |
|-------|-------------|-----------|
| scans | Many-to-One | users.user_id |
| scans | Many-to-One | disease_profiles.disease_id (detected_disease) |
| recommendations | Many-to-One | disease_profiles.disease_id |

> **Note:** The **scans** table acts as a fact table in BI; **users**, **disease_profiles**, and **crop_types** act as dimension tables.
(./images/database_schema.png)<img width="1358" height="666" alt="DDI3" src="https://github.com/user-attachments/assets/efe0b0cf-d5c3-44af-ae97-b0956ca328f5" />

# Phase IV: Database Creation & Configuration
## Project: Smart Crop Disease Detection & Management System

**Student:** Docile (ID: 27549)  
**Group:** Wednesday  
**Date:** December 7, 2025

---

## Screenshot 1: Database Creation

(../screenshots/phase4_database_creation/01_database_created.png)<img width="938" height="678" alt="phase IV scr1" src="https://github.com/user-attachments/assets/ee6fce90-714b-4f3c-b01e-bc6c179a3564" />


---

## Screenshot 2: Pluggable Databases Verification

(../screenshots/phase4_database_creation/02_pluggable_databases.png)<img width="847" height="504" alt="phase IV scr2" src="https://github.com/user-attachments/assets/d90424fa-1225-4017-9e56-9b8157c905d8" />


---

## Screenshot 3: Session Connected to Database

(../screenshots/phase4_database_creation/03_session_connected.png)<img width="872" height="271" alt="phase IV scr3" src="https://github.com/user-attachments/assets/f1f27f1d-c54c-4017-a376-3adb61e74c5d" />


---

## Screenshot 4: Privileges Granted

(../screenshots/phase4_database_creation/04_privileges_granted.png)<img width="471" height="535" alt="phase IV scr4" src="https://github.com/user-attachments/assets/713e1028-52bf-4a31-91e7-637ba4ebe048" />


---

## Screenshot 5: Tablespaces Created

(../screenshots/phase4_database_creation/05_tablespaces_created.png)<img width="404" height="526" alt="phase IV scr5" src="https://github.com/user-attachments/assets/4df94b44-7485-4999-9093-425e8b9998d4" />


---

## Screenshot 6: Tablespace Verification

(../screenshots/phase4_database_creation/06_tablespace_verification.png)<img width="599" height="506" alt="phase IV scr6" src="https://github.com/user-attachments/assets/8f84a854-c474-4f45-93a2-098d278e4f94" />



##  Memory Configuration

(../screenshots/phase4_database_creation/07_memory_configuration.png)<img width="863" height="429" alt="phase IV scr7" src="https://github.com/user-attachments/assets/5dea99aa-88f6-401e-8835-67b449857ceb" />

## 5. Database Setup 

### Naming Convention Compliance
| Component | Value |
|-----------|-------|
| Group Name | wed |
| Student ID | 27549 |
| First Name | docile |
| Project Name | smartcropdiseasedetectionandmanagementsystem |
| **Full Database Name** | **wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db** |

### Admin User Details
| Attribute | Value |
|-----------|-------|
| Username | crop_admin |
| Password | docile |
| Privileges | Super admin (all CREATE privileges) |

### Tablespace Configuration
| Tablespace | Type | Size | Autoextend |
|-----------|------|------|-----------|
| crop_data_ts | PERMANENT | 100MB | ON (10MB increments) |
| crop_index_ts | PERMANENT | 50MB | ON (5MB increments) |
| crop_temp_ts | TEMPORARY | 50MB | ON (5MB increments) |

### Memory Parameters
| Parameter | Value |
|-----------|-------|
| S
# PHASE V: TABLE IMPLEMENTATION & DATA INSERTION
##  TABLE STRUCTURES

### Table 1: USERS

**Purpose:** Store user information (farmers, admins, agronomists)

**SQL Creation Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="742" height="646" alt="phase V scr1" src="https://github.com/user-attachments/assets/a89e6316-b7ce-4da3-b103-45aaab9ea871" />




CREATE SEQUENCE users_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

(https://user-images.githubusercontent.com/12345/image.png)<img width="822" height="389" alt="phase V scr3 - Copy" src="https://github.com/user-attachments/assets/8c194d35-3721-4cde-9258-64491dc88de8" />


**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| user_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| name | VARCHAR2(100) | NOT NULL | User's full name |
| email | VARCHAR2(100) | UNIQUE, NOT NULL | User's email address |
| password | VARCHAR2(100) | NOT NULL | Hashed password |
| role | VARCHAR2(20) | NOT NULL, CHECK | User role (farmer/admin/agronomist) |
| created_date | DATE | DEFAULT SYSDATE | Registration date |

---

### Table 2: CROP_TYPES

**Purpose:** Store information about different crop types
**SQL Creation Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="822" height="389" alt="phase V scr3" src="https://github.com/user-attachments/assets/5a0ebe18-b544-4e96-926d-c0854209b874" />

**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| crop_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| crop_name | VARCHAR2(100) | NOT NULL, UNIQUE | Common crop name |
| scientific_name | VARCHAR2(150) | NULL | Scientific/Latin name |
| growing_season | VARCHAR2(50) | NULL | Optimal growing season |
| created_date | DATE | DEFAULT SYSDATE | Record creation date |

---

### Table 3: DISEASE_PROFILES

**Purpose:** Store comprehensive disease information and management strategies

**SQL Creation Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="945" height="547" alt="phase V scr4" src="https://github.com/user-attachments/assets/6afc669e-74f8-47ee-adf2-2031631f6df9" />

**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| disease_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| disease_name | VARCHAR2(150) | NOT NULL | Disease name |
| symptoms | VARCHAR2(1000) | NULL | Visible symptoms |
| causes | VARCHAR2(1000) | NULL | Disease causes |
| treatment | VARCHAR2(2000) | NULL | Treatment methods |
| prevention | VARCHAR2(2000) | NULL | Prevention strategies |
| severity_level | VARCHAR2(20) | CHECK | Severity (low/medium/high/critical) |
| created_date | DATE | DEFAULT SYSDATE | Record creation date |



### Table 4: RECOMMENDATIONS

**Purpose:** Store treatment recommendations for each disease

**SQL Creation Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="1071" height="461" alt="phase V scr5" src="https://github.com/user-attachments/assets/61c20992-b32e-4a6b-a504-cfc3093cebc3" />

**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| rec_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| disease_id | NUMBER(10) | NOT NULL, FK | References disease_profiles |
| recommendation | VARCHAR2(2000) | NOT NULL | Recommendation text |
| rec_type | VARCHAR2(50) | CHECK | Type (chemical/organic/cultural/biological) |
| created_date | DATE | DEFAULT SYSDATE | Record creation date |



### Table 5: SCANS

**Purpose:** Store disease detection scan records

**SQL Creation Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="1175" height="665" alt="phase V scr6 - Copy" src="https://github.com/user-attachments/assets/ea8454a9-c034-49d1-9737-19e3fb5ee840" />

**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| scan_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| user_id | NUMBER(10) | NOT NULL, FK | References users |
| image_path | VARCHAR2(500) | NOT NULL | Path to uploaded image |
| detected_disease | NUMBER(10) | FK | References disease_profiles |
| confidence_score | NUMBER(5,2) | CHECK (0-100) | AI confidence percentage |
| scan_date | DATE | DEFAULT SYSDATE | Scan timestamp |
| scan_status | VARCHAR2(20) | CHECK | Status (pending/completed/failed) |
| crop_id | NUMBER(10) | FK | References crop_types |

---

##  DATA INSERTION SCRIPTS

### Sample Data: USERS Table

**Total Records Inserted:** 10
```sql
-- Farmers
(https://user-images.githubusercontent.com/12345/image.png)<img width="1198" height="680" alt="phase V scr11" src="https://github.com/user-attachments/assets/52eb9c18-4f38-421e-865a-3aee6bcf501b" />



### Sample Data: DISEASE_PROFILES Table

**Total Records Inserted:** 54
(https://user-images.githubusercontent.com/12345/image.png)<img width="1336" height="696" alt="phase V scr13" src="https://github.com/user-attachments/assets/f1033652-dc84-48cf-8406-9da726ce2f16" />


### Sample Data: SCANS Table

**Total Records Inserted:** 25+
(https://user-images.githubusercontent.com/12345/image.png)<img width="1107" height="681" alt="phase V scr17" src="https://github.com/user-attachments/assets/e7f6464f-27a2-48eb-995e-517203d22d24" />


### Sample Data: RECOMMENDATIONS Table

**Total Records Inserted:** 30
(https://user-images.githubusercontent.com/12345/image.png)<img width="1292" height="691" alt="phase V scr18" src="https://github.com/user-attachments/assets/bd1e5c3b-086a-453e-a53f-393582c01497" />


# PHASE VI: DATABASE INTERACTION & TRANSACTIONS
## Project: Smart Crop Disease Detection & Management System

**Student:** DOCILE  
**Student ID:** 27549  
**Group:** Wednesday  
**Date:** December 7, 2025  
**Institution:** Adventist University of Central Africa (AUCA)

---

## Phase VI Overview

This phase implements PL/SQL stored procedures, functions, packages, cursors, and window functions to enable robust database interactions, transaction management, and analytical capabilities.

### Deliverables:
- 5 Stored Procedures with exception handling
- 5 Functions with proper return types
- Explicit cursors for multi-row processing
- Window functions (ROW_NUMBER, RANK, LAG, LEAD)
- 2 Complete packages (specification + body)
- Comprehensive testing and validation

---

## 1. STORED PROCEDURES

### Overview
Created 5 production-ready stored procedures with comprehensive exception handling, input validation, and transaction management.

### Procedure List:
1. **sp_register_user** - Register new users with email validation
2. **sp_record_scan** - Record disease detection scans
3. **sp_update_disease** - Update disease profile information
4. **sp_add_recommendation** - Add treatment recommendations
5. **sp_delete_old_scans** - Archive old scan records

---

## 2. TEST 1: REGISTER USER PROCEDURE

The `sp_register_user` procedure registers new farmers and admin users with duplicate email checking and proper exception handling.

**Features:**
- Email uniqueness validation
- Custom exception for duplicate emails
- OUT parameters for user_id and status message
- Transaction management (COMMIT/ROLLBACK)

**Screenshot 1: Test 1 - Register User**

(../screenshots/phase6/01_test_register_user.png)
![Screenshot 1](https://github.com/user-attachments/assets/your-image-id-here)

**Test Results:**
- User registered successfully with ID: 6
- Procedure executed without errors
- Transaction committed successfully
- Output: "User registered successfully with ID: 6"

---

## 3. TEST 2: RECORD SCAN PROCEDURE

The `sp_record_scan` procedure records disease detection scans with validation of user existence and confidence score range.

**Features:**
- User ID validation (FK constraint)
- Confidence score range check (0-100)
- Foreign key validation for diseases
- Automatic timestamp with SYSDATE

**Screenshot 2: Test 2 - Record Scan**

(../screenshots/phase6/02_test_record_scan.png)
![Screenshot 2](https://github.com/user-attachments/assets/your-image-id-here)

**Test Results:**
- Scan recorded successfully with ID: 9
- User validation passed
- Confidence score validated (91.5%)
- Output: "Scan recorded successfully with ID: 9"

---

## 4. FUNCTIONS

### Overview
Created 5 reusable functions for calculations, validations, and data lookups with proper return types and exception handling.

### Function List:
1. **fn_avg_confidence** - Calculate average confidence score for a user
2. **fn_total_scans** - Count total scans by user
3. **fn_validate_email** - Email format validation using REGEXP
4. **fn_disease_name** - Lookup disease name by ID
5. **fn_detection_rate** - Calculate disease detection rate percentage

---

## 5. TEST 3: FUNCTIONS TEST

All 5 functions tested successfully with different input parameters and return types.

**Screenshot 3: Test 3 - All Functions**

(../screenshots/phase6/03_test_functions.png)
![Screenshot 3](https://github.com/user-attachments/assets/your-image-id-here)

**Test Results:**
```
=== TEST 3: Functions ===
Avg Confidence User 1: 90.15
Total Scans User 1: 4
Email Valid: VALID
Disease Name: Tomato Late Blight
```

**Function Details:**
- `fn_avg_confidence(1)` returned 90.15% average
- `fn_total_scans(1)` returned 4 scans
- `fn_validate_email('test@email.com')` returned VALID
- `fn_disease_name(1)` returned "Tomato Late Blight"

---

## 6. PACKAGES

### Overview
Created 2 complete packages with specifications and bodies to organize related procedures and functions.

### Package 1: pkg_user_mgmt
- `register()` - Register new users
- `authenticate()` - Verify user credentials
- `get_role()` - Get user role

### Package 2: pkg_disease_mgmt
- `add_disease()` - Add new disease profiles
- `get_info()` - Retrieve disease information

---

## 7. TEST 4: PACKAGE TEST

Testing the `pkg_user_mgmt.register()` procedure from the user management package.

**Screenshot 4: Test 4 - Package Execution**

(../screenshots/phase6/04_test_package.png)
(https://github.com/user-attachments/assets/your-image-id-here)

**Test Results:**
```
=== TEST 4: Package ===
User registered successfully with ID: 7
```

**Package Features Demonstrated:**
- Package procedure called successfully
- Encapsulation of related operations
- Public interface working correctly
- No compilation errors

---

## 8. CURSORS

### Overview
Implemented explicit cursors for multi-row processing with proper OPEN/FETCH/CLOSE cycle and exception handling.

### Cursor Procedure:
**sp_display_user_scans** - Display user scan history using explicit cursor with LEFT JOIN to disease_profiles table.

**Cursor Features:**
- Explicit cursor declaration
- %ROWTYPE for record variables
- LEFT JOIN for optional disease data
- Proper OPEN/FETCH/CLOSE cycle
- %NOTFOUND for loop exit

---

## 9. TEST 5: CURSOR OUTPUT

Testing the explicit cursor procedure that retrieves and displays all scans for a specific user.

**Screenshot 5: Test 5 - Cursor Execution**

(../screenshots/phase6/05_test_cursor.png)
(https://github.com/user-attachments/assets/your-image-id-here)<img width="1297" height="588" alt="phase VI scre5" src="https://github.com/user-attachments/assets/4a36262a-3ce4-481c-b85e-79a04d84143b" />


**Cursor Output:**
```
=== Scan History for User 1 ===
Scan ID: 9 | Disease: Tomato Late Blight | Confidence: 91.5%
Scan ID: 8 | Disease: Tomato Late Blight | Confidence: 89.3%
Scan ID: 2 | Disease: Tomato Late Blight | Confidence: 92.3%
Scan ID: 1 | Disease: Tomato Late Blight | Confidence: 87.5%
```

**Cursor Processing:**
- 4 scan records fetched successfully
- Disease names retrieved via LEFT JOIN
- Confidence scores displayed correctly
- Cursor opened, fetched, and closed properly
- NVL used for NULL disease handling

---

## 10. WINDOW FUNCTIONS & VIEWS

### Overview
Created analytical views using advanced window functions (RANK, LAG, LEAD, aggregations with OVER clause).

### Views Created:
1. **vw_user_rankings** - User rankings by total scans using RANK()
2. **vw_disease_trends** - Disease trends with LAG/LEAD functions
3. **vw_monthly_stats** - Monthly scan statistics with GROUP BY

---

## 11. TEST 6: WINDOW FUNCTIONS - USER RANKINGS

Query using RANK() window function to rank users by their total number of scans.

**Screenshot 6: Test 6 - User Rankings and Monthly Statistics**

(../screenshots/phase6/06_test_window_functions.png)
(https://github.com/user-attachments/assets/your-image-id-here)<img width="899" height="686" alt="phase VI scr6" src="https://github.com/user-attachments/assets/996056ee-c6fe-4914-a316-b4a40ca7757b" />


**User Rankings Results:**
```
USER_ID  NAME           TOTAL_SCANS  RANK
-------  ------------   -----------  ----
1        John Farmer    4            1
2        Mary Smith     2            2
4        Peter Green    2            2
5        Sarah Brown    1            4
6        Test User      0            5
```

**Window Function Used:**
```sql
RANK() OVER (ORDER BY COUNT(s.scan_id) DESC) AS rank
```

**Monthly Statistics Results:**
```
MONTH     TOTAL_SCANS  AVG_CONFIDENCE
-------   -----------  --------------
2025-11   4            85.975
2025-12   5            91.22
```

**Features Demonstrated:**
- RANK() window function
- GROUP BY with aggregations
- LEFT JOIN to include users with no scans
- Proper handling of ties (rank 2 appears twice)
- Monthly trend analysis

---

## 12. VIEW CREATION

Creating the `vw_monthly_stats` view with aggregation functions and date formatting.

**Screenshot 7: View Creation SQL**

(../screenshots/phase6/07_view_creation.png)
(https://github.com/user-attachments/assets/your-image-id-here)<img width="1038" height="706" alt="phase VI scr7" src="https://github.com/user-attachments/assets/e145ce2c-4941-4d70-868f-8e94521991ab" />


**View Definition:**
```sql
CREATE OR REPLACE VIEW vw_monthly_stats AS
SELECT TO_CHAR(scan_date, 'YYYY-MM') AS month,
       COUNT(*) AS total_scans,
       AVG(confidence_score) AS avg_confidence
FROM scans
GROUP BY TO_CHAR(scan_date, 'YYYY-MM')
ORDER BY month;
```


## 13. PACKAGE CREATION

Creating the user management package with specification and body.

**Screenshot 8: Package Creation**

(../screenshots/phase6/08_package_creation.png)
(https://github.com/user-attachments/assets/your-image-id-here)<img width="986" height="698" alt="phase VI scr8" src="https://github.com/user-attachments/assets/abe77116-7168-4cc0-8fe6-8cc57a51de27" />


**Package Components:**

### Package Specification:
```sql
CREATE OR REPLACE PACKAGE pkg_user_mgmt AS
    PROCEDURE register(...);
    FUNCTION authenticate(...) RETURN NUMBER;
    FUNCTION get_role(...) RETURN VARCHAR2;
END pkg_user_mgmt;
```

### Package Body:
```sql
CREATE OR REPLACE PACKAGE BODY pkg_user_mgmt AS
    -- Implementation of procedures and functions
END pkg_user_mgmt;
```

**Status:** Package created successfully

---

## 14. ALL OBJECTS VERIFICATION

Verification of all database objects created in Phase V and Phase VI showing object names, types, and compilation status.

**Screenshot 9: All Objects Status**

(../screenshots/phase6/09_all_objects_status.png
(https://github.com/user-attachments/assets/your-image-id-here)<img width="864" height="671" alt="phase VI scr9" src="https://github.com/user-attachments/assets/07a3d365-d134-49e3-9fc8-a0e64681ecfe" />


**Total Objects Created:** 25

### Object Summary:

| Object Type | Count | Status |
|-------------|-------|--------|
| FUNCTION | 5 | VALID |
| PACKAGE | 2 | VALID |
| PACKAGE BODY | 2 | VALID |
| PROCEDURE | 6 | VALID |
| SEQUENCE | 5 | VALID |
| TABLE | 5 | VALID |
| VIEW | 2 | VALID |

**All objects compiled successfully with VALID status!**

### Detailed Object List:

**Functions:**
- FN_AVG_CONFIDENCE
- FN_DETECTION_RATE
- FN_DISEASE_NAME
- FN_TOTAL_SCANS
- FN_VALIDATE_EMAIL

**Packages:**
- PKG_DISEASE_MGMT (spec + body)
- PKG_USER_MGMT (spec + body)

**Procedures:**
- SP_ADD_RECOMMENDATION
- SP_DELETE_OLD_SCANS
- SP_DISPLAY_USER_SCANS
- SP_RECORD_SCAN
- SP_REGISTER_USER
- SP_UPDATE_DISEASE

**Sequences:**
- CROP_SEQ
- DISEASE_SEQ
- REC_SEQ
- SCAN_SEQ
- USER_SEQ

**Tables:**
- CROP_TYPES
- DISEASE_PROFILES
- RECOMMENDATIONS
- SCANS
- USERS

**Views:**
- VW_MONTHLY_STATS
- VW_USER_RANKINGS

---

