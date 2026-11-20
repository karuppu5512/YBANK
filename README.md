# YBank

A Java console application for bank operations: branches, employees, customers, accounts and transactions. Users log in by role. Data is stored in PostgreSQL through JDBC.

## Features

**Start menu**: Login, Application page (apply for a job or an account), Exit

**Admin**
- Add and view branches and branch employees
- Add employees and post new job openings
- Review applications

**Accounts and customers**
- Add customers and open accounts (minor, major, senior and simple account types)
- Account verification, details, statements and closing
- Check application status

**Transactions**
- Deposits and withdrawals
- Transaction records

## Requirements

- JDK 8 or later (tested with JDK 17)
- PostgreSQL running on `localhost:5432`
- PostgreSQL JDBC driver (`postgresql-<version>.jar`) from https://jdbc.postgresql.org/download/

## Database setup

1. Create an empty database:
   ```sql
   CREATE DATABASE ybank;
   ```
2. Edit `SRC/db.properties` to match your PostgreSQL install:
   ```properties
   url=jdbc:postgresql://localhost:5432/ybank
   user=postgres
   pass=<your password>
   ```
3. You don't need to create any tables. On startup the app creates them (`Tables.java`) and inserts default data, including account types and a default admin login (`Defaultdata.java`).

## Build and run

The app reads `db.properties` from the **current folder**, so run it from inside `SRC`. Put the JDBC driver jar in `YBANK/lib/`, then:

```bash
cd YBANK/SRC
javac -d ../out *.java
java -cp "../out;../lib/postgresql-42.7.4.jar" YBank.Ybank
```

> On Linux/macOS, use `:` instead of `;` in the classpath.

## Project structure

All source files are in `SRC/`. They're in package `YBank`, and helper classes are in `YBank.utils`.

| File(s) | Purpose |
|---|---|
| `Ybank.java` | Entry point and start menu |
| `LoginView.java`, `ApplicationView.java` | Login and application page |
| `Admin*.java`, `Branch*.java`, `AddEmployeeView.java`, `AddNewJobView.java` | Admin, branch and employee management |
| `Account*.java`, `AddCustomerView.java` | Customer and account management |
| `BankTransaction*.java`, `AddDeposit.java`, `AddWithdraw.java`, `AddTransactionView.java` | Transactions |
| `*Caller.java`, `*Controler.java`, `*Model.java`, `*View.java` | Caller / controller / model / view layers |
| `Database.java`, `db.properties` | Database connection |
| `Tables.java`, `Defaultdata.java` | Schema and default data |
| `Accountnumber.java`, `Calculations.java`, `Selections.java` | Utilities (`YBank.utils`) |
