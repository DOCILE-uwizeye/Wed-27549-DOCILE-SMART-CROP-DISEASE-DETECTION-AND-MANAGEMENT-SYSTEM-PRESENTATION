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
 **PDB Name** wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db 
 **Admin Username**  crop_admin 
**Admin Password**  docile
 **Oracle Version** Oracle Database 21c Express Edition Release 21.0.0.0.0 
**CDB Container** CDB$ROOT



## 3. Pluggable Database Creation

### **Connect to Container Database & Create PDB**
```sql
-- Connect as SYSDBA
sqlplus / as sysdba

-- Set container to root
ALTER SESSION SET CONTAINER = CDB$ROOT;
SHOW CON_NAME;

-- Drop existing PDB (cleanup)
DROP PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
  INCLUDING DATAFILES;

-- Create new PDB
CREATE PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
  ADMIN USER crop_admin IDENTIFIED BY docile
  FILE_NAME_CONVERT = ('pdbseed', 'wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db');

-- Open PDB
ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db OPEN;


**Results:**
- `Pluggable database dropped.`
- `Pluggable database created.`
- `Pluggable database altered.`

(./images/PhaseIV_01.png)<img width="938" height="678" alt="phase IV scr1" src="https://github.com/user-attachments/assets/c6193309-7c97-4115-844d-1ee4609ecc04" />





### **Save PDB State & Verify**
```sql
-- Save state for auto-start
ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db SAVE STATE;

-- Verify PDB status
SELECT name, open_mode FROM v$pdbs;
```

**Verification Results:**
| NAME | OPEN_MODE |
|------|-----------|
| PDB$SEED | READ ONLY |
| AI_TO_DELETE_PDB_27292 | MOUNTED |
| DO_PDB_27549 | READ WRITE |
| AI_PDB_27292 | READ WRITE |
| WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB | READ WRITE |

(./images/PhaseIV_02.png)<img width="847" height="504" alt="phase IV scr2" src="https://github.com/user-attachments/assets/f1727b15-4c2a-4997-b3ad-d4f8b3de284d" />



## 4. Switch to PDB Context

### **Connect to PDB**
```sql
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;
SHOW CON_NAME;
```

**Result:** `WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB`

(./images/_PhaseIV_03.png)<img width="872" height="271" alt="phase IV scr3" src="https://github.com/user-attachments/assets/7219c699-2ecc-4ab6-ab77-470c917ebe04" />




## 5. User Privileges Configuration

### **Grant Super Admin Privileges**
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

**Privileges Granted:**
| Privilege | Purpose |
|-----------|---------|
| CREATE SESSION | Login access to database |
| CREATE TABLE | Create data tables |
| CREATE VIEW | Create database views |
| CREATE PROCEDURE | Create stored procedures |
| CREATE SEQUENCE | Create auto-increment sequences |
| CREATE TRIGGER | Create database triggers |
| CREATE TYPE | Create custom data types |
| CREATE SYNONYM | Create object aliases |
| UNLIMITED TABLESPACE | Unrestricted storage access |

**Result:** `Grant succeeded.` (for each privilege)

(./images/PhaseIV_04.png)<img width="471" height="535" alt="phase IV scr4" src="https://github.com/user-attachments/assets/39117ec1-ff6d-40fb-88aa-4fea70f97e9b" />




## 6. Tablespace Creation

### **Create Data Tablespace (crop_data_ts)**
```sql
CREATE TABLESPACE crop_data_ts
  DATAFILE 'crop_data_ts.dbf'
  SIZE 100M
  AUTOEXTEND ON
  NEXT 10M
  MAXSIZE UNLIMITED
  EXTENT MANAGEMENT LOCAL
  SEGMENT SPACE MANAGEMENT AUTO;


### **Create Index Tablespace (crop_index_ts)**
```sql
CREATE TABLESPACE crop_index_ts
  DATAFILE 'crop_index_ts.dbf'
  SIZE 50M
  AUTOEXTEND ON
  NEXT 5M
  MAXSIZE UNLIMITED
  EXTENT MANAGEMENT LOCAL
  SEGMENT SPACE MANAGEMENT AUTO;


### **Create Temporary Tablespace (crop_temp_ts)**
```sql
CREATE TEMPORARY TABLESPACE crop_temp_ts
  TEMPFILE 'crop_temp_ts.tmp'
  SIZE 50M
  AUTOEXTEND ON
  NEXT 5M
  MAXSIZE UNLIMITED;


