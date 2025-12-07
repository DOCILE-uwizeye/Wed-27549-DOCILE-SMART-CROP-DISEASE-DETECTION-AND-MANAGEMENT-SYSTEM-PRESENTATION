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

---

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

---

## 4. BPMN/UML Notations Used
- **Start Event:** Upload image  
- **Tasks:** Analyze image, fetch disease info, store scan, generate recommendation  
- **Decision Point:** Is a disease detected?  
- **End Event:** Results displayed  
- **Data Stores:** Users, disease_profiles, scans, recommendations  

---

## 5. Logical Flow Validation
- Fully linear from image upload → analysis → results.
- Decision paths clear (diseased or healthy).
- No missing dependencies.
- All actors have defined responsibilities.

---

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

---

## Deliverables
- BPMN Diagram (PNG/JPG)
- This documentation file
DRAW I.O
  (./<img width="1275" height="582" alt="DDI1" src="https://github.com/user-attachments/assets/95f7173b-6643-45ff-ad1c-08192e193208" />
)


# PHASE III: Logical Data Model (ERD + 3NF + Data Dictionary)

---

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

---

## 2. Normalization Summary (Up to 3NF)

| Normal Form | Description |
|------------|-------------|
| **1NF** | All tables contain atomic values. Each record is unique. |
| **2NF** | All non-key attributes fully depend on the primary key. No partial dependencies exist. |
| **3NF** | No transitive dependencies. All attributes depend only on the table's primary key. |

---

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

---

## 4. BI Considerations

| Aspect | Notes |
|--------|------|
| Fact Table Candidate | **scans** |
| Dimension Tables | users, disease_profiles, crop_types |
| Slowly Changing Dimensions (SCD) | Disease treatments may change over time |
| Audit Trail | Recommended: log table for user actions, scan attempts |

---

## 5. Assumptions

1. Each scan is linked to exactly one user.  
2. Each scan detects only one disease at a time.  
3. Recommendations are tied to diseases.  
4. Crop types may be linked later for future expansion.  
5. Users, scans, and recommendations are maintained in a consistent format to ensure data integrity.  

---

## 6. ERD Relationships (Summary)

| Table | Relationship | Reference |
|-------|-------------|-----------|
| scans | Many-to-One | users.user_id |
| scans | Many-to-One | disease_profiles.disease_id (detected_disease) |
| recommendations | Many-to-One | disease_profiles.disease_id |

> **Note:** The **scans** table acts as a fact table in BI; **users**, **disease_profiles**, and **crop_types** act as dimension tables.



(./images/database_schema.png)<img width="1358" height="666" alt="DDI3" src="https://github.com/user-attachments/assets/efe0b0cf-d5c3-44af-ae97-b0956ca328f5" />
# Phase IV: Database Creation & Configuration

**Student:** Docile (ID: 27549)  
**Group:** Wednesday  
**Project:** Smart Crop Disease Detection & Management System  
**Database:** wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db  
**Date:** December 7, 2025

---

## Screenshot 1: Database Creation
(../screenshots/phase4_database_creation/01_database_created.png)<img width="938" height="678" alt="phase IV scr1" src="https://github.com/user-attachments/assets/0a43a2e9-83b7-45d8-ad7f-632a18d1cee5" />


### Description
Initial database creation command execution showing the DROP and CREATE PLUGGABLE DATABASE commands with successful completion. The database was created with the naming convention following the project requirements.

### SQL Commands Executed
```sql
DROP PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db 
INCLUDING DATAFILES;

CREATE PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
ADMIN USER crop_admin IDENTIFIED BY docile
FILE_NAME_CONVERT = ('pdbseed', 'wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db');

ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db OPEN;

ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db SAVE STATE;
```

### Key Details
- **Database Name:** wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
- **Admin User:** crop_admin
- **Password:** docile
- **Status:** Pluggable database created and opened successfully

---

## Screenshot 2: Pluggable Databases Verification

(../screenshots/phase4_database_creation/02_pluggable_databases.png)<img width="847" height="504" alt="phase IV scr2" src="https://github.com/user-attachments/assets/d9b468b1-f8b5-40b2-8ed6-e7af5841164e" />


### Description
Verification query showing all pluggable databases in the container database. The screenshot confirms that the newly created database is in READ WRITE mode and fully operational.

### Query Used
```sql
SELECT name, open_mode FROM v$pdbs;
```

### Results
| Database Name | Open Mode | Status |
|--------------|-----------|--------|
| PDB$SEED | READ ONLY | System seed database |
| AI_TO_DELETE_PDB_27292 | MOUNTED | Other PDB |
| DO_PDB_27549 | READ WRITE | Other PDB |
| **WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB** | **READ WRITE** | **✓ Active** |

---

## Screenshot 3: Session Connected to Database

![Session Connected](../screenshots/phase4_database_creation/03_session_connected.png)

### Description
Demonstrates successful session switch to the newly created pluggable database. The SHOW CON_NAME command confirms the session is now connected to the correct container.

### Commands Executed
```sql
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

SHOW CON_NAME;
```

