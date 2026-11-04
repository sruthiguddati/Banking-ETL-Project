# Banking Data Warehouse – Business Requirements Document

**Document Version:** 1.0  
**Project:** Banking ETL Testing  
**Testing Type:** End-to-End ETL Testing

## 1. Business Objective

The bank wants to integrate customer, account, transaction and branch information from multiple source files into a centralized SQL Server Data Warehouse.

The Data Warehouse will support business reporting, transaction analysis and customer insights.

## 2. Source Systems and Files

| Source File | Format | Business Information |
|---|---|---|
| customers.csv | CSV | Customer details |
| accounts.csv | CSV | Bank account details |
| transactions.csv | CSV | Financial transactions |
| branch_master.xlsx | Excel | Branch reference information |

## 3. Target Data Warehouse

The target system is SQL Server.

Expected target tables:

- Dim_Customer
- Dim_Account
- Dim_Branch
- Fact_Transaction

## 4. High-Level Business Requirements

1. All valid customer records must be loaded into the customer dimension.
2. Each account must belong to a valid customer.
3. Each transaction must reference a valid account.
4. Branch information must be validated against the branch master.
5. Duplicate source records must be handled according to business rules.
6. Invalid records must be rejected or moved to an error table.
7. Transaction amounts must be loaded accurately.
8. Source and target record counts must be reconciled.
9. Incremental changes must be processed correctly.
10. Package failures and rejected records must be logged.

## 5. Testing Scope

- Source file validation
- CSV and Excel structure validation
- Source data profiling
- Source-to-target mapping validation
- ETL package testing
- Transformation testing
- Data reconciliation
- Negative testing
- Error handling and restartability
- Incremental load testing

## 6. Expected Outcome

The ETL process must load accurate, complete and consistent banking data into the target Data Warehouse, with proper error handling and execution logging.

**Note:** Detailed transformation rules, rejection criteria and expected results will be finalized in the Source-to-Target Mapping and Business Rules documents.