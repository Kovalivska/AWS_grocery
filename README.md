
# 🛒 GroceryMate – Cloud-Native E-Commerce Platform

[![Python](https://img.shields.io/badge/Language-Python%2C%20JavaScript-blue)](https://www.python.org/)
[![OS](https://img.shields.io/badge/OS-Linux%2C%20Windows%2C%20macOS-green)](https://www.kernel.org/)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-336791)](https://www.postgresql.org/)
[![GitHub Release](https://img.shields.io/github/v/release/AlejandroRomanIbanez/AWS_grocery)](https://github.com/AlejandroRomanIbanez/AWS_grocery/releases/tag/v2.0.0)
[![Free](https://img.shields.io/badge/Free_for_Non_Commercial_Use-brightgreen)](#-license)

⭐ **Star us on GitHub** — it motivates us a lot!

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Cloud Architecture](#-cloud-architecture)
- [Screenshots & Demo](#-screenshots--demo)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🚀 Overview

GroceryMate is a cloud-native, full-featured e-commerce application developed as part of the Masterschools program by **Alejandro Roman Ibanez**. It offers a complete solution for online grocery shopping, featuring user-friendly design, robust backend, and AWS-powered infrastructure.

---

## 🛒 Features

- **🛡️ User Authentication** – Secure registration, login, and session management.
- **🔒 Protected Routes** – Role-based access control.
- **🔎 Product Search & Filters** – Find products easily.
- **⭐ Favorites** – Save and manage favorite items.
- **🛍️ Shopping Basket** – Add/remove/checkout functionality.
- **💳 Checkout** – Secure payment flow and order handling.
- **📦 Cloud Integration** – Avatar images stored on S3, PostgreSQL via RDS.

---

## ☁️ Cloud Architecture

### 🔧 Infrastructure Components

- **EC2 Instance**:
  - Hosts Dockerized GroceryMate App.
  - Assumes IAM Role with S3 access.
- **Amazon RDS (PostgreSQL)**:
  - Used for relational data (products, users, orders).
  - Deployed in a private subnet.
- **Amazon S3 Bucket**:
  - Stores avatar images in `/avatars/` folder.
  - IAM role ensures access only from EC2.
- **IAM Role**:
  - Attached to EC2, granting S3 permissions.
- **VPC Network**:
  - Public subnet (EC2) & private subnet (RDS).

### 📐 Diagram (draw.io layout)

![image](https://github.com/user-attachments/assets/b609967d-4aa2-4403-baad-9a25afb8499d)


### 🛠 Docker Deployment

```bash
docker run --network host \
  -e S3_BUCKET_NAME=grocerymate-avatars \
  -e S3_REGION=eu-central-1 \
  -e USE_S3_STORAGE=true \
  -e POSTGRES_USER=grocery_user \
  -e POSTGRES_PASSWORD=grocery_test \
  -e POSTGRES_DB=grocerymate_db \
  -e POSTGRES_HOST=<your-rds-endpoint> \
  -e POSTGRES_URI=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:5432/${POSTGRES_DB} \
  -p 5000:5000 grocerymate
```

---

## 📸 Screenshots & Demo

![imagen](https://github.com/user-attachments/assets/ea039195-67a2-4bf2-9613-2ee1e666231a)
![imagen](https://github.com/user-attachments/assets/a87e5c50-5a9e-45b8-ad16-2dbff41acd00)
![imagen](https://github.com/user-attachments/assets/589aae62-67ef-4496-bd3b-772cd32ca386)
![imagen](https://github.com/user-attachments/assets/2772b85e-81f7-446a-9296-4fdc2b652cb7)

---

## 📋 Prerequisites

- Python >= 3.11
- PostgreSQL
- Git

---

## ⚙️ Installation

### 🔹 Clone Repository

```bash
git clone --branch version2 https://github.com/AlejandroRomanIbanez/AWS_grocery.git && cd AWS_grocery
```

### 🔹 Set Up PostgreSQL

```bash
psql -U postgres -c "CREATE DATABASE grocerymate_db;"
psql -U postgres -c "CREATE USER grocery_user WITH ENCRYPTED PASSWORD '<your_password>';"
psql -U postgres -c "ALTER USER grocery_user WITH SUPERUSER;"
```

### 🔹 Populate the DB

```bash
psql -U grocery_user -d grocerymate_db -f backend/app/sqlite_dump_clean.sql
```

### 🔹 Python Environment

```bash
cd backend
pip install -r requirements.txt
```

### 🔹 .env File

```ini
JWT_SECRET_KEY=<your_generated_key>
POSTGRES_USER=grocery_user
POSTGRES_PASSWORD=<your_password>
POSTGRES_DB=grocerymate_db
POSTGRES_HOST=localhost
POSTGRES_URI=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@${POSTGRES_HOST}:5432/${POSTGRES_DB}
```

### 🔹 Start App

```bash
python3 run.py
```

---

## 📖 Usage

- Open [http://localhost:5000](http://localhost:5000)
- Register and log in
- Search for products
- Add to basket and checkout

---

## 🤝 Contributing

We welcome PRs and ideas! Please fork, branch, and submit.

---

## 📜 License

Licensed under the MIT License.
