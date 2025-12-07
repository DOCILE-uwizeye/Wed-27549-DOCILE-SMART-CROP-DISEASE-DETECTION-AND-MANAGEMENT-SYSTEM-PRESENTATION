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
