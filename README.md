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

##  Database Creation

(../screenshots/phase4_database_creation/01_database_created.png)<img width="938" height="678" alt="phase IV scr1" src="https://github.com/user-attachments/assets/ee6fce90-714b-4f3c-b01e-bc6c179a3564" />




##  Pluggable Databases Verification

(../screenshots/phase4_database_creation/02_pluggable_databases.png)<img width="847" height="504" alt="phase IV scr2" src="https://github.com/user-attachments/assets/d90424fa-1225-4017-9e56-9b8157c905d8" />




##  Session Connected to Database

(../screenshots/phase4_database_creation/03_session_connected.png)<img width="872" height="271" alt="phase IV scr3" src="https://github.com/user-attachments/assets/f1f27f1d-c54c-4017-a376-3adb61e74c5d" />


##  Privileges Granted

(../screenshots/phase4_database_creation/04_privileges_granted.png)<img width="471" height="535" alt="phase IV scr4" src="https://github.com/user-attachments/assets/713e1028-52bf-4a31-91e7-637ba4ebe048" />


##  Tablespaces Created

(../screenshots/phase4_database_creation/05_tablespaces_created.png)<img width="404" height="526" alt="phase IV scr5" src="https://github.com/user-attachments/assets/4df94b44-7485-4999-9093-425e8b9998d4" />


##  Tablespace Verification

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



##  DATA INSERTION SCRIPTS

### Sample Data: USERS Table

**Total Records Inserted:** 10
```sql
-- Farmers
(./screenshots/Screenshot1.png)<img width="1198" height="680" alt="phase V scr11" src="https://github.com/user-attachments/assets/5695684a-1be8-4a45-9012-ed312508c675" />





### Sample Data: DISEASE_PROFILES Table

**Total Records Inserted:** 54
(https://user-images.githubusercontent.com/12345/image.png)<img width="1336" height="696" alt="phase V scr13" src="https://github.com/user-attachments/assets/f1033652-dc84-48cf-8406-9da726ce2f16" />


### Sample Data: SCANS Table

**Total Records Inserted:** 25+
(https://user-images.githubusercontent.com/12345/image.png)<img width="1107" height="681" alt="phase V scr17" src="https://github.com/user-attachments/assets/e7f6464f-27a2-48eb-995e-517203d22d24" />


### Sample Data: RECOMMENDATIONS Table

**Total Records Inserted:** 30
(https://user-images.githubusercontent.com/12345/image.png)<img width="1292" height="691" alt="phase V scr18" src="https://github.com/user-attachments/assets/bd1e5c3b-086a-453e-a53f-393582c01497" />

# PHASE VI: Database Interaction & Transactions


## Testing Results

### Test 1: Register User and Record Scan

**Test Script:**
(https://user-images.githubusercontent.com/12345/image.png)<img width="885" height="481" alt="phase VI  scre" src="https://github.com/user-attachments/assets/73580332-1123-4f75-b3d5-2a258e05d1bb" />






**Result:**
-  **Test 1: Register User**
- Result: User registered successfully with ID: 6
- PL/SQL procedure successfully completed.

**Result:**
-  **Test 2: Record Scan**
- Result: Scan recorded successfully with ID: 9
- PL/SQL procedure successfully completed.


### Test 3: Functions

**Test Script:**
```sql
--  Functions
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== TEST 3: Functions ===');
    DBMS_OUTPUT.PUT_LINE('Avg Confidence User 1: ' || fn_avg_confidence(1));
    DBMS_OUTPUT.PUT_LINE('Total Scans User 1: ' || fn_total_scans(1));
    DBMS_OUTPUT.PUT_LINE('Email Valid: ' || fn_validate_email('test@email.com'));
    DBMS_OUTPUT.PUT_LINE('Disease Name: ' || fn_disease_name(1));
    DBMS_OUTPUT.PUT_LINE(' ');
END;
/


