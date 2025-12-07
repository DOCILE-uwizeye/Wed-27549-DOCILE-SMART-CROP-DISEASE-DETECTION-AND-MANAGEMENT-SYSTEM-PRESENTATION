# Phase II: Business Process Modeling
## Project: Smart Crop Disease Detection & Management System

---

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


---

## 1. Database Creation Scripts

### **Pluggable Database Creation**
```sql
DROP PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db 
INCLUDING DATAFILES;

CREATE PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
ADMIN USER crop_admin IDENTIFIED BY docile
FILE_NAME_CONVERT = ('pdbseed', 'wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db');

ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db OPEN;

ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db SAVE STATE;
```

### **Database Verification**
```sql
SELECT name, open_mode FROM v$pdbs;

ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

SHOW CON_NAME;
```

---

## 2. Tablespace Configuration

### **Data Tablespace**
```sql
CREATE TABLESPACE crop_data_ts
DATAFILE 'crop_data_ts.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 10M
MAXSIZE UNLIMITED
EXTENT MANAGEMENT LOCAL
SEGMENT SPACE MANAGEMENT AUTO;
```

### **Index Tablespace**
```sql
CREATE TABLESPACE crop_index_ts
DATAFILE 'crop_index_ts.dbf'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED
EXTENT MANAGEMENT LOCAL
SEGMENT SPACE MANAGEMENT AUTO;
```

### **Temporary Tablespace**
```sql
CREATE TEMPORARY TABLESPACE crop_temp_ts
TEMPFILE 'crop_temp_ts.tmp'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED;
```

### **Tablespace Verification**
```sql
SELECT tablespace_name, status, contents 
FROM dba_tablespaces 
WHERE tablespace_name LIKE 'CROP%';
```

---

## 3. User Setup Documentation

### **Privileges Granted**
```sql
GRANT CREATE SESSION TO crop_admin;
GRANT CREATE TABLE TO crop_admin;
GRANT CREATE VIEW TO crop_admin;
GRANT CREATE PROCEDURE TO crop_admin;
GRANT CREATE SEQUENCE TO crop_admin;
GRANT CREATE TRIGGER TO crop_admin;
GRANT CREATE TYPE TO crop_admin;
GRANT CREATE SYNONYM TO crop_admin;
GRANT UNLIMITED TABLESPACE TO crop_admin;
```

### **Tablespace Assignment**
```sql
ALTER USER crop_admin
DEFAULT TABLESPACE crop_data_ts
TEMPORARY TABLESPACE crop_temp_ts
QUOTA UNLIMITED ON crop_data_ts
QUOTA UNLIMITED ON crop_index_ts;
```

### **User Verification**
```sql
SELECT username, default_tablespace, temporary_tablespace
FROM dba_users
WHERE username = 'CROP_ADMIN';
```

---

## 4. Memory Configuration

### **PGA Configuration**
```sql
ALTER SYSTEM SET pga_aggregate_target = 256M SCOPE=BOTH;
```

### **Memory Verification**
```sql
SELECT name, value
FROM v$parameter
WHERE name IN ('sga_target', 'pga_aggregate_target');
```

### **Archive Log Status**
```sql
ARCHIVE LOG LIST;
```

---

