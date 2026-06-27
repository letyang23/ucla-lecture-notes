# Q1

A primary key (PK) in a table row is like a ‘pointer’, in the sense that it ‘points’ to all the non-prime attributes. We don’t call that ‘pointing’ - what is the proper DB terminology for this?

##### Answer

- 1 point: **Determination** (or ‘functional dependency’). The key is used to determine other (non-prime, ie non-key) values of the row 

- 0.5 points: Some points can be considered for mentioning full functional dependency and arguing that the PK itself comprises the set of determinants. 
- 0 points: Irrelevant answers



In theory, what PK-related ‘issue’ can occur in a single table, and what is the issue called?

##### Answer

- 1 point: The issue is called ‘**entity integrity violation**’ - happens when entire rows become identical on account of null or replicate (ie identical) PKs. 
- 0.5 points: The student names the issue but does not describe the issue itself. Or the student describes the relevant issue, but does not provide the name of the issue. 
- 0 points: Irrelevant answers



In theory, what PK-related ‘issue’ can occur in two related tables? What is the issue called?

##### Answer

- 1 point: Foreign keys may refer to an absent or deleted row in the other table, which leads to the **violation of Referential Integrity**. 
  - Any other relevant answer that makes sense and is correctly named would yield full credit for the student 
- 0.5 points: The student names the issue but does not describe the issue itself. Or the student describes the relevant issue, but does not provide the name of the issue. 
- 0 points: Irrelevant answers



###### Gemini Answer

That "pointer" analogy is actually a great way to visualize how a database row works. In formal relational database theory, however, we use language based on mathematical relations and logic rather than pointers.

Here is the proper terminology for the concepts you are describing.

### 1. The Terminology for "Pointing"

In database theory, we don't say the Primary Key (PK) "points" to non-prime attributes; instead, we say the non-prime attributes are **functionally dependent** on the Primary Key.

- **Term:** **Functional Dependency**
- **Concept:** A functional dependency exists when one attribute uniquely **determines** another attribute. If you know the value of the Primary Key, you are guaranteed to know the exact values of the non-prime attributes in that row.
- **Notation:** In database design, this is often written as $PK \rightarrow \text{Attribute}$, which is read aloud as "PK determines Attribute."

### 2. Single-Table PK Issues

When we look at functional dependencies within a single table, the most common structural issues arise when the strict rule of "the non-prime attributes depend *entirely* and *directly* on the Primary Key" is broken.

- **Issue 1:** **Partial Dependency**
  - **What it is:** This occurs in tables that have a *composite* Primary Key (a PK made of two or more columns). A partial dependency happens if a non-prime attribute relies on only a *part* of that composite key, rather than the whole thing.
  - **The Fix:** This violates **Second Normal Form (2NF)**. The solution is to break the table apart so that every non-prime attribute depends on the entire primary key.
- **Issue 2:** **Transitive Dependency**
  - **What it is:** This happens when a non-prime attribute doesn't depend directly on the Primary Key, but instead depends on *another* non-prime attribute (which in turn depends on the PK). Conceptually, $A \rightarrow B$ and $B \rightarrow C$.
  - **The Fix:** This violates **Third Normal Form (3NF)**. The solution is to move the transitively dependent attributes into their own table.

Both of these design flaws lead to **Data Anomalies** (specifically Update, Insertion, and Deletion anomalies), where modifying data in one place forces you to make redundant updates elsewhere or risks accidental data loss.

### 3. Two-Table PK Issues

When dealing with two related tables, the relationship is established by placing the Primary Key of the "Parent" table into the "Child" table. In the child table, this column is called a **Foreign Key (FK)**.

- **Issue:** **Referential Integrity Violation** (or **Orphaned Records**)
  - **What it is:** This occurs when a Foreign Key in the child table references a Primary Key value in the parent table that *does not exist*. This usually happens if a user tries to insert a child record with an invalid FK, or if a user deletes/updates a parent record while child records are still "pointing" to its Primary Key.
  - **The Fix:** Modern relational databases enforce **Referential Integrity Constraints** (Foreign Key Constraints). If properly configured, the database will outright block any action that would result in an orphaned record, or it will use cascading rules (like `CASCADE DELETE`) to automatically clean up the child records when a parent's PK is removed.



# Q2

What is the issue with ‘too much’ table normalization? What is the remedy?

##### Answer

- (2 pt): The student mentions any content related to “**increase query latency/cost/decrease efficiency**” - due to excessive JOINs that need to occur in a normalized set of tables 
- (1pt): The student mentions the remedy is to do table **denormalization**. 
- (0pt): Irrelevant answers



###### Gemini Answer

While normalization is essential for maintaining data integrity and preventing anomalies, taking it "too far" creates a different set of problems.

In database theory, the issue with excessive normalization is **Performance Degradation (specifically, "The Join Penalty")**, and the formal remedy is called **Denormalization**.

Here is a breakdown of why this happens and how to fix it:

### The Issue: The "Join" Penalty

When you heavily normalize a database (pushing into 4th Normal Form, 5th Normal Form, or strictly applying 3NF to every single attribute), you end up fragmenting your data across dozens or hundreds of highly specialized, narrow tables.

While this makes the data incredibly pure and mathematically sound, it creates a massive bottleneck when you actually need to *read* it.

To reconstruct a complete, meaningful piece of information—like a single invoice or a user profile—the database engine must execute complex **`JOIN`** operations to stitch all those separate tables back together.

- **CPU and Memory Tax:** `JOIN` operations are computationally expensive. If a single user query requires joining 10 different tables to load a dashboard, the database will consume massive resources and slow down significantly.
- **Developer Complexity:** Queries become massive, complex, and difficult to maintain or debug.

### The Remedy: Denormalization

The primary remedy for over-normalization is **Denormalization**.

Denormalization is the **deliberate and strategic introduction of redundancy** back into a database to improve read performance. It is a calculated compromise: you are intentionally violating normal forms (like 2NF or 3NF) to save the database from having to perform expensive joins.

**A Concrete Example:**

Imagine a database for an online store. Strictly normalized, an `Orders` table might only store the `UserID`, and to get the user's name, you must join it with the `Users` table.

- If your application frequently displays the `UserName` next to the `OrderID` on a high-traffic live dashboard, that join becomes a bottleneck.
- **The Denormalization fix:** You copy the `UserName` directly into the `Orders` table. Yes, the name is now stored in two places (redundancy), but the dashboard can now read the `Orders` table instantly without any joins.

### Alternative Remedies

If you do not want to alter your underlying table schema through Denormalization, modern database architecture offers a few other ways to solve the join penalty:

- **Materialized Views:** The database pre-calculates and physically saves the result of a complex `JOIN` query like a static table. It updates itself periodically, allowing you to query the pre-joined data instantly.
- **Caching Layer:** Using an in-memory database (like Redis) to temporarily store the fully assembled "joined" data so the main relational database isn't constantly re-calculating it.
- **OLAP vs. OLTP:** Splitting the database entirely. You keep a highly normalized database for handling live transactions (OLTP), and periodically copy that data into a massive, intentionally denormalized "Data Warehouse" (OLAP) specifically designed for heavy reading and analytics.



# Q3 

The table format (ie relational model) for storing data is nearly perfect, with only a few drawbacks. 

What is a (significant) drawback that JSON can trivially fix? Illustrate with a simple example (showing the problem occurring in a table, and the JSON fix). 

Hint - we discussed this in class.

##### Answer

- (1 point) Major issue: **Inability to handle hierarchical or nested data structures** without resorting to complex join operations or creating numerous related tables; another equally valid answer: **inability to represent multi-valued attributes directly** (ie. in a cell/field, ie row column intersection) 
- (1 point) example of a relational database where storing hierarchical or nested data become complex, or, an example that shows multi-valued attrs (eg. in the ‘degree’ column in a student table there is no way to specify ‘BS, MS, PhD’) 
- (1 point) Representing the same database using json clearly illustrating how it fixes the issues. Eg in the multivalued attr example, in JSON we would have “degree”: [‘BS’,’MS’,’PhD’], ie. use an array for the multiple values of the attribute.



###### Gemini Answer

You are spot on—the relational model is an incredibly powerful, mathematically sound way to store data. However, its strict adherence to a fixed structure creates a major friction point.

A significant drawback of the relational model that JSON trivially fixes is **Schema Rigidity when handling highly variable or sparse attributes.** In a relational table, the schema is strictly defined upfront: every row in a table *must* conform to the exact same columns. If you are storing entities that share a few common traits but have wildly different specific details, the relational model forces you into awkward compromises. JSON fixes this because it is fundamentally **schema-less and supports nested hierarchies**.

Here is a simple illustration of this problem and its JSON remedy.

### The Problem: The "Sparse Table" of NULLs

Imagine you are building an e-commerce database for a store that sells both clothing and electronics. Every product has an ID, a name, and a price. But a T-shirt has a "Size" and "Color", while a Laptop has "RAM" and a "CPU".

To force this into a single relational `Products` table, you often end up creating a "wide table" where you must add a column for every possible attribute any product might ever have.

**Table: `Products`**

| **ProductID** | **Name** | **Price** | **Category** | **Size** | **Color** | **RAM** | **CPU** |
| ------------- | -------- | --------- | ------------ | -------- | --------- | ------- | ------- |
| 1             | T-Shirt  | $20       | Apparel      | M        | Red       | NULL    | NULL    |
| 2             | ThinkPad | $900      | Laptop       | NULL     | NULL      | 16GB    | i7      |
| 3             | Mug      | $15       | Kitchen      | NULL     | NULL      | NULL    | NULL    |

**The Relational Pain Points:**

- **Storage Waste & Clutter:** Your table becomes riddled with `NULL` values (sparse data). If you add a "Bicycle" with a "TireSize" attribute tomorrow, you have to alter the entire database schema to add a new column, which will be `NULL` for 99% of your other products.
- **The EAV Alternative:** The common relational workaround is the Entity-Attribute-Value (EAV) anti-pattern (splitting attributes into rows in a secondary table), which absolutely destroys read performance and requires massive, complex `JOIN` operations to reconstruct a single item.

### The JSON Fix: Document Flexibility

JSON eliminates this issue entirely through structural flexibility. Because JSON does not enforce a rigid row-and-column grid, an object only holds the exact data relevant to it. Furthermore, JSON allows for nested data, letting you logically group unique attributes together without touching a master schema.

**The JSON Equivalent:**

JSON

```
[
  {
    "product_id": 1,
    "name": "T-Shirt",
    "price": 20,
    "category": "Apparel",
    "specifications": {
      "size": "M",
      "color": "Red"
    }
  },
  {
    "product_id": 2,
    "name": "ThinkPad",
    "price": 900,
    "category": "Laptop",
    "specifications": {
      "ram": "16GB",
      "cpu": "i7"
    }
  },
  {
    "product_id": 3,
    "name": "Mug",
    "price": 15,
    "category": "Kitchen"
  }
]
```

**Why JSON Wins Here:**

- **Zero Schema Migrations:** If you add a "Bicycle" tomorrow, you simply drop in a new JSON object with `"gears": 21`. No database table needs to be altered.
- **No `NULL` Clutter:** If an attribute doesn't apply to an item (like the Mug), the key simply doesn't exist. There are no empty placeholders.
- **Self-Contained Retrieval:** You can fetch the entire, fully-detailed product in a single, lightning-fast database read, completely avoiding the expensive joins required by highly normalized relational workarounds.



# Q4

Prior to relational tables, digital file systems were used to store and process data, where the significant drawback was ‘structural dependency’. 

[2 points] 

What is ‘structural dependency’? Illustrate with a simple/brief example. 

[1 point]

The relational (table) format appears to make the problem (of structural dependency) go away - but it never really does! Where does it go, then? Be brief, be specific. 

Hint: we did cover this!

##### Answer

(1 point) Definition: Program logic is tied to the physical (or positional) layout of a data file. Any change in that layout forces program changes. Other phrasing: Fields are located by absolute position; if you add, move or resize a field you must rewrite every program that reads the file. 

(1 point) Any illustrative examples are fine. E.g. A payroll file stores EmpID in bytes 1-5 and Salary in bytes 6-11. If a new MiddleName field is inserted after EmpID, every COBOL routine that assumes Salary starts at byte 6 breaks and must be recoded 

(1 point) Structural dependency is pushed up to the logical schema / SQL interface: changing a table’s column order, name, datatype, or splitting/merging tables still breaks any stored procedures, queries, OR-mappers, or application code that reference the old structure. Views can hide some changes, but without them the dependency now lives in the application layer instead of the file layout. Another way to state this: the structural dependency is now at the data representation level, which is not accessible/visible to users [in other words the DB driver for the specific DB handles structurally-dependent data access, while users ‘simply’ write SQL for this, which offers them positional independence]. 

(Award 0 pt if the answer simply says “the problem is solved” or gives an unrelated explanation.)



###### Gemini Answer

### What is Structural Dependency?

**Structural dependency** occurs when an application's code is strictly tied to the physical layout and format of the data it reads. In pre-relational systems, data and the logic to access it were tightly coupled. If you changed how the data was organized on the disk, you had to manually rewrite the program that accessed it.

### A Simple Example

Imagine a payroll program reading a fixed-width text file of employee records. The program's code is hardcoded to read characters 50 through 60 to extract the "Salary."

If you update the file structure to add a "Middle Name" field before the salary, everything shifts. The application immediately breaks or calculates the wrong paychecks because it is still blindly reading characters 50 through 60. To fix it, a programmer must physically alter the application's source code to account for the new structural layout.

### Where Does the Dependency Go in the Relational Model?

The relational model gives applications **data independence**. You can add a new column to a table, and your existing `SELECT Name, Salary FROM Employees` queries will continue to work perfectly without requiring any code changes.

However, the structural dependency doesn't vanish—it is simply **shifted from the application code to the Database Management System (DBMS).**

Specifically, the burden of structural dependency is absorbed by the **Database Catalog (or Data Dictionary)**. The DBMS acts as a massive abstraction layer. It tracks the exact physical layout, data types, and disk locations of every table. When your application requests data logically via SQL, the DBMS engine internally manages the structural dependency, mapping your logical request to the actual bytes on the disk so your application never has to.



# Q5 

a. [1 point] Complete these two, name (expand) what they stand for: 

2P[ ] 

2P[ ] 

b. [1 point] What do the two ‘2P?’ have in common, ie how are they related? 

c. [1 point] What do the two ‘2P?’ have by way of difference, ie how are they not the same (ie. what is each for)?

##### Answer

Q5a 

+0.5: 2PL (Two-phase Locking) 

+0.5: 2PC (Two-phase Commit) 

Q5b 

+1: Both are used to maintain correctness when multiple resources or nodes are involved, that need to carry out multiple concurrent transactions. 

Q5c 

+1: 2PL is a concurrency control mechanism, 2PC is a distributed commit protocol 

(or: 2PL is for serializability vs 2PC is for atomic commit) 

(or: 2PL is for a single node, whereas 2PC is for an entire collection of nodes in a distributed DB)



###### Gemini Answer

In the context of database theory and transaction management, those two acronyms are frequently taught together—and frequently confused.

Here are the completions and what they stand for:

### 1. The Expansions

- **2PL:** Two-Phase **Locking**
- **2PC:** Two-Phase **Commit**

### 2. What They Have in Common (The Relationship)

While they solve different problems, they are closely related in the broader context of database architecture:

- **Transaction Safety:** Both are protocols designed to enforce **ACID** properties in database transactions to prevent data corruption.
- **The "Two-Phase" Structure:** Both rely on a strict, two-step chronological process. They both have a "preparation" phase where conditions are set or verified, followed by an irreversible "execution" phase where the final action is taken or undone.
- **Safety Over Speed:** Both protocols inherently introduce bottlenecks (waiting for locks or waiting for network responses) to prioritize absolute data integrity over maximum performance.

### 3. What They Have by Way of Difference (What Each is For)