**Results:**
- **Test 3: Functions**
- Avg Confidence User 1: 90.15
- Total Scans User 1: 4
- Email Valid: VALID
- Disease Name: Tomato Late Blight
- PL/SQL procedure successfully completed.

![Test 3: Functions](screenshots/phase6_test3_functions.png)



###  Package

**Test Script:**
```sql
-- Test 4: Package
DECLARE
    v_user_id NUMBER;
    v_message VARCHAR2(500);
BEGIN
    DBMS_OUTPUT.PUT_LINE('=== TEST 4: Package ===');
    pkg_user_mgmt.register('Package Test', 'pkg@test.com', 'pass', v_user_id, v_message);
    DBMS_OUTPUT.PUT_LINE(v_message);
    DBMS_OUTPUT.PUT_LINE(' ');
END;
/


**Result:**
-  Package**
- User registered successfully with ID: 7
- PL/SQL procedure successfully completed.

![Test 4: Package](screenshots/phase6_test4_package.png)



###  Cursor

**Test Script:**
```sql
-- Test 5: Cursor
BEGIN
    sp_display_user_scans(1);
END;
/


**Results:**
- **Test 5: Cursor - Scan History for User 1**
- Scan ID: 9 | Disease: Tomato Late Blight | Confidence: 91.5%
- Scan ID: 8 | Disease: Tomato Late Blight | Confidence: 89.3%
- Scan ID: 2 | Disease: Tomato Late Blight | Confidence: 92.3%
- Scan ID: 1 | Disease: Tomato Late Blight | Confidence: 87.5%
- PL/SQL procedure successfully completed.

(screenshots/phase6_test5_cursor.png)

###  Views

**View 1: User Rankings**
```sql
SELECT * FROM vw_user_rankings WHERE ROWNUM <= 5;


**Results:**

| USER_ID | NAME | TOTAL_SCANS | RANK |
|---------|------|-------------|------|
| 1 | John Farmer | 4 | 1 |
| 2 | Mary Smith | 2 | 2 |
| 4 | Peter Green | 2 | 2 |
| 5 | Sarah Brown | 1 | 4 |
| 6 | Test User | 0 | 5 |

**View 2: Monthly Statistics**
```sql
SELECT * FROM vw_monthly_stats;


**Results:**

| MONTH | TOTAL_SCANS | AVG_CONFIDENCE |
|-------|-------------|----------------|
| 2025-11 | 4 | 85.975 |
| 2025-12 | 5 | 91.22 |

![Test 6: Views](screenshots/phase6_test6_views.png)



##  Verification of All Objects

**Query:**
```sql
SELECT object_name, object_type, status
FROM user_objects
WHERE object_type IN ('TABLE','PROCEDURE','FUNCTION','PACKAGE','VIEW','SEQUENCE')
ORDER BY object_type, object_name;
```

**All Objects Status:**

| OBJECT_NAME | OBJECT_TYPE | STATUS |
|-------------|-------------|--------|
| FN_AVG_CONFIDENCE | FUNCTION | VALID |
| FN_DETECTION_RATE | FUNCTION | VALID |
| FN_DISEASE_NAME | FUNCTION | VALID |
| FN_TOTAL_SCANS | FUNCTION | VALID |
| FN_VALIDATE_EMAIL | FUNCTION | VALID |
| PKG_DISEASE_MGMT | PACKAGE | VALID |
| PKG_USER_MGMT | PACKAGE | VALID |
| SP_ADD_RECOMMENDATION | PROCEDURE | VALID |
| SP_DELETE_OLD_SCANS | PROCEDURE | VALID |
| SP_DISPLAY_USER_SCANS | PROCEDURE | VALID |
| SP_RECORD_SCAN | PROCEDURE | VALID |
| SP_REGISTER_USER | PROCEDURE | VALID |
| SP_UPDATE_DISEASE | PROCEDURE | VALID |
| CROP_SEQ | SEQUENCE | VALID |
| DISEASE_SEQ | SEQUENCE | VALID |
| REC_SEQ | SEQUENCE | VALID |
| SCAN_SEQ | SEQUENCE | VALID |
| USER_SEQ | SEQUENCE | VALID |
| CROP_TYPES | TABLE | VALID |
| DISEASE_PROFILES | TABLE | VALID |
| RECOMMENDATIONS | TABLE | VALID |
| SCANS | TABLE | VALID |
| USERS | TABLE | VALID |
| VW_MONTHLY_STATS | VIEW | VALID |
| VW_USER_RANKINGS | VIEW | VALID |

