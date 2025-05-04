
# 📦 B2B Logistics Intelligence Pipeline (Pathway + RAG)
# Built at **HackWithChicago 2025**, hosted by Microsoft and organized by HackWithIndia.
## 🧾 Overview

This project simulates a real-world B2B logistics pipeline for tracking product deliveries, shipping events, and customer orders. It integrates real-time data streaming in Ubuntu using **Pathway**, document reasoning using **RAG (Retrieval-Augmented Generation)**, and natural language answering using **OpenAI GPT models**.

Built at **HackWithChicago 2025**, hosted by Microsoft and organized by HackWithIndia.

---

## 📁 Datasets

### 1. `Table1_Products.csv`

Contains product catalog information:

* `product_id` (PK): Unique ID for each product
* `category`, `subcategory`: Product classification
* `list_price`, `discount`, `final_price`
* `supplier_count`, `suppliers`
* `availability`: Stock status
* `eta`: Estimated time of arrival

### 2. `Table2_Shipping.csv`

Tracks shipment status for each product:

* `shipment_id` (PK): Unique shipment record
* `product_id` (FK): References Table1
* `carrier`, `origin`, `destination`
* `status`: Live shipping state (e.g., Delivered, Exception)
* `last_update`: Timestamp of last change

### 3. `Table3_Orders.csv`

Logs customer orders:

* `order_id` (PK): Unique order
* `customer_name`, `order_time`, `delivery_location`
* `product_id` (FK): References Table1
* `quantity`, `payment_method`

---

## 🧠 Company Policy Document

* `Company_Policy_Logistics.pdf`: Contains rule-based clauses related to delivery timelines, returns, shipping exceptions, and supplier evaluation.
* This document is parsed and indexed for retrieval in the RAG system.

---

## 🔁 Workflow Overview

### 1. Start the Pipeline

* `flow.py` orchestrates the full pipeline by running multiple scripts via `subprocess` in sequence.
* Ensures a clean, step-by-step execution of simulation, policy parsing, and retrieval setup.

### 2. Simulate and Ingest Data

* `simulate_data.py`: Generates synthetic logistics datasets (`Table1_Products.csv`, `Table2_Shipping.csv`, `Table3_Orders.csv`).
* These CSVs are ingested in **real-time** using **Pathway** to simulate live updates and streaming.

### 3. Parse Policy Document

* `extract_policy.py`: Reads the `Company_Policy_Logistics.pdf` and saves extracted content to `policy_clauses.txt` for indexing.

### 4. Semantic Retrieval using RAG

* `retri.py`:

  * Loads the policy clauses.
  * Creates semantic embeddings using FAISS.
  * Uses an OpenAI GPT model to respond to user queries contextually.
  * Run from terminal to ask natural language questions.

### 5. Main Integration Logic

* `main.py`: Bridges the different modules and can serve as an interactive layer between streaming and querying logic.

---

## ⚙️ Tech Stack & Tools

* `pathway` – real-time data streaming
* `pandas`, `faker` – synthetic dataset generation
* `sentence-transformers`, `faiss` – document embedding + retrieval
* `openai` – GPT-based question answering
* `fpdf` – PDF creation for policies

---

## 🔍 Example Queries

* "What is the ETA for product PDT015?"
* "Was there any damage report in the last 48 hours?"
* "Which clause applies if the shipment is marked Exception?"
* "What is the company’s return policy window?"

---

## ✅ Deliverables

* CSV Datasets:

  * `Table1_Products.csv`, `Table2_Shipping.csv`, `Table3_Orders.csv`
* Company Policy PDF:

  * `Company_Policy_Logistics.pdf`
* Code:

  * `simulate_data.py`, `extract_policy.py`, `flow.py`, `retri.py`, `main.py`
* README (this file)

---

## 🧑‍💻 Getting Started

### 1. Install Requirements

```bash
pip install -r req.txt
```

### 2. Set Environment Variable

```bash
export OPENAI_API_KEY=your-openai-api-key
```

### 3. Run the Full Pipeline

```bash
python flow.py
```

### 4. Query via Terminal

```bash
python retri.py
```

---


