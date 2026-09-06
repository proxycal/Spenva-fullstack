# Spenva 💸

A full-stack expense & debt management platform inspired by Splitwise track shared expenses, manage groups and friends, and settle debts with a minimal number of transactions.

Live App:  splitwise-backend-five.vercel.app

# 🚀 Tech Stack
Backend

Java + Spring Boot
PostgreSQL (via JPA/Hibernate)
Spring Security + JWT Authentication
Maven

Frontend

React + TypeScript
Tailwind CSS
Context API (theme persistence)

# ✨ Features
1. Secure authentication (JWT-based, password hashing, role-based access)
2. Friend management (add,accept,manage friends)
3. Expense tracking within groups or direct friend pairings
4. Real-time balance calculation across users and groups
5. Debt simplification algorithm - minimizes the number of settlement transactions needed to clear all balances
6. Dark/light theme switching (persisted)
7. Responsive dashboards (Main / Friends / Group views)

# 🏗️ Architecture

The backend follows a clean layered architecture:

Controller  ->  Service  ->  Repository  ->  PostgreSQL

1.Controller Layer - exposes REST endpoints, handles request/response mapping

2.Service Layer - houses business logic (balance computation, debt simplification, validation), transaction boundaries

3.Repository Layer - Spring Data JPA interfaces over Hibernate entities

# 🧮 Debt Simplification Algorithm

Instead of surfacing every raw pairwise IOU, Spenva reduces group debts to the minimum number of transactions needed to settle everyone up:

->Aggregate all expenses/splits into a net balance per user (positive = owed, negative = owes).

->Partition users into creditors and debtors based on balance sign.

->Greedily match the largest creditor with the largest debtor, settle the smaller amount, and repeat until all balances reach zero.

This greedy approach gives a close-to-optimal reduction in settlement transactions with efficient time complexity, avoiding the need to track every individual expense-level debt. 

# 🔐 Authentication & Security

Stateless JWT authentication - token issued on login, validated per-request via a security filter

Passwords hashed with BCrypt (never stored in plaintext)

Role-based, member-scoped access to group and expense operations

# 📡 API Overview
REST endpoints organized by resource:

/api/auth         - register, login

/api/users        - user profile management

/api/friends      - friend requests & management

/api/groups       - group creation & membership

/api/expenses     - expense creation, splitting

/api/settlements  - debt settlement records

Validation (e.g. split totals matching expense amount, settlement amounts not exceeding owed balance) happens at the service layer before persistence.

# 🛠️ Getting Started

**Prerequisites

Java 17+

Maven

PostgreSQL

Node.js + npm (for frontend)

**Backend Setup

bash

cd backend

mvn clean install

mvn spring-boot:run

**Frontend Setup

bash

cd frontend

npm install

npm run dev

# 📌 Note

No AI component , this is a purely algorithmic project.

Built as a portfolio/resume project to demonstrate full-stack engineering: secure REST API design, relational data modeling, and a genuine algorithmic component beyond CRUD.