**Tablespace Configuration:**
| Tablespace | Size | Autoextend | Next | Max Size |
|-----------|------|------------|------|----------|
| crop_data_ts | 100MB | ON | 10MB | UNLIMITED |
| crop_index_ts | 50MB | ON | 5MB | UNLIMITED |
| crop_temp_ts | 50MB | ON | 5MB | UNLIMITED |

**Result:** `Tablespace created.` (for each)

(./images/PhaseIV_05.png)<img width="404" height="526" alt="phase IV scr5" src="https://github.com/user-attachments/assets/e03da63e-2ea8-46f9-990d-8e622f5b63d7" />




## 7. Tablespace & User Verification

### **Verify Tablespaces**
```sql
SELECT tablespace_name, status, contents
FROM dba_tablespaces
WHERE tablespace_name LIKE 'CROP%';


**Tablespace Status:**
| TABLESPACE_NAME | STATUS | CONTENTS |
|----------------|--------|----------|
| CROP_DATA_TS | ONLINE | PERMANENT |
| CROP_INDEX_TS | ONLINE | PERMANENT |
| CROP_TEMP_TS | ONLINE | TEMPORARY |

### **Assign Tablespaces to User**
```sql
ALTER USER crop_admin
  DEFAULT TABLESPACE crop_data_ts
  TEMPORARY TABLESPACE crop_temp_ts
  QUOTA UNLIMITED ON crop_data_ts
  QUOTA UNLIMITED ON crop_index_ts;


**Result:** `User altered.`

### **Verify User Configuration**
```sql
SELECT username, default_tablespace, temporary_tablespace
FROM dba_users
WHERE username = 'CROP_ADMIN';


**User Configuration:**
| USERNAME | DEFAULT_TABLESPACE | TEMPORARY_TABLESPACE |
|----------|-------------------|---------------------|
| CROP_ADMIN | CROP_DATA_TS | CROP_TEMP_TS |

(./images/PhaseIV_06.png)<img width="599" height="506" alt="phase IV scr6" src="https://github.com/user-attachments/assets/04ae6e6e-8d10-4a01-95b4-0362c3ffc5eb" />




## 8. Memory Parameters & Archive Logging

### **Configure PGA Memory**
```sql
ALTER SYSTEM SET pga_aggregate_target = 256M SCOPE=BOTH;
```

**Result:** `System altered.`

### **Verify Memory Parameters**
```sql
SELECT name, value
FROM v$parameter
WHERE name IN ('sga_target', 'pga_aggregate_target');


**Memory Configuration:**
| NAME | VALUE | Description |
|------|-------|-------------|
| sga_target | 536870912 (~512MB) | System Global Area |
| pga_aggregate_target | 268435456 (~256MB) | Program Global Area |

### **Check Archive Log Status**
```sql
ARCHIVE LOG LIST;
```

**Archive Configuration:**
```
Database log mode              No Archive Mode
Automatic archival             Disabled
Archive destination            C:\app\HP-\product\21c\homes\OraDBI21Home1\RDBMS
Oldest online log sequence     27
Current log sequence           29


| Setting | Value |
|---------|-------|
| Database log mode | No Archive Mode |
| Automatic archival | Disabled |
| Current log sequence | 29 |

**Note:** Archive logging currently disabled for development environment.

(./images/_PhaseIV_07.png)<img width="863" height="429" alt="phase IV scr7" src="https://github.com/user-attachments/assets/84aceddd-7e8d-4966-9316-709286931d8b" />




## Complete Configuration Summary

### **Final Database Setup**
| Component | Configuration | Status |
|-----------|--------------|--------|
| PDB Name | wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db | ✅ |
| Admin User | crop_admin (password: docile) | ✅ |
| Super Admin Privileges | All CREATE privileges granted | ✅ |
| Data Tablespace | 100MB, autoextend 10MB, UNLIMITED | ✅ |
| Index Tablespace | 50MB, autoextend 5MB, UNLIMITED | ✅ |
| Temp Tablespace | 50MB, autoextend 5MB, UNLIMITED | ✅ |
| SGA Target | 512MB | ✅ |
| PGA Target | 256MB | ✅ |
| Archive Logging | Disabled (development) | ⚠️ |
| Database Status | OPERATIONAL | ✅ |



## MIS Functions Supported

- Centralized data storage with optimized performance
- Scalable storage management with autoextend
- Memory optimization for concurrent users
- Foundation for transaction processing
- Ready for application deployment



##  Organizational Impact

- Ready for immediate application deployment
- Supports high-performance data operations
- Provides secure, managed database environment
- Enables future BI and reporting capabilities