**Total Objects:** 25 rows selected

![Verification of All Objects](screenshots/phase6_verification_all_objects.png)

---

##  Test Summary

| Test Case | Description | Status |
|-----------|-------------|--------|
| Test 1 | Register User |  PASSED |
| Test 2 | Record Scan |  PASSED |
| Test 3 | Functions (4 functions) |  PASSED |
| Test 4 | Package |  PASSED |
| Test 5 | Cursor |  PASSED |
| Test 6 | Views (2 views) |  PASSED |

---

## Final Status

```
===== ALL TESTS COMPLETE =====
===== ALL TESTS COMPLETE =====
===== Phase V + VI Successfully Implemented =====^S
```

**All 25 database objects are VALID and functional:**
-  5 Functions
-  2 Packages
-  6 Procedures
-  5 Sequences
-  5 Tables
-  2 Views

![Final Status](screenshots/phase6_final_status.png)




# PHASE VII: Advanced Programming & Auditing
**Objective:** Implement triggers, business rules, and comprehensive auditing

**Critical Business Rule:** Employees CANNOT INSERT/UPDATE/DELETE on:
- WEEKDAYS (Monday-Friday)
- PUBLIC HOLIDAYS (upcoming month only)

##  Holiday Management

### Public Holidays Table Creation and Insert holiday data

**Purpose:** Store public holidays to enforce operation restrictions

### Verification Query

```sql
-- Verify holidays are loaded
SELECT holiday_id, holiday_date, holiday_name 
FROM public_holidays 
ORDER BY holiday_date;


(./images/Screenshot1.png)<img width="782" height="656" alt="phase VIIscr1" src="https://github.com/user-attachments/assets/a71a296b-8ea3-4029-97f5-6332ac5daa65" />



**Result:**
-  5 public holidays loaded
- Dates cover upcoming month
-  Unique constraint on holiday_date enforced


## Audit Log Table

### Table Creation and Create Performance Indexes

**Purpose:** Comprehensive audit trail for all database operations


(screenshots/01_audit_table_creation.png)<img width="740" height="569" alt="phase VII scr2" src="https://github.com/user-attachments/assets/1ada1205-c530-4bd1-82c2-943ab3c01c9e" />


**Features Implemented:**
-  Auto-incrementing audit_id
-  Tracks table name and operation type
-  Captures user name and date/day
-  Records operation status (ALLOWED/DENIED)
-  Stores error messages for denied operations
-  Captures IP address and session ID
-  Preserves old and new values as CLOB
-  Check constraints enforce valid values
-  Performance indexes on key columns


##  Audit Logging Function

### Function Implementation

**Purpose:** Autonomous function to log all operations regardless of transaction outcome

(screenshots/02_audit_function.png)<img width="735" height="688" alt="phase VII scr3" src="https://github.com/user-attachments/assets/dac3eae3-8472-4da6-8884-987dad6f70fa" />


**Key Features:**
-  **PRAGMA AUTONOMOUS_TRANSACTION** - Logs persist even if main transaction rolls back
-  **Context Capture** - Retrieves IP_ADDRESS and SESSIONID from system
-  **Error Handling** - Gracefully handles context retrieval failures
-  **Parameter Flexibility** - Optional parameters for error messages and data changes
-  **Return Value** - Returns audit_id for reference
-  **Independent Commit** - Audit log commits separately from main transaction

**Function Parameters:**
| Parameter | Type | Required | Purpose |
|-----------|------|----------|---------|
| p_table_name | VARCHAR2 | Yes | Table being accessed |
| p_operation | VARCHAR2 | Yes | INSERT/UPDATE/DELETE |
| p_status | VARCHAR2 | Yes | ALLOWED/DENIED |
| p_error_msg | VARCHAR2 | No | Error message if denied |
| p_old_values | CLOB | No | Previous data state |
| p_new_values | CLOB | No | New data state |

---

## Restriction Check Function

### Function Implementation
**Business Logic:**


┌─────────────────────────────────────────┐
│     check_operation_allowed()           │
├─────────────────────────────────────────┤
│ 1. Get current day of week              │
│ 2. Check if today is a holiday          │
│                                          │
│ IF Monday-Friday:                        │
│    → RETURN "DENIED: WEEKDAY"            │
│                                          │
│ IF Public Holiday:                       │
│    → RETURN "DENIED: HOLIDAY"            │
│                                          │
│ ELSE (Weekend, not holiday):             │
│    → RETURN "ALLOWED"                    │
└─────────────────────────────────────────┘
```