The easiest way to separate them is by the specific problem they solve: **2PL is about \*Concurrency\* (Isolation), while 2PC is about \*Distributed Systems\* (Atomicity).**

**2PL (Two-Phase Locking)**

- **What it is for:** Controlling **concurrency** on a single database.
- **The Problem it Solves:** When multiple users are trying to read and write to the exact same rows at the exact same time, 2PL prevents them from stepping on each other's toes, ensuring the final result looks as if the transactions happened sequentially (Serializability).
- **The Two Phases:** 1.  **Growing Phase:** The transaction acquires all the locks it needs (read/write) but cannot release any.
  2. **Shrinking Phase:** The transaction releases its locks but cannot acquire any new ones.

**2PC (Two-Phase Commit)**

- **What it is for:** Ensuring **atomicity** across multiple, separate databases (a distributed system).
- **The Problem it Solves:** If a single transaction requires updating a database in New York and a database in London, 2PC ensures that *both* databases commit the change, or *neither* do. It prevents a scenario where one succeeds and the other fails, leaving the system out of sync.
- **The Two Phases:** 1.  **Prepare Phase:** A central coordinator asks every database node, "Are you ready and able to commit this transaction?" The nodes vote Yes or No.
  2. **Commit/Abort Phase:** If *every* node voted Yes, the coordinator tells them all to commit. If even one node voted No (or timed out), the coordinator tells them all to abort and roll back.



# Q6

[verify De Morgan’s Law] 

Set A = {C, D, E, F}, Set B = {E, F, G, H} 

Prove/verify that ¬(A ∪ B) = ¬A ∩ ¬B 

##### Answer

LHS: A ∪ B = {C, D, E, F, G, H} 

​	¬(A ∪ B) = {A, B, I, J} 

RHS: ¬A = {A, B, G, H, I, J} 

​	¬B = {A, B, C, D, I, J} 

​	¬A ∩ ¬B = {A, B, I, J} 

LHS = RHS

- 3 points: Student correctly creates LHS and RHS step by step and the result of each side equals {A, B, I, J}. Students can use any of the three different notations. 
- -1 point: Student doesn’t create LHS and RHS step by step (-0.5 points if only one of them is not created step by step) 
- -2 points: Student doesn’t give correct results of LHS and RHS (-1 point if only one of them is wrong) 
- 0 point: If no answer or irrelevant answer.



###### Gemini Answer

The equation you are asking to verify is known as **De Morgan's Law** for sets.

To prove and verify this using your specific sets, we must first establish a **Universal Set ($U$)**. The complement of a set (denoted by the $\neg$ symbol) means "everything in the Universal Set that is *not* in our current set."

Let's define a concrete Universal Set that contains some extra letters to make the "not" ($\neg$) operations visible.

Assume our Universal Set is $U = \{A, B, C, D, E, F, G, H, I, J\}$.

Here are your starting sets:

- $A = \{C, D, E, F\}$
- $B = \{E, F, G, H\}$

Let's solve both sides of the equation step-by-step to verify they match.

### Part 1: Evaluate the Left Side $\neg(A \cup B)$

**Step 1: Find $A \cup B$ (A Union B)**

The union represents all unique elements that are in $A$, in $B$, or in both.

- $A \cup B = \{C, D, E, F, G, H\}$

**Step 2: Find $\neg(A \cup B)$ (The complement of the Union)**

We take our Universal Set $U$ and remove everything that is inside $A \cup B$.

- $U = \{A, B, \textbf{C, D, E, F, G, H}, I, J\}$
- **$\neg(A \cup B) = \{A, B, I, J\}$**

### Part 2: Evaluate the Right Side $\neg A \cap \neg B$

**Step 1: Find $\neg A$ (The complement of A)**

We take $U$ and remove everything that is in $A$ ($\{C, D, E, F\}$).

- $U = \{A, B, \textbf{C, D, E, F}, G, H, I, J\}$
- $\neg A = \{A, B, G, H, I, J\}$

**Step 2: Find $\neg B$ (The complement of B)**

We take $U$ and remove everything that is in $B$ ($\{E, F, G, H\}$).

- $U = \{A, B, C, D, \textbf{E, F, G, H}, I, J\}$
- $\neg B = \{A, B, C, D, I, J\}$

**Step 3: Find $\neg A \cap \neg B$ (The intersection of the Complements)**

The intersection ($\cap$) represents only the elements that exist in *both* $\neg A$ and $\neg B$.

- $\neg A = \{\textbf{A}, \textbf{B}, G, H, \textbf{I}, \textbf{J}\}$
- $\neg B = \{\textbf{A}, \textbf{B}, C, D, \textbf{I}, \textbf{J}\}$
- **$\neg A \cap \neg B = \{A, B, I, J\}$**

### Conclusion

By comparing the final results of both sides:

- Left Side $\neg(A \cup B) = \{A, B, I, J\}$
- Right Side $\neg A \cap \neg B = \{A, B, I, J\}$

Both sides yield the exact same resulting set. Therefore, we have successfully verified that **$\neg(A \cup B) = \neg A \cap \neg B$**.



# Q7

Provide three examples of ‘special purpose’ databases - what would they store, what might their interface be? No need for diagrams - but do mention why they would be ‘special’. Hint - we went through a molecule DB in class.

##### Answer

Examples could be in these domains: genealogy, stocks, bitcoin, videogame, fingerprint, astronomy… 

**1pt per example**: The student gets the full score if he/she explain **what** it stores, what the **interface** is (eg. might contain a dedicated viewer or a search engine or calculator, etc), and **why** it is special (ie. why it is more than just a standard relational DB) for that example. If any part is missing in an example, the student only gets **0.5** for that example.



###### Gemini Answer

Building on the molecule database example from your class, "special purpose" databases exist to handle highly specific types of data and queries that standard relational tables or document stores (like JSON) struggle to process efficiently.

Here are three examples of special-purpose databases, including the molecular one:

### 1. Chemical / Molecular Databases (e.g., PubChem, ChEMBL)

- **What it stores:** Chemical structures, 2D and 3D atomic coordinates, bond types (single, double, aromatic), molecular weights, and physical properties.
- **The Interface:** A visual "sketchpad" GUI. Instead of typing SQL queries, a user literally draws a chemical structure (like a benzene ring with a specific functional group attached) using their mouse.
- **Why it is "Special":** Relational tables are terrible at storing complex, multi-directional graphs (which is what a molecule is). A molecular database uses specialized indexing to perform **substructure searching**—mathematically identifying if a small molecular graph exists inside a larger, completely different molecular graph. Standard text or numerical indexing cannot compute chemical graph isomorphism.

### 2. Spatial / Geographic Databases (e.g., PostGIS)

- **What it stores:** Geometric and topological objects like points (a specific GPS coordinate), lines (a river or road), and complex polygons (the exact border of a city or a delivery zone).
- **The Interface:** A map-based dashboard. Users query the database by drawing bounding boxes on a map, dropping pins, or using a slider to adjust a radius.
- **Why it is "Special":** Standard databases use one-dimensional indexes (like alphabetical order or numerical order). Spatial databases require **multi-dimensional indexes** (like R-trees). This allows them to instantly calculate complex geometry, answering queries like, "Find all coffee shop 'points' that geometrically intersect with this 5-mile 'polygon' around my current location," without having to scan the entire database.

### 3. Time-Series Databases (e.g., InfluxDB, Prometheus)

- **What it stores:** Massive volumes of time-stamped data points generated at high frequencies. Think of IoT temperature sensors recording every second, server CPU metrics, or stock market ticker prices.
- **The Interface:** Real-time visual dashboards (like Grafana) featuring line charts, heat maps, and time-window sliders that allow users to instantly zoom in from a "yearly average" to a "second-by-second" view.
- **Why it is "Special":** They are strictly optimized for "append-only" workloads. Unlike a regular database where you frequently update or delete rows, time-series data is never altered once recorded. Because of this, the database is specially engineered to ingest millions of writes per second. They also feature native **downsampling**—automatically compressing older, second-by-second data into hourly averages to save physical disk space, a lifecycle feature general databases lack.



# Q8 

An(y) entity can be described by a set of characteristics (ie. “columns”) - that is what ‘data’ actually is, as you know. 
In principle, practically ANY entity might have in common, some characteristics/properties/columns with ANY OTHER entity! 
a. Why is a raven like a writing desk?
b. What’s common between a flash drive and an auditorium? 
c. What’s common between a baseball game and a (theatrical) play? 

##### Answer

a. both are **black, have feet, have flat surfaces, are shiny**, etc. 

b. both **contain something** (data/information/content, vs. people). 

c. both **happen in real-time (‘live’) in front of an audience.**



###### Gemini Answer

You are absolutely right—from a data modeling perspective, the universe is just one massive table waiting to be joined. If you zoom out far enough, any two entities can share a schema.

Here is how we can map the shared "columns" (attributes) for your three examples:

### a. Why is a raven like a writing desk?

This is Lewis Carroll’s famously unsolvable riddle from *Alice in Wonderland*, but if we treat both as entities in a database, they share several distinct columns:

- **`Associated_Author` (String):** Edgar Allan Poe wrote *on* a writing desk, and he wrote *about* a raven.
- **`Produces_Notes` (Boolean):** `TRUE` for both. A raven produces musical notes (calls), and a desk is where written notes are produced. (Carroll himself eventually offered this as the official punchline: *"Because it can produce a few notes, tho they are very flat!"*)
- **`Leg_Count` (Integer):** Depending on the desk design, both entities have a non-zero integer value for legs.
- **`Primary_Color` (String):** If the desk is made of ebony wood, both share the value `"Black"`.

### b. What’s common between a flash drive and an auditorium?

At first glance, one fits in your pocket and the other fits thousands of people, but their core data structure revolves around **containment and flow**.

- **`Max_Capacity` (Integer):** Both are defined by a strict upper limit of what they can hold. For the flash drive, the unit is Gigabytes; for the auditorium, the unit is Seats/People.
- **`Current_Occupancy` (Float/Percentage):** Both have a measurable state of being empty, partially full, or at maximum capacity.
- **`I_O_Ports` (Integer):** Both require physical entry and exit points for data/people to flow in and out (USB connectors vs. physical doors).
- **`Corruption_State` (Boolean):** A flash drive can have corrupted sectors; an auditorium can have broken or unusable seats.

### c. What’s common between a baseball game and a (theatrical) play?

These two entities are surprisingly similar. In a database, they would likely both inherit from a parent `Live_Events` table.

- **`Roster_List` (Array of Strings):** Both require a predetermined list of performers (The Cast vs. The Lineup).
- **`Scheduled_Breaks` (Integer):** Both have structured pauses built into the timeline (Intermissions vs. Inning stretches).
- **`Director_ID` (Foreign Key):** Both are guided by a non-performing manager who dictates strategy and personnel changes (The Stage Director vs. The Team Manager).
- **`Venue_ID` (Foreign Key):** Both must be hosted at a specific physical location with a set capacity (The Theater vs. The Stadium).
- **`Ticket_Price` (Decimal):** Both are monetized via admission fees.
- **`Start_Time` and `End_Time` (Timestamp):** Both are temporal entities that exist only for a specific duration.



# Q9 

‘Joins’ occupy a special place in relational DBs. Discuss them: what they are, how the table notion facilitates them.

##### Answer

- **(1 point)** Clearly defines joins as operations that combine rows from two or more tables based on a related column (typically using a foreign key). 
- **(1 point)** Mentions types of joins (e.g., inner, left, right) or gives a concrete example. 
- **(1 point)** Discusses how the consistent structure of tables (e.g., shared columns, referential integrity) allows efficient and meaningful joining.



###### Gemini Answer

Joins are the absolute beating heart of the relational database. If normalization is the process of tearing data apart to keep it pure and anomaly-free, joins are the mechanism for stitching it back together to make it human-readable and useful.

Here is a breakdown of what they are and why the table structure makes them uniquely powerful.

### What is a Join?

At its core, a join is a logical operation that combines rows from two or more tables based on a shared characteristic (a related column) between them.

When you query a database using a join, you are telling the Database Management System (DBMS): *"Look at the values in Table A's column, look at the values in Table B's column, and whenever they match, fuse those two rows together into a single, unified row in the final output."*

- **Inner Join:** Only keep the fused rows where there is a match in both tables.
- **Outer Join (Left/Right/Full):** Keep the matched rows, but also keep the unmatched rows from one (or both) tables, filling in the blanks with `NULL` values.

### How the "Table Notion" Facilitates Joins

The fact that relational databases strictly use the "table notion" (rows and columns) is exactly what makes joins mathematically and practically possible. Here is how the format facilitates the operation:

**1. The Principle of Closure (Tables in, Tables out)**

In the relational model, tables are implementations of mathematical **sets**. Because of this strict mathematical foundation, any operation performed on tables—including a join—always outputs *another table*.

This is called the relational closure property. It means you can join Table A and Table B to create a virtual "Table C," and then instantly join that virtual "Table C" to Table D. The uniformity of the table format allows joins to be endlessly chained and nested.

**2. Shared Attributes (The Key System)**

As we established with the raven and the writing desk, any two entities can share an attribute. The table format formalizes this. By strictly organizing data into typed columns, a join simply becomes an exercise in matching values. The concept of Primary Keys (the unique identifier) and Foreign Keys (the reference to the identifier) acts as the standardized "hook and loop" fastener that allows two completely separate tables to snap together perfectly.

**3. The Cartesian Product Foundation**

Because tables are sets of rows, the database can rely on standard set theory to execute a join. Under the hood, the most basic way to think of a join is a **Cartesian Product** followed by a filter.

If Table A has 10 rows and Table B has 100 rows, the table format allows the database to theoretically cross-multiply them (creating a temporary grid of 1,000 combinations) and then instantly filter out only the rows where the shared columns match.

**4. Logical Abstraction (Data Independence)**

Because tables are purely logical structures (as opposed to physical disk addresses), you do not need to write complex navigational code to tell the database *how* to traverse a tree or follow a physical pointer to find related data. You just declare the logical relationship (`JOIN ON TableA.ID = TableB.ID`), and the DBMS's query optimizer figures out the fastest way to physically retrieve and combine the data.

We've covered how joins logically link data together, but the physical execution can be a massive bottleneck if not handled correctly. Would you like to dive into how the database engine actually executes these matches under the hood (e.g., Hash Joins vs. Nested Loops), or is there another relational concept you'd like to explore?



# Q10

How does the SQL ‘EXISTS’ operator work? 

##### Answer