### Output Verification
```
CON_NAME
------------------------------------------------------------
WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB
```

**Status:** ✓ Session successfully connected to target PDB

---

## Screenshot 4: Privileges Granted

![Privileges Granted](../screenshots/phase4_database_creation/04_privileges_granted.png)

### Description
Shows all system privileges granted to the crop_admin user. These privileges enable the admin user to create all necessary database objects for the project.

### SQL Commands Executed
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

### Privilege Summary Table

| Privilege | Purpose | Status |
|-----------|---------|--------|
| CREATE SESSION | Connect to database | ✓ Granted |
| CREATE TABLE | Create tables | ✓ Granted |
| CREATE VIEW | Create views | ✓ Granted |
| CREATE PROCEDURE | Create stored procedures | ✓ Granted |
| CREATE SEQUENCE | Create sequences | ✓ Granted |
| CREATE TRIGGER | Create triggers | ✓ Granted |
| CREATE TYPE | Create custom types | ✓ Granted |
| CREATE SYNONYM | Create synonyms | ✓ Granted |
| UNLIMITED TABLESPACE | No space restrictions | ✓ Granted |

---

## Screenshot 5: Tablespaces Created

![Tablespaces Created](../screenshots/phase4_database_creation/05_tablespaces_created.png)

### Description
Shows the creation of three tablespaces with proper configuration: data tablespace for storing tables, index tablespace for storing indexes, and temporary tablespace for sorting operations.

### Tablespace Configuration

#### Data Tablespace
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

#### Index Tablespace
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

#### Temporary Tablespace
```sql
CREATE TEMPORARY TABLESPACE crop_temp_ts
TEMPFILE 'crop_temp_ts.tmp'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED;
```

### Tablespace Summary

| Tablespace Name | Type | Initial Size | Autoextend | Purpose |
|----------------|------|--------------|------------|---------|
| crop_data_ts | PERMANENT | 100MB | ON (10MB increments) | Store table data |
| crop_index_ts | PERMANENT | 50MB | ON (5MB increments) | Store indexes |
| crop_temp_ts | TEMPORARY | 50MB | ON (5MB increments) | Sorting operations |

---

## Screenshot 6: Tablespace Verification

![Tablespace Verification](../screenshots/phase4_database_creation/06_tablespace_verification.png)

### Description
Verification queries confirming all tablespaces are ONLINE and properly configured. Also shows the user's default and temporary tablespace assignments.

### Verification Queries

#### Tablespace Status Query
```sql
SELECT tablespace_name, status, contents 
FROM dba_tablespaces 
WHERE tablespace_name LIKE 'CROP%';
```

#### Results
| Tablespace Name | Status | Contents |
|----------------|--------|----------|
| CROP_DATA_TS | ONLINE | PERMANENT |
| CROP_INDEX_TS | ONLINE | PERMANENT |
| CROP_TEMP_TS | ONLINE | TEMPORARY |

#### User Configuration Query
```sql
SELECT username, default_tablespace, temporary_tablespace
FROM dba_users
WHERE username = 'CROP_ADMIN';
```

#### User Tablespace Assignment
```sql
ALTER USER crop_admin
DEFAULT TABLESPACE crop_data_ts
TEMPORARY TABLESPACE crop_temp_ts
QUOTA UNLIMITED ON crop_data_ts
QUOTA UNLIMITED ON crop_index_ts;
```

#### Results
| Username | Default Tablespace | Temporary Tablespace |
|----------|-------------------|---------------------|
| CROP_ADMIN | CROP_DATA_TS | CROP_TEMP_TS |

**Status:** ✓ All tablespaces ONLINE and user properly configured

---

## Screenshot 7: Memory Configuration

![Memory Configuration](../screenshots/phase4_database_creation/07_memory_configuration.png)

### Description
Shows memory parameter configuration and archive log mode status. The PGA aggregate target was set to 256MB for optimal performance during development.

### Memory Configuration Command
```sql
ALTER SYSTEM SET pga_aggregate_target = 256M SCOPE=BOTH;
```

### Memory Verification Query
```sql
SELECT name, value
FROM v$parameter
WHERE name IN ('sga_target', 'pga_aggregate_target');
```

### Memory Settings Results

| Parameter | Value | Description |
|-----------|-------|-------------|
| sga_target | 536870912 (512MB) | System Global Area |
| pga_aggregate_target | 268435456 (256MB) | Program Global Area |

### Archive Log Status
```sql
ARCHIVE LOG LIST;
```

### Archive Configuration

| Setting | Value | Notes |
|---------|-------|-------|
| Database log mode | No Archive Mode | Development environment |
| Automatic archival | Disabled | Not required for development |
| Archive destination | Not configured | Will be configured in production |
| Oldest online log sequence | 27 | Current log tracking |
| Current log sequence | 29 | Active log number |

**Note:** Archive logging is disabled for the development environment but should be enabled in production for point-in-time recovery.

---

## Database Setup Summary

### Naming Convention Compliance
✓ Database name follows the required format:
```
GrpName_StudentId_FirstName_ProjectName_DB
wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
```

### Admin User Details
- **Username:** crop_admin (Identifiable)
- **Password:** docile (First name as required)
- **Privileges:** Super admin (all CREATE privileges granted)

### Tablespace Configuration
| Component | Specification | Status |
|-----------|--------------|--------|
| Data tablespace | 100MB, autoextend | ✓ Created |
| Index tablespace | 50MB, autoextend | ✓ Created |
| Temporary tablespace | 50MB, autoextend | ✓ Created |
| Extent management | LOCAL | ✓ Configured |
| Segment space management | AUTO | ✓ Configured |

### Memory Parameters
| Parameter | Value | Status |
|-----------|-------|--------|
| SGA Target | 512MB | ✓ Default |
| PGA Aggregate Target | 256MB | ✓ Configured |
| Autoextend | ON | ✓ Enabled |

### System Configuration
| Setting | Value | Status |
|---------|-------|--------|
| Archive logging | Disabled | ✓ Development mode |
| Pluggable database | Open READ WRITE | ✓ Active |
| Auto-start | Save state enabled | ✓ Configured |

---

## GitHub Documentation Structure

### Database Scripts Location
```
database/
└── scripts/
    ├── 01_database_creation.sql
    ├── 02_tablespace_configuration.sql
    ├── 03_user_setup.sql
    └── 04_memory_configuration.sql
```

### Screenshots Location
```
screenshots/
└── phase4_database_creation/
    ├── 01_database_created.png
    ├── 02_pluggable_databases.png
    ├── 03_session_connected.png
    ├── 04_privileges_granted.png
    ├── 05_tablespaces_created.png
    ├── 06_tablespace_verification.png
    ├── 07_memory_configuration.png
    └── README.md
```

### Documentation Location
```
documentation/
└── phase4_database_creation.md (this file)
```

---

## Project Structure Overview

### Database Architecture
```
CDB$ROOT (Container Database)
├── PDB$SEED (Seed Database)
├── wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db (Project PDB)
│   ├── crop_admin (Admin User)
│   ├── Tablespaces
│   │   ├── crop_data_ts (Data storage)
│   │   ├── crop_index_ts (Index storage)
│   │   └── crop_temp_ts (Temporary storage)
│   └── Configuration
│       ├── Memory: PGA 256MB
│       ├── Archive Mode: Disabled
│       └── Auto-start: Enabled
```

### System Components

#### 1. Database Layer
- Oracle 21c Express Edition
- Pluggable Database Architecture
- Multi-tenant container database

#### 2. Storage Layer
- Permanent tablespaces for data and indexes
- Temporary tablespace for operations
- Autoextend enabled for growth

#### 3. Security Layer
- Admin user with controlled privileges
- Role-based access ready for implementation
- Unlimited tablespace quotas

#### 4. Memory Management
- SGA: 512MB (system default)
- PGA: 256MB (configured)
- Automatic memory management

---

## Technical Specifications

### Environment Details
| Component | Specification |
|-----------|--------------|
| Database Version | Oracle Database 21c Express Edition Release 21.0.0.0.0 |
| Operating System | Microsoft Windows (Version 10.0.19045.5466) |
| SQL*Plus Version | Release 21.0.0.0.0 - Production (Version 21.3.0.0.0) |
| Creation Date | December 4, 2025 |
| Project Due Date | December 7, 2025 |

### Database Information
| Attribute | Value |
|-----------|-------|
| PDB Name | wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db |
| Admin User | crop_admin |
| Character Set | AL32UTF8 (default) |
| National Character Set | AL16UTF16 (default) |
| Open Mode | READ WRITE |
| Restricted | NO |

---

## Phase IV Completion Checklist

### Database Creation
- [x] Pluggable database created with correct naming convention
- [x] Database opened in READ WRITE mode
- [x] Save state enabled for automatic startup
- [x] Verification queries executed successfully

### User Configuration
- [x] Admin user (crop_admin) created with identifiable username
- [x] Password set to first name (docile)
- [x] All CREATE privileges granted
- [x] Unlimited tablespace privilege granted

### Tablespace Setup
- [x] Data tablespace (crop_data_ts) created - 100MB
- [x] Index tablespace (crop_index_ts) created - 50MB
- [x] Temporary tablespace (crop_temp_ts) created - 50MB
- [x] All tablespaces configured with autoextend
- [x] User default tablespace assigned
- [x] User temporary tablespace assigned
- [x] Unlimited quotas granted on data and index tablespaces

### Memory Configuration
- [x] PGA aggregate target set to 256MB
- [x] Memory parameters verified
- [x] Archive log mode status checked

### Documentation
- [x] All SQL scripts created and tested
- [x] Seven screenshots captured with visible database name
- [x] Screenshot explanations written
- [x] README documentation completed
- [x] GitHub repository structure defined
- [x] Project overview documented

### GitHub Organization
- [x] Scripts organized in database/scripts/ folder
- [x] Screenshots organized in screenshots/phase4_database_creation/ folder
- [x] Documentation file created
- [x] All files ready for commit

---

