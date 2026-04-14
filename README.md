# phase1_week5_assignment_seiferth
Product Quality Dashboard
# Product Information Quality Dashboard

A Streamlit web application that helps analyze the completeness of product listings in a SQLite database. It flags products with inadequate information so that issues can be identified and resolved before they confuse customers.

---

## Features

- View all products in an interactive table
- Filter products by category (electronics or grocery)
- Add new products via a sidebar form
- Automatically scores each product's information completeness
- Flags products with low information scores for review
- Seed script to populate the database with fake product data for testing

---

## Tech Stack

- **Python 3.10+**
- **Streamlit** — frontend dashboard
- **SQLAlchemy** — ORM and database management
- **SQLite** — lightweight local database
- **Faker** — generates fake seed data

---

## Project Structure

```
project-info-quality/
├── app.py          # Main Streamlit dashboard
├── database.py     # Database connection and engine setup
├── models.py       # SQLAlchemy Product model
├── seed.py         # Script to seed the database with fake data
└── test.db         # Auto-generated SQLite database (created on first run)
```

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/your-username/project-info-quality.git
cd project-info-quality
```

### 2. Install dependencies

```bash
pip3 install streamlit sqlalchemy faker
```

### 3. Seed the database

```bash
python3 seed.py
```

This will populate the database with 10 electronics and 15 grocery products.

### 4. Run the dashboard

```bash
streamlit run app.py
```

The app will open automatically in your browser at `http://localhost:8501`.

---

## Code Walkthrough

### `models.py`
Defines the `Product` database model using SQLAlchemy. Each product has a name, category, description, a JSON-encoded `attributes` field for category-specific data, and an `information_score` computed at insert time.

### `database.py`
Creates the SQLite engine and session factory using SQLAlchemy. Also runs `create_all()` on startup to initialize the database schema if it doesn't already exist.

### `seed.py`
Uses the `Faker` library to generate realistic fake products. Electronics get a random battery life, and grocery items get randomized gluten-free and fiber attributes. The script clears the table before re-seeding so it can be run repeatedly.

### `app.py`
The main Streamlit application. It has three main responsibilities:
- **Sidebar form** — allows users to add new products manually
- **All Products table** — displays every product in the database with optional category filtering
- **Flagged Products table** — displays any product whose `information_score` is below 2, indicating missing or thin information

### Information Scoring
Each product is scored out of a maximum of 2 points:
| Criterion | Points |
|---|---|
| Description is 80+ characters | +1 |
| Electronics: battery life is provided | +1 |
| Grocery: gluten-free status is provided | +1 |
| Grocery: fiber status is provided | +1 |

Products scoring below 2 are flagged in the dashboard.

---

## Example Products

| Name | Category | Score | Flagged? |
|---|---|---|---|
| Bright Smartwatch | electronics | 2 | No |
| Cloud Smartwatch | electronics | 1 | Yes |
| Pepper | grocery | 3 | No |
| Rice | grocery | 1 | Yes |

---

## Author

Julian Emil Seiferth  
AI Engineer Fellow
