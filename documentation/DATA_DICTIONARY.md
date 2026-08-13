# Healthcare BI Dashboard — Data Dictionary

> **Note:** This project uses synthetic healthcare data for educational and portfolio purposes. It does not contain real patient information.

## Overview

This data dictionary documents the tables, fields, data types, and business meaning used in the Healthcare Business Intelligence & Analytics Dashboard.

The dataset is organized into patient, doctor, appointment, treatment, billing, and date-dimension tables.

---

# 1. Patients

The `patients` table contains demographic, contact, geographic, and registration information for patients.

| Column | Description | Typical Data Type |
|---|---|---|
| `patient_id` | Unique identifier for each patient | Integer / Text |
| `full_name` | Patient's full name | Text |
| `age` | Patient age | Whole Number |
| `gender` | Patient gender code such as M or F | Text |
| `age_group` | Categorized patient age group | Text |
| `blood_group` | Patient blood group | Text |
| `chronic_condition` | Recorded chronic health condition | Text |
| `city` | Patient city | Text |
| `address` | Patient address | Text |
| `email` | Patient email address | Text |
| `contact_number` | Patient contact number | Text |
| `date_of_birth` | Patient date of birth | Date |
| `registration_date` | Date the patient was registered | Date |

### Business Use

The table supports:

- Patient population analysis
- Age-group analysis
- Gender distribution
- Chronic-condition analysis
- Geographic analysis
- Patient registration trends

### Primary Key

```text
patient_id