**Function Returns:**
- `"ALLOWED"` - Operation can proceed
- `"DENIED: ... on WEEKDAYS (MONDAY)"` - Blocked due to weekday
- `"DENIED: ... on PUBLIC HOLIDAY (Christmas Day)"` - Blocked due to holiday

---

## S Simple Triggers

### Trigger on USERS Table , Trigger on SCANS Table and Compound Trigger on DISEASE_PROFILES

**Purpose:** Enforce operation restrictions on USERS table
**Purpose:** Enforce operation restrictions on SCANS table
**Purpose:** Demonstrate advanced trigger with multiple timing points

(screenshots/03_trigger_test_denied.png)<img width="1131" height="686" alt="phase VII scr6" src="https://github.com/user-attachments/assets/7a1b869d-f611-4b62-9661-bed11c72502c" />


**Test Result:**
-  INSERT attempt on USERS table on Monday
-  Trigger blocked operation with error ORA-20002
-  Error message: "DENIED: INSERT on USERS NOT ALLOWED on WEEKDAYS (MONDAY)"
-  Audit log captured the denied attempt
-  Transaction rolled back automatically

**Compound Trigger Features:**
-  **BEFORE STATEMENT** - Executes once before the entire operation
-  **AFTER STATEMENT** - Executes once after the entire operation
-  **Shared State** - Can maintain variables across timing points
-  **Performance** - More efficient than multiple separate triggers
-  **Logging** - Provides operation start/end timestamps

**Structure:**
```
COMPOUND TRIGGER trg_disease_compound
├── BEFORE STATEMENT
│   └── Log operation start
│
├── BEFORE EACH ROW (optional)
│   └── Row-level validations
│
├── AFTER EACH ROW (optional)
│   └── Row-level audit
│
└── AFTER STATEMENT
    └── Log operation completion
`


## All Triggers

(screenshots/05_triggers_list.png)<img width="860" height="475" alt="phase VII scr7" src="https://github.com/user-attachments/assets/bd35fc86-e3d6-4ff1-af25-810030e7982c" />


### Implemented Triggers

| Trigger Name | Table | Type | Purpose |
|--------------|-------|------|---------|
| **TRG_DISEASE_COMPOUND** | DISEASE_PROFILES | COMPOUND | Advanced logging with timing |
| **TRG_SCANS_RESTRICT** | SCANS | BEFORE EACH ROW | Weekday/holiday restrictions |
| **TRG_USERS_RESTRICT** | USERS | BEFORE EACH ROW | Weekday/holiday restrictions |

**Coverage:**
-  All critical tables protected
-  INSERT, UPDATE, DELETE monitored
-  Weekday restrictions enforced
-  Holiday restrictions enforced
-  All operations logged

---

## Testing Requirements & Results