- 2 points: Clearly explains that EXISTS checks for the existence of rows returned by a subquery. **Explicitly notes that it returns TRUE if the subquery returns at least one row, otherwise, it returns FALSE.** 
- 1 point: Mentions it checks for the existence of rows, but misses a key detail (e.g., doesn't specify the TRUE/FALSE behavior or talks vaguely). 
- 0 points: Incorrect or no answer provided.



What makes a ‘correlated subquery’ become correlated? 

##### Answer

- 1 point: Clearly states that a correlated subquery references one or more columns from the outer (‘main’) query. **Need to** additionally mention that the subquery is evaluated once per row of the outer query. 
- 0.5 points: Demonstrates partial understanding but is vague or incomplete (e.g., mentions a dependency or relationship between subquery and outer query without clearly stating column reference or per-row evaluation). 
- 0 point: Incorrect or no answer provided.



###### Gemini Answer

To understand both `EXISTS` and correlated subqueries, it helps to look at them together, because in SQL, they are almost always used as a pair.

Here is a breakdown of how the operator works, and what makes a subquery "correlated."

### 1. The `EXISTS` Operator

The `EXISTS` operator is a logical function in SQL. Its only job is to evaluate a subquery and return a boolean value: **`TRUE`** or **`FALSE`**.

Here is how it works under the hood:

- **It only looks for presence, not data:** `EXISTS` does not care *what* data the subquery returns. It only cares *if* the subquery returns at least one row.
- **The `SELECT 1` Convention:** Because the actual data doesn't matter, you will almost always see developers write `EXISTS (SELECT 1 FROM...)` or `EXISTS (SELECT * FROM...)`. The database engine ignores the `SELECT` list entirely; it just checks if a row exists that meets the `WHERE` clause.
- **Short-circuiting (Performance):** `EXISTS` is highly efficient. The moment the database engine finds the *very first* row that matches the subquery's condition, it stops searching, returns `TRUE`, and moves on. It doesn't waste time scanning the rest of the table.

### 2. What makes a subquery "Correlated"?

A standard (uncorrelated) subquery is independent. It runs exactly one time, fetches its results, and passes those results to the outer query.

A **correlated subquery** becomes "correlated" the moment **the inner query references a column from the outer query**.

Because the inner query relies on a piece of data from the outer query, it cannot run independently. Instead, it forces the database engine into a loop.

1. The outer query looks at its first row.
2. It passes a value from that row into the inner query.
3. The inner query executes using that specific value.
4. The outer query moves to the second row and repeats the process.

### Tying them together: An Example

Let's look at a classic example: *Find all Customers who have placed at least one Order.*

SQL

```sql
SELECT CustomerName
FROM Customers c
WHERE EXISTS (
    SELECT 1 
    FROM Orders o 
    WHERE o.CustomerID = c.CustomerID  -- <-- This is the correlation!
);
```

**How the database processes this step-by-step:**

1. **The Outer Loop:** The database looks at the first row in the `Customers` table (let's say, Alice, whose `CustomerID` is 100).
2. **The Correlation:** It takes Alice's ID (100) and passes it into the subquery. The subquery effectively becomes: `SELECT 1 FROM Orders WHERE CustomerID = 100`.
3. **The `EXISTS` Check:** The database peeks into the `Orders` table. It finds an order with `CustomerID = 100`. Because it found a row, `EXISTS` immediately returns `TRUE`.
4. **The Result:** Because the `WHERE EXISTS` clause evaluated to `TRUE`, Alice's name is added to the final result set.
5. **Repeat:** The database moves to the next customer (Bob, ID 101), passes "101" into the inner query, and repeats the process.

**In Summary:** A subquery is correlated because it is structurally "tied" to the outer query via a column reference, forcing it to execute row-by-row. `EXISTS` is simply the highly efficient mechanism used to ask that correlated subquery, *"Did you find anything for this specific row?"*



# Q11 

[1 point] Identify FROM + JOIN construct 

- 1 point: States that FROM/JOIN correspond to **iteration** across collections, typically implemented as nested loops (outer loop over rows of the first table, inner loop over rows of the second, or an equivalent join algorithm). In other words, FROM+JOIN is equivalent to a **for()** loop. 
- 0.5 point: Identifies “loop/iteration” but does not acknowledge nested loops / pairing logic. 

[1 point] Identify WHERE construct 

- 1 point: States that WHERE is a **conditional** filter, i.e., an if (or similar) that keeps rows only when the predicate is true. IOW, WHERE is equivalent to an if() statement. 
- 0.5 point: Mentions “filter” or “condition” but omits the control-flow term (if, case, etc.). 

[1 point] Provide coherent pseudocode combining the two 

- 1 point: Supplies pseudocode that: 1) initializes a result container; 2) iterates (via one or more loops) over the table(s); 3) applies an if condition to implement the WHERE; 4) appends or outputs matching rows/selected fields. The order must be logically correct (loop(s) → if → collect).

  Acceptable too [doesn’t have to be verbatim, but shows the nesting]: 

  **for** each row 

  ​	**if** a condition (can be a single one or an expression connected by Booleans) is true 

  ​	**output/print** the row’s requested columns 

- 0.5 point: Minor syntax/ordering issue or omits the result-collection step, but the logic is still clear.



###### Gemini Answer

To understand how these two constructs interact, it helps to look at them through the lens of **logical execution order**. A database engine doesn't process SQL top-to-bottom the way a human reads it; it builds the data in phases.

Here is the breakdown of the constructs and how they combine.

### 1. The `FROM` + `JOIN` Construct: The Assembler

In SQL execution logic, this construct is the **starting point**. Before the database can filter, group, or select anything, it must first assemble the raw workspace.

- **What it does:** It identifies the data sources and dictates exactly how different tables stitch together to form a cohesive dataset.
- **The Mechanism:** The `JOIN` (paired with an `ON` clause) acts as the bridge. It mathematically aligns the tables, usually by matching primary keys to foreign keys.
- **The Output:** A temporary, combined "super-table" in the database's memory containing all matched rows and columns from the joined tables.

### 2. The `WHERE` Construct: The Filter

This construct operates **after** the `FROM` and `JOIN` phases have built that initial super-table.

- **What it does:** It acts as a strict row-by-row gatekeeper.
- **The Mechanism:** It applies a boolean logical test (e.g., `Age > 30` or `Status = 'Active'`) to the assembled data.
- **The Output:** A pruned dataset. If a row evaluates to `TRUE`, it stays in the pipeline. If it evaluates to `FALSE` or `NULL`, it is permanently discarded from the current query's results.

### 3. Coherent Pseudocode (The Execution Engine)

To see how they combine, let's look at the pseudocode for how a database engine actually processes a query behind the scenes.

Imagine a user wants to find all active employees in the Engineering department. They write:

```
SELECT Name FROM Employees JOIN Departments ON Employees.DeptID = Departments.ID WHERE Status = 'Active';
```

Here is the pseudocode combining the two constructs:

Plaintext

```
// ==========================================
// PHASE 1: The FROM + JOIN Construct
// ==========================================
CREATE empty temporary dataset WorkingTable

// The engine attempts to match the tables based on the ON clause
FOR EACH emp_row IN Employees_Table:
    FOR EACH dept_row IN Departments_Table:
        
        IF emp_row.DeptID == dept_row.ID THEN
            // A match is found! Stitch them together.
            combined_row = MERGE(emp_row, dept_row)
            ADD combined_row TO WorkingTable
        END IF
        
    END FOR
END FOR

// At this point, WorkingTable contains ALL employees and their departments.

// ==========================================
// PHASE 2: The WHERE Construct
// ==========================================
CREATE empty temporary dataset FilteredTable

// The engine now filters the newly assembled dataset
FOR EACH row IN WorkingTable:
    
    // Evaluate the condition
    IF row.Status == 'Active' THEN
        ADD row TO FilteredTable
    ELSE
        DISCARD row
    END IF
    
END FOR

// ==========================================
// PHASE 3: The SELECT Construct (For completeness)
// ==========================================
// Finally, the engine pulls only the requested columns for the final output.
RETURN EXTRACT_COLUMN(Name) FROM FilteredTable
```



# Q12

[1 point] Why is ‘closure’ a BFD for table operations? 

- 1 point: Student correctly explains that closure ensures results stay within the same domain, essential for predictability and chaining operations (table operations such as SELECT, UNION etc result in a table as output, i.e. the **TYPE is PRESERVED**). Acceptable phrasing includes: "So you can combine rows without breaking the system," or "You stay inside the table." 
- 0.5 points: Students give a vague or partially correct answer (e.g., "Because it works" or "It makes things easier") without explaining why closure matters. 
- 0 points: No answer or irrelevant answer. 

[1 point] What is an operation that BREAKS closure on square matrices? 

- 1 point: Student gives a valid operation that takes square matrices and produces something outside that set. Acceptable examples: Taking the **determinant** (returns a scalar, not a matrix), **Eigenvalue decomposition** (returns vectors or non-square structures), or the **rank** operation. 
- 0.5 points: Student gives an operation on matrices but doesn’t explain why it breaks closure or is ambiguous (e.g., "inverse", which preserves closure on invertible matrices). 
- 0 points: Incorrect or missing. 

[1 point] What is an operation that PRESERVES closure on colors ([r,g,b])? 

- 1 point: Student gives a valid operation that maps one or more colors to another [r,g,b] color. Acceptable examples: **Addition** with clipping (e.g., [r1,g1,b1] + [r2,g2,b2], clipped to max 255), Averaging colors (blur), Scalar multiplication with clipping (brightening/darkening). Also - contrast enhancement, sharpening, median filter… 
- 0.5 points: Partially valid operation (e.g., "adding colors" without noting clipping or staying in bounds) 
- 0 points: Irrelevant or invalid operation (e.g., converting to grayscale without returning [r,g,b]).



###### Gemini Answer

In mathematics and computer science, **closure** means that when you perform an operation on an item (or items) within a specific set, the result is an item that belongs to that exact same set. You never "escape" the domain.

Here is why that is a massive deal for databases, along with your examples for matrices and colors.

### 1. Why Closure is a BFD for Table Operations

In relational algebra (the math underlying SQL), closure is a Big Fucking Deal because **the input is a table, and the output is always a table.** Why does this matter? **Infinite composability.** Because an operation (like `JOIN`, `WHERE`, or `SELECT`) spits out a valid table, you can immediately feed that output into *another* operation. This is the exact property that allows you to write nested queries, chain together multiple `JOIN`s, and build incredibly complex data pipelines.

If relational databases lacked closure—if, for example, a `JOIN` returned a text string or an unstructured list instead of a table—the query would hit a dead end. You couldn't filter it with a `WHERE` clause afterward because `WHERE` only knows how to process tables. Closure is the glue that makes SQL work.

### 2. An Operation that BREAKS Closure on Square Matrices

Finding the **Determinant**.

If your set is "$n \times n$ square matrices," operations like matrix addition or matrix multiplication preserve closure because they output another $n \times n$ square matrix.

Taking the determinant, however, **breaks closure** because it takes a square matrix as its input, but outputs a **scalar** (a single real number). For example, you feed it a $2 \times 2$ grid of numbers, and it spits out the number $14$. Because $14$ is a scalar and not a $2 \times 2$ matrix, you have broken closure. You can no longer perform matrix-specific operations on the result.

### 3. An Operation that PRESERVES Closure on Colors (`[r, g, b]`)

**Color Inversion** (or calculating the "negative" of a color).

In digital systems, an RGB color is a vector where each component is strictly bounded (usually integers from $0$ to $255$).

- *What breaks it:* Regular addition breaks closure here. If you add a bright grey $[200, 200, 200]$ to a dark grey $[100, 100, 100]$, you get $[300, 300, 300]$, which is out of bounds and therefore not a valid 8-bit RGB color.
- *What preserves it:* **Inversion**. The formula to invert a color is to subtract each current value from the maximum value: $[255-r, 255-g, 255-b]$.

If your input is a valid color (e.g., a teal: $[0, 128, 255]$), the inverted output ($[255, 127, 0]$, an orange) is mathematically guaranteed to still be bounded between $0$ and $255$. It outputs a valid RGB color, keeping you safely inside the domain.
