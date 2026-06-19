# Executive Workforce Analytics & Compensation Optimization

## Project Overview
This end-to-end business intelligence project addresses corporate workforce attrition risks and salary compression. By blending HR data infrastructure with market compensation benchmarks, this pipeline identifies financial exposure caused by critical staff retention risks and highlights departments operating under market-competitive salary medians.

### Business Value Delivered:
* **Quantified Financial Exposure:** Pinpointed exactly how much corporate salary capital is tied up in high-risk attrition categories.
* **Compensation Audit Autonomy:** Automated the detection of underpaid talent segments against target market medians using a dynamic cross-filtering dashboard.

---

## Technical Architecture & Tool Stack
* **Excel:** Initial data architecture, data quality normalization, and structural logic profiling.
* **SQL (SQLite):** Relational database design (Star Schema), window functions for internal compensation ranking, and multi-level data aggregations.
* **Power BI:** Relational data modeling, advanced DAX engineering (`SUMX`, `CALCULATE`, `RELATED`), and interactive executive dashboard design.

---

## Pipeline Stage Breakdown

### Stage 1: Excel Data Architecture & Engineering
Transformed messy payroll system text exports into normalized, structured tables. Engineered primary logical check columns to flag organizational health:
* **Department Normalization:** Mapped internal shortcodes to official business units via robust error-handling lookups.
* **Tenure Analytics:** Computed precise employee lifespans using dynamic date-differential algorithms.
* **Market Compensation Auditing:** Constructed logical statements comparing individual pay against department targets to instantly isolate compensation deficits.

### Stage 2: SQL Relational DB Design & Deep Querying
Migrated flat-file data layers into an optimized SQL relational structure consisting of a central Fact table (`employees`) and a Dimension table (`departments`). 

Constructed high-impact business query scripts including:
1. **Internal Compensation Compression Analysis:** Utilized SQL window functions (`RANK() OVER (PARTITION BY...)`) to evaluate internal salary hierarchies per department.
2. **Financial Attrition Exposure Matrix:** Authored multi-level aggregation queries (`GROUP BY`) grouping headcount and calculating total salary capital sitting in high-risk categories.

*(The full production script is saved in this repository as `business_queries.sql`).*

### Stage 3: Power BI Semantic Modeling & UI Canvas
Imported database assets and established a clean **1-to-Many Star Schema** data model. Authored custom Data Analysis Expressions (DAX) to build dynamic corporate KPIs rather than static aggregations:
* `Total Salary Budget = SUM(employee_data[CurrentSalary])`
* `High Risk Attrition Rate = DIVIDE(CALCULATE(COUNT(employee_data[EmployeeID]), employee_data[LeavingRisk] = "High"), COUNT(employee_data[EmployeeID]), 0)`
* `Total Market Deficit = SUMX(employee_data, RELATED(department_mapping[TargetMedianSalary]) - employee_data[CurrentSalary])`

#### Executive Dashboard Interface Design:
* **KPI Card Banner:** Displays high-level budget, market variance metrics, and flight risk percentages.
* **Operational Heatmap:** A horizontal bar chart identifying business units suffering from severe under-market budget variances.
* **Risk Breakdown Matrix:** An interactive donut chart highlighting workforce retention distribution that cross-filters the entire dashboard layout upon user engagement.

  <img width="764" height="427" alt="HR Financial Attrition Power BI" src="https://github.com/user-attachments/assets/c41e24d7-42e2-4f1d-b4e8-a36633e712b8" />