###  INSERT on Weekday (DENIED)  and **Audit Log Query:**
(screenshots/03_trigger_test_denied.png)<img width="867" height="605" alt="phase VII scr5" src="https://github.com/user-attachments/assets/01d2b1a7-5eb1-4f84-bc0f-48fe7f90d9c5" />

**Expected Result:**
- Operation blocked on Monday-Friday
- Error: ORA-20002
- Message: "DENIED: INSERT on USERS NOT ALLOWED on WEEKDAYS (MONDAY)"

**Status:** PASSED
-  INSERT blocked on Monday
-  Error ORA-20002 raised
-  Clear error message displayed
-  Audit log captured attempt
**Result:**
```
AUDIT_ID  TABLE_NAME  OPERATION_TYPE  STATUS   OPERATION_DAY  ERROR_MESSAGE
--------  ----------  --------------  -------  -------------  -------------
1         USERS       INSERT          DENIED   MONDAY         DENIED: INSERT on USERS NOT ALLOWED on WEEKDAYS (MONDAY)

### Test Case 2: INSERT on Weekend (ALLOWED) 

**Test Script:**


**Expected Result:**
- Operation succeeds on Saturday/Sunday
- No error raised
- Message: "SUCCESS: Operation Allowed"

**Status:** PASSED
-  INSERT successful on Saturday
-  No error raised
-  Audit log shows status='ALLOWED'

**Audit Log:**
```
AUDIT_ID  TABLE_NAME  OPERATION_TYPE  STATUS   OPERATION_DAY  ERROR_MESSAGE
--------  ----------  --------------  -------  -------------  -------------
2         USERS       INSERT          ALLOWED  SATURDAY       NULL
```

---

### Test Case 3: INSERT on Public Holiday (DENIED) 

**Test Script:**
```sql
-- Test on December 25, 2025 (Christmas Day)
SET SERVEROUTPUT ON;
BEGIN
    DBMS_OUTPUT.PUT_LINE('Testing INSERT on PUBLIC HOLIDAY...');
    INSERT INTO users (user_id, name, email, password, role)
    VALUES (user_seq.NEXTVAL, 'Test Holiday', 'holiday@test.com', 'pass', 'farmer');
    COMMIT;
    DBMS_OUTPUT.PUT_LINE('SUCCESS: Allowed');
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('DENIED: ' || SQLERRM);
        ROLLBACK;
END;
/
```

**Expected Result:**
- Operation blocked on public holiday
- Error: ORA-20002
- Message: "DENIED: INSERT on USERS NOT ALLOWED on PUBLIC HOLIDAY (Christmas Day)"

**Status:**  PASSED
-  INSERT blocked on holiday
-  Error raised with holiday name
-  Audit log captured with holiday details

**Audit Log:**
```
AUDIT_ID  TABLE_NAME  OPERATION_TYPE  STATUS   OPERATION_DAY  ERROR_MESSAGE
--------  ----------  --------------  -------  -------------  -------------
3         USERS       INSERT          DENIED   THURSDAY       DENIED: INSERT on USERS NOT ALLOWED on PUBLIC HOLIDAY (Christmas Day)
```

---

### Test Case 4: Audit Log Captures All Attempts 

**Verification Query:**
```sql
SELECT 
    audit_id,
    table_name,
    operation_type,
    user_name,
    TO_CHAR(operation_date, 'DD-MON-YYYY HH24:MI:SS') as operation_time,
    operation_day,
    status,
    error_message,
    ip_address,
    session_id
