# Healthcare Business Intelligence & Analytics Dashboard

## Overview

A comprehensive healthcare Business Intelligence solution developed using Microsoft Power BI to transform healthcare operational, clinical, patient, and financial data into interactive dashboards and actionable insights.

The project focuses on supporting data-driven decision-making across patient management, appointment operations, treatment performance, and financial reporting.

The solution demonstrates practical experience in:

- Business Intelligence
- Data visualization
- Data modeling
- DAX
- Data analysis
- Data quality validation
- KPI development
- Interactive reporting
- Healthcare analytics
- Management reporting

---

## Business Problem

Healthcare organizations generate large volumes of data across multiple operational areas, including:

- Patient registration
- Appointments
- Doctors and departments
- Treatments
- Billing
- Insurance
- Claims
- Payment status

When this information is distributed across different datasets, management may struggle to obtain a unified view of operational and financial performance.

This project addresses that challenge by integrating multiple healthcare datasets into a centralized Power BI analytical model.

The dashboard enables stakeholders to answer questions such as:

- How many patients are being served?
- What is the appointment demand over time?
- Which departments have the highest workload?
- What is the appointment no-show rate?
- Which treatment categories have the highest volume?
- What is the treatment success rate?
- How much has been billed?
- How much has been collected?
- What amount remains outstanding?
- How does insurance contribute to healthcare revenue?
- Which areas require management attention?

---

# Project Objectives

The primary objectives of the project are to:

1. Build a centralized healthcare BI reporting solution.
2. Integrate patient, appointment, treatment, doctor, and billing data.
3. Develop a structured relational data model.
4. Create reusable DAX measures for business KPIs.
5. Design interactive dashboards for different stakeholder needs.
6. Identify operational, clinical, and financial trends.
7. Improve data-driven decision-making.
8. Demonstrate data quality and reporting best practices.

---

# Technology Stack

| Technology | Purpose |
|---|---|
| Microsoft Power BI | Dashboard development and reporting |
| Power Query | Data extraction and transformation |
| DAX | KPI and analytical measure development |
| Microsoft Excel / CSV | Source datasets |
| SQL Concepts | Data modeling and analytical thinking |
| Data Modeling | Relationships and analytical architecture |

---

# Dataset Structure

The project uses multiple healthcare datasets.

### Patients

Contains patient demographic and registration information.

Key fields include:

- patient_id
- full_name
- age
- gender
- age_group
- blood_group
- chronic_condition
- city
- registration_date

### Doctors

Contains healthcare provider information.

Key fields include:

- doctor_id
- first_name
- last_name
- department
- specialization
- hospital_branch

### Appointments

Contains patient appointment and operational information.

Key fields include:

- appointment_id
- patient_id
- doctor_id
- appointment_date
- appointment_type
- status
- wait_time_min
- visit_duration_min

### Treatments

Contains treatment and clinical performance information.

Key fields include:

- treatment_id
- appointment_id
- treatment_category
- treatment_type
- treatment_date
- cost
- treatment_duration_min
- success_flag

### Billing

Contains financial and claims information.

Key fields include:

- bill_id
- treatment_id
- patient_id
- bill_date
- amount
- payment_status
- insurance_covered_amount
- patient_paid_amount
- outstanding_amount
- claim_status
- claim_processing_days

### Date Dimension

A dedicated date dimension was created for time-based analysis.

Key fields include:

- date
- date_key
- year
- quarter
- month
- month_number
- month_year
- week_number
- day
- day_name
- is_weekend

---

# Data Model

The Power BI model connects the major healthcare entities through a structured relational model.

```text
                 Doctors
                    |
                    | 1 : *
                    |
Patients  1 : *  Appointments
                    |
                    | 1 : *
                    |
                Treatments
                    |
                    | 1 : *
                    |
                  Billing
