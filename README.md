# Design and Implementation of a SQL-Based Customer Churn Prediction System using Postgresql

SQL-Based Customer Churn Prediction System
📌 Project Overview
This project presents a PostgreSQL-based customer churn prediction platform designed to support data analysis and predictive modeling in the retail banking domain. The system processes and organizes customer data into a normalized relational schema, supports SQL-driven analytics, and integrates with BI tools for visualization and reporting.

🧠 Key Features
✅ Normalized Relational Schema up to BCNF for efficient querying and clean data structure

🔐 Data Integrity & Constraints using primary/foreign keys, triggers, and cascading rules

📊 Churn Modeling support with behavioral and financial indicators

🧑‍💼 User-Friendly Queries & Views for business users, analysts, and ML engineers

⚙️ Stored Procedures & Functions for automating customer management

📈 Optimized Performance with indexed queries and explain plan analysis

🚨 Trigger-based Validation for duplicate prevention and error handling

📂 Dataset
Records: ~10,000 customers

Columns:

CustomerId, Surname, CreditScore, Geography, Gender, Age, Tenure, Balance

NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary, Exited

🧱 Database Schema
The database (MainDB) is composed of 13 relational tables with clearly defined dependencies and constraints:

🔹 Core Tables
| Table                  | Description                                 |
| ---------------------- | ------------------------------------------- |
| `Customer`             | Central entity holding personal data        |
| `LoanApplication`      | Loan details per customer                   |
| `Account`              | Account info like balance, tenure, etc.     |
| `CreditCard`           | One-to-one card details per customer        |
| `ActivityStatus`       | Captures customer login activity            |
| `SalaryDetails`        | Estimated salary, increment, linked account |
| `RiskScoreDetails`     | Credit score and risk category              |
| `ChurnStatus`          | Churn flag, reason, last contact date       |
| `StatusFlag`           | Boolean flags (high-value, review-needed)   |
| `CustomerLog`          | Action audit trail per customer             |
| `SalaryBandMapping`    | Maps salary values to salary bands          |
| `ScoreCategoryMapping` | Maps credit scores to score categories      |


⚠️ Constraints
Email uniqueness enforced by both a UNIQUE constraint and a trigger

ON DELETE CASCADE / SET NULL rules ensure referential integrity

All tables were validated against expected data types and nullability rules

🧪 Sample Operations
Inserts: New customers, loan applications, etc.

Updates: Salary increments, account balances

Deletes: Customer cascade delete

Joins: Profile-building, churn insights

Stored Procedures:

FlagHighRiskCustomers()

AddLoanApp(custid, amt, status)

UpdateBalance(custid, new_balance)

DeleteCustomerAndDependencies(custid)

Functions:

GetSalaryBand(custid)

GetChurnReason(custid)

🚀 Query Optimization
🔍 Tools Used: EXPLAIN PLAN, ANALYZE
| Query Description                         | Before Index | After Index |
| ----------------------------------------- | ------------ | ----------- |
| Customers under 60 with Standard accounts | 732.30       | 726.62      |
| Pending loans count for age < 50          | 67,199.09    | 37,371.39   |
| Ranking balances with window functions    | 2323.25      | N/A\*       |

* Sequential scan remained optimal for smaller datasets.

🔐 Transaction Handling & Trigger Logic
Trigger: trg_customer_prevent_duplicate_email

Prevents duplicate email insertions with a custom exception

Transactions are atomic and rollback upon failure

Enforced using PostgreSQL's ACID compliance (Atomicity, Consistency, Isolation, Durability)

📊 Target Users
💼 Banking Professionals — Understand customer attrition

📈 Data Analysts — Run BI queries and generate reports

🤖 AI/ML Engineers — Use normalized data for model training

🎓 Students & Educators — Learn relational DB design with real-world use case

🛠️ DB Admins — Maintain schema, enforce constraints, and evolve system

✅ Technologies Used
PostgreSQL for schema and data operations

Python (pandas) for data cleaning and loading

🔧 Setup Instructions
1. Install PostgreSQL
2. Create the database:
   
CREATE DATABASE MainDB;

Run the table creation scripts from create_tables.sql

Load CSVs into corresponding tables using COPY or psql commands

Execute stored procedures, triggers, and functions using the .sql files provided

# Author
Padmavathi Moorthy
