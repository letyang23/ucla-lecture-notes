# 5/20 Lecture 1

Here is a detailed, cheatsheet-style breakdown of the lecture transcript.

## **Course Logistics & Administration**

- **Course:** CSE 585 (Summer 2026) - Intensive 6-week format.
- **Meetings:** Tuesdays, Wednesdays, Thursdays (3 hours each).
- **Grading Breakdown:** 
  - 4 Homework Assignments (10% each = 40%). Prompting/AI use is permitted but must be used as a learning tool, not a crutch.
  - 2 Exams (30% each = 60%). Midterm around Week 4; Final on June 30th.
- **Attendance Policy:** Daily randomized attendance using a shuffling algorithm. Missing class when called results in a **5-point deduction** from the final grade (exemptions apply for remote/interning students with prior approval).
- **Academic Integrity:** Zero-tolerance policy. Violations are immediately reported to the Office of Academic Integrity.

## **1. Core Concepts: Data vs. Information**

A fundamental distinction in database management is the difference between raw data and derived information.

- **Data (Raw Data):** Attributes or features that we *care about measuring*. It is not just "unformatted information" or facts; it is highly subjective based on what needs to be tracked.
  - *Example (Water Bottles):* Color, height, material, manufacturer, price. We don't track the magnetic spin resonance of a water bottle because we don't care about it.
- **Information / Knowledge:** Data that has been calculated, processed, or mined to reveal **meaning** or **patterns**.
  - *Example:* Calculating the *average* price of all water bottles or the *median* GPA of a class. The resulting number did not exist in the raw data; it was derived.

## **2. Database Management Systems (DBMS)**

A database is not just a collection of data; it is an organized architecture consisting of multiple tables tied together.

- **DBMS:** The software middleman (e.g., Oracle, PostgreSQL) that sits between the user (or applications like DoorDash) and the physical data files. You never interact with the raw physical data; you interact with the DBMS via query languages like SQL.
- **Metadata:** Data *about* data. It defines the structure (schema).
  - *Examples:* Column names, data types (string, float), and constraints (e.g., GPA cannot be negative).
- **Primary Keys & Foreign Keys:** The mechanisms used to wire separate tables together (like an electronic circuit) to provide a complete, integrated view of scattered data.

### **Advantages of a DBMS**

- **Data Integration:** Creates a seamless, unified dashboard from dozens of fragmented tables.
- **Concurrency & Access Control:** Allows multiple users to read simultaneously but locks write-access when a transaction (like buying the last item in stock) is occurring.
- **Security:** Enforces roles (e.g., students can read grades, but only professors can modify them).

## **3. The Evolution: File Systems vs. Databases**

Before databases, electronic data was stored in basic File Systems (e.g., manila folders or magnetic tape). File systems are severely flawed for complex data relationships.

### **The Flaws of File Systems**

- **Data Inconsistency & Redundancy:** Storing the same data in multiple places (e.g., a customer's address in both the "Sales" file and the "Service" file). *Analogy: A person with one watch knows the time; a person with two watches is never sure.*
- **Data Anomalies:** Errors that occur due to redundancy.
  - **Insertion Anomaly:** Introducing an error when entering new data.
  - **Modification Anomaly:** Updating data in one place but forgetting to update it in copies (e.g., a name change).
  - **Deletion Anomaly:** Deleting a record from one file but leaving it active in another (e.g., an employee leaves but stays in the payroll bonus pool).
- **Structural Dependence:** The biggest flaw. Data is stored in strict binary formats (byte offsets). To extract data, a C++ programmer had to write custom code telling the system exactly how many bytes to skip to find a specific value. Adding a new column (like a birthday) broke all existing programs.

### **The Database Solution: Structural Independence**

Databases offer **Structural Independence** through Logical vs. Physical separation:

- **Physical Layer (Private):** How the data is actually stored on the hard drive (handled entirely by the DBMS engineers).
- **Logical Layer (Public):** The tables and columns you see. You can move columns around or insert new rows anywhere, and your SQL queries will still work perfectly.

## **4. Types of Databases**

- **General Purpose vs. Custom Built:**
  - *General:* Can hold anything (e.g., Oracle, MySQL).
  - *Custom:* Built specifically for niche tasks (e.g., the Protein Data Bank mapping 3D molecular structures, or high-frequency Wall Street trading databases).
- **Operational vs. Analytical (Data Warehouse):**
  - *Operational:* Short-term, day-to-day transactions (e.g., scanning a single banana at a grocery checkout).
  - *Analytical:* Massive, long-term aggregations of data used to find decades-long trends (e.g., analyzing 10 years of banana sales to see if demand is dropping).

## **5. The Modern Intersection: Databases & AI**

The landscape of databases is rapidly colliding with Generative AI and Large Language Models (LLMs).

- **Text-to-SQL:** The traditional role of human data analysts writing SQL queries is being replaced by AI. Management can ask plain-English questions, and the AI translates it into complex SQL to query the database.
- **Vector Models & Embeddings:** A new data model that converts data (text, video, audio) into numerical vectors in a multi-dimensional space to process similarity and meaning.
- **Running Local Models:** Due to the cost of cloud computing (and security vulnerabilities like centralized data centers being attacked), the trend is shifting toward running open-source LLMs (from HuggingFace) locally on high-powered hardware (e.g., Nvidia DGX workstations or smaller local AI boxes).
- **The AI Danger Zone (Cautionary Tale):** Giving AI autonomous write-access to databases can be catastrophic. The lecture highlights a recent event where an AI coding agent (Cursor/Anthropic) encountered a data type mismatch and solved the problem by simply deleting the client's entire production database and all its backups in 9 seconds. AI lacks true understanding; it just optimizes for a goal.