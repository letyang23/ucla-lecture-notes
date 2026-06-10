# 5/20 Lecture 1

## Course Logistics & Mechanics

### Basic Information

- **Format:** 6-week summer intensive class (covers a 14-week curriculum).
- **Schedule:** Tuesdays, Wednesdays, and Thursdays for 3 hours each (with a break around 4:30 PM).
- **Instructor Background:** 22-year career in computer graphics (Dreamworks 1996-2012, credits include *Shrek*, *Kung Fu Panda*), shifted to ML, Data Science, and Non-Symbolic AI (biologically motivated AI).
- **Communication:** Piazza is the primary platform; Discord is available for casual chat.
- **Platforms Used:** Course website (HTML rendered from Markdown), Brightspace (for homework submissions and grades).

### Grading Breakdown

| **Assessment**   | **Count** | **Weight**     | **Details**                                  |
| ---------------- | --------- | -------------- | -------------------------------------------- |
| **Homework**     | 4         | 40% (10% each) | No extra credit homeworks; strict deadlines. |
| **Midterm Exam** | 1         | 30%            | Week 4 (Wednesday); 1-hour duration.         |
| **Final Exam**   | 1         | 30%            | Held on June 30th; 1-hour duration.          |

### Policies

- **Attendance:** Mandatory. A random-shuffle script selects names during class. Missing a called attendance results in a **5-point deduction** from the final grade. (Exemptions apply for officially remote/interning students).
- **Remote Students:** Must be >100 miles from campus. Exams require a local proctor (manager), a testing center, or Honorlock.
- **Academic Integrity:** Zero-tolerance policy. Violations are reported blindly to the Office of Academic Integrity; penalties often include failing the course or job rescission.
- **Regrading:** Requesting a regrade prompts a full top-to-bottom review of the submission, risking a lower score if prior grading errors favored the student (double jeopardy).
- **Generative AI Usage:** Allowed and encouraged as a learning tool to generate SQL or ER diagrams, but submitting purely AI-generated work without understanding it defeats the purpose.

## Part 1: The Modern AI Landscape

### Industry Shifts

- **Generative AI & Jobs:** AI tools (like Gemini Omni) can now write complete applications and generate cinematic video, disrupting traditional software engineering and creative roles.
- **Public Pushback:** Tech leaders (like Eric Schmidt) and commencement speakers praising AI are facing heavy backlash and booing from students concerned about job displacement.
- **AI Risks in Production:** A "Cursor" AI agent recently went rogue and deleted a company’s entire production database (and backups) in 9 seconds to forcefully resolve a string-to-integer casting error. AI lacks true understanding; it strictly follows prompt instructions or reward-hacks.

### Local vs. Cloud LLMs

- **Cloud Vulnerability:** Centralized cloud data centers are vulnerable to physical attacks and outages.
- **Local Processing:** NVIDIA and others are pushing desktop supercomputers (e.g., DGX Station, Spark) to run massive parameter models locally for speed and privacy.
- **Hugging Face:** An open-source repository containing millions of pre-trained LLMs that can be downloaded locally and integrated via simple Python APIs (Gradio, Streamlit) to build apps instantly.

## Part 2: Core Database Concepts

### What is Data?

- **Definition:** Data is strictly the **attributes or features that we care about measuring**.
- **Subjective Modeling:** Data collection requires idealizing and abstracting the real world. For a water bottle, you might care about color, weight, and price. A physicist might care about magnetic resonance. The columns you choose to record *are* the data model.

### Data vs. Information vs. Knowledge

| **Term**                    | **Definition**                                               |
| --------------------------- | ------------------------------------------------------------ |
| **Data (Raw Data)**         | The raw attributes stored in columns and rows. Contains patterns, but the patterns are not immediately obvious. |
| **Processing**              | The mechanism applied to the data (e.g., averaging, ML algorithms, data mining). |
| **Information / Knowledge** | The output of processing. It reveals meaning or insights not explicitly present in the raw data (e.g., the median GPA of a class, the average home price). |

### Database Architecture

- **Database:** Software holding organized tables of data, wired together logically.
- **Metadata:** Data about the data. Includes column names, data types, schema definitions, and constraints (e.g., "GPA cannot be negative").
- **DBMS (Database Management System):** The middleman abstraction layer between raw storage and the end-user.
- **SQL (Structured Query Language):** The language used to query the DBMS, which traverses multiple tables using Primary and Foreign keys to return integrated information.

### DBM Functions

- **Data Integration:** Seamlessly joins data from dozens of tables into a unified dashboard.
- **Concurrency / Sharing:** Allows multiple users to read simultaneously but locks write-access so two users cannot buy the same exact item concurrently.
- **Authentication / Security (IAM):** Controls who has read vs. write privileges.
- **Storage Management:** Optimizes where data is physically stored (RAM vs. slow hard drives).

## Part 3: File Systems vs. Databases

### The Flaws of Legacy File Systems

- **Isolation:** Data is siloed in separate manila folders or isolated binary files, making it nearly impossible to cross-reference (e.g., comparing HR files to Sales files).
- **Redundancy & Inconsistency:** Data is copied multiple times. If a name changes in one file but not another, you get conflicting data and don't know which is true (the "two watches" problem).
- **Structural Dependence:** Programs reading the files rely on strict byte-offsets. If you add a new column (like "Birthday"), all existing programs crash because the data layout changed.
- **Data Dependence:** The program assumes specific data formats (e.g., assuming a name is strictly 12 bytes long).

### The Database Solution

- **Structural Independence:** You can add, move, or shuffle columns and rows in a database without breaking the SQL queries querying them.
- **Public Interface vs. Private Storage:** Just like a C++ class with a `public` interface and `private` variables, a DBMS hides the chaotic, physically dependent file layout (private) behind a clean SQL interface (public). You do not need to know the byte offsets to query it.

### Data Anomalies (Caused by Redundancy)

- **Insertion Anomaly:** Errors introduced when inputting redundant data into a system.
- **Modification Anomaly:** Updating a value (like a last name) in one table but forgetting to update it in duplicate locations.
- **Deletion Anomaly:** Deleting a record from the main database but failing to delete it from secondary lists (e.g., an employee leaves but remains on the payroll database).

## Part 4: Database Types

| **Database Category**      | **Description**                                              | **Example**                                                  |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Single-User**            | Local database meant for one active user or device.          | SQLite (used in Android contacts)                            |
| **Multi-User**             | Designed for concurrent access by a department (Workgroup) or whole company (Enterprise). | Amazon catalog, Bank of America                              |
| **Centralized**            | A legacy model where all data lives on one physical mainframe. Highly vulnerable to localized disasters. | Old IBM 360 systems                                          |
| **Distributed**            | Data is scattered globally across nodes. Improves speed and fault tolerance. | Modern Cloud Providers (AWS)                                 |
| **General Purpose**        | Can hold any text, number, or standard format data.          | Oracle, PostgreSQL                                           |
| **Special Purpose**        | Custom-built for a highly specific industry or data structure. | Protein Data Bank (3D chemical structures), Wall Street HFT algorithms |
| **Operational**            | Stores live, day-to-day transactional data.                  | A retail store checkout lane                                 |
| **Analytical (Warehouse)** | Stores massive, historical data dumps optimized for long-term data mining. | Corporate sales trend databases                              |



# 5/21 Lecture 2

## Fundamentals of Data Modeling

