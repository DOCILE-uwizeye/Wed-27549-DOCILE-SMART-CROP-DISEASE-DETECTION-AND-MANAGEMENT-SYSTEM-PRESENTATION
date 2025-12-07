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
# Phase IV: Database Creation - Files for GitHub

## Folder Structure to Add

```
database/
├── scripts/
│   ├── 01_database_creation.sql
│   ├── 02_tablespace_configuration.sql
│   ├── 03_user_setup.sql
│   └── 04_memory_configuration.sql
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

---

## File 1: database/scripts/01_database_creation.sql

```sql
-- =====================================================
-- PHASE IV: DATABASE CREATION
-- Project: Smart Crop Disease Detection and Management System
-- Student: Docile (ID: 27549) - Wednesday Group
-- Database: wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
-- Date: December 7, 2025
-- =====================================================

-- Connect as SYSDBA
CONNECT / AS SYSDBA;

-- Set container to root
ALTER SESSION SET CONTAINER = CDB$ROOT;

-- Display current container
SHOW CON_NAME;

-- Drop existing pluggable database if exists
DROP PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db 
INCLUDING DATAFILES;

-- Create new pluggable database
CREATE PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
ADMIN USER crop_admin IDENTIFIED BY docile
FILE_NAME_CONVERT = ('pdbseed', 'wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db');

-- Open the pluggable database
ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db OPEN;

-- Save state for automatic startup
ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db SAVE STATE;

-- Verify database creation
SELECT name, open_mode FROM v$pdbs;

-- Connect to the new pluggable database
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

-- Display current container name
SHOW CON_NAME;

PROMPT
PROMPT =====================================================
PROMPT Database created successfully!
PROMPT Database: wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
PROMPT Admin User: crop_admin
PROMPT Password: docile
PROMPT =====================================================
```

---

## File 2: database/scripts/02_tablespace_configuration.sql

```sql
-- =====================================================
-- TABLESPACE CONFIGURATION
-- Project: Smart Crop Disease Detection and Management System
-- Student: Docile (ID: 27549)
-- =====================================================

-- Connect to pluggable database as SYSDBA
CONNECT / AS SYSDBA;
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

-- Create data tablespace
CREATE TABLESPACE crop_data_ts
DATAFILE 'crop_data_ts.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 10M
MAXSIZE UNLIMITED
EXTENT MANAGEMENT LOCAL
SEGMENT SPACE MANAGEMENT AUTO;

-- Create index tablespace
CREATE TABLESPACE crop_index_ts
DATAFILE 'crop_index_ts.dbf'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED
EXTENT MANAGEMENT LOCAL
SEGMENT SPACE MANAGEMENT AUTO;

-- Create temporary tablespace
CREATE TEMPORARY TABLESPACE crop_temp_ts
TEMPFILE 'crop_temp_ts.tmp'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED;

-- Verify tablespace creation
SELECT tablespace_name, status, contents 
FROM dba_tablespaces 
WHERE tablespace_name LIKE 'CROP%';

PROMPT
PROMPT =====================================================
PROMPT Tablespaces created successfully!
PROMPT - crop_data_ts (100MB, autoextend)
PROMPT - crop_index_ts (50MB, autoextend)
PROMPT - crop_temp_ts (50MB, temporary)
PROMPT =====================================================
```

---

## File 3: database/scripts/03_user_setup.sql

```sql
-- =====================================================
-- USER SETUP AND PRIVILEGES
-- Project: Smart Crop Disease Detection and Management System
-- Student: Docile (ID: 27549)
-- =====================================================

-- Connect as SYSDBA
CONNECT / AS SYSDBA;
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

-- Grant comprehensive privileges to crop_admin
GRANT CREATE SESSION TO crop_admin;
GRANT CREATE TABLE TO crop_admin;
GRANT CREATE VIEW TO crop_admin;
GRANT CREATE PROCEDURE TO crop_admin;
GRANT CREATE SEQUENCE TO crop_admin;
GRANT CREATE TRIGGER TO crop_admin;
GRANT CREATE TYPE TO crop_admin;
GRANT CREATE SYNONYM TO crop_admin;
GRANT UNLIMITED TABLESPACE TO crop_admin;

-- Set default and temporary tablespaces for crop_admin
ALTER USER crop_admin
DEFAULT TABLESPACE crop_data_ts
TEMPORARY TABLESPACE crop_temp_ts
QUOTA UNLIMITED ON crop_data_ts
QUOTA UNLIMITED ON crop_index_ts;

-- Verify user configuration
SELECT username, default_tablespace, temporary_tablespace
FROM dba_users
WHERE username = 'CROP_ADMIN';

