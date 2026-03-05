# 🏥 TARDIS – Medical Insurance Data Engineering Project

---

## 📌 1. Project Overview

- **Client:** TORUS (UK)
- **Project Name:** TARDIS
- **Domain:** Healthcare / Medical Insurance
- **Team Size:** 10 Members
- **Project Duration:** 2 Years
- **Module:** Insurance Module
- ---
## Role in the Project

- Created 30 SSIS Packages for Full Load and Incremental Load processing
- Worked extensively on SQL and T-SQL (Stored Procedures, Views, Functions)
- Created and maintained 100+ SSRS Reports
- Attended client and internal team meetings
- Prepared technical documentation
- Performed coding and database development tasks
- Conducted Knowledge Transfer (KT) sessions
- Handled performance tuning and error handling in ETL processes

## Project Description

- It is a Medical Insurance Project from the UK.
- Any customer can purchase a medical policy through web, online platforms, agents, brokers, or third-party channels.
- Policies can be renewed and are purchased from various locations.
- Customers receive deductions when purchasing a policy.
- Each policy has a defined limit on the insured amount.
- Customers pay a premium amount for the given policy on a yearly basis.
  
<p align="center">
  <img src="Torus.png" width="100%" />
</p>

## Project Objectives
- Growth rate in terms of number of customers and profit
- Growth rate for renewals over the last few years
- Analyze new customers ratio
- Analyze renewals ratio
- Analyze time taken to issue new policies
- Analyze customers and their existing policies, and provide recommendations
- Analyze number of claim settlements over the last few years
- Analyze claim settlement amounts over the last few years

<p align="center">
  <img src="SSI_Loading_The_Data.png" width="100%" />
</p>

## Tables Used in the Project

### DB Tables (OLTP Source)

- Policy
- RevenueType
- [Finance].[Currency]
- TransactionType

### Excel Source Tables

- PolicySection
- PolicyCoverage
- Premium
- Limit
- Deduction
<p align="center">
  <img src="SSIS_LOAD.png" width="100%" />
</p>

### Example: Stage_LoadCurrency
---

**Example:**  
This example shows how a table is loaded into the **staging layer** using the package **Stage_LoadCurrency**.

---

### Control Flow for `Stage_LoadCurrency`

<p align="center">
  <img src="Stage_LoadCurrency_1.png" width="100%" />
</p>

---

### Data Flow for `Stage_LoadCurrency`

<p align="center">
  <img src="Stage_LoadData_flow_1.png" width="100%" />
</p>

---

### Error Logging

In this project, we have implemented **two types of logging**:

- **Custom Logging (Success Logging)**  
  For this, we create a **custom SQL Server table** to log successful package execution.

<p align="center">
  <img src="Custom_Logging _01.png" width="100%" />
</p>

- **Built-in SSIS Logging**  
  SSIS provides a **built-in logging mechanism** to capture execution details and errors.  
  Here we use the **OnError** and **OnTaskFailed** event handlers for logging.
<p align="center">
  <img src="Built_in_SSIS_Logging_01.png" width="100%" />
</p>
---

### Custom Logging Table

```sql
CREATE TABLE SSIS_Logs
(
    ID INT PRIMARY KEY IDENTITY(1,1),
    PkgName VARCHAR(100) NOT NULL,
    PkgExecTime DATETIME NOT NULL,
    RowCnt INT NOT NULL,
    PkgExecStatus VARCHAR(100) NOT NULL
);
GO

SELECT * FROM SSIS_Logs;
GO

INSERT INTO SSIS_Logs
VALUES (?, GETDATE(), ?, 'Success. Package executed successfully.');
```



