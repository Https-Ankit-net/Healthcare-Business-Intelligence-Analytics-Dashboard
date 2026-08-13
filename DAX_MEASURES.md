# Healthcare BI Dashboard — DAX Measures

> **Note:** This dashboard uses synthetic healthcare data for educational and portfolio purposes. It does not contain real patient information.

## 1. Patient KPIs

### Total Patients
```DAX
Total Patients =
DISTINCTCOUNT(patients[patient_id])
```

### Average Patient Age
```DAX
Average Patient Age =
AVERAGE(patients[age])
```

### Male Patients
```DAX
Male Patients =
CALCULATE(
    [Total Patients],
    patients[gender] = "M"
)
```

### Female Patients
```DAX
Female Patients =
CALCULATE(
    [Total Patients],
    patients[gender] = "F"
)
```

## 2. Appointment & Operations KPIs

### Total Appointments
```DAX
Total Appointments =
DISTINCTCOUNT(appointments[appointment_id])
```

### Completed Appointments
```DAX
Completed Appointments =
CALCULATE(
    [Total Appointments],
    appointments[status] = "Completed"
)
```

### No Show Appointments
```DAX
No Show Appointments =
CALCULATE(
    [Total Appointments],
    appointments[status] = "No-show"
)
```

### No Show Rate
```DAX
No Show Rate =
DIVIDE(
    [No Show Appointments],
    [Total Appointments],
    0
)
```

**Format:** Percentage, 2 decimal places.

### Average Wait Time
```DAX
Average Wait Time =
AVERAGE(appointments[wait_time_min])
```

### Average Visit Duration
```DAX
Average Visit Duration =
AVERAGE(appointments[visit_duration_min])
```

## 3. Treatment & Clinical KPIs

### Total Treatments
```DAX
Total Treatments =
DISTINCTCOUNT(treatments[treatment_id])
```

### Total Treatment Cost
```DAX
Total Treatment Cost =
SUM(treatments[cost])
```

### Successful Treatments
```DAX
Successful Treatments =
CALCULATE(
    [Total Treatments],
    treatments[success_flag] = "Yes"
)
```

### Treatment Success Rate
```DAX
Treatment Success Rate =
DIVIDE(
    [Successful Treatments],
    [Total Treatments],
    0
)
```

**Format:** Percentage, 2 decimal places.

### Average Treatment Cost
```DAX
Average Treatment Cost =
AVERAGE(treatments[cost])
```

### Average Treatment Duration
```DAX
Average Treatment Duration =
AVERAGE(treatments[treatment_duration_min])
```

## 4. Financial KPIs

### Total Billed Amount
```DAX
Total Billed Amount =
SUM(billing[amount])
```

**Format:** Currency.

### Insurance Coverage
```DAX
Insurance Coverage =
SUM(billing[insurance_covered_amount])
```

**Format:** Currency.

### Patient Payments
```DAX
Patient Payments =
SUM(billing[patient_paid_amount])
```

**Format:** Currency.

### Outstanding Amount
```DAX
Outstanding Amount =
SUM(billing[outstanding_amount])
```

**Format:** Currency.

### Paid Bills
```DAX
Paid Bills =
CALCULATE(
    COUNTROWS(billing),
    billing[payment_status] = "Paid"
)
```

### Pending Bills
```DAX
Pending Bills =
CALCULATE(
    COUNTROWS(billing),
    billing[payment_status] = "Pending"
)
```

### Average Claim Processing Days
```DAX
Average Claim Processing Days =
AVERAGE(billing[claim_processing_days])
```

### Insurance Coverage Rate
```DAX
Insurance Coverage Rate =
DIVIDE(
    [Insurance Coverage],
    [Total Billed Amount],
    0
)
```

**Format:** Percentage, 2 decimal places.

## 5. Optional Advanced Measures

### Appointment Completion Rate
```DAX
Appointment Completion Rate =
DIVIDE(
    [Completed Appointments],
    [Total Appointments],
    0
)
```

### Cancelled Appointments
```DAX
Cancelled Appointments =
CALCULATE(
    [Total Appointments],
    appointments[status] = "Cancelled"
)
```

Use only if `Cancelled` exists in `appointments[status]`.

### Cancellation Rate
```DAX
Cancellation Rate =
DIVIDE(
    [Cancelled Appointments],
    [Total Appointments],
    0
)
```

### Outstanding Rate
```DAX
Outstanding Rate =
DIVIDE(
    [Outstanding Amount],
    [Total Billed Amount],
    0
)
```

### Patient Collection Rate
```DAX
Patient Collection Rate =
DIVIDE(
    [Patient Payments],
    [Total Billed Amount],
    0
)
```

## 6. Time Intelligence Measures

These require a correctly configured `dim_date` table.

### Previous Month Appointments
```DAX
Previous Month Appointments =
CALCULATE(
    [Total Appointments],
    DATEADD(
        dim_date[date],
        -1,
        MONTH
    )
)
```

### Appointment Month-over-Month %
```DAX
Appointment MoM % =
DIVIDE(
    [Total Appointments] - [Previous Month Appointments],
    [Previous Month Appointments],
    0
)
```

### Previous Month Billing
```DAX
Previous Month Billing =
CALCULATE(
    [Total Billed Amount],
    DATEADD(
        dim_date[date],
        -1,
        MONTH
    )
)
```

### Billing Month-over-Month %
```DAX
Billing MoM % =
DIVIDE(
    [Total Billed Amount] - [Previous Month Billing],
    [Previous Month Billing],
    0
)
```

## 7. Management Indicator Measures

### Outstanding Financial Exposure
```DAX
Outstanding Financial Exposure =
[Outstanding Amount]
```

### No Show Performance
```DAX
No Show Performance =
IF(
    [No Show Rate] > 0.10,
    "Needs Attention",
    "Within Target"
)
```

> The 10% threshold is a project-defined dashboard threshold, not a healthcare industry standard.

### Treatment Performance
```DAX
Treatment Performance =
IF(
    [Treatment Success Rate] >= 0.50,
    "Strong",
    "Needs Investigation"
)
```

> The 50% threshold is a project-defined portfolio threshold, not a clinical benchmark.

## 8. Measure Inventory

### Patient
- Total Patients
- Average Patient Age
- Male Patients
- Female Patients

### Appointments
- Total Appointments
- Completed Appointments
- No Show Appointments
- No Show Rate
- Average Wait Time
- Average Visit Duration

### Treatment
- Total Treatments
- Total Treatment Cost
- Successful Treatments
- Treatment Success Rate
- Average Treatment Cost
- Average Treatment Duration

### Financial
- Total Billed Amount
- Insurance Coverage
- Patient Payments
- Outstanding Amount
- Paid Bills
- Pending Bills
- Average Claim Processing Days
- Insurance Coverage Rate

### Optional
- Appointment Completion Rate
- Cancelled Appointments
- Cancellation Rate
- Outstanding Rate
- Patient Collection Rate
- Previous Month Appointments
- Appointment MoM %
- Previous Month Billing
- Billing MoM %
- Outstanding Financial Exposure
- No Show Performance
- Treatment Performance

## 9. Formatting Standards

| Measure Type | Recommended Format |
|---|---|
| Patient counts | Whole number / thousands |
| Appointment counts | Whole number / thousands |
| Treatment counts | Whole number / thousands |
| Currency measures | Currency, 2 decimals |
| Rates | Percentage, 2 decimals |
| Wait time | Decimal number, minutes |
| Visit duration | Decimal number, minutes |
| Treatment duration | Decimal number, minutes |
| Claim processing | Decimal number, days |

## 10. Validation Notes

Before adding optional measures, validate:

- Actual appointment status values
- Actual treatment `success_flag` values
- Actual payment status values
- Date dimension relationships
- Missing and duplicate identifiers
- Financial totals
- Unexpected categorical values

The main sections contain the core measures used for the dashboard. Optional measures should only be added after their underlying data and relationships have been verified.