PROMPT
PROMPT =====================================================
PROMPT User configuration completed!
PROMPT Username: crop_admin
PROMPT Default Tablespace: crop_data_ts
PROMPT Temporary Tablespace: crop_temp_ts
PROMPT All necessary privileges granted
PROMPT =====================================================
```

---

## File 4: database/scripts/04_memory_configuration.sql

```sql
-- =====================================================
-- MEMORY CONFIGURATION
-- Project: Smart Crop Disease Detection and Management System
-- Student: Docile (ID: 27549)
-- =====================================================

-- Connect as SYSDBA
CONNECT / AS SYSDBA;
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;

-- Set PGA aggregate target to 256MB
ALTER SYSTEM SET pga_aggregate_target = 256M SCOPE=BOTH;

-- Verify memory settings
SELECT name, value
FROM v$parameter
WHERE name IN ('sga_target', 'pga_aggregate_target');

-- Check archive log mode status
ARCHIVE LOG LIST;

PROMPT
PROMPT =====================================================
PROMPT Memory configuration completed!
PROMPT PGA Aggregate Target: 256MB
PROMPT Archive Log Mode: Check output above
PROMPT =====================================================
```

---

## File 5: screenshots/phase4_database_creation/README.md

```markdown
# Phase IV: Database Creation Screenshots

This directory contains screenshots documenting the complete database creation process for the Smart Crop Disease Detection and Management System.

## Screenshot Documentation

### Screenshot 1: Database Creation

![01_database_created.png](01_database_created.png)

**Description:** Initial database creation command execution
- Shows the DROP and CREATE PLUGGABLE DATABASE commands
- Displays successful database creation message
- Database name: `wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db`
- Admin user: `crop_admin`
- Password identifier: docile

**Key SQL Commands:**
```sql
DROP PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db INCLUDING DATAFILES;
CREATE PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db
ADMIN USER crop_admin IDENTIFIED BY docile
FILE_NAME_CONVERT = ('pdbseed', 'wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db');
ALTER PLUGGABLE DATABASE wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db OPEN;
```

---

### Screenshot 2: Pluggable Databases Verification

![02_pluggable_databases.png](02_pluggable_databases.png)

**Description:** Verification of pluggable database status
- Query results from `v$pdbs` showing all pluggable databases
- Confirms the new database is in READ WRITE mode
- Shows database status and accessibility

**Query Used:**
```sql
SELECT name, open_mode FROM v$pdbs;
```

**Results:**
- PDB$SEED: READ ONLY
- AI_TO_DELETE_PDB_27292: MOUNTED
- DO_PDB_27549: READ WRITE
- WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB: READ WRITE ✓

---

### Screenshot 3: Session Connected to Database

![03_session_connected.png](03_session_connected.png)

**Description:** Session connection to the new pluggable database
- Demonstrates successful container switch
- Shows current container name
- Confirms session is connected to the correct PDB

**Commands:**
```sql
ALTER SESSION SET CONTAINER = wed_27549_docile_smartcropdiseasedetectionandmanagementsystem_db;
SHOW CON_NAME;
```

**Output:**
- CON_NAME: WED_27549_DOCILE_SMARTCROPDISEASEDETECTIONANDMANAGEMENTSYSTEM_DB

---

### Screenshot 4: Privileges Granted

![04_privileges_granted.png](04_privileges_granted.png)

**Description:** Comprehensive privilege grants to crop_admin user
- All necessary database object privileges assigned
- Unlimited tablespace access granted
- Ready for database development

**Privileges Granted:**
- CREATE SESSION ✓
- CREATE TABLE ✓
- CREATE VIEW ✓
- CREATE PROCEDURE ✓
- CREATE SEQUENCE ✓
- CREATE TRIGGER ✓
- CREATE TYPE ✓
- CREATE SYNONYM ✓
- UNLIMITED TABLESPACE ✓

---

### Screenshot 5: Tablespaces Created

![05_tablespaces_created.png](05_tablespaces_created.png)

**Description:** Tablespace creation with proper configuration
- Data tablespace: crop_data_ts (100MB)
- Index tablespace: crop_index_ts (50MB)
- Temporary tablespace: crop_temp_ts (50MB)
- All configured with autoextend enabled

**Tablespace Configuration:**
```sql
CREATE TABLESPACE crop_data_ts
DATAFILE 'crop_data_ts.dbf'
SIZE 100M
AUTOEXTEND ON
NEXT 10M
MAXSIZE UNLIMITED;

CREATE TABLESPACE crop_index_ts
DATAFILE 'crop_index_ts.dbf'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED;

CREATE TEMPORARY TABLESPACE crop_temp_ts
TEMPFILE 'crop_temp_ts.tmp'
SIZE 50M
AUTOEXTEND ON
NEXT 5M
MAXSIZE UNLIMITED;
```

---

### Screenshot 6: Tablespace Verification

![06_tablespace_verification.png](06_tablespace_verification.png)

**Description:** Verification of tablespace status and user configuration
- Confirms all tablespaces are ONLINE
- Shows tablespace types (PERMANENT/TEMPORARY)
- Displays user's default and temporary tablespace assignments

**Verification Query:**
```sql
SELECT tablespace_name, status, contents 
FROM dba_tablespaces 
WHERE tablespace_name LIKE 'CROP%';
```

**Results:**
| Tablespace Name | Status | Contents |
|----------------|--------|----------|
| CROP_DATA_TS | ONLINE | PERMANENT |
| CROP_INDEX_TS | ONLINE | PERMANENT |
| CROP_TEMP_TS | ONLINE | TEMPORARY |

**User Configuration:**
```sql
SELECT username, default_tablespace, temporary_tablespace
FROM dba_users
WHERE username = 'CROP_ADMIN';
```

**Results:**
- Username: CROP_ADMIN
- Default Tablespace: CROP_DATA_TS
- Temporary Tablespace: CROP_TEMP_TS

---

### Screenshot 7: Memory Configuration

![07_memory_configuration.png](07_memory_configuration.png)

**Description:** Memory parameter configuration and archive log status
- PGA aggregate target set to 256MB
- Archive log mode status displayed
- Memory configuration optimized for development

**Memory Settings:**
```sql
ALTER SYSTEM SET pga_aggregate_target = 256M SCOPE=BOTH;
```

**Configuration Results:**
- sga_target: 536870912 (512MB)
- pga_aggregate_target: 268435456 (256MB)

**Archive Log Status:**
- Database log mode: No Archive Mode
- Automatic archival: Disabled
- Archive destination: (Not configured for development)
- Oldest online log sequence: 27
- Current log sequence: 29

---

## Phase IV Completion Checklist

- [x] Pluggable database created with correct naming convention
- [x] Admin user (crop_admin) created and configured
- [x] Three tablespaces created (data, index, temporary)
- [x] Tablespaces configured with autoextend
- [x] All necessary privileges granted
- [x] User default and temporary tablespaces assigned
- [x] Memory parameters configured (PGA: 256MB)
- [x] Archive log status verified
- [x] All creation scripts documented
- [x] Screenshots captured with visible database name
- [x] README documentation completed

## Technical Specifications

**Database Version:** Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production  
**Operating System:** Microsoft Windows (Version 10.0.19045.5466)  
**SQL*Plus Version:** Release 21.0.0.0.0 - Production (Version 21.3.0.0.0)  
**Creation Date:** December 4, 2025  
**Project Due Date:** December 7, 2025

---

*All screenshots are original work by Docile (Student ID: 27549) for the Database Development with PL/SQL course at AUCA.*
```

---

## How to Add to Your Existing GitHub Repository

### Step 1: Create Folder Structure in VS Code

In your existing repository, create these folders:
```
database/scripts/
screenshots/phase4_database_creation/
```

### Step 2: Create the SQL Files

Create these 4 files in `database/scripts/` folder:
1. `01_database_creation.sql`
2. `02_tablespace_configuration.sql`
3. `03_user_setup.sql`
4. `04_memory_configuration.sql`

Copy the SQL content from above into each file.

### Step 3: Add Your Screenshots

Place your 7 screenshot images in `screenshots/phase4_database_creation/` with these exact names:
- `01_database_created.png`
- `02_pluggable_databases.png`
- `03_session_connected.png`
- `04_privileges_granted.png`
- `05_tablespaces_created.png`
- `06_tablespace_verification.png`
- `07_memory_configuration.png`

### Step 4: Create Screenshot README

Create `README.md` in `screenshots/phase4_database_creation/` folder and copy the screenshot documentation content from above.

### Step 5: Commit and Push to GitHub

In VS Code terminal:

```bash
# Add all new files
git add database/scripts/
git add screenshots/phase4_database_creation/

# Commit with message
git commit -m "Phase IV: Database Creation and Configuration"

# Push to GitHub
git push origin main
```

### Step 6: Verify on GitHub

Visit your repository on GitHub and verify:
- ✅ `database/scripts/` folder contains 4 SQL files
- ✅ `screenshots/phase4_database_creation/` contains 7 images + README.md
- ✅ All files are properly formatted and visible

---

**That's it! Your Phase IV is now documented on GitHub.** 🎉