FROM audit_log
ORDER BY audit_id DESC;
```

**Expected Behavior:**
- All INSERT/UPDATE/DELETE attempts logged
- Both ALLOWED and DENIED operations captured
- User context (name, IP, session) recorded
- Timestamps accurate

**Status:**  PASSED
-  All operations logged (3/3)
-  User name captured (DOCILE)
- IP address recorded
-  Session ID captured
-  Timestamps accurate
-  Status correctly marked

---

### Test Case 5: Error Messages Are Clear 

**Review Error Messages:**

| Test | Error Message | Clarity Score |
|------|---------------|---------------|
| Weekday | "DENIED: INSERT on USERS NOT ALLOWED on WEEKDAYS (MONDAY)" |  Excellent |
| Holiday | "DENIED: INSERT on USERS NOT ALLOWED on PUBLIC HOLIDAY (Christmas Day)" | Excellent |
| Weekend | No error (operation allowed) |  N/A |

**Error Message Components:**
1.  **Action** - "DENIED: INSERT"
2.  **Target** - "on USERS"
3.  **Reason** - "NOT ALLOWED on WEEKDAYS"
4.  **Details** - "(MONDAY)" or "(Christmas Day)"

**Status:**  PASSED
-  Messages are descriptive
-  Include operation type and table
-  Specify exact reason (weekday/holiday)
-  Include day name or holiday name

---

### Test Case 6: User Info Properly Recorded 

**Verification Query:**
```sql
SELECT 
    user_name,
    ip_address,
    session_id,
    COUNT(*) as operation_count
FROM audit_log
GROUP BY user_name, ip_address, session_id;
```

**Expected Data:**
- User name from database session
- IP address from SYS_CONTEXT
- Session ID from SYS_CONTEXT

**Status:**  PASSED
- User name: "DOCILE" (correct database user)
-  IP address: Retrieved from context
-  Session ID: Retrieved from context
-  Handles NULL gracefully if context unavailable



**Result on Weekday:**  DENIED
**Result on Weekend:**  ALLOWED

---

### Test DELETE Operation

```sql
BEGIN
    DELETE FROM scans 
    WHERE scan_id = 1;
    COMMIT;
EXCEPTION
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('DENIED: ' || SQLERRM);
        ROLLBACK;
END;
/
```

**Result on Weekday:**  DENIED
**Result on Weekend:**  ALLOWED

---

## Testing Summary

| Test Case | Expected | Actual | Status |
|-----------|----------|--------|--------|
| 1. INSERT on Weekday | DENIED | DENIED |  PASSED |
| 2. INSERT on Weekend | ALLOWED | ALLOWED |  PASSED |
| 3. INSERT on Holiday | DENIED | DENIED |  PASSED |
| 4. Audit Log Captures | All logged | All logged |  PASSED |
| 5. Error Messages | Clear | Clear |  PASSED |
| 6. User Info Recorded | Complete | Complete |  PASSED |
| 7. UPDATE on Weekday | DENIED | DENIED |  PASSED |
| 8. DELETE on Weekday | DENIED | DENIED | PASSED |

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    USER APPLICATION                          │
└────────────────────┬────────────────────────────────────────┘
                     │
                     │ DML Operation (INSERT/UPDATE/DELETE)
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                 TRIGGER (trg_users_restrict)                 │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ 1. Determine operation type (INSERT/UPDATE/DELETE)   │  │
│  │ 2. Call check_operation_allowed()                    │  │
│  │ 3. If DENIED:                                         │  │
│  │    - Log to audit_log (autonomous)                   │  │
│  │    - RAISE_APPLICATION_ERROR                         │  │
│  │ 4. If ALLOWED:                                        │  │
│  │    - Log to audit_log (autonomous)                   │  │
│  │    - Allow operation to proceed                      │  │
│  └──────────────────────────────────────────────────────┘  │
└────────────┬────────────────────────────┬───────────────────┘
             │                            │
             │ check_operation_allowed()  │ log_audit_event()
             ▼                            ▼
┌────────────────────────┐   ┌──────────────────────────────┐
│  RESTRICTION FUNCTION  │   │   AUDIT LOGGING FUNCTION     │
│  ┌──────────────────┐  │   │  ┌────────────────────────┐ │
│  │ Check day of week │  │   │  │ PRAGMA AUTONOMOUS      │ │
│  │ Check holidays    │  │   │  │ Get IP/Session         │ │
│  │ Return ALLOWED or │  │   │  │ INSERT audit_log       │ │
│  │ DENIED with msg   │  │   │  │ COMMIT independently   │ │
│  └──────────────────┘  │   │  └────────────────────────┘ │
└────────────────────────┘   └──────────────────────────────┘
             │                            │
             │ Query                      │ Insert
             ▼                            ▼
┌────────────────────────┐   ┌──────────────────────────────┐
│   PUBLIC_HOLIDAYS      │   │       AUDIT_LOG              │
│  ┌──────────────────┐  │   │  ┌────────────────────────┐ │
│  │ Christmas Day    │  │   │  │ All operations logged  │ │
│  │ New Year         │  │   │  │ Status: ALLOWED/DENIED │ │
│  │ Genocide Day     │  │   │  │ User context captured  │ │
│  └──────────────────┘  │   │  └────────────────────────┘ │
└────────────────────────┘   └──────────────────────────────┘
```

---

## Key Implementation Highlights

### 1. Autonomous Transactions 
```sql
PRAGMA AUTONOMOUS_TRANSACTION;
```
- Audit logs persist even if main transaction fails
- Independent commit/rollback
- Ensures audit integrity

### 2. System Context Capture 
```sql
SYS_CONTEXT('USERENV', 'IP_ADDRESS')
SYS_CONTEXT('USERENV', 'SESSIONID')
```
- Retrieves client IP address
- Captures database session ID
- Enables security tracking

### 3. CLOB for Data History 
```sql
old_values CLOB
new_values CLOB
```
- Stores complete before/after state
- Supports large data changes
- Enables change tracking and rollback

### 4. Check Constraints 
```sql
CHECK (operation_type IN ('INSERT', 'UPDATE', 'DELETE'))
CHECK (status IN ('ALLOWED', 'DENIED'))
```
- Enforces data integrity
- Prevents invalid values
- Database-level validation

---

## Security Benefits

1. **Compliance** 
   - Complete audit trail for regulatory requirements
   - Immutable log (autonomous transactions)
   - Timestamp and user tracking

2. **Access Control** 
   - Prevents unauthorized weekend work
   - Respects public holidays
   - Clear error messages for users

3. **Forensics** 
   - Track who attempted what operation
   - When and from where (IP address)
   - What data would have changed

4. **Accountability** 
   - User name captured automatically
   - Session tracking
   - Cannot be bypassed

---

## Performance Considerations

### Indexes Created 
```sql
CREATE INDEX idx_audit_date ON audit_log(operation_date);
CREATE INDEX idx_audit_user ON audit_log(user_name);
CREATE INDEX idx_audit_status ON audit_log(status);
CREATE INDEX idx_audit_table ON audit_log(table_name);
```

**Benefits:**
- Fast queries by date range
- Quick user activity lookups
- Efficient status filtering
- Table-specific audits

### Autonomous Transaction Impact
- **Pros:** Audit integrity, independent commits
- **Cons:** Slight performance overhead
- **Mitigation:** Lightweight function, minimal data

---

## Maintenance & Monitoring

### Monitor Audit Log Growth
```sql
SELECT 
    COUNT(*) as total_records,
    ROUND(SUM(DBMS_LOB.GETLENGTH(old_values))/1024/1024, 2) as old_values_mb,
    ROUND(SUM(DBMS_LOB.GETLENGTH(new_values))/1024/1024, 2) as new_values_mb
FROM audit_log;
```

### Archive Old Audit Records
```sql
-- Archive records older than 1 year
CREATE TABLE audit_log_archive AS
SELECT * FROM audit_log
WHERE operation_date < ADD_MONTHS(SYSDATE, -12);

DELETE FROM audit_log
WHERE operation_date < ADD_MONTHS(SYSDATE, -12);
```

### Add New Holidays
```sql
INSERT INTO public_holidays (holiday_date, holiday_name)
VALUES (TO_DATE('2026-07-04', 'YYYY-MM-DD'), 'Liberation Day');
```