- **Definition:** Data modeling is the process of using mathematics/structures to represent the real world by deliberately abstracting away unnecessary details.
- **The Golden Rule:** As statistician George Box stated, *"All models are wrong, but some are useful."* They are "wrong" because they leave out real-world intricacies (like modeling a skyscraper as a simple cuboid), but they are exactly detailed enough to be functional.
- **Domain Knowledge & Business Rules:** Database designers are not industry experts. To build a model, you must interview domain experts (e.g., animators at Dreamworks, factory floor machinists) to capture their "business rules" or domain knowledge.
- **Self-Documenting:** A good database should be clear and use the common terminology of the industry (e.g., using "Revenue" instead of abstract variable names).

## The Evolution of Data Models

Data models have evolved across ten major variations over the decades. The primary models include:

| **Model Type**      | **Key Concept**                                              | **Real-World Examples**                                      |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Hierarchical**    | Tree data structure. A parent can have many children, but a child only has one parent. | Org charts, US Military hierarchy, Carl Linnaeus' biological classification, course prerequisites. |
| **Network**         | Graph data structure. Solved the tree limitation by allowing a child to have multiple parents. | Early complex systems where data couldn't fit a strict tree. |
| **Relational**      | Data is forced into tables (rows and columns). Invented by Edgar F. Codd (IBM) in 1970. Subsumes both hierarchical and network models. | Oracle (founded by Larry Ellison based on Codd's paper).     |
| **Object-Oriented** | Rows of data are stored and manipulated directly as programmatic objects. Database community resisted this, but it works well for complex designs. | CAD software (SolidWorks, AutoCAD), Revit architecture.      |
| **NoSQL**           | Non-tabular models for unstructured data, including Document, Graph, Column, and Key-Value. | MongoDB, CouchDB.                                            |
| **Vector**          | Data (images, text, audio) is embedded as coordinate points in n-dimensional space. Searched using cosine similarity (dot product). | Pinecone (used for RAG - Retrieval-Augmented Generation).    |

## The Relational Model (Tables)

The relational model organizes data into physically separate tables that are virtually connected. It operates with **100% positional independence**, meaning the order of the columns and the rows does not matter to the software.

| **Database Term** | **Alternative Names / Analogies**         | **Conceptual Rules**                                      |
| ----------------- | ----------------------------------------- | --------------------------------------------------------- |
| **Table**         | Entity, Relation                          | Must be a **Noun** (e.g., Students, Courses, Traffic).    |
| **Column**        | Attribute, Field, Feature, Characteristic | Must be single-valued (no arrays/lists in a single cell). |
| **Row**           | Tuple, Record, Instance, Occurrence       | Represents one specific instantiation of the entity.      |
| **Connection**    | Relationship                              | Must be a **Verb** (e.g., "Enrolls", "Teaches").          |

- **Constraints:** Security mechanisms placed on columns to ensure clean data entry (e.g., GPA must be between 0 and 4; Hourly wage cannot be negative).

## Keys and Table Connectivity

There are only three possible ways to connect any two tables. Tables are stitched together using **Keys**:

- **Primary Key (PK):** A column where the identifier occurs only *once* in that table (e.g., Student ID in the Students table). Cannot repeat.
- **Foreign Key (FK):** A column that references another table's Primary Key. This value *can* repeat many times.

### 1. One-to-Many (1:M)

The most common relationship. One row in the left table participates with many rows in the right table.

- **Example 1:** One Painter (Monet - PK) paints Many Paintings (FKs pointing to Monet).
- **Example 2:** One Customer generates Many Invoices.
- **Example 3:** One Doctor writes Many Prescriptions.

### 2. Many-to-Many (M:N)

The second most common relationship. It acts as a two-way one-to-many relationship and **requires a third "Bridge" table** (often called an enrollment or line-item table) to hold the foreign keys from both original tables.

- **Example 1:** Many Students take Many Courses. (Bridge: Enrollment table).
- **Example 2:** Many Authors publish in Many Conferences.

### 3. One-to-One (1:1)

The rarest relationship.

- **Example 1:** Exactly One Employee manages Exactly One Starbucks store.
- **Example 2:** Exactly One Professor chairs Exactly One University Department.

## Diagrams and Schemas

- **ER Diagrams (Entity-Relationship):** A visual communication tool detailing tables, columns, and relationships so stakeholders can verify the design before code is written.
- **Sub-schemas:** A filtered piece of the overall schema shown to specific stakeholders (e.g., only showing the Facilities team the building capacity tables, hiding academic records).
- **Notations:** Visual symbols used to draw relationships.
  - **Crow's Foot:** The most popular industry notation (uses a split foot symbol for "many").
  - **UML (Unified Modeling Language):** Originally designed for Object-Oriented programming classes, adapted for database diagramming.
  - **Chen:** Uses diamond shapes for relationships.

## Implementation & Architecture

### SQL Operations

Instead of interacting with underlying file structures, users write **SQL (Structured Query Language)**.

- **DDL (Data Definition Language):** Creates the empty table structures based on the ER diagram (e.g., `CREATE TABLE`).
- **DML (Data Manipulation Language):** Populates, modifies, or extracts data from those tables (e.g., `INSERT INTO`).

### Object-Relational Storage

To bridge the gap between relational databases and object-oriented frontends (like Java or Python), developers use Object-Relational mapping. Data is stored as tables on disk but read into memory as objects.

- In Python, turning an object into a storable byte-stream is called **Pickling** (serialization).
- In JavaScript, this is done using `JSON.stringify()` (to text) and `JSON.parse()` (back to object).

### Data Independence Levels

- **External/Conceptual Model:** The high-level API. This is what the SQL programmer and database designer see (Tables, relationships, columns).
- **Physical/Internal Model:** The actual binary file format on the hard drive. DBMS vendors (like Oracle) keep this **strictly private**. If they published the file format, users would write code directly against it, permanently preventing Oracle from ever upgrading or altering their backend implementation.

# 5/26 Lecture 3

### Data Modeling Layers

Data models exist on different levels of abstraction, moving from the human perspective down to the machine level.

| **Model Level** | **Description**                           | **Key Characteristics**                                      |
| --------------- | ----------------------------------------- | ------------------------------------------------------------ |
| **External**    | The naive end-user or stakeholder view.   | Highly fragmented. Users only see the narrow slice of the database they care about (e.g., a student only sees course registration). |
| **Conceptual**  | The unified global view for the designer. | High-level picture. Combines all external views into one diagram containing only table names and relationships (no column details yet). |
| **Internal**    | The database implementation view.         | Adds exact details. Includes specific column names, data types, and SQL schema definitions. |
| **Physical**    | The lowest hardware-level view.           | Highly detailed binary file formats custom to the specific vendor (e.g., Oracle vs. SQLite). Provides "physical independence" so backend systems can change without breaking the SQL layer. |

### Entity-Relationship (ER) Basics

ER diagrams conceptually model how data is organized across the database.

- **Entities:** Visualized as rectangles. They represent entire tables (e.g., "Student" or "Chair").
- **Attributes:** The specific columns that make up an entity.
- **Primary Key (Identifier):** A required attribute that uniquely identifies each row. It cannot be null and cannot be duplicated. Single-column random integers are best practice.
- **Composite Key:** A primary key made of two or more combined columns (e.g., First Name + Last Name). Generally considered bad practice compared to a single random ID.
- **Optional Attribute:** A column that is allowed to accept null values.
- **Domain:** The restricted range of legal values for a column (e.g., GPA must be between 0.0 and 4.0).
- **Compound Attribute:** An attribute that can be subdivided into smaller pieces (e.g., an Address broken into Street, City, ZIP).
- **Simple Attribute:** An attribute that cannot be further divided (e.g., Salary).
- **Multi-valued Attribute:** An attribute trying to hold multiple values (e.g., multiple programming languages). Tables do not allow this natively; you must resolve it by creating a separate table.
- **Derived Attribute:** A value calculated from other existing data (e.g., deriving Age from Birthdate). You must trade off computation cost versus storage space when deciding to store or calculate these.

### Relationships & Cardinality

Relationships dictate how tables interact with one another.

- **Connectivity:** Broadly defines the type of relationship (1 to 1, 1 to Many, Many to Many).
- **Cardinality (Min/Max):** Puts strict numerical limits on the connectivity. Expressed as a minimum and maximum (e.g., a professor teaches a minimum of 1 and a maximum of 4 classes). Read backwards (right to left) on diagrams.
- **Mandatory Participation:** The minimum cardinality is at least 1.
- **Optional Participation:** The minimum cardinality is 0.
- **Table Cardinality:** A separate definition referring simply to the total number of rows in a table.
- **Table Degree:** A separate definition referring simply to the total number of columns in a table.

### Dependency & Weak Entities

Not all tables stand on their own; some rely entirely on the existence of others.

- **Standalone / Strong Entity:** Exists independently (e.g., an Employee table).
- **Dependent Entity:** Its existence relies on a parent table (e.g., an Employee Dependents/Spouses table). If the parent row is deleted, the dependent row must also vanish.
- **Weak Entity:** A dependent entity that uses its parent's primary key as part of its own composite primary key. This creates a "strong relationship" (tight coupling) which can be poor design.
- **Non-Weak Dependent Entity:** A dependent entity that uses a standard Foreign Key to link to the parent, while maintaining its own unique, standalone Primary Key (e.g., a random 10-digit ID).

### Degrees of Participation & Bridge Tables

The "degree" of a relationship refers to how many distinct tables are actively participating in the connection.

| **Degree**   | **Relationship Type** | **Example**                                                  |
| ------------ | --------------------- | ------------------------------------------------------------ |
| **Degree 1** | Unary / Recursive     | An Employee table linking to itself (Employees managing Employees). |
| **Degree 2** | Binary                | A Professor table linking to a Classes table.                |
| **Degree 3** | Ternary               | Doctors, Patients, and Drugs all linking together via a Prescription table. |

- **Bridge Tables:** Also known as composite tables. They resolve "Many to Many" relationships.
- **Bridge Table Structure:** They contain the primary keys of the participating entities as foreign keys.
- **Bridge Table Extensibility:** You can add extra columns to a bridge table (e.g., adding a "Grade" column to a Student-Course enrollment bridge).

### Extended ER (EER) & Specialization Hierarchies

EER introduces object-oriented concepts like inheritance into database diagrams to prevent repetitive boilerplate.

- **Super-types & Sub-types:** Works exactly like single-parent inheritance in Java. A sub-table automatically inherits all columns and relationships from the super-table.
- **Disjoint Constraint (D):** An entity can only exist in ONE sub-type. (e.g., An airline employee is a Pilot OR a Mechanic, never both). Requires a "Subtype Discriminator" column to identify their role.
- **Overlap Constraint (O):** An entity can exist in multiple sub-types simultaneously (e.g., An employee can be an Administrator AND a Professor).
- **Partial Constraint (1 Line):** The list of sub-types is incomplete. Entities can exist in the super-type without belonging to any sub-type yet (e.g., a "predatory hire" with no assigned department).
- **Total/Complete Constraint (2 Lines):** The list of sub-types is exhaustive. Every single entity in the super-type MUST belong to at least one sub-type.
- **Union Types:** An upside-down hierarchy where multiple distinct tables funnel into one. For example, individuals, banks, and companies all union together into a generic "Owner" table for vehicle registration.

### Diagram Clustering

- **Visual Clusters:** For incredibly complex databases (hundreds of tables), designers can visually sweep related tables together into collapsed nodes.
- **Function:** Double-clicking the node expands it into a sub-schema, keeping the global architectural view clean and readable.

### Professor's Trivia & Tangents

The lecture included a few colorful diversions worth noting for context:

| **Topic**            | **Note**                                                     |
| -------------------- | ------------------------------------------------------------ |
| **RGB Colors**       | 24-bit color results in roughly 16.7 million possible combinations. Used as an analogy for compound attributes. |
| **AI vs. Humans**    | The professor highlighted that AI coding agents are becoming too expensive in token costs, suggesting human software engineers are cheaper and safer from replacement than the hype implies. |
| **Mutual Recursion** | Illustrated using an "is_even" and "is_odd" function calling each other to determine parity. |
| **Thor Scaling**     | A concept mentioned regarding advanced chip architecture (logic folding) that minimizes signal distance travel rather than relying strictly on transistor density (Moore's Law). |



# 5/27 Lecture 4

## Lecture Cheat Sheet: Relational Database Modeling & Algebra

### 1. Table & Relation Basics

A relational database is built on the simple, multi-billion-dollar idea of 2D table structures.

- **Relation:** Can refer to a Table (2D structure of rows and columns), a Relationship (how tables connect), or a Cell (intersection of a row and column).
- **Row:** Also called a Tuple, Record, Entity Occurrence, or Object.
- **Column:** Also called an Attribute. Contains values of the exact same data type.
- **Domain:** The legal range of values allowed in a specific column (e.g., GPA must be between 0 and 4.0).
- **Structural Independence:** The order of rows and columns is entirely immaterial. You can shuffle them logically without changing the data's meaning.

### 2. The Anatomy of Keys & Functional Dependency

Keys act as pointers. Their primary job is **Determination**: a key determines all the non-key attributes in a row.

| **Key Type**         | **Definition & Example**                                     |
| -------------------- | ------------------------------------------------------------ |
| **Super Key**        | Any set of columns that *could* uniquely identify a row (even if it contains useless extra columns). |
| **Candidate Key**    | A minimal Super Key. Stripped of all extra garbage columns; every remaining column is strictly necessary for uniqueness. |
| **Primary Key (PK)** | The ultimate winner of the Candidate Keys. Usually a single, numeric column (e.g., Student ID). |
| **Composite Key**    | A key made of multiple columns (e.g., First Name + Last Name + Middle Initial). |
| **Foreign Key (FK)** | A Primary Key from one table placed into another table to establish a relationship. Values here *can* repeat. |
| **Secondary Key**    | An alternate lookup method used purely for data retrieval (e.g., using a Phone Number for a Ralph's Club Card). |
| **Surrogate Key**    | A meaningless, system-generated number (e.g., Amazon Order ID). **Best practice.** |
| **Natural Key**      | A key based on real-world data (e.g., Social Security Number, Address). **Bad practice—avoid due to privacy/security risks.** |

**The "Court Oath" Rule of Functional Dependency**

For a Composite Primary Key, you must achieve **Full Functional Dependency**. You must use *"The truth (the key), the whole truth (don't leave any columns out), and nothing but the truth (don't add extra unnecessary columns)."* If you can look up a value using only a *partial* piece of the composite key, your table is poorly designed (Partial Functional Dependency) and needs normalization.

### 3. Database Integrity & NULLs

Database software (like Oracle or MySQL) enforces rules to ensure your data isn't corrupted.

- **Entity Integrity:** Applies to a *single table*. The Primary Key must be unique, and it cannot be NULL. No two rows can be 100% identical.
- **Referential (Foreign Key) Integrity:** Applies across *two tables*. Every Foreign Key must point to a valid, existing Primary Key (no "dead pointers"). If you delete a Primary Key, the system must handle the orphaned Foreign Keys via operations like **Cascade Delete** or **Cascade Update**.
- **NULL Values:** Represents missing, unknown (like finding life in other galaxies via Drake's Equation), or inapplicable data.
- **Handling NULLs:** Avoid them when possible. Workarounds include setting a `NOT NULL` constraint (which forces you to input fake placeholder data), using error codes (e.g., `-1`), or using flags.

### 4. Relational Algebra & Closure

This is Edgar Codd's genius underlying all SQL. The magic lies in **Closure**: an operation takes a table as an input and outputs a *new table* of the exact same data type. Because the output is always a table, you can infinitely chain operations together (Data Flow).

| **Operation**           | **Type**          | **Function**                                                 | **SQL Equivalent**      |
| ----------------------- | ----------------- | ------------------------------------------------------------ | ----------------------- |
| **Select (Restrict)**   | Unary (1 Table)   | Filters **rows** to create a horizontal subset (e.g., only students with > 3.5 GPA). | `WHERE` clause          |
| **Project**             | Unary (1 Table)   | Filters **columns** to create a vertical subset (e.g., returning only the "Price" column). | `SELECT col_names`      |
| **Union**               | Binary (2 Tables) | Merges rows from two tables, discarding duplicates. Tables must be "Union Compatible" (exact same columns). Commutative. | `UNION`                 |
| **Intersection**        | Binary (2 Tables) | Returns only rows that exist in *both* tables. Commutative.  | `INTERSECT`             |
| **Difference**          | Binary (2 Tables) | Subtraction ($A - B$). Returns rows in A that are NOT in B. **Not Commutative.** | `EXCEPT` / `MINUS`      |
| **Product (Cartesian)** | Binary (2 Tables) | Multiplies every row in A by every row in B. Yields $M \times N$ rows and $P + Q$ columns. | `CROSS JOIN`            |
| **Divide**              | Binary (2 Tables) | Matches values in Table A against *all* values in a specific column of Table B. | (No direct SQL command) |

### 5. Table Joins

Joins intelligently combine tables at runtime by cutting and pasting matching rows next to each other based on common values. A Join is essentially a Product operation followed by a Select (filtering) operation.

- **Inner Join:** The standard join. Only combines rows where the join columns find a match.
- **Natural Join:** Implicitly joins based on columns that share the exact same name across both tables.
- **Equi-join:** Joins based on strict equality (`=`).
- **Theta Join:** Joins based on any other mathematical operator (`<`, `>`, `!=`).
- **Left Outer Join:** Returns *all* rows from the left table, even if there is no match on the right. Missing right-side values appear as blanks (NULLs). Great for exposing data holes (e.g., a customer with no assigned salesperson).
- **Right Outer Join:** Returns *all* rows from the right table, regardless of matches on the left.
- **Full Outer Join:** A Union of the Left and Right Outer joins. Returns everything from both sides, with NULLs wherever matches are missing.

### 6. Metadata Terminology

Data about your data. Don't mix up your naming conventions!

- **Data Dictionary / System Catalog:** Where the system stores non-table data, such as column names, data types, constraints, and disk size.
- **Homonyms:** Using the same name for two different things (e.g., calling both Salary and Grade Point Average "GPA"). Don't do this.
- **Synonyms:** Using different names for the exact same thing across tables (e.g., "GPA" in one table and "Grade_Point_Avg" in another). Don't do this either.

# 5/28 Lecture 5

## Database Architecture & Design Basics

### The Full Stack Context

- **Frontend:** The app or browser the user interacts with.
- **Backend/Server:** The intermediary that handles logic and requests.
- **Database:** The storage layer. Apps *never* log directly into the database; they go through the server.

### What is Normalization?

Normalization is a systematic database design process applied to **one table at a time** to reduce data redundancy and eliminate data anomalies.

- **Goal:** Ensure the table structure is "well-formed" (every non-key attribute depends on the *key, the whole key, and nothing but the key*).
- **Redundancy:** Repeating the same data in multiple rows (wastes space and slows down updates).
- **Anomalies:** Errors that occur during data manipulation (Insert, Update, Delete) due to poor structure.

### Types of Dependencies to Fix

- **Partial Dependency:** When a non-prime column only depends on *part* of a composite primary key. (e.g., In a table keyed by `Project_ID` and `Employee_ID`, the `Employee_Name` only depends on `Employee_ID`).
- **Transitive Dependency:** When a non-prime column depends on another non-prime column, rather than the primary key. (e.g., `Employee_ID` -> `Job_Title` -> `Hourly_Rate`).

## The Normal Forms (NFs)

Normalization happens in progressive, sequential steps. You cannot skip straight to 3NF.

| **Normal Form**              | **Requirements & Characteristics**                           |
| ---------------------------- | ------------------------------------------------------------ |
| **0NF (Unnormalized)**       | Raw data, often from spreadsheets. Contains repeating groups, blanks/nulls, and positional dependencies. Lacks primary keys. |
| **1NF (First Normal Form)**  | Fill in all blank spaces. Eliminate repeating groups. Identify a Primary Key. Data is now tabular, but partial/transitive dependencies remain. |
| **2NF (Second Normal Form)** | Must be in 1NF. **Remove all Partial Dependencies** by creating new tables. (Transitive dependencies may still exist). |
| **3NF (Third Normal Form)**  | Must be in 2NF. **Remove all Transitive Dependencies** by creating new tables. This is the ideal state for most business databases. |

### Advanced Database Concepts

- **Dependency Diagrams:** Visual checklists used during design. Primary keys are highlighted, and arrows map dependencies. Top arrows show correct key dependencies; bottom arrows highlight partial/transitive errors to be fixed.
- **Denormalization:** Intentionally stepping backward (e.g., from 3NF to 2NF) to reintroduce redundancy. Done *only* when end-users complain about slow query speeds caused by joining too many highly normalized tables.
- **Indexing:** Creating a separate, sorted background table (like a book's index) pointing to row IDs. Speeds up searches exponentially by allowing binary search (converting an $O(N)$ linear scan into an $O(\log N)$ search).

## Introduction to SQL (Structured Query Language)

SQL is fundamentally divided into two distinct categories: defining the table structure and manipulating the actual data.

### 1. DDL (Data Definition Language)

Used to define or modify database schemas (the structure, not the data).

- **CREATE TABLE:** Sets up a new, empty table with defined columns and data types.
- **ALTER TABLE:** Changes existing table structure (e.g., adding or dropping a column).
- **DROP TABLE:** Completely deletes a table and its structure.
- **CREATE INDEX / CREATE VIEW:** Builds indexes for speed or temporary views for querying.

### 2. DML (Data Manipulation Language)

Used to insert, modify, and query the actual data inside the tables.

- **INSERT INTO:** Adds a new row of data. Values must match the exact count, order, and type of the table definition.
- **UPDATE:** Modifies existing data. Always paired with a `WHERE` clause (e.g., `SET price = 20 WHERE product_id = 5`).
- **DELETE:** Removes rows from a table. (If used without a `WHERE` clause, it deletes all rows).
- **SELECT:** Queries data from the database.

### Core SQL Data Types

- **NUMBER:** Used for integers and decimals. Example: `NUMERIC(4,2)` means 4 total digits, 2 of which are after the decimal (e.g., 99.99).
- **CHAR:** Fixed-length strings (e.g., `CHAR(2)` for US State abbreviations).
- **VARCHAR2 / NVARCHAR2:** Variable-length strings. `NVARCHAR2` supports Unicode/foreign characters.
- **DATE:** Used for calendar dates. Allows mathematical operations (e.g., `Invoice_Date + 30` to calculate Net 30 payment terms).

### Important Table Constraints

Constraints dictate the rules for the data entering your table during the `CREATE TABLE` phase.

- **PRIMARY KEY:** Uniquely identifies each row. Cannot be null.
- **FOREIGN KEY:** Links to a primary key in another table. Can use `ON UPDATE CASCADE` (if the parent key changes, child keys update automatically) or `ON DELETE CASCADE`.
- **NOT NULL:** Prevents a column from being left blank.
- **UNIQUE:** Ensures no duplicate values exist in a specific column.
- **DEFAULT:** Automatically fills a predefined value if the user leaves it blank during insertion.

## Mastering the SELECT Statement

The `SELECT` command is the heart of SQL, acting similarly to a `for` loop combined with an `if` statement.

### The Anatomy of a Query

- **SELECT:** Chooses the columns to display (Projection). `SELECT *` grabs all columns.
- **FROM:** Specifies the target table.
- **WHERE:** Acts as the filter (`if` statement) for rows. Can use operators like `=`, `<`, `>`, `<=`, `>=`, `<>` (not equal).
- **GROUP BY:** Clusters data into subsets (e.g., finding the average GPA per major).
- **HAVING:** Acts as a `WHERE` filter specifically for grouped data.
- **ORDER BY:** Sorts the visual output (does not alter the actual table data).

### Logical & Special Operators

- **AND / OR / NOT:** Combines multiple `WHERE` conditions.
- **BETWEEN:** Syntactic sugar for ranges (e.g., `BETWEEN 2010 AND 2015`).
- **IS NULL / IS NOT NULL:** Specifically searches for missing data.
- **LIKE:** String matching using wildcards (e.g., `LIKE 'L%'` finds names starting with L).
- **IN:** Checks if a value exists within a provided list (e.g., `IN ('Shirts', 'Pants')`).
- **DISTINCT:** Filters out duplicate outputs in the results (e.g., showing unique graduation months).

### Aggregate Functions (Column Operations)

These run math operations vertically down a single column.

- **AVG():** Calculates the average.
- **SUM():** Adds all numbers together.
- **MIN() / MAX():** Finds the lowest or highest value.
- **COUNT():** Returns the total number of rows. `COUNT(*)` includes null values.

### Transactions

- **COMMIT:** Permanently writes your local session changes to the master database. Cannot be undone.
- **ROLLBACK:** Undoes changes made in the current session *before* a commit occurs.

## Recommended SQL Practice Tools

- **Browser-based (Zero setup):** SQL Fiddle, IDEone, W3Schools SQL tutorial, Khan Academy SQL.
- **Local Installs:** Oracle Express Edition (XE), PostgreSQL via Docker.
- **Cloud Tier (Free options):** AWS, Google Cloud Platform (GCP), Azure.



# 6/2 Lecture 6

## 📝 Midterm Announcements & Exam Strategy

- **Format:** Open-ended, interview-style questions. No multiple choice.
- **Focus:** Practical application and critical thinking. No rote memorization required.
- **Resources:** Cheat sheets are allowed (like a "comfy blanket"), but understanding concepts is what truly matters.

## 💾 Core SQL Commands & Concepts

### 1. Data Definition Language (DDL) vs. Data Manipulation Language (DML)

- **DDL (Defining the schema):** `CREATE`, `DROP`, `ALTER`
- **DML (Modifying the data):** `INSERT`, `SELECT`, `UPDATE`, `DELETE`

### 2. Table Creation & Row Manipulation

- **`CREATE TABLE`:** Acts similarly to a C-struct (public data members, no methods). Defines columns, data types, primary keys, and foreign keys.
- **`INSERT INTO`:** Adds rows. **Crucial:** The order of the inserted values *must* match the order of the columns defined in the `CREATE TABLE` schema.
- **`UPDATE`:** Modifies existing cell values. Always use with a `WHERE` clause to avoid overwriting the entire column.
- **`DELETE FROM` vs. `DROP TABLE`:**

| **Command**          | **Action**                   | **Table Structure (Schema)**           |
| -------------------- | ---------------------------- | -------------------------------------- |
| `DELETE FROM table;` | Wipes out all row data.      | Kept intact.                           |
| `DROP TABLE table;`  | Destroys the table entirely. | Wiped out. Must recreate to use again. |

### 3. Modifying Existing Tables (`ALTER TABLE`)

Used to change table metadata without destroying the table.

- **`ADD`:** Add a new column.
- **`DROP`:** Remove a column (some DBs require you to set all values to `NULL` first to prevent accidental data loss).
- **`MODIFY`:** Change column properties (e.g., widen from `CHAR(3)` to `CHAR(5)`). *Note: Shrinking columns is usually blocked to prevent data loss.*

## 🧠 Operators & Filtering Data (`WHERE` Clause)

SQL has no assignment operator variables, so the `=` sign is strictly used for **comparison**, not assignment (unlike `==` in Python/C++).

### Computed Columns & Math Precedence

You can compute new columns on the fly (e.g., `price * quantity`).

- **Alias (`AS`):** Rename your computed columns for readability (e.g., `price * qty AS total_value`).
- **Precedence:** `()` > Exponents > `*` , `/` > `+` , `-`.

### Advanced Logic & Pattern Matching

- **`BETWEEN a AND b`:** Inclusive range query. Replaces `val >= a AND val <= b`.
- **`IS NULL`:** Flags empty/missing fields.
- **`LIKE`:** String pattern matching.
  - `%`: Matches zero or more characters (e.g., `J%` matches "John" or "J").
  - `_`: Matches exactly *one* character (e.g., `_m_th` matches "Smith").
- **De Morgan's Laws:** Apply these to simplify complex `WHERE` logic:
  - `NOT (A OR B)` $\equiv$ `NOT A AND NOT B`
  - `NOT (A AND B)` $\equiv$ `NOT A OR NOT B`

## 🔄 Subqueries & Advanced Filtering

A subquery is like a function call inside your main query. The main query waits for the subquery to finish before executing.

- **`IN` (Static vs. Dynamic):**
  - *Static:* `WHERE vendor_id IN (1, 2, 3)` (Hardcoded at compile time).
  - *Dynamic:* `WHERE vendor_id IN (SELECT id FROM active_vendors)` (Evaluated at runtime. Highly flexible). *Note: The subquery must return only ONE column.*
- **`EXISTS` / `NOT EXISTS`:** A "secret handshake" between tables without explicit `JOIN` syntax. Evaluates to True if the subquery returns *any* rows. `NOT EXISTS` is simply the mathematical complement.

### Bulk Data Updates

Instead of row-by-row insertion, you can transfer data in bulk:

1. **Two-Step:** Create an empty table $\rightarrow$ `INSERT INTO new_table SELECT * FROM old_table;`
2. **One-Step:** `CREATE TABLE new_table AS SELECT * FROM old_table;`

- *Note:* The one-step method transfers data but may drop constraint definitions (like Primary Keys), requiring a subsequent `ALTER TABLE` to fix.

## 📊 Analytics: Sorting, Grouping, & Aggregates

### 1. Visual Ordering & Distinct Values

- **`ORDER BY`:** Sorts the output purely for visualization. Cascades via commas (e.g., `ORDER BY last_name ASC, first_name ASC`). Default is Ascending (`ASC`).
- **`DISTINCT`:** Collapses identical values into one. Great for finding unique categories.

### 2. Aggregate Operations (Column Operations)

Functions that compute across rows to return a single value: `SUM()`, `AVG()`, `COUNT()`, `MIN()`, `MAX()`.

- **The `NULL` Trap:** * `COUNT(column_name)` counts only non-null values.
  - `COUNT(*)` counts *all* rows, including nulls. Nulls can severely distort averages.
- **Performance Inefficiency:** You cannot use an aggregate directly in a `WHERE` statement. `WHERE price = (SELECT MAX(price) FROM table)` forces the DB to compute the max, then rescan the *entire* table row-by-row to compare.

### 3. `GROUP BY` & `HAVING` (Data Categorization)

- **`GROUP BY`:** Partitions data into categories (e.g., finding the average GPA *per department* rather than a single global average).
- **`HAVING`:** The equivalent of a `WHERE` clause, but specifically used to filter **aggregated/grouped data**. (e.g., Group by department, `HAVING AVG(GPA) > 3.5`).

## 🚀 Optimization & Real-World Tech Stack

### Math Optimization Tangent (The "Lerp" Trick)

When computing Linear Interpolation (Lerp) for things like Trig Tables:

- Standard Formula: $x = b \cdot f + a \cdot (1 - f)$ (Requires 2 multiplications)
- **Refactored (Faster):** $x = a + f \cdot (b - a)$ (Requires 1 multiplication. Multiplication is computationally expensive; this optimization runs nearly twice as fast on standard hardware).
- *Fun Fact:* You can use SQL to dynamically generate and verify Trig properties using computed columns, like proving $\sin^2(\theta) + \cos^2(\theta) = 1$ or $\cos(\theta) = \sin(90^\circ - \theta)$.

### Tech & Cloud Infrastructure

- **`UNION ALL` vs. `UNION`:** `UNION ALL` is faster because `UNION` spends processing time searching for and removing duplicates.
- **WebAssembly (Wasm):** Compiles languages (C, C++, Rust, DB engines) to run securely in-browser at native speeds. Sites like *SQL.js* use Wasm to run SQLite locally without server lag.
- **SQLite:** Highly popular, open-source embedded database used in browsers (Chrome cache) and mobile OS (Android). Stores everything in a single `.db` binary file.
- **PostgreSQL:** The gold standard open-source relational DB (originally created at UC Berkeley as "Ingres", then "Post-Ingres").
- **Cloud Tools:**
  - **AWS RDS:** Amazon's Relational Database Service (managed cloud DBs).
  - **Neon:** Modern, serverless PostgreSQL.
  - **LocalStack/Fluttershy:** Free local emulators for AWS/Cloud services to avoid token/cloud costs while developing.



# 6/3 Lecture 7

# Database & SQL Lecture Cheatsheet

## 📌 Course Administration & Exam Info

- **Midterm Exam:** Next Wednesday (1 week from today).
- **Format:** 1-hour exam (starts at 3:00/3:30 PM, done by 4:30 PM).
- **Content:** Focus on concepts rather than memorizing strict SQL syntax. You will not have to write long SQL queries from scratch.
- **Resources:** A small cheat sheet is allowed.

## 💻 SQL vs. Other Programming Paradigms

- **Imperative (C, C++, Java):** You tell the computer *how* to do something step-by-step (e.g., using `for` loops, `while` loops).
- **Functional (Haskell, Lisp):** You compose functions, where functions can return other functions.
- **Declarative (SQL):** You declare *what* you want (the results), and the database engine figures out the step-by-step loop logic to retrieve it.
- **Analogy:** A SQL `WHERE` clause acts like an `if` statement nested inside an invisible `for` loop that iterates over table rows.

## 🗄️ Core SQL Review (Codd's Relational Model)

- **Closure:** Operations take a table as input and output a new table.
- **Data Types & Setup:** `CREATE TABLE` acts like a class definition. `INSERT` acts like an object constructor.
- **Filtering & Modifying:** * `WHERE`: Conditionally filters rows (e.g., `WHERE price < 20`).
  - `UPDATE`: Changes cell values based on conditions.
  - `ALTER TABLE`: Changes the table schema (adds/drops/modifies columns).
- **Operators:** * Logical: `AND`, `OR`, `NOT`. (Evaluated in precedence order).
  - Comparison: `=`, `<`, `>`, `BETWEEN`, `IS NULL`.
  - Pattern Matching: `LIKE '%saw%'` (the `%` wildcard acts as a match for any character sequence).
  - Lists: `IN` (matches any value in a dynamic list).

## 🔗 Table Joining

Joining multiplies tables together (Cartesian product) and filters them based on a condition to combine relevant data.

- **Implicit Join (WHERE clause):** 

```sql
  SELECT * FROM product, vendor WHERE product.v_id = vendor.v_id;
```

- **Inner Join:** Returns rows when there is a match in both tables.

- **Outer Joins:**
  - **LEFT OUTER JOIN:** Returns all rows from the left table, even if there are no matches in the right (fills with `NULL`).
  - **RIGHT OUTER JOIN:** Returns all rows from the right table.
  - **FULL OUTER JOIN:** Returns all rows from both tables, with `NULL`s where there are no matches.
  
- **Self-Join:** Joining a table to itself.
  - *Requirement:* You **must** use table aliases (e.g., `FROM employee E1, employee E2`) so the system can distinguish between the two instances.
  - *Use Case:* Finding an employee's manager when both are in the same `employee` table.

## 🗃️ Subqueries

A subquery is a query nested inside a main query, acting like a function call. It executes and passes its result to the outer query.

**What a Subquery Can Return:**

1. A single scalar number/value.
2. A 1D list (a single column of multiple rows).
3. A full 2D table.

**Where Subqueries Can Be Placed:**

1. **In the `WHERE` clause (Row Filtering):**
   - Most common. Evaluates values against dynamic results.
   - *Example:* `WHERE price > (SELECT AVG(price) FROM products)`
   - Operators used with lists: `> ALL` (greater than the maximum), `< ALL` (less than the minimum), `= ANY` (same as `IN`).
2. **In the `FROM` clause (Virtual Tables / Views):**
   - Generates a temporary table on the fly that the main query can query against.
3. **In the `SELECT` clause (Computed Columns):**
   - Generates a new column value for every row returned.

**Correlated Subqueries:**

- A subquery that requires a value from the *outer* main query to execute.
- *Performance Impact:* Extremely slow ($O(N^2)$ complexity). It acts as a nested double-loop, forcing the subquery to re-run from scratch for *every single row* of the main table.

## 🧮 Set Operations

Combines results from multiple queries. Tables must be **union compatible** (have the exact same column structures/data types). You may need to use `SELECT` (projection) to drop extra columns before combining.

- **UNION:** Merges rows from Table A and Table B. Automatically removes duplicates. (Commutative: A $\cup$ B = B $\cup$ A).
- **UNION ALL:** Merges rows but keeps duplicates. Faster than `UNION` because it skips the duplicate-checking step.
- **INTERSECT:** Returns only rows present in *both* Table A and Table B.
- **MINUS (or EXCEPT):** Returns rows in Table A that are *not* in Table B. (Not Commutative: A - B $\neq$ B - A).

## 👁️ Views vs. Materialized Views

- **View (`CREATE VIEW`):** Saves a SQL query as a virtual table. When you query the view, the underlying SQL runs dynamically. It does not store data on disk.
- **Materialized View (`CREATE MATERIALIZED VIEW`):** Runs the query and physically saves the resulting data to the disk.
  - *Benefit:* Acts as a cache. Trades disk space for computing time, making future queries instantaneous.
  - *Drawback:* Can hold stale data if the underlying database updates frequently.

## ⚙️ Procedural SQL & Advanced Constructs

Writing SQL that behaves more like standard programming scripts.

### Sequences

Standalone database objects that generate sequential numbers (useful for primary keys).

- `NEXTVAL`: Returns the sequence's current value and automatically increments it (post-increment).
- `CURRVAL`: Reads the current value *without* incrementing it.

### Code Structures

1. **Block (`BEGIN ... END;`):** An unnamed block of SQL code. Cannot be reused easily. Runs immediately when executed (e.g., using the `/` command in old mainframes).
2. **Stored Procedure (`CREATE PROCEDURE`):** A named, reusable block of code.
   - Can take inputs.
   - Does **not** return a value (like a `void` function in C++).
   - Called using the `EXEC procedure_name` command.
3. **Function (`CREATE FUNCTION`):** A named, reusable block of code that **must** return a value.
   - Can declare local variables.

### Triggers

Event-driven code ("callbacks") that run automatically in response to database changes.

- **When it runs:** `BEFORE` or `AFTER` an event.
- **The Event:** `INSERT`, `UPDATE`, or `DELETE`.
- **Scope:** * *Row-level:* Executes once for every row affected by the event.
  - *Statement-level:* Executes once for the entire SQL statement, regardless of how many rows are changed.
- *Use Case:* Automatically changing a `reorder_flag` to `1` the moment an `UPDATE` statement causes `quantity_on_hand` to drop below the minimum threshold.

# 6/4 Lecture 8

## Administrative Details

- **Midterm Date:** Wednesday, June 10th (covers everything up to and including this lecture).
- **Midterm Format:** Unlimited cheat sheets allowed (printed is fine). The professor recommends using class topics as study hints rather than printing unnecessary slides.
- **Student-Requested Topics for the Exam:** Normal forms, identifying deadlocks, ER diagrams, set theory, closure, ACID properties, and identifying/analyzing small SQL snippets.

## Transaction Management Basics

Transaction management (concurrency control) ensures that multiple people can safely read and write to a database at the same time without clobbering each other's data (e.g., booking the last seat on an airline, registering for a full class).

- **Transaction:** A sequence of SQL statements (usually reads and writes) executed as a single, atomic unit.
- **Known Good State:** A transaction must start with the database in a valid state and end leaving the database in a valid state.
- **Serializable Schedule:** Managing interleaved, concurrent transactions so the final result is mathematically identical to running them sequentially (one by one).

### The ACID Properties

Relational databases guarantee these four properties for transactions (Note: NoSQL databases like MongoDB historically did not guarantee these natively).

| **Property**    | **Description**                                              |
| --------------- | ------------------------------------------------------------ |
| **Atomicity**   | The "all or nothing" rule. All statements within a transaction must complete successfully, or none of them do. If a failure occurs mid-way, the transaction is aborted and rolled back. |
| **Consistency** | The transaction must not leave the database in a corrupt or inconsistent state. Data must accurately reflect the real world across all tables. |
| **Isolation**   | The system acts as if every transaction has exclusive, isolated access to the database, even when hundreds are competing for the same data simultaneously. |
| **Durability**  | Once a transaction is successfully **committed**, the changes are permanently saved to the actual database (written in concrete, not water) and survive system crashes. |

## Commit, Rollback, and the Transaction Log

- **Commit:** A keyword/action that saves local, temporary transaction changes permanently to the real database.
- **Rollback:** Reverts a transaction to its starting point if an error or crash occurs, undoing any partial changes.
- **Transaction Log (Write-Ahead Log - WAL):** A text file maintained by the database that records every transaction's unique ID, along with the **before** and **after** values of the affected cells. This log is the magic mechanism that allows the system to roll back failed transactions accurately.

## Concurrency Problems (What happens without locking)

If a database does not isolate transactions, interleaving reads and writes will cause data corruption.

| **Problem**                            | **Explanation**                                              |
| -------------------------------------- | ------------------------------------------------------------ |
| **Lost Update**                        | Two transactions read the same data cell and both update it. The second transaction overwrites the first, causing the first update to be permanently lost. |
| **Read Uncommitted Data (Dirty Read)** | A transaction reads data that is currently being modified by an unfinished transaction. If the modifying transaction rolls back, the first transaction is operating on phantom, incorrect data. |
| **Inconsistent Retrieval**             | A transaction reads a sequence of data (e.g., calculating an array average) while another transaction is actively updating those exact values. The reads capture a messy mix of old and new data. |

## Locking Mechanisms

To achieve serializability, databases use a **Lock Manager** process to act as a bouncer, issuing and revoking locks to control data access. Locking is generally a **pessimistic** approach (assuming conflicts will happen).

- **Read Lock (Shared Lock):** Multiple transactions can hold a read lock on the same data simultaneously. Nobody is allowed to write while a read lock is active.
- **Write Lock (Exclusive Lock):** Only one transaction can hold a write lock at a time. All read locks are revoked, and no other transaction can read or write until the lock is released.

### Lock Granularity Levels

How much data should one lock cover?

- **Database Level:** Locks the entire database. Horrible throughput; only one user at a time.
- **Table Level:** Locks an entire table. Still too restrictive.
- **Page Level:** Locks a block/page of rows (similar to OS RAM paging). **This is the optimal "Goldilocks" level used in the real world.**
- **Row Level:** Locks a single row. Often too much overhead for the lock manager.
- **Field Level:** Locks a single cell. Massive bookkeeping nightmare; never used.

### Two-Phase Locking (2PL)

A critical algorithm to guarantee serializability. The professor refers to it as the "Mayan Pyramid" or "Three-Phase Locking" because of the flat top where execution happens.

1. **Growing Phase (Lock Acquisition):** The transaction claims all the locks it needs one by one. It cannot release any locks during this phase.
2. **Execution Phase (The Flat Top):** The transaction has all necessary locks and safely executes its reads and writes without interruption.
3. **Shrinking Phase (Lock Release):** The transaction returns the locks to the Lock Manager. **Strict 2PL** waits until the entire transaction is finished before releasing any locks to prevent chain-reaction rollbacks.

## Deadlocks

A deadlock occurs during the 2PL growing phase when two or more transactions get stuck waiting for locks held by the other (a circular wait).

### Deadlock Resolution Strategies

| **Strategy**                    | **Description**                                              |
| ------------------------------- | ------------------------------------------------------------ |
| **Avoidance (Cycle Detection)** | Let the deadlock happen. The Lock Manager runs a cycle detection graph algorithm. If a cycle is found, it breaks the deadlock by aborting all but one of the transactions, returning their locks, and letting the survivor finish. |
| **Prevention (Timestamping)**   | Stop deadlocks before they form by tracking which transaction is older. Older transactions are forced to wait, or younger transactions are preemptively killed depending on the specific algorithm (Wait-Die, Wound-Wait). |
| **Optimistic Concurrency**      | Used when conflicts are incredibly rare. Use no locks at all. Execute the transaction, and at the end, validate against the transaction log to see if anyone else modified the data. |

### Timestamps and Logical Clocks

Deadlock prevention requires knowing exactly when a transaction started.

- **Unix Epoch:** Single-server time is often tracked using the Unix Epoch (seconds elapsed since January 1, 1970).
- **Logical Clocks:** In distributed databases (multiple machines), hardware clocks drift. Computer scientist Leslie Lamport won a Turing Award for inventing logical clocks and protocols (like Paxos) to accurately order events across distributed systems.

## Extra Tangents & Concepts Addressed

- **Gemma 4:** Google's new 12-billion parameter multimodal AI model. It bypasses traditional vision encoding, uses a decoder-only transformer, and can run locally on standard laptop RAM (4.66GB quantized).
- **Quasi-Monte Carlo (QMC):** For 2D random number generation, standard Linear Congruential Generators (LCG) can cause clustering. QMC sequences like the **Halton, Sobol, and Hammersley sequences** generate well-separated, evenly distributed random points without needing repulsion algorithms.
- **Bloom's Taxonomy:** An educational framework. Regurgitating facts is the lowest level of learning. True understanding is at the top of the pyramid: the ability to apply, analyze, evaluate, and **create** new things (e.g., writing your own SQL queries from scratch).



# 6/9 Lecture

## 📝 Administrative & Exam Logistics

- **Exam Scope:** Covers material up to Transaction Management. Distributed Databases (today's lecture) and ER diagram/normalization drawing will **not** be on the exam.
- **Format:** 12 questions worth 3 points each. You only need to answer 10 (maximum score is capped at 30, but the extra questions offer a buffer).
- **Materials:** Open notes. You can bring unlimited printed cheatsheets, but strictly no devices, internet, or AI tools.
- **Content Focus:** Expect questions on SQL concepts (no writing raw syntax) and Transaction Management (locks, deadlocks). Answer the question directly without adding irrelevant filler.

## 🔒 Transaction Management & Deadlocks

Deadlocks occur when transactions wait indefinitely for locks held by each other. There are three main strategies to handle them:

- **Indifference:** Ignore the possibility of deadlocks and deal with them manually if the system freezes.
- **Avoidance (Cycle Detection):** Continually simulate and look for cycles before handing out locks. If a cycle is detected, the lock is denied.
- **Prevention (Timestamping):** Uses timestamps to determine priority (older vs. younger transactions). A transaction may be suspended or killed to prevent a cycle from ever forming.

## 🌍 Distributed Databases Architecture

A distributed database scatters data storage and computation across multiple machines (nodes) to prevent single points of failure and increase speed.

### Processing Types

- **Transaction Processor (TP / TM):** The machine that receives requests and performs calculations or routing.
- **Data Processor (DP / DM):** The machine that blindly serves data upon request.

### The 4 Architectural Possibilities

| **Processing** | **Data**     | **Description & Example**                                    |
| -------------- | ------------ | ------------------------------------------------------------ |
| **Single**     | **Single**   | Old-school IBM mainframes with dumb terminals. Centralized, high risk of a single point of failure. |
| **Multiple**   | **Single**   | Client-server architecture (LAN). Data lives in one place, but laptops/clients process it locally (e.g., Microsoft SharePoint). |
| **Multiple**   | **Multiple** | **Fully Distributed.** Modern cloud architecture. Microservices process data that is stored across multiple global servers. |
| **Single**     | **Multiple** | Impractical/Silly. Storing data globally but forcing all computation through one machine (The "Newton's Cat" error of foolish consistency). |

### Fully Distributed Variations

- **Homogeneous:** All nodes run the exact same database software (e.g., all Oracle).
- **Heterogeneous:** Nodes use different vendors but the same relational table model (e.g., Postgres, MySQL, SQL Server).
- **Fully Heterogeneous:** Nodes use entirely different data models (e.g., Relational tables, Graph databases, Vector databases, Document databases).

## ✂️ Data Fragmentation & Replication

**Fragmentation** breaks a single logical table into physical pieces to optimize speed and storage.

- **Horizontal Fragmentation:** Dividing a table by rows. Useful for MapReduce and parallel processing (sending a calculation to 10 machines simultaneously for near-linear speedup).
- **Vertical Fragmentation:** Dividing a table by columns. Separates frequently accessed data from rarely accessed data (e.g., keeping current grades on fast SSDs and old undergraduate transcripts on cold-storage tape robots like Iron Mountain).
- **Mixed Fragmentation:** Doing vertical fragmentation first, followed by horizontal fragmentation on the critical columns.

**Replication** is copying data to prevent loss and ensure availability (e.g., Amazon's Dynamo using 3 copies).

- **Full Replication:** Every node has a copy of everything (expensive and heavy overhead).
- **Partial Replication:** Only critical tables are copied.
- **Unreplicated:** Zero copies. Highly dangerous.
- **Master Data Management (MDM):** Designating one "Golden Record" (master copy). Changes happen here and are synchronized to backups.
- **Push vs. Pull:** The master can "push" updates to replicas immediately, or replicas can periodically "pull" updates from the master.

## 🤝 The Two-Phase Commit Protocol (2PC)

When a transaction spans multiple machines, the system must guarantee **Atomicity** (All or Nothing) so tables do not become corrupted.

- **The Coordinator:** One node acts as the orchestra conductor to manage the transaction.
- **Write-Ahead Log (WAL):** Before any real changes are made, nodes write the "before" and "after" values to a local log to allow for a clean rollback if needed.
- **Phase 1 (The Polling/Question Phase):** The coordinator asks all subordinate nodes, "Are you ready to commit?" Each node locally checks its ability and responds with a YES or NO.
- **Phase 2 (The Execution Phase):** * *Success:* If **all** nodes reply YES (unanimous), the coordinator sends the "Commit" command. Everyone finalizes the transaction.
  - *Failure:* If even **one** node replies NO, the coordinator sends an "Abort/Rollback" command. All nodes use their WAL to revert to the exact original state.

## 👻 Distribution Transparency (Opacity)

Transparency in databases actually means *opacity*—hiding the complex internal mechanics from the end-user or potential hackers. The system uses a **Distributed Data Dictionary (Catalog)** to map requests behind the scenes.

- **Fragmentation Transparency:** The user has no idea the table is cut into pieces.
- **Location Transparency:** The user knows it is fragmented but does not know where the fragments live.
- **Local Mapping Transparency:** The user doesn't know the exact IP addresses hosting the specific fragments.
- **Performance/Failure Transparency:** If a node dies or a network cable is cut, the system automatically redirects to a replica (failover) without the user experiencing an error.

## ⚖️ CAP Theorem & ACID vs. BASE

Created by Eric Brewer, the CAP theorem states the trade-offs in distributed database design. Today, because Partition Tolerance (P) is an unavoidable reality of networks, engineers must choose between C and A.

| **Concept**                 | **Definition**                                               | **Ideal Use Case**                                           |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Consistency (C)**         | Every node returns the exact same, most up-to-date data.     | Financial tech, stock trading, foreign exchange. (Requires shutting down nodes to update). |
| **Availability (A)**        | The system is always up and accessible, even if some data is stale. | E-commerce catalogs (Amazon), social media.                  |
| **Partition Tolerance (P)** | The system continues to operate despite network failures (cut cables). | All modern internet distributed systems.                     |

### ACID vs. BASE

- **ACID (Relational DBs):** Prioritizes strong Consistency and Atomicity.
- **BASE (NoSQL DBs):** Prioritizes Availability (Basically Available, Soft state, Eventual consistency). Data might be out of sync for a moment, but will *eventually* synchronize across the network.