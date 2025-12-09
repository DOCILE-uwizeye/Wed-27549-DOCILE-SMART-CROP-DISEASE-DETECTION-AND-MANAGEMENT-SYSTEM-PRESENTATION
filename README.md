# Smart Crop Disease Detection and Management System
- **Name:** Docile - Uwizeye
- **Student ID:** 27549
- **Group:** Wednesday
- **Institution:** Adventist University of Central Africa (AUCA)
- **Course:** Database Development with PL/SQL (INSY 8311)
- **Lecturer:** Eric Maniraguha

## Problem Statement

Farmers struggle to identify crop diseases early, leading to reduced yields and significant crop losses. Traditional diagnosis methods are slow, require expert knowledge, and are not always accessible to small-scale farmers. This Smart Crop Disease Detection and Management System provides instant disease detection through AI-powered image analysis, helping farmers take timely action to protect their crops and improve agricultural productivity.

## Key Objectives

1. **Enable Quick Disease Detection** - Provide instant crop disease identification through image upload and automated analysis

2. **Comprehensive Disease Information** - Maintain a database of 54+ disease profiles with symptoms, causes, treatments, and prevention strategies

3. **Treatment Recommendations** - Deliver personalized, actionable recommendations based on detected diseases to help farmers respond effectively

4. **Historical Tracking** - Store and track scan history over time, enabling farmers to monitor crop health trends and patterns

5. **Multi-Role Support** - Support different user types (farmers, agronomists, administrators) with appropriate access levels and functionality

6. **Data-Driven Insights** - Provide analytics and business intelligence capabilities through views, reports, and statistical analysis

7. **Security & Compliance** - Implement comprehensive auditing, operation restrictions, and security controls to protect data integrity

8. **Scalability & Performance** - Design a robust Oracle PL/SQL database system with optimized queries, indexes, and efficient data structures

# Phase II: Business Process Modeling
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




# Phase VI: Database Interaction & Transactions

This phase validates all PL/SQL operations implemented in the Smart Crop Disease Detection & Management System.  
The tests include procedures, functions, packages, cursors, and views.  
All results and screenshots are included below.

---

##  **Test 1: Register User & Record Scan**

### **Screenshot**
![Register User & Record Scan](./screenshots/phase_VI_scre.png)<img width="885" height="481" alt="phase VI  scre" src="https://github.com/user-attachments/assets/ec184b95-056f-4246-9de6-7874be946f0f" />


### **Results**
- User registration executed successfully  
- Scan recording completed successfully  
- No errors encountered during procedure execution  

---

## ✅ **Test 2: Testing Functions & Package Execution**

### **Screenshot**
![Functions & Package](./screenshots/phase_VI_scre2.png)<img width="891" height="647" alt="phase VI scre2" src="https://github.com/user-attachments/assets/d1586ec0-38c8-4161-ae4c-c67ffce65469" />


### **Results**
- All PL/SQL functions returned correct values  
- Email validation, detection rate, and confidence calculations working  
- Package operations (PKG_USER_MGMT / PKG_DISEASE_MGMT) executed successfully  
- No errors returned  

---

## ✅ **Test 3: Cursor, Views, User Rankings & Monthly Stats**

### **Screenshot**
![Cursor and Views](./screenshots/phase_VI_scre4.png)<img width="1306" height="695" alt="phase VI scre4" src="https://github.com/user-attachments/assets/56a3426e-95a4-4d4b-914b-56b794464b03" />


### **Cursor Output**
Cursor for displaying user scan history executed successfully:  
- Returned all associated scans  
- Displayed disease, confidence, and dates correctly  

### **Views Tested**

#### **1. User Rankings View**
Executed query:
```sql
SELECT * FROM vw_user_rankings WHERE ROWNUM < 5;



# PHASE VII: Advanced Programming & Auditing
**Objective:** Implement triggers, business rules, and comprehensive auditing.  
This phase ensures secure operations, strict restriction checks, and full system auditing.

---

## 🔒 Critical Business Rule  
Employees are **NOT allowed** to INSERT, UPDATE, or DELETE on:

- **WEEKDAYS (Monday–Friday)**
- **PUBLIC HOLIDAYS** (Upcoming month only)

These rules are enforced automatically using PL/SQL functions and triggers.

---

# 1. Holiday Management

##  Public Holidays Table + Insert Data  
**Purpose:** Store holiday dates used to block operations.

### 📷 Screenshot  
![Public Holidays](./images/phase%20VIIscr1.png)<img width="782" height="656" alt="phase VIIscr1" src="https://github.com/user-attachments/assets/d187bc0f-7455-4edc-bbca-b08cf8ae7bf0" />


###  Result
- 5 public holidays successfully inserted  
- All dates fall within the upcoming month  
- Unique constraint on `holiday_date` enforced  

---

# 2. Audit Log Table

##  Table Creation + Performance Indexes  
**Purpose:** Maintain a complete audit trail for ALL database operations.

###  Screenshot  
![Audit Table Creation](screenshots/01_audit_table_creation.png)

###  Features Implemented
- Auto-incrementing `audit_id`
- Tracks:
  - Table name  
  - Operation type (INSERT/UPDATE/DELETE)  
  - Username  
  - Timestamp and day  
  - Operation status (**ALLOWED / DENIED**)  
  - Error message (if denied)  
- Records old and new values (CLOB)  
- Stores IP address and session ID  
- Check constraints for valid audit values  
- Indexes created for performance:  
  - `operation_date`  
  - `table_name`  
  - `username`

---

# 3. Audit Logging Function

##  Function Implementation  
**Purpose:** Log every operation using an autonomous transaction.

###  Screenshot  
![Audit Function](screenshots/02_audit_function.png)

###  Key Features
- Uses **PRAGMA AUTONOMOUS_TRANSACTION**
- Logs persist even if the main transaction rolls back  
- Captures IP address, session ID, and context values  
- Handles exceptions gracefully  
- Accepts optional parameters  
- Returns generated `audit_id`  
- Independently commits audit entries  

###  Function Parameters

| Parameter | Type | Required | Purpose |
|-----------|------|----------|---------|
| p_table_name | VARCHAR2 | Yes | Table being accessed |
| p_operation | VARCHAR2 | Yes | INSERT/UPDATE/DELETE |
| p_status | VARCHAR2 | Yes | ALLOWED or DENIED |
| p_error_msg | VARCHAR2 | No | Error details if blocked |
| p_old_values | CLOB | No | Data before change |
| p_new_values | CLOB | No | Data after change |

---

# 4 Restriction Check Function

##  Business Logic Flow



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
    
### Test Case : INSERT on Weekend (ALLOWED) 
** Result:**
- Operation succeeds on Saturday/Sunday
- No error raised
- Message: "SUCCESS: Operation Allowed"

**Status:** PASSED
-  INSERT successful on Saturday
-  No error raised
-  Audit log shows status='ALLOWED'

### Test Case : INSERT on Public Holiday (DENIED) 
**Result:**
- Operation blocked on public holiday
- Error: ORA-20002
- Message: "DENIED: INSERT on USERS NOT ALLOWED on PUBLIC HOLIDAY (Christmas Day)"

**Status:**  PASSED
-  INSERT blocked on holiday
-  Error raised with holiday name
-  Audit log captured with holiday details

### Test Case : Audit Log Captures All Attempts 
**Behavior:**
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



### Test Case : Error Messages Are Clear 

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
-  Include day name or holiday n

### Test Case : User Info Properly Recorded 
** Data:**
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

### Test DELETE Operation
**Result on Weekday:**  DENIED
**Result on Weekend:**  ALLOWED

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

# Architecture Diagram
        
