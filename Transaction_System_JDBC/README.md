# ☕ Java JDBC Transaction System

A **Java JDBC-based transaction handling system** demonstrating 🔐 **ACID properties**, manual transaction management, ⚠️ **deadlock prevention**, and 🧾 **transaction history logging** using MySQL.

This project simulates a real-world banking fund transfer system where money is transferred between accounts while maintaining database consistency and reliability.

---

# 🚀 Features

- 💸 Fund transfer between accounts
- 🔄 Manual transaction control using `commit()` and `rollback()`
- 🔒 Deadlock prevention using ordered row locking
- 🗄️ MySQL row-level locking using `FOR UPDATE`
- 🧾 Transaction history logging (SUCCESS / FAILED)
- 🔐 Secure database configuration using environment variables
- ⚡ Atomic debit and credit operations
- 🛡️ Error handling with rollback mechanism

---

# 🔐 Configuration (Security)

Database credentials are **not hardcoded** inside the source code.

Set the following environment variables before running the application:

```bash
export DB_URL="jdbc:mysql://localhost:3306/banking"
export DB_USERNAME="your_username"
export DB_PASSWORD="your_password"
```

---

# 📸 Transaction Flow Implementation

The application uses JDBC transaction management to maintain data consistency and follow ACID principles.

### Transaction Handling

- Manual transaction control using `setAutoCommit(false)`
- Debit and credit operations using `PreparedStatement`
- `commit()` after successful transaction completion
- `rollback()` when any operation fails
- Transaction status logging with SUCCESS / FAILED states

<img src="./image/transaction-flow.png" alt="JDBC Transaction Flow" width="900"/>

---

# 🏗️ How It Works

The transaction workflow follows these steps:

1. 🧪 Validates sender and receiver accounts
2. 🔐 Locks account rows in a fixed order to prevent deadlocks
3. 💰 Checks whether sender has sufficient balance
4. ➖ Deducts amount from sender account
5. ➕ Adds amount to receiver account
6. 🧾 Stores transaction details with status
7. ✅ Commits transaction if all operations succeed
8. ❌ Rolls back changes if any operation fails

---

# 🔒 Transaction Management

The project demonstrates database transaction concepts:

### Commit

A transaction is committed only when:

- Sender balance update succeeds
- Receiver balance update succeeds
- Transaction history is stored successfully

### Rollback

Rollback is performed when:

- Insufficient balance
- Invalid account
- Database operation failure

This ensures that partial transactions never corrupt account balances.

---

# 🔐 Deadlock Prevention

To prevent deadlocks during concurrent transactions:

- Accounts are locked using:

```sql
SELECT account_number 
FROM accounts 
WHERE account_number = ?
FOR UPDATE;
```

- Locks are acquired in a fixed order using account numbers.

Example:

```
Transaction A:
Account 101 → Account 102

Transaction B:
Account 101 → Account 102
```

Both transactions follow the same locking order, reducing deadlock possibility.

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| ☕ Java | Application logic |
| 🔌 JDBC | Database connectivity |
| 🐬 MySQL | Data storage |
| 📄 SQL | Queries and transactions |
| 🔧 Git/GitHub | Version control |

---

# 📂 Project Structure

```
Transaction_System_JDBC

│
├── src
│   └── Transaction_handling.java
│
├── image
│   └── transaction-flow.png
│
├── README.md
└── .gitignore
```

---

# ▶️ How To Run

### 1. Clone Repository

```bash
git clone https://github.com/Ignorantashwin/java-backend-engineering-lab.git
```

### 2. Configure Database

Create MySQL database:

```sql
CREATE DATABASE banking;
```

Configure your environment variables:

```bash
export DB_URL="jdbc:mysql://localhost:3306/banking"
export DB_USERNAME="your_username"
export DB_PASSWORD="your_password"
```

### 3. Run Application

Compile and execute:

```bash
javac Transaction_handling.java

java Transaction_handling
```

---

# 🧠 Learning Outcomes

Through this project, I implemented:

- JDBC transaction management
- ACID principles
- Database consistency handling
- PreparedStatement usage
- Commit and rollback mechanism
- Row-level locking
- Deadlock prevention strategy
- Exception handling
- Real-world banking transaction workflow

---

# 🔮 Future Improvements

Possible improvements:

- Convert into Spring Boot REST API
- Add authentication using Spring Security + JWT
- Add transaction pagination
- Add Docker setup
- Add unit testing with JUnit and Mockito
- Add database migration using Flyway

---

# 👤 Author

**Ashwin**

GitHub:
https://github.com/Ignorantashwin