## 5. Database Setup Summary

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
(https://github.com/yourrepo/.../image.png)![Uploading phase V scr1.png…]()



CREATE SEQUENCE users_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;
```

**Table Description:**
```sql
DESC users;
```

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
```sql
CREATE TABLE crop_types (
    crop_id NUMBER(10) PRIMARY KEY,
    crop_name VARCHAR2(100) NOT NULL UNIQUE,
    scientific_name VARCHAR2(150),
    growing_season VARCHAR2(50),
    created_date DATE DEFAULT SYSDATE
);

CREATE SEQUENCE crop_types_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;
```

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
```sql
CREATE TABLE disease_profiles (
    disease_id NUMBER(10) PRIMARY KEY,
    disease_name VARCHAR2(150) NOT NULL,
    symptoms VARCHAR2(1000),
    causes VARCHAR2(1000),
    treatment VARCHAR2(2000),
    prevention VARCHAR2(2000),
    severity_level VARCHAR2(20) CHECK (severity_level IN ('low', 'medium', 'high', 'critical')),
    created_date DATE DEFAULT SYSDATE
);

CREATE SEQUENCE disease_profiles_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

CREATE INDEX idx_disease_name ON disease_profiles(disease_name);
```

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

---

### Table 4: RECOMMENDATIONS

**Purpose:** Store treatment recommendations for each disease

**SQL Creation Script:**
```sql
CREATE TABLE recommendations (
    rec_id NUMBER(10) PRIMARY KEY,
    disease_id NUMBER(10) NOT NULL,
    recommendation VARCHAR2(2000) NOT NULL,
    rec_type VARCHAR2(50) CHECK (rec_type IN ('chemical', 'organic', 'cultural', 'biological')),
    created_date DATE DEFAULT SYSDATE,
    CONSTRAINT fk_rec_disease FOREIGN KEY (disease_id) 
        REFERENCES disease_profiles(disease_id) ON DELETE CASCADE
);

CREATE SEQUENCE recommendations_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

CREATE INDEX idx_rec_disease ON recommendations(disease_id);
```

**Column Details:**

| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| rec_id | NUMBER(10) | PRIMARY KEY | Unique identifier |
| disease_id | NUMBER(10) | NOT NULL, FK | References disease_profiles |
| recommendation | VARCHAR2(2000) | NOT NULL | Recommendation text |
| rec_type | VARCHAR2(50) | CHECK | Type (chemical/organic/cultural/biological) |
| created_date | DATE | DEFAULT SYSDATE | Record creation date |

---

### Table 5: SCANS

**Purpose:** Store disease detection scan records

**SQL Creation Script:**
```sql
CREATE TABLE scans (
    scan_id NUMBER(10) PRIMARY KEY,
    user_id NUMBER(10) NOT NULL,
    image_path VARCHAR2(500) NOT NULL,
    detected_disease NUMBER(10),
    confidence_score NUMBER(5,2) CHECK (confidence_score BETWEEN 0 AND 100),
    scan_date DATE DEFAULT SYSDATE,
    scan_status VARCHAR2(20) CHECK (scan_status IN ('pending', 'completed', 'failed')),
    crop_id NUMBER(10),
    CONSTRAINT fk_scan_user FOREIGN KEY (user_id) 
        REFERENCES users(user_id) ON DELETE CASCADE,
    CONSTRAINT fk_scan_disease FOREIGN KEY (detected_disease) 
        REFERENCES disease_profiles(disease_id) ON DELETE SET NULL,
    CONSTRAINT fk_scan_crop FOREIGN KEY (crop_id) 
        REFERENCES crop_types(crop_id) ON DELETE SET NULL
);

CREATE SEQUENCE scans_seq START WITH 1 INCREMENT BY 1 NOCACHE NOCYCLE;

CREATE INDEX idx_scan_user ON scans(user_id);
CREATE INDEX idx_scan_disease ON scans(detected_disease);
CREATE INDEX idx_scan_date ON scans(scan_date);
CREATE INDEX idx_scan_crop ON scans(crop_id);
```

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
INSERT INTO users VALUES (users_seq.NEXTVAL, 'John Mugisha', 'john.mugisha@farm.rw', 'hashed_pwd_123', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Mary Uwase', 'mary.uwase@farm.rw', 'hashed_pwd_456', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Peter Nkusi', 'peter.nkusi@farm.rw', 'hashed_pwd_789', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Alice Mukamana', 'alice.m@farm.rw', 'hashed_pwd_101', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'David Kayitare', 'david.k@farm.rw', 'hashed_pwd_102', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Sarah Iradukunda', 'sarah.i@farm.rw', 'hashed_pwd_103', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'James Niyonzima', 'james.n@farm.rw', 'hashed_pwd_104', 'farmer', SYSDATE);
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Rose Mutesi', 'rose.m@farm.rw', 'hashed_pwd_105', 'farmer', SYSDATE);

-- Admin
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Grace Kamali', 'grace.kamali@auca.ac.rw', 'hashed_pwd_admin', 'admin', SYSDATE);

-- Agronomist
INSERT INTO users VALUES (users_seq.NEXTVAL, 'Dr. Emmanuel Habimana', 'e.habimana@rab.gov.rw', 'hashed_pwd_agro', 'agronomist', SYSDATE);

COMMIT;
```

---

### Sample Data: CROP_TYPES Table

**Total Records Inserted:** 10
```sql
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Maize (Corn)', 'Zea mays', 'Summer', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Rice', 'Oryza sativa', 'Summer/Monsoon', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Wheat', 'Triticum aestivum', 'Winter', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Beans', 'Phaseolus vulgaris', 'Summer', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Cassava', 'Manihot esculenta', 'Year-round', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Potato', 'Solanum tuberosum', 'Spring/Fall', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Tomato', 'Solanum lycopersicum', 'Summer', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Banana', 'Musa species', 'Year-round', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Coffee', 'Coffea arabica', 'Year-round', SYSDATE);
INSERT INTO crop_types VALUES (crop_types_seq.NEXTVAL, 'Tea', 'Camellia sinensis', 'Year-round', SYSDATE);

COMMIT;
```

---

### Sample Data: DISEASE_PROFILES Table

**Total Records Inserted:** 54
```sql
-- Major crop diseases (showing first 10 of 54)
INSERT INTO disease_profiles VALUES (disease_profiles_seq.NEXTVAL, 'Maize Streak Virus', 'Yellow streaks on leaves, stunted growth', 'Leafhopper-transmitted virus', 'Remove infected plants, control leafhoppers with insecticides', 'Use resistant varieties, early planting', 'high', SYSDATE);

INSERT INTO disease_profiles VALUES (disease_profiles_seq.NEXTVAL, 'Bacterial Wilt (Beans)', 'Wilting leaves, yellowing, plant death', 'Ralstonia bacteria in soil', 'Remove infected plants, soil solarization', 'Crop rotation, disease-free seeds', 'critical', SYSDATE);

INSERT INTO disease_profiles VALUES (disease_profiles_seq.NEXTVAL, 'Rice Blast', 'Diamond lesions on leaves, neck rot', 'Magnaporthe fungus, high humidity', 'Apply fungicides like tricyclazole', 'Resistant varieties, proper spacing', 'high', SYSDATE);

-- ... (44 more disease records follow same pattern)

COMMIT;
```

---

### Sample Data: SCANS Table

**Total Records Inserted:** 25+
```sql
-- Scans by different users
INSERT INTO scans VALUES (scans_seq.NEXTVAL, 1, '/uploads/scans/2025/12/scan_001.jpg', 1, 87.5, SYSDATE-30, 'completed', 1);
INSERT INTO scans VALUES (scans_seq.NEXTVAL, 1, '/uploads/scans/2025/12/scan_002.jpg', 11, 92.3, SYSDATE-28, 'completed', 1);
INSERT INTO scans VALUES (scans_seq.NEXTVAL, 2, '/uploads/scans/2025/12/scan_006.jpg', 10, 91.2, SYSDATE-29, 'completed', 4);
INSERT INTO scans VALUES (scans_seq.NEXTVAL, 3, '/uploads/scans/2025/12/scan_011.jpg', 3, 94.5, SYSDATE-31, 'completed', 2);

-- Failed scans (edge cases)
INSERT INTO scans VALUES (scans_seq.NEXTVAL, 1, '/uploads/scans/2025/12/scan_004.jpg', NULL, 45.2, SYSDATE-20, 'failed', 1);

-- ... (20 more scan records)

COMMIT;
```

---

### Sample Data: RECOMMENDATIONS Table

**Total Records Inserted:** 30
```sql
-- Recommendations for Maize Streak Virus (disease_id=1)
INSERT INTO recommendations VALUES (recommendations_seq.NEXTVAL, 1, 'Apply systemic insecticides to control leafhopper vectors during early crop growth stages', 'chemical', SYSDATE);
INSERT INTO recommendations VALUES (recommendations_seq.NEXTVAL, 1, 'Plant maize intercropped with legumes to reduce leafhopper populations naturally', 'cultural', SYSDATE);
INSERT INTO recommendations VALUES (recommendations_seq.NEXTVAL, 1, 'Use neem-based organic sprays to repel leafhopper insects', 'organic', SYSDATE);

-- ... (27 more recommendation records)

COMMIT;
```

---

##  DATA VALIDATION QUERIES

### Query 1: Count Records in All Tables
```sql
SELECT 'USERS' as table_name, COUNT(*) as row_count FROM users
UNION ALL
SELECT 'CROP_TYPES', COUNT(*) FROM crop_types
UNION ALL
SELECT 'DISEASE_PROFILES', COUNT(*) FROM disease_profiles
UNION ALL
SELECT 'SCANS', COUNT(*) FROM scans
UNION ALL
SELECT 'RECOMMENDATIONS', COUNT(*) FROM recommendations
ORDER BY table_name;
```

**Expected Output:**
```
TABLE_NAME           ROW_COUNT
-------------------- ----------
CROP_TYPES                   10
DISEASE_PROFILES             54
RECOMMENDATIONS              30
SCANS                        25
USERS                        10
```

---

### Query 2: Verify User Role Distribution
```sql
SELECT role, COUNT(*) as user_count
FROM users
GROUP BY role
ORDER BY role;
```

**Expected Output:**
```
ROLE                USER_COUNT
------------------- ----------
admin                        1
agronomist                   1
farmer                       8
```

---

### Query 3: Verify Disease Severity Levels
```sql
SELECT severity_level, COUNT(*) as disease_count
FROM disease_profiles
GROUP BY severity_level
ORDER BY severity_level;
```

**Expected Output:**
```
SEVERITY_LEVEL      DISEASE_COUNT
------------------- -------------
critical                        8
high                           30
low                             2
medium                         14
```

---

### Query 4: Verify Scan Status Distribution
```sql
SELECT scan_status, COUNT(*) as scan_count
FROM scans
GROUP BY scan_status
ORDER BY scan_status;
```

**Expected Output:**
```
SCAN_STATUS         SCAN_COUNT
------------------- ----------
completed                   22
failed                       3
```

---

### Query 5: Verify Recommendation Types
```sql
SELECT rec_type, COUNT(*) as rec_count
FROM recommendations
GROUP BY rec_type
ORDER BY rec_type;
```

---

### Query 6: Test Foreign Key Relationships
```sql
-- Verify all scans have valid user_ids
SELECT s.scan_id, s.user_id, u.name
FROM scans s
JOIN users u ON s.user_id = u.user_id
WHERE ROWNUM <= 5;
```

---

### Query 7: Test Join Operations (Multi-table)
```sql
-- Get scan details with user and disease information
SELECT 
    s.scan_id,
    u.name as user_name,
    c.crop_name,
    d.disease_name,
    s.confidence_score,
    s.scan_status,
    s.scan_date
FROM scans s
JOIN users u ON s.user_id = u.user_id
LEFT JOIN crop_types c ON s.crop_id = c.crop_id
LEFT JOIN disease_profiles d ON s.detected_disease = d.disease_id
WHERE ROWNUM <= 10
ORDER BY s.scan_date DESC;
```

---

### Query 8: Aggregate Query with GROUP BY
```sql
-- Count scans per user
SELECT 
    u.name,
    u.role,
    COUNT(s.scan_id) as total_scans,
    AVG(s.confidence_score) as avg_confidence,
    MAX(s.scan_date) as last_scan_date
FROM users u
LEFT JOIN scans s ON u.user_id = s.user_id
GROUP BY u.user_id, u.name, u.role
HAVING COUNT(s.scan_id) > 0
ORDER BY total_scans DESC;
```

---

### Query 9: Subquery Example
```sql
-- Find diseases with more than 2 recommendations
SELECT 
    d.disease_name,
    d.severity_level,
    (SELECT COUNT(*) FROM recommendations r WHERE r.disease_id = d.disease_id) as rec_count
FROM disease_profiles d
WHERE (SELECT COUNT(*) FROM recommendations r WHERE r.disease_id = d.disease_id) > 2
ORDER BY rec_count DESC;
```



### Query 10: Data Completeness Check
```sql
-- Check for NULL values in important columns
SELECT 
    'SCANS with NULL disease' as check_type,
    COUNT(*) as null_count
FROM scans
WHERE detected_disease IS NULL
UNION ALL
SELECT 
    'SCANS with low confidence',
    COUNT(*)
FROM scans
WHERE confidence_score < 50;
```


## SCREENSHOTS SECTION

### Screenshot 1: Table Structures
**File Location:** `screenshots/phase5/01_table_structures.png`

**Description:** Shows DESC command output for all 5 tables displaying columns, data types, and constraints



### Screenshot 2: Users Data Sample
**File Location:** `screenshots/phase5/02_users_data.png`

**Description:** Display first 10 user records




### Screenshot 3: Crop Types Data
**File Location:** `screenshots/phase5/03_crop_types_data.png`

**Description:** Display all crop types



### Screenshot 4: Disease Profiles Sample
**File Location:** `screenshots/phase5/04_disease_profiles.png`

**Description:** Display first 10 disease records



### Screenshot 5: Scans Data Sample
**File Location:** `screenshots/phase5/05_scans_data.png`

**Description:** Display scan records with details

### Screenshot 6: Recommendations Data
**File Location:** `screenshots/phase5/06_recommendations_data.png`

**Description:** Display recommendation records

### Screenshot 7: Data Validation - Row Counts
**File Location:** `screenshots/phase5/07_row_counts.png`

**Description:** Shows count of records in all tables



### Screenshot 8: Foreign Key Test
**File Location:** `screenshots/phase5/08_foreign_key_test.png`

**Description:** Shows join between scans, users, and diseases



### Screenshot 9: Aggregation Query
**File Location:** `screenshots/phase5/09_aggregation_query.png`

**Description:** Shows scans per user with statistics

### Screenshot 10: Edge Cases - Failed Scans
**File Location:** `screenshots/phase5/10_edge_cases.png`

**Description:** Shows failed scans and low confidence cases



