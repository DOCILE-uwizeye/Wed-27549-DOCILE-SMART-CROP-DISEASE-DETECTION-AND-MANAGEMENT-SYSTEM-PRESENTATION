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

---

## 7. Optional Notes for GitHub/VS Code

- You can render this Markdown directly in GitHub to see tables and headings.  
- For visual ERD, you may later add ASCII diagrams or link images using `![ERD](path/to/image.png)`.  
- All foreign keys are clearly indicated in the Data Dictionary and ERD Relationships table.

