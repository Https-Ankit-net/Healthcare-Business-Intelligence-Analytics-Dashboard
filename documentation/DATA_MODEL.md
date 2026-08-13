# Healthcare BI Dashboard — Data Model

> **Note:** This project uses synthetic healthcare data for educational and portfolio purposes. It does not contain real patient information.

## 1. Model Overview

The Healthcare BI Dashboard uses a relational Power BI data model combining patient, provider, appointment, treatment, billing, and date information.

The model is designed to support:

- Patient analytics
- Appointment and operational analytics
- Treatment and clinical analytics
- Financial analytics
- Time-based reporting
- Department-level analysis
- Management decision support

The model follows a fact-and-dimension approach where transactional healthcare activities are analyzed using descriptive dimensions.

---

# 2. High-Level Architecture

```text
                         ┌─────────────────┐
                         │     Doctors     │
                         │                 │
                         │ doctor_id (PK)  │
                         │ department      │
                         │ specialization  │
                         └────────┬────────┘
                                  │
                                  │ 1 : *
                                  │
┌─────────────────┐        ┌──────▼──────────┐
│    Patients     │        │   Appointments  │
│                 │        │                 │
│ patient_id (PK) │───────►│ appointment_id  │
│ age             │  1 : * │ patient_id (FK) │
│ gender          │        │ doctor_id (FK)  │
│ age_group       │        │ status          │
│ condition       │        │ wait_time       │
└─────────────────┘        └────────┬────────┘
                                    │
                                    │ 1 : *
                                    │
                             ┌──────▼──────────┐
                             │    Treatments   │
                             │                 │
                             │ treatment_id    │
                             │ appointment_id  │
                             │ category        │
                             │ cost             │
                             │ success_flag     │
                             └────────┬────────┘
                                      │
                                      │ 1 : *
                                      │
                               ┌──────▼────────┐
                               │    Billing     │
                               │                │
                               │ bill_id        │
                               │ treatment_id   │
                               │ patient_id     │
                               │ amount         │
                               │ payment_status │
                               └────────────────┘

                         ┌─────────────────┐
                         │    Dim_Date     │
                         │                 │
                         │ date (PK)       │
                         │ year            │
                         │ quarter         │
                         │ month           │
                         │ month_year      │
                         └────────┬────────┘
                                  │
                    ┌─────────────┼─────────────┐
                    │             │             │
                    ▼             ▼             ▼
              Appointments   Treatments      Billing
