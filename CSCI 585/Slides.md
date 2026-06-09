# Introduction

## Database system

<img src="Slides.assets/Screenshot 2026-06-08 at 9.42.32 PM.png" style="zoom:50%;" />

### What you will learn:

### Learning Objectives

- In this chapter, you will learn:
  - The difference between data and information
  - What a database is, the various types of databases, and why they are valuable assets for decision making
  - The importance of database design
  - How modern databases evolved from file systems

### Learning Objectives

- In this chapter, you will learn:
  - About flaws in file system data management
  - The main components of the database system
  - The main functions of a database management system (DBMS)

### Data != information!

### Data vs. Information

#### Data

- Raw facts
  - Raw data - Not yet been processed to reveal the meaning
- Building blocks of information
- **Data management**
  - Generation, storage, and retrieval of data

#### Information

- Produced by **processing** data
- Reveals the meaning of data
- Enables **knowledge** creation
- Should be accurate, relevant, and timely to enable good decision making

### DB

### Database

- Shared, integrated computer structure that stores a collection of:
  - End-user data - Raw facts of interest to end user
  - **Metadata**: Data about data, which the end-user data are integrated and managed
    - Describe data characteristics and relationships
- **Database management system (DBMS)**
  - Collection of programs
  - Manages the database structure
  - Controls access to data stored in the database

### DBMS is a go-between

#### User $\leftrightarrow$ DBMS $\leftrightarrow$ data:

Figure 1.2 - The DBMS Manages the Interaction between the End User and the Database

<img src="Slides.assets/Screenshot 2026-06-08 at 9.43.32 PM.png" style="zoom:50%;" />

### Role of the DBMS

- Intermediary between the user and the database
- Enables data to be shared
- Presents the end user with an integrated view of the data
- Receives and translates application requests into operations required to fulfill the requests
- Hides database's internal complexity from the application programs and users

### DBMS: advantages

### Advantages of the DBMS

- Better data integration and less data inconsistency
  - **Data inconsistency:** Different versions of the same data appear in different places
- Increased end-user productivity
- Improved:
  - Data sharing
  - Data security
  - Data access
  - Decision making
    - **Data quality:** Promoting accuracy, validity, and timeliness of data

### Types of DBs

#### DBs can be categorized in multiple ways...

### Types of Databases

- **Single-user database:** Supports one user at a time
  - **Desktop database:** Runs on PC
- **Multiuser database:** Supports multiple users at the same time
  - **Workgroup databases:** Supports a small number of users or a specific department
  - **Enterprise database:** Supports many users across many departments

### Types of Databases

- **Centralized database:** Data is located at a single site
- **Distributed database:** Data is distributed across different sites
- **Cloud database:** Created and maintained using cloud data services that provide defined performance measures for the database

### Types of Databases

- **General-purpose databases:** Contains a wide variety of data used in multiple disciplines
- **Discipline-specific databases:** Contains data focused on specific subject areas

### Types of Databases

- **Operational database:** Designed to support a company's day-to-day operations

---

- **Analytical database:** Stores historical data and business metrics used exclusively for tactical or strategic decision making
- **Data warehouse:** Stores data in a format optimized for decision support
  - **Online analytical processing (OLAP)**
    - Enable retrieving, processing, and modeling data from the data warehouse
  - **Business intelligence:** Captures and processes business data to generate information that support decision making

### Types of Databases

- **Unstructured data:** It exists in their original state
- **Structured data:** It results from formatting
  - Structure is applied based on type of processing to be performed
- **Semistructured data:** Processed to some extent
- ~~▪ **Extensible Markup Language (XML)**~~
  - ~~▪ Represents data elements in textual format~~

#### Early DBs: file systems

#### Evolution of File System Data Processing

<img src="Slides.assets/Screenshot 2026-06-08 at 9.44.20 PM.png" alt="Screenshot 2026-06-08 at 9.44.20 PM" style="zoom:50%;" />

#### File systems

Table 1.2 - Basic File Terminology

| TERM          | DEFINITION                                                   |
| ------------- | ------------------------------------------------------------ |
| <b>Data</b>   | Raw facts, such as a telephone number, a birth date, a customer name, and a year-to-date (YTD) sales value. Data have little meaning unless they have been organized in some logical manner. |
| <b>Field</b>  | A character or group of characters (alphabetic or numeric) that has a specific meaning. A field is used to define and store data. |
| <b>Record</b> | A logically connected set of one or more fields that describes a person, place, or thing. For example, the fields that constitute a record for a customer might consist of the customer's name, address, phone number, date of birth, credit limit, and unpaid balance. |
| <b>File</b>   | A collection of related records. For example, a file might contain data about the students currently enrolled at Gigantic University. |

#### File system

Figure 1.6 - A Simple File System

<img src="Slides.assets/Screenshot 2026-06-08 at 9.45.03 PM.png" style="zoom:50%;" />

#### File systems: problems

#### Problems with File System Data Processing

Lengthy development times

Difficulty of getting quick answers

Complex system administration

Lack of security and limited data sharing

Extensive programming

### 'Structural' dependence (not a good thing!)

### Structural and Data Dependence

- **Structural dependence:** Access to a file is dependent on its own structure
  - All file system programs are modified to conform to a new file structure
- **Structural independence:** File structure is changed without affecting the application's ability to access the data

### Structural dependence [cont'd]

### Structural and Data Dependence

- Data dependence
  - Data access changes when data storage characteristics change
- Data independence
  - Data storage characteristics is changed without affecting the program's ability to access the data
- Practical significance of data dependence is difference between logical and physical format

### Redundancy of data (again, not a good thing!)

### Data Redundancy

- Unnecessarily storing same data at different places
- **Islands of information:** Scattered data locations
  - Increases the probability of having different versions of the same data

### Data Redundancy Implications

- Poor data security
- Data inconsistency
- Increased likelihood of data-entry errors when complex entries are made in different files
- **Data anomaly:** Develops when not all of the required changes in the redundant data are made successfully

### Types of Data Anomaly

Update Anomalies

Insertion Anomalies

Deletion Anomalies

## DB systems

### Database Systems

- Logically related data stored in a single logical data repository
  - Physically distributed among multiple storage facilities
  - DBMS eliminates most of file system's problems
- Current generation DBMS software:
  - Stores data structures, relationships between structures, and access paths
  - Defines, stores, and manages all access paths and components

### DBMS

### DBMS Functions

<img src="Slides.assets/Screenshot 2026-06-08 at 9.46.27 PM.png" alt="Screenshot 2026-06-08 at 9.46.27 PM" style="zoom:50%;" />

### DBMSs vs file systems

Figure 1.8 - Contrasting Database and File Systems

<img src="Slides.assets/Screenshot 2026-06-08 at 9.46.48 PM.png" style="zoom:50%;" />

#### DBMS - why

### DBMS Functions

#### Multiuser access control

- Sophisticated algorithms ensure that multiple users can access the database concurrently without compromising its integrity

#### Backup and recovery management

- Enables recovery of the database after a failure

#### Data integrity management

- Minimizes redundancy and maximizes consistency

#### DBMS - why#2

### DBMS Functions

### Database access languages and application programming interfaces

- **Query language:** Lets the user specify what must be done without having to specify how
- **Structured Query Language (SQL):** De facto query language and data access standard supported by the majority of DBMS vendors

### Database communication interfaces

- Accept end-user requests via multiple, different network environments

## Data Modeling

<img src="Slides.assets/Screenshot 2026-06-08 at 9.47.36 PM.png" alt="Screenshot 2026-06-08 at 9.47.36 PM" style="zoom:50%;" />

### Learning Objectives

- In this chapter, you will learn:
  - About data modeling and why data models are important
  - About the basic data-modeling building blocks
  - What business rules are and how they influence database design

### Learning Objectives

- In this chapter, you will learn:
  - How the major data models evolved
  - About emerging alternative data models and the need they fulfill
  - How data models can be classified by their level of abstraction

### . "All models are wrong, but some are useful"

### Data Modeling and Data Models

- **Data modeling:** Iterative and progressive process of creating a specific data model for a determined problem domain
- **Data models:** Simple representations of complex real-world data structures
- Useful for supporting a specific problem domain
- **Model** - Abstraction of a real-world object or event

### Importance of Data Models

Are a communication tool

Give an overall view of the database

Organize data for various users

Are an abstraction for the creation of good database

### . 3 types of relationships

### Data Model Basic Building Blocks

- **Entity:** Unique and distinct object used to collect and store data
  - **Attribute:** Characteristic of an entity
- **Relationship:** Describes an association among entities
  - **One-to-many (1:M)**
  - **Many-to-many (M:N or M:M)**
  - **One-to-one (1:1)**
- **Constraint:** Set of rules to ensure data integrity

Regardless of the model type, TWO entities are relatable in exactly three ways: 1:M, M:N, 1:1.

### . 'Business' (DOMAIN) rules: sources of entities and relationships

<img src="Slides.assets/Screenshot 2026-06-08 at 10.14.23 PM.png" style="zoom:50%;" />

#### Sources of Business Rules

<img src="Slides.assets/Screenshot 2026-06-08 at 10.14.39 PM.png" style="zoom:50%;" />

#### Reasons for Identifying and Documenting Business Rules

- Help standardize company's view of data
- Communications tool between users and designers
- Allow designer to:
  - Understand the nature, role, scope of data, and business processes
  - Develop appropriate relationship participation rules and constraints
  - Create an accurate data model

#### Translating Business Rules into Data Model Components

- Nouns translate into entities
- Verbs translate into relationships among entities
- Relationships are bidirectional
- Questions to identify the relationship type
  - How many instances of B are related to one instance of A?
  - How many instances of A are related to one instance of B?

#### Naming Conventions

- Entity names - Required to:
  - Be descriptive of the objects in the business environment
  - Use terminology that is familiar to the users
- Attribute name - Required to be descriptive of the data represented by the attribute
- Proper naming:
  - Facilitates communication between parties
  - Promotes self-documentation

### Hierarchical modeling

<img src="Slides.assets/Screenshot 2026-06-08 at 10.15.05 PM.png" style="zoom:50%;" />

#### Hierarchical Model

#### Advantages

- Promotes data sharing
- Parent/child relationship promotes conceptual simplicity and data integrity
- Database security is provided and enforced by DBMS
- Efficient with 1:M relationships

#### Disadvantages

- Requires knowledge of physical data storage characteristics
- Navigational system requires knowledge of hierarchical path
- Changes in structure require changes in all application programs
- Implementation limitations
- No data definition
- Lack of standards

**At first, data was stored in individual files (transitioned from paper). The next improvement was a 'hierarchical DB model', where data was structured in the form of a tree [similar to a modern filesystem]. Data, in the form of nodes, are linked in a tree-like fashion. To traverse the tree, we need to know the underlying format ('class hierarchy, to make an analogy with classes and objects), and the actual path [eg. to relate A1 and D2, we need to traverse A1->B1->C3>D2].**

**Hierarchies are good for '1:M' [tree], but not 'M:N' [graph or multiple inheritance].**

### Network modeling

<img src="Slides.assets/Screenshot 2026-06-08 at 10.15.32 PM.png" style="zoom:50%;" />

#### Network Model

#### Advantages

- Conceptual simplicity
- Handles more relationship types
- Data access is flexible
- Data owner/member relationship promotes data integrity
- Conformance to standards
- Includes data definition language (DDL) and data manipulation language (DML)

#### Disadvantages

- System complexity limits efficiency
- Navigational system yields complex implementation, application development, and management
- Structural changes require changes in all application programs

**A network model is better than a hierarchical one, because it can capture M:N [in addition to the above, another example is 'products and orders'].**

### Hierarchical and Network Models

#### Hierarchical Models

- Manage large amounts of data for complex manufacturing projects
- Represented by an upside-down tree which contains segments
  - **Segments:** Equivalent of a file system's record type
- Depicts a set of one-to-many (1:M) relationships

#### Network Models

- Represent complex data relationships
- Improve database performance and impose a database standard
- Depicts both one-to-many (1:M) and many-to-many (M:N) relationships

### Data creation, querying

### Standard Database Concepts

#### Schema

- Conceptual organization of the entire database as viewed by the database administrator

#### Subschema

- Portion of the database seen by the application programs that produce the desired information from the data within the database

#### Schema data definition language (DDL)

- Enables the database administrator to define the schema components

#### Data manipulation language (DML)

- Environment in which data can be managed and is used to work with the data in the database

### Relational model

#### The Relational Model

- Based on a relation
  - **Relation** or **table**: Matrix composed of intersecting tuple and attribute
  - **Tuple**: Rows
  - **Attribute**: Columns
- Describes a precise set of data manipulation constructs

#### Relational Model

##### Advantages

- Structural independence is promoted using independent tables
- Tabular view improves conceptual simplicity
- Ad hoc query capability is based on SQL
- Isolates the end user from physical-level details
- Improves implementation and management simplicity

##### Disadvantages (x)

- Requires substantial hardware and system software overhead
- Conceptual simplicity gives untrained people the tools to use a good system poorly
- May promote information problems

#### Relational Database Management System(RDBMS)

- Performs basic functions provided by the hierarchical and network DBMS systems
- Makes the relational data model easier to understand and implement
- Hides the complexities of the relational model from the user

#### SQL-Based Relational Database Application

- End-user interface
  - Allows end user to interact with the data
- Collection of tables stored in the database
  - Each table is independent from another
  - Rows in different tables are related based on common values in common attributes
- SQL engine
  - Executes all queries

##### E-R

## Figure 2.2 - A Relational Diagram

<img src="Slides.assets/Screenshot 2026-06-08 at 10.16.57 PM.png" style="zoom:50%;" />

### The Entity Relationship Model

- Graphical representation of entities and their relationships in a database structure
- **Entity relationship diagram (ERD)**
  - Uses graphic representations to model database components
- **Entity instance or entity occurrence**
  - Rows in the relational table
- **Connectivity:** Term used to label the relationship types

#### Entity Relationship Model

#### Advantages

- Visual modeling yields conceptual simplicity
- Visual representation makes it an effective communication tool
- Is integrated with the dominant relational model

#### Disadvantages

- Limited constraint representation
- Limited relationship representation
- No data manipulation language
- Loss of information content occurs when attributes are removed from entities to avoid crowded displays

#### Notations

Figure 2.3 - The ER Model Notations

<img src="Slides.assets/Screenshot 2026-06-08 at 10.17.26 PM.png" style="zoom:50%;" />

**Additional reading: here is information on, and comparison between, four ER notations: Chen, Crow, Rein85, IDEFIX.**

#### Two more models [loosely, 'semantic']: O-O, O-R

O-O DBs: also called 'object stores', these dbs offer(ed) a way to store ("persist") objects on disk. The objects (entity instances) are instanced from classes (entities), like with standard OO programming practice.

##### Advantages:

- 'cleaner' design - objects mimic real-world counterparts
- inheritance and encapsulation possible
- richer datatypes (attributes) available
- good for CAD, multimedia..

##### Drawbacks:

- harder to query (compared to relational DBs) - no straightforward way to build and traverse relations between objects
- relations are simpler in certain situations

The RDBMS community collectively ignored this development..

---

O-R DBs are a compromise between RDBs and OODBs - they feature an O-O front-end over a relational architecture. Interfacing applications do so in an O-O way, and queries/modifications are translated to/from relational form ("ORM").

##### Benefits:

- easy to access the data from an O-O application
- queries can be simpler (can use objects' structure)

##### Drawback:

- **performance can be poor on account of the two-way translation**

#### Data models: hierarchical => => NoSQL => =>...

Figure 2.6 - The Evolution of Data Models

<img src="Slides.assets/Screenshot 2026-06-08 at 10.18.00 PM.png" style="zoom:50%;" />

Data models have evolved - from 'hierarchical' (very rigid) to 'NoSQL' (VERY flexible).

The evolution continues... the **vector model** is used to represent data (text, images, audio, video...) as n-D vectors (aka 'embeddings'). Vector DBs (eg. Pinecone and MANY others) store such vectors, and enable their querying (based on SIMILARITY to an input).

#### Layered data abstraction

Figure 2.7 - Data Abstraction Levels

<img src="Slides.assets/Screenshot 2026-06-08 at 10.18.16 PM.png" style="zoom:50%;" />

### External ['user'] model

#### The External Model

- End users' view of the data environment
- ER diagrams are used to represent the external views
- **External schema:** Specific representation of an external view

Figure 2.8 - External Models for Tiny College

<img src="Slides.assets/Screenshot 2026-06-08 at 10.18.29 PM.png" style="zoom:50%;" />

An external model is a collection of '**fragmented**' (from stakeholders' POV) views of a DB.

### Conceptual ['designer'] model

#### The Conceptual Model

- Represents a global view of the entire database by the entire organization
- **Conceptual schema:** Basis for the identification and high-level description of the main data objects
- Has a macro-level view of data environment
- Is software and hardware independent
- **Logical design:** Task of creating a conceptual data model

Figure 2.9 - Conceptual Model for Tiny College

<img src="Slides.assets/Screenshot 2026-06-08 at 10.18.44 PM.png" style="zoom:50%;" />

**A conceptual model unifies the external views into a cohesive one.**

### Internal ['programmer'] model

#### The Internal Model

- Representing database as seen by the DBMS  
mapping conceptual model to the DBMS
- **Internal schema:** Specific representation of an internal model
  - Uses the database constructs supported by the chosen database
- Is software dependent and hardware independent
- **Logical independence:** Changing internal model without affecting the conceptual model

Figure 2.10 - Internal Model for Tiny College

<img src="Slides.assets/Screenshot 2026-06-08 at 10.18.58 PM.png" style="zoom:50%;" />

**The internal model is more detailed, has attribute names+types for each entity.**

### Physical ['implementer'] model

#### The Physical Model

- Operates at lowest level of abstraction
- Describes the way data are saved on storage media such as disks or tapes
- Requires the definition of physical storage and data access methods
- Relational model aimed at logical level
  - Does not require physical-level details
- **Physical independence:** Changes in physical model do not affect internal model

**The physical model specifies actual data storage specifics [file format (private), APIs (public)].**

# ER

### ER{M,D} - a visual summary

### Entity Relationship Model (ERM)

- Basis of an entity relationship diagram (ERD)
- ERD depicts the:
  - Conceptual database as viewed by end user
  - Database's main components
    - Entities
    - Attributes
    - Relationships
- Entity - Refers to the entity set and not to a single entity occurrence

#### ATTRIBUTES - one of the MOST important concepts [EVER]!

#### Attributes

- Characteristics of entities
- **Required attribute:** Must have a value, cannot be left empty
- **Optional attribute:** Does not require a value, can be left empty
- Domain - Set of possible values for a given attribute
- **Identifiers:** One or more attributes that uniquely identify each entity instance

An identifier is also called a KEY, or PRIMARY KEY - this is one of the 'key' concepts in all of database theory!! We'll talk much more about keys later.

Figure 4.1 - The Attributes of the Student Entity: Chen and Crow's Foot

<img src="Slides.assets/Screenshot 2026-06-08 at 10.23.45 PM.png" style="zoom:50%;" />

##### Attributes - so many kinds

## Attributes

- **Composite identifier:** Primary key composed of more than one attribute
- ~~Composite~~ **Compound attribute:** Attribute that can be subdivided to yield additional attributes
- **Simple attribute:** Attribute that cannot be subdivided
- **Single-valued attribute:** Attribute that has only a single value
- **Multivalued attributes:** Attributes that have many values

FYI - here is a page on the various types of attributes.

## Attributes

- **Multivalued attributes:** Attributes that have many values and require creating:
  - Several new attributes, one for each component of the original multivalued attribute
  - A new entity composed of the original multivalued attribute's components
- **Derived attribute:** Attribute whose value is calculated from other attributes
  - Derived using an algorithm

# Figure 4.3 - A Multivalued Attribute in an Entity

<img src="Slides.assets/Screenshot 2026-06-08 at 10.24.44 PM.png" style="zoom:50%;" />

In Crow's Foot notation, '**bold**' attributes are 'required' (can't be null).

##### Derived attributes

Figure 4.6 - Depiction of a Derived Attribute

<img src="Slides.assets/Screenshot 2026-06-08 at 10.24.57 PM.png" style="zoom:50%;" />

Table 4.2 - Advantages and Disadvantages of Storing Derived Attributes

|              | STORED                                                       | NOT STORED                                                   |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Advantage    | Saves CPU processing cycles<br>Saves data access time<br>Data value is readily available<br>Can be used to keep track of historical data | Saves storage space<br>Computation always yields current value |
| Disadvantage | Requires constant maintenance to ensure derived value is current, especially if any values used in the calculation change | Uses CPU processing cycles<br>Increases data access time<br>Adds coding complexity to queries |

#### RELATIONSHIPS between entities

#### Relationships

- Association between entities that always operate in both directions
- **Participants:** Entities that participate in a relationship
- **Connectivity:** Describes the relationship classification
- **Cardinality:** Expresses the minimum and maximum number of entity occurrences associated with one occurrence of related entity

Figure 4.7 - Connectivity and Cardinality in an ERD

<img src="Slides.assets/Screenshot 2026-06-08 at 10.25.29 PM.png" style="zoom:50%;" />

 1:1, 1:M or M:N (three diff ways by which two entities are related).

**Cardinality:** (min,max) for 1:1, 1:M or M:N (eg. 1:1 can have (1,0) as its cardinality, 1:M can have (0,4) as its cardinality). Sometimes, min is called 'modality' (and max is cardinality). The 'inside' symbols denotes min, and the outside ones, max.

Confusingly, the # rows in a table is ALSO called table's cardinality (and, # of columns is called the table's degree).

Also confusingly, 1:1, 1:M, M:N are called 'cardinality ratios'!

##### In/dependence ['can I exist apart from you?']

<img src="Slides.assets/Screenshot 2026-06-08 at 10.25.58 PM.png" style="zoom:50%;" />

An entity B is "existent dependent" on another entity A, if, a row in B can only exist when its FK is NOT NULL, ie. a corresponding entry exists in A.

Eg. if A is EMPLOYEE and B is DEPENDENT, a dependent (eg. child) in B can only exist if there is a corresponding employee (eg. Dad) in A. But - this alone DOES NOT make 'B' a weak entity!

IOW: existence independence implies a strong entity; but, existence dependence (alone, ie. by itself) does NOT imply a weak entity (there needs to be one more condition, based on 'relationship strength', for it to become 'weak').

In other words, **we need to look at where the FK in the dependent entity is located, to determine if the dependent entity is weak, or not-weak.**

#### Relationship strength [weak vs strong]

Again, it's all about the FK [WHERE it goes], in the dependent entity!

## Relationship Strength

### Weak (non-identifying) relationship

- Primary key of the related entity does not contain a primary key component of the parent entity

### Strong (identifying) relationships

- Primary key of the related entity contains a primary key component of the parent entity

##### Not-weak, weak

Figure 4.8 - A Weak (Non-Identifying) Relationship between COURSE and CLASS

<img src="Slides.assets/Screenshot 2026-06-08 at 10.26.20 PM.png" style="zoom:75%;" />

In the above, CLASS is **not** a weak entity [is existent-dependent BUT has a weak relationship].

Figure 4.9 - A Strong (Identifying) Relationship between COURSE and CLASS

<img src="Slides.assets/Screenshot 2026-06-08 at 10.27.06 PM.png" style="zoom:80%;" />

CLASS above is now a weak entity (is existence dependent AND has a strong relationship). 'Strong' means 'shared PK'.

##### Weak entity [two conditions]

##### Weak Entity

- Conditions
  - Existence-dependent
  - Has a primary key that is partially or totally derived from parent entity in the relationship
- Database designer determines whether an entity is weak based on business rules

**A weak entity needs to satisfy two conditions: existence dependence, strong (identifying/owning) relationship with a parent.**

**Note that a weak entity implies existence dependence, but existence dependence does not imply a weak entity!**

**Note too that a weak entity implies a strong ("owning" or "identifying") relationship.**

**Removing the controlling (owning) entity's key from a weak entity's PK will result in **\*\*duplicates\*\*** for remaining PK(s) - THAT is what makes it 'weak'.**

##### Weak entity - another example

<img src="Slides.assets/Screenshot 2026-06-08 at 10.28.01 PM.png" style="zoom:50%;" />

**Payment cannot exist independent of Loan, AND needs Loan's key to be part of its own key, so it (Payment) is a weak entity.**

##### Weak entity - ERD and table depiction

Figure 4.10 - A Weak Entity in an ERD

<img src="Slides.assets/Screenshot 2026-06-08 at 10.28.14 PM.png" style="zoom:80%;" />

Figure 4.11 - A Weak Entity

<img src="Slides.assets/Screenshot 2026-06-08 at 10.28.31 PM.png" alt="Screenshot 2026-06-08 at 10.28.31 PM" style="zoom:80%;" />

#### Relationship Participation

##### Optional participation

- One entity occurrence does not require a corresponding entity occurrence in a particular relationship

##### Mandatory participation

- One entity occurrence requires a corresponding entity occurrence in a particular relationship

###### Table 4.3 - Crow's Foot Symbols

<img src="Slides.assets/Screenshot 2026-06-08 at 10.29.50 PM.png" alt="Screenshot 2026-06-08 at 10.29.50 PM" style="zoom:67%;" />

Figure 4.13 - CLASS is Optional to COURSE

<img src="Slides.assets/Screenshot 2026-06-08 at 10.30.10 PM.png" style="zoom:80%;" />

Figure 4.14 - COURSE and CLASS in a Mandatory Relationship

<img src="Slides.assets/Screenshot 2026-06-08 at 10.45.30 PM.png" style="zoom:80%;" />

#### Relationship DEGREE

#### Relationship Degree

- Indicates the number of entities or participants associated with a relationship
- **Unary relationship:** Association is maintained within a single entity
  - **Recursive relationship:** Relationship exists between occurrences of the same entity set
- **Binary relationship:** Two entities are associated
- **Ternary relationship:** Three entities are associated

<img src="Slides.assets/Screenshot 2026-06-08 at 10.45.55 PM.png" style="zoom:70%;" />

#### Recursive:

Figure 4.17 - An ER Representation of Recursive Relationships

<img src="Slides.assets/Screenshot 2026-06-08 at 10.46.13 PM.png" style="zoom:67%;" />

##### Bridge entities

##### Associative Entities

- Also known as composite or bridge entities
- Used to represent an M:N relationship between two or more entities
- Is in a 1:M relationship with the parent entities
  - Composed of the primary key attributes of each parent entity
- May also contain additional attributes that play no role in connective process

Figure 4.23 - Converting the M:N Relationship into Two 1:M Relationships

<img src="Slides.assets/Screenshot 2026-06-08 at 10.46.50 PM.png" alt="Screenshot 2026-06-08 at 10.46.50 PM" style="zoom:80%;" />

# Figure 4.25 - A Composite Entity in an ERD

<img src="Slides.assets/Screenshot 2026-06-08 at 11.44.05 PM.png" style="zoom:50%;" />

#### Putting together an ERD

##### Developing an ER Diagram

- Create a detailed narrative of the organization's description of operations
- Identify business rules based on the descriptions
- Identify main entities and relationships from the business rules
- Develop the initial ERD
- Identify the attributes and primary keys that adequately describe entities
- Revise and review ERD

#### ERD - piece by piece

Figure 4.26 - The First Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-08 at 11.44.28 PM.png" style="zoom:50%;" />

Figure 4.27 - The Second Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-08 at 11.44.39 PM.png" style="zoom:50%;" />

### Figure 4.28 - The Third Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-08 at 11.44.55 PM.png" style="zoom:50%;" />

### Figure 4.29 - The Fourth Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-08 at 11.45.06 PM.png" style="zoom:50%;" />

### Figure 4.30 - The Fifth Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-08 at 11.45.22 PM.png" style="zoom:50%;" />

### Figure 4.31 - The Sixth Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-09 at 3.50.31 PM.png" style="zoom:50%;" />

### Figure 4.32 - The Seventh Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-09 at 3.50.47 PM.png" style="zoom:50%;" />

### Figure 4.33 - The Eighth Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-09 at 3.51.04 PM.png" style="zoom:50%;" />

## Figure 4.34 - The Ninth Tiny College ERD Segment

<img src="Slides.assets/Screenshot 2026-06-09 at 3.51.19 PM.png" style="zoom:50%;" />

##### The full schema

The full list ['BOM'] can be presented as a table, or as a diagram:

Table 4.4 - Components of the ERM

| ENTITY     | RELATIONSHIP | CONNECTIVITY | ENTITY     |
| ---------- | ------------ | ------------ | ---------- |
| SCHOOL     | operates     | 1:M          | DEPARTMENT |
| DEPARTMENT | has          | 1:M          | STUDENT    |
| DEPARTMENT | employs      | 1:M          | PROFESSOR  |
| DEPARTMENT | offers       | 1:M          | COURSE     |
| COURSE     | generates    | 1:M          | CLASS      |
| PROFESSOR  | is dean of   | 1:1          | SCHOOL     |
| PROFESSOR  | chairs       | 1:1          | DEPARTMENT |
| PROFESSOR  | teaches      | 1:M          | CLASS      |
| PROFESSOR  | advises      | 1:M          | STUDENT    |
| STUDENT    | enrolls in   | M:N          | CLASS      |
| BUILDING   | contains     | 1:M          | ROOM       |
| ROOM       | is used for  | 1:M          | CLASS      |

Note: ENROLL is the composite-entity that implements the M:N relationship "STUDENT enrolls in CLASS."



The Completed Tiny College ERD

<img src="Slides.assets/Screenshot 2026-06-09 at 3.52.05 PM.png" style="zoom:75%;" />

"All together now!"

#### Extended ER ("EER")

## Database Systems Design, Implementation, and Management

# Chapter 5 Advanced Data Modeling

### Extended Entity Relationship Model (EERM)

- Result of adding more semantic constructs to the original entity relationship (ER) model
- **EER diagram (EERD):** Uses the EER model

#### Entity Supertypes and Subtypes

- **Entity supertype:** Generic entity type related to one or more entity subtypes
  - Contains common characteristics
- **Entity subtype:** Contains unique characteristics of each entity subtype
- Criteria to determine the usage
  - There must be different, identifiable kinds of the entity in the user's environment
  - The different kinds of instances should each have one or more attributes that are unique to that kind of instance

#### Specialization Hierarchy

- Depicts arrangement of higher-level entity supertypes and lower-level entity subtypes
- Relationships are described in terms of “is-a” relationships
- Subtype exists within the context of a supertype
- Every subtype has one supertype to which it is directly related
- Supertype can have many subtypes

#### Specialization Hierarchy

- Provides the means to:
  - Support attribute inheritance
  - Define a special supertype attribute known as the subtype discriminator
  - Define disjoint/overlapping constraints and complete/partial constraints

###### Figure 5.2 - Specialization Hierarchy

<img src="Slides.assets/Screenshot 2026-06-09 at 3.53.07 PM.png" style="zoom:67%;" />

##### Inheritance

- Enables an entity subtype to inherit attributes and relationships of the supertype
- All entity subtypes inherit their primary key attribute from their supertype
- At the implementation level, supertype and its subtype(s) maintain a 1:1 relationship
- Entity subtypes inherit all relationships in which supertype entity participates
- Lower-level subtypes inherit all attributes and relationships from its upper-level supertypes

##### Subtype Discriminator

- Attribute in the supertype entity that determines to which entity subtype the supertype occurrence is related
- Default comparison condition is the equality comparison

##### Disjoint vs overlapping subtypes

##### Disjoint and Overlapping Constraints

- **Disjoint subtypes:** Contain a unique subset of the supertype entity set
  - Known as **nonoverlapping subtypes**
  - Implementation is based on the value of the subtype discriminator attribute in the supertype
- **Overlapping subtypes:** Contain nonunique subsets of the supertype entity set
  - Implementation requires the use of one discriminator attribute for each subtype

## Figure 5.4 - Specialization Hierarchy with Overlapping Subtypes

<img src="Slides.assets/Screenshot 2026-06-09 at 3.53.59 PM.png" style="zoom:67%;" />

##### Completeness Constraint

- Specifies whether each supertype occurrence must also be a member of at least one subtype
- Types
  - **Partial completeness:** Not every supertype occurrence is a member of a subtype
  - **Total completeness:** Every supertype occurrence must be a member of any

## Table 5.2 - Specialization Hierarchy Constraint Scenarios

<img src="Slides.assets/Screenshot 2026-06-09 at 3.54.31 PM.png" alt="Screenshot 2026-06-09 at 3.54.31 PM" style="zoom:67%;" />

##### 'Union'

What if we flipped the DISJOINT subtype concept?

Example of categories  
(UNION TYPE)

<img src="Slides.assets/Screenshot 2026-06-09 at 3.54.50 PM.png" style="zoom:50%;" />

#### 'Lattice'

What if we allowed a child table to have >1 parent?

##### Specialization / Generalization Lattice Example (UNIVERSITY)

<img src="Slides.assets/Screenshot 2026-06-09 at 3.55.08 PM.png" style="zoom:67%;" />

#### A completely unrelated idea: 'clusters' [grouping]

Figure 5.5 - Tiny College ERD Using Entity Clusters

<img src="Slides.assets/Screenshot 2026-06-09 at 3.55.20 PM.png" style="zoom:67%;" />

### Relational Modeling

### Logical view: 'relation'

#### A Logical View of Data

- Relational database model enables logical representation of the data and its relationships
- Logical simplicity yields simple and effective database design methodologies
- Facilitated by the creation of data relationships based on a logical construct called a relation

#### Relational tables

Table 3.1 - Characteristics of a Relational Table

|      |                                                              |
| ---- | ------------------------------------------------------------ |
| 1    | A table is perceived as a two-dimensional structure composed of rows and columns. |
| 2    | Each table row ( <b>tuple</b> ) represents a single entity occurrence within the entity set. |
| 3    | Each table column represents an attribute, and each column has a distinct name. |
| 4    | Each intersection of a row and column represents a single data value. |
| 5    | All values in a column must conform to the same data format. |
| 6    | Each column has a specific range of values known as the <b>attribute domain</b> . |
| 7    | The order of the rows and columns is immaterial to the DBMS. |
| 8    | Each table must have an attribute or combination of attributes that uniquely identifies each row. |

#### Keys

#### Keys

- Consist of one or more attributes that determine other attributes
- Used to:
  - Ensure that each row in a table is uniquely identifiable
  - Establish relationships among tables and to ensure the integrity of the data
- **Primary key (PK):** Attribute or combination of attributes that uniquely identifies any given row

##### "determines"

#### Determination

- State in which knowing the value of one attribute makes it possible to determine the value of another
- Is the basis for establishing the role of a key
- Based on the relationships among the attributes

##### Determinants determine dependents [via] dependencies :)

#### Dependencies

- **Functional dependence:** Value of one or more attributes determines the value of one or more other attributes
  - **Determinant:** Attribute whose value determines another
  - **Dependent:** Attribute whose value is determined by the other attribute
- **Full functional dependence:** Entire collection of attributes in the determinant is necessary for the relationship

'Full' functional dependence is a "good" thing.

##### Functional dependency

**STU\_ID[determinant] ->[functionally determines] STU\_LNAME[dependent]**

**STU\_ID,STU\_LNAME -> GPA is NOT a 'full functional dependency' because the determinant contains an extra (unwanted) attr (STU\_LNAME)**

**STU\_LNAME,STU\_FNAME -> GPA is a 'full functional dependency' (assuming lastname,firstname is unique)**

**Solemnly swear: "The key, the whole key, and nothing but the key, so help me Codd."  
:):)**

#### Composite key; entity integrity

#### Types of Keys

- **Composite key:** Key that is composed of more than one attribute
- **Key attribute:** Attribute that is a part of a key
- **Entity integrity:** Condition in which each row in the table has its own unique identity
  - All of the values in the primary key must be unique
  - No key attribute in the primary key can contain a null

**A table 'cannot not' have entity integrity!!**

##### Nulls; referential integrity

#### Types of Keys

- **Null:** Absence of any data value that could represent:
  - An unknown attribute value
  - A known, but missing, attribute value
  - A inapplicable condition
- **Referential integrity:** Every reference to an entity instance by another entity instance is valid

Whereas entity integrity has to do with a single table, referential integrity relates to two tables (loosely, 'don't allow invalid pointers').

##### Types (categories) of keys

Table 3.3 - Relational Database Keys

| KEY TYPE      | DEFINITION                                                   |
| ------------- | ------------------------------------------------------------ |
| Superkey      | An attribute or combination of attributes that uniquely identifies each row in a table |
| Candidate key | A minimal (irreducible) superkey; a superkey that does not contain a subset of attributes that is itself a superkey |
| Primary key   | A candidate key selected to uniquely identify all other attribute values in any given row; cannot contain null entries |
| Foreign key   | An attribute or combination of attributes in one table whose values must either match the primary key in another table or be null |
| Secondary key | An attribute or combination of attributes used strictly for data retrieval purposes |

##### Keys: many types

- \* primary (foreign) keys are a subset of candidate keys are a subset of superkeys (note - superkeys could be 'wasteful', ie. contain superfluous, non-needed attrs)
- \* simple keys vs composite keys
- \* natural keys - keys that are created from real-world entities (eg. for a US resident, their SSN could be a natural key)
- \* surrogate keys (just make up brand new unique keys)
- \* secondary, or 'alternate' keys

You can read a bit more keys [here](#).

##### Example relation

<img src="Slides.assets/Screenshot 2026-06-09 at 3.57.19 PM.png" alt="Screenshot 2026-06-09 at 3.57.19 PM" style="zoom:67%;" />

#### Nulls - avoid where possible!

#### Ways to Handle Nulls

- **Flags:** Special codes used to indicate the absence of some value
- **NOT NULL constraint** - Placed on a column to ensure that every row in the table has a value for that column
- **UNIQUE constraint** - Restriction placed on a column to ensure that no duplicate values exist for that column

In RL, NULLs can't be entirely avoided (look here, for 'interpreted as any of the following').

#### Relational 'algebra' [fun with one, two or more tables]

#### Relational Algebra

- Theoretical way of manipulating table contents using relational operators
- **Relvar**: Variable that holds a relation
  - Heading contains the names of the attributes and the body contains the relation
- Relational operators have the property of closure
  - **Closure**: Use of relational algebra operators on existing relations produces new relations

What if a table were a datatype (similar to an int, Vec3D, ComplexNumber, odd #s, prime #s, etc)?! Specifically, what operations could be performed on them (eg. similar to addition, square root on doubles)?!

#### Operations on tables [table(s) in, table out, ie. "closure"]

There are (only) EIGHT 'relational set operators' (defined by Ed Codd, at IBM, in 1970), which are all used to operate ("perform relational algebra") on tables: **Select, Project, Union, Intersect, Difference, Product, Divide, Join** - 'UNDERSTAND → KNOW' THESE WELL!!.

This is no exaggeration: these operators are the basis for SQL, and the entire relational DB industry!

#### SELECT; PROJECT; UNION; INTERSECT

#### Relational Set Operators

##### Select (Restrict)

- Unary operator that yields a horizontal subset of a table

##### Project

- Unary operator that yields a vertical subset of a table

##### Union

- Combines all rows from two tables, excluding duplicate rows
- **Union-compatible**: Tables share the same number of columns, and their corresponding columns share compatible domains

##### Intersect

- Yields only the rows that appear in both tables
- Tables must be union-compatible to yield valid results

##### SELECT [outputs a subset of rows]

Figure 3.4 - Select

<img src="Slides.assets/Screenshot 2026-06-09 at 3.58.05 PM.png" style="zoom:67%;" />

##### PROJECT [outputs a subset of cols]

Figure 3.5 - Project

<img src="Slides.assets/Screenshot 2026-06-09 at 3.58.19 PM.png" style="zoom:67%;" />

##### UNION [eqvt to 'cat a b > c']

Figure 3.6 - Union

<img src="Slides.assets/Screenshot 2026-06-09 at 3.58.38 PM.png" alt="Screenshot 2026-06-09 at 3.58.38 PM" style="zoom:67%;" />

##### INTERSECT [rows common to a and b]

Figure 3.7 - Intersect

<img src="Slides.assets/Screenshot 2026-06-09 at 4.00.02 PM.png" alt="Screenshot 2026-06-09 at 4.00.02 PM" style="zoom:67%;" />

#### Difference; Product

#### Relational Set Operators

##### - **Difference**

- Yields all rows in one table that are not found in the other table
- Tables must be union-compatible to yield valid results

##### - **Product**

- Yields all possible pairs of rows from two tables

##### Difference [a - b]

Figure 3.8 - Difference

<img src="Slides.assets/Screenshot 2026-06-09 at 4.00.24 PM.png" alt="Screenshot 2026-06-09 at 4.00.24 PM" style="zoom:67%;" />

##### Product [multiply rows, add columns]

Figure 3.9 - Product

<img src="Slides.assets/Screenshot 2026-06-09 at 4.00.50 PM.png" alt="Screenshot 2026-06-09 at 4.00.50 PM" style="zoom:67%;" />

#### DIVIDE

##### ■ Divide

- Uses one 2-column table as the dividend and one single-column table as the divisor
- Output is a single column that contains all values from the second column of the dividend that are associated with every row in the divisor

Figure 3.16 - Divide

<img src="Slides.assets/Screenshot 2026-06-09 at 4.01.05 PM.png" style="zoom:67%;" />

We're dividing by A and B in the divisor (bottom) table. There's (A,5) and (B,5) in the dividend (top) table, so we output 5 as the result; if the dividend were to contain (A,9) and (B,9) also, then we'd output 5 9 as the result.

#### JOIN

#### - **Join**

- Allows information to be intelligently combined from two or more tables

#### Types of Joins

- **Natural join:** Links tables by selecting only the rows with common values in their common attributes
  - **Join columns:** Common columns
- **Equijoin:** Links tables on the basis of an equality condition that compares specified columns of each table
- **Theta join:** Extension of natural join, denoted by adding a theta subscript after the JOIN symbol

#### JOIN [cont'd]

#### Types of Joins

- **Inner join:** Only returns matched records from the tables that are being joined
- **Outer join:** Matched pairs are retained and unmatched values in the other table are left null
  - **Left outer join:** Yields all of the rows in the first table, including those that do not have a matching value in the second table
  - **Right outer join:** Yields all of the rows in the second table, including those that do not have matching values in the first table

#### Tables to illustrate JOIN operations

Figure 3.10 - Two Tables That Will Be Used in JOIN Illustrations

<img src="Slides.assets/Screenshot 2026-06-09 at 4.01.46 PM.png" alt="Screenshot 2026-06-09 at 4.01.46 PM" style="zoom:80%;" />

##### Natural join

A natural join links tables by selecting from two tables, only those rows that have common (identical) values for common attributes.

These three steps result in a natural join: create product, select, project.

**Cartesian product of the two tables (product of rows, juxtaposition of columns):**

<img src="Slides.assets/Screenshot 2026-06-09 at 4.02.11 PM.png" alt="Screenshot 2026-06-09 at 4.02.11 PM" style="zoom:80%;" />

**Select only rows with identical values in the common (joining) columns:**

<img src="Slides.assets/Screenshot 2026-06-09 at 4.02.27 PM.png" alt="Screenshot 2026-06-09 at 4.02.27 PM" style="zoom:80%;" />

**Project away, ie. remove one of the two duplicate columns:**

<img src="Slides.assets/Screenshot 2026-06-09 at 4.02.44 PM.png" alt="Screenshot 2026-06-09 at 4.02.44 PM" style="zoom:80%;" />

**Result (the table above): natural join.**

##### Left outer join, right outer join, full outer join

Output all rows of the left (CUSTOMER) table, including ones for which there are no matching values in the join column in the other (AGENT) table:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.03.03 PM.png" alt="Screenshot 2026-06-09 at 4.03.03 PM" style="zoom:80%;" />

Note that an outer join is an "inner join plus" [it is NOT an opposite of inner join].

Output all rows of the right (AGENT) table, including ones for which there are no matching values in the join column in the other (CUSTOMER) table:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.03.34 PM.png" alt="Screenshot 2026-06-09 at 4.03.34 PM" style="zoom:80%;" />

Outer joins are useful in exposing missing information [in our example, customers who don't seem to have an agent, and, agents who don't seem to have customers].

A 'full outer join' is a union of left outer join and right outer join - output all the rows from both tables, including ones for which there are no matches in the other table - this could result in nulls on the left side of some rows, as well as nulls on the right side of others.

This clip shows the various types of joins:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.03.45 PM.png" style="zoom:80%;" />

### Dictionaries [hold metadata]

#### Data Dictionary and the System Catalog

- **Data dictionary:** Description of all tables in the database created by the user and designer
- **System catalog:** System data dictionary that describes all objects within the database
- Homonyms and synonyms must be avoided to lessen confusion
  - **Homonym:** Same name is used to label different attributes
  - **Synonym:** Different names are used to describe the same attribute

**A data dictionary is metadata about tables (only); a system catalog, that includes (is a superset of, although confusingly, the two are conflated in RL) the data dictionary, and more.**



# (De/)Normalization

### On tap

### Learning Objectives

- In this chapter, students will learn:
  - What normalization is and what role it plays in the database design process
  - About the normal forms 1NF, 2NF, 3NF, BCNF, and 4NF
  - How normal forms can be transformed from lower normal forms to higher normal forms
  - That normalization and ER modeling are used concurrently to produce a good database design
  - That some situations require denormalization to generate information efficiently

#### The goal of normalization

Loosely speaking:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.04.29 PM.png" style="zoom:80%;" />

#### Goal: reduce redundancies, anomalies

#### Normalization is a design step:

#### Normalization

- Evaluating and correcting table structures to minimize data redundancies
- Reduces data anomalies
- Assigns attributes to tables based on determination
- Normal forms
  - First normal form (1NF)
  - Second normal form (2NF)
  - Third normal form (3NF)

#### Higher normal forms → cleaner designs:

#### Normalization

- Structural point of view of normal forms
  - Higher normal forms are better than lower normal forms
- Properly designed 3NF structures meet the requirement of fourth normal form (4NF)
- **Denormalization:** Produces a lower normal form
  - Results in increased performance and greater data redundancy

#### Normalization is best performed **EARLY** in the overall design process:

#### Need for Normalization

- Used while designing a new database structure
  - Analyzes the relationship among the attributes within each entity
  - Determines if the structure can be improved
- Improves the existing data structure and creates an appropriate database design

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

#### A construction company db

Employees of the construction company work on projects. Each employee has an ID, name, job title and corresponding hourly rate.

Each project has a number, name and assigned employees. An employee can be assigned to more than one project.

The company bills clients for projects, based on hours worked by employees.

<img src="Slides.assets/Screenshot 2026-06-09 at 4.05.07 PM.png" alt="Screenshot 2026-06-09 at 4.05.07 PM" style="zoom:80%;" />

The construction company periodically generates a report like so:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.05.19 PM.png" alt="Screenshot 2026-06-09 at 4.05.19 PM" style="zoom:80%;" />

#### Issues with our db

Here is our table again:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.05.39 PM.png" alt="Screenshot 2026-06-09 at 4.05.39 PM" style="zoom:80%;" />

There are numerous issues in our 'table':

- the PROJ\_NUM attr could be used as a PK (or part of a PK, along with PROJ\_NAME) but it contains nulls
- possibilities for data inconsistencies exist, eg. if someone's name or title is misspelled
- the redundancies that exist, could lead to insertion anomalies (eg. a new employee needs to be assigned to some project, even a fake one), update anomalies (eg. if an employee's JOB\_CLASS changes, it has to be modified multiple times), deletion anomalies (eg. if a project has just one employee and that employee leaves, deleting the lone employee record would lead to the project itself getting deleted!)
- data redundancy leads to wasted storage space

We have 'repeating groups' (for each project, we list all details about each employee) - our table is un-normalized, ie. is in 'ONF' :)

So, we need to clean up the design!

Objective:

#### Normalization Process

- Objective is to ensure that each table conforms to the concept of well-formed relations
  - Each table represents a single subject
  - No data item will be unnecessarily stored in more than one table
  - All nonprime attributes in a table are dependent **wholly; nothing but** on the primary key
  - Each table is void of insertion, update, and deletion anomalies

#### Normal forms

Normalization is a systematic process that yields progressively higher 'normal forms' (NFs) for each entity (table) in our db. We want **at least 3NF** for each table; in RL, we stop at 3NF.

Table 6.2 - Normal Forms

<img src="Slides.assets/Screenshot 2026-06-09 at 4.06.24 PM.png" alt="Screenshot 2026-06-09 at 4.06.24 PM" style="zoom:80%;" />

#### The process

#### Normalization Process

- Ensures that all tables are in at least 3NF
- Higher forms are not likely to be encountered in business environment
- Works one relation at a time
- Starts by:
  - Identifying the dependencies of a relation (table)
  - Progressively breaking the relation into new set of relations

**Normalization how-to, in one sentence: work on one relation (table) at a time: identify dependencies, then 'normalize' - progressively break it down into smaller relations (tables), based on the dependencies we identify in the original relation so that "only the PK, the whole PK and nothing but the PK" acts as a determinant! But how?? Details follow..**

### Functional dependence, determination

#### Functional Dependence Concepts

| Concept                                        | Definition                                                   |
| ---------------------------------------------- | ------------------------------------------------------------ |
| Functional dependence                          | The attribute B is fully functionally dependent on the attribute A if each value of A determines one and only one value of B. |
| Functional dependence (Generalized definition) | Attribute A determines attribute B if all of the rows in the table that agree in value for attribute A also agree in value for attribute B. |
| Fully functional dependence (composite key)    | If attribute B is functionally dependent on a composite key A but not on any Subset of that composite key, the attribute B is fully functionally dependent on A. |

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

##### Partial dependency, transitive dependency:

##### Types of Functional Dependencies

- **Partial dependency:** Functional dependence in which the determinant is only part of the primary key
  - Assumption - One candidate key
  - Straight forward
  - Easy to identify
- **Transitive dependency:** An attribute functionally depends on another nonkey attribute

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

If (A,B) is a primary key, we have **partial** dependence if  $(A,B) \rightarrow (C,D)$  and  $B \rightarrow C$  [C is only partially dependent on the PK, ie. we only need B to determine C]. In other words, a part of an existing PK is acting like a PK on its own.

If X is a primary key, we have a **transitive** dependency if  $X \rightarrow Y$  and  $Y \rightarrow Z$  [Z is transitively dependent on X, not directly so]. In other words, a non-PK (regular attr) is acting like a PK.

##### ONF->1NF: eliminate repeating groups

##### Conversion to First Normal Form

- **Repeating group:** Group of multiple entries of same type can exist for any single key attribute occurrence
  - Existence proves the presence of data redundancies
- Enable reducing data redundancies
- Steps
  - Eliminate the repeating groups
  - Identify the primary key
  - Identify all dependencies

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

In other words, "fill in the blanks" so that there are no nulls. Now we have an actual relation (table) [with a value in each cell - no more blanks].

Further, identify the PK! In our example, it is (PROJ\_NUM,EMP\_NUM).

##### ONF->INF [cont'd]

##### Conversion to First Normal Form

- **Dependency diagram:** Depicts all dependencies found within given table structure
  - Helps to get an overview of all relationships among table's attributes
  - Makes it less likely that an important dependency will be overlooked

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

**Create a **dependency diagram**, showing relationships (dependencies) between the attributes - this will help us systematically normalize the table.**

##### Dependency diagram

Indicate full dependencies on the top, and partial and transitive dependencies on the bottom. "Top good, bottom bad". Also, color the PK components in a different color (and underline them). Result:

![](3d590ad29ecfe728f07432e6fcb59064_img.jpg)

**PROJ\_NAME** has only a partial dependency on the PK (since it is only dependent on PROJ\_NUM, which is just a part of the PK).

**CHG\_HOUR** is dependent on **JOB\_CLASS**, which is a non-prime attribute that is itself dependent on **EMP\_NUM**. So **JOB\_CLASS**  $\rightarrow$  **CHG\_HOUR** is a signaling dependency, indicating a **EMP\_NUM**  $\rightarrow$  **CHG\_HOUR** transitive dependency.

##### ONF->1NF [cont'd]

##### Conversion to First Normal Form

- 1NF describes tabular format in which:
  - All key attributes are defined
  - There are no repeating groups in the table
  - All attributes are dependent on the primary key
- All relational tables satisfy 1NF requirements
- Some tables contain partial dependencies
  - Subject to data redundancies and various anomalies

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

###### 1NF → 2NF: remove partial dependencies

##### Conversion to Second Normal Form

- Steps
  - Make new tables to eliminate partial dependencies
  - Reassign corresponding dependent attributes
- Table is in 2NF when it:
  - Is in 1NF
  - Includes no partial dependencies

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

###### 1NF->2NF [cont'd]

We eliminate partial dependencies by creating separate tables of such dependencies, and removing the dependent attributes from the starter table.

![](f3c73e8e478b8b2d9f6a96a970040556_img.jpg)

###### 2NF->3NF: remove transitive dependencies

We promote the non-prime keys that masquerade as PKs, into actual PKs (give them their own tables).

Whether we eliminate partial dependencies (to create 2NF) or transitive ones (to create 3NF), we follow the same process: create a new relation for each 'problem' dependency!

##### Conversion to Third Normal Form

- Steps
  - Make new tables to eliminate transitive dependencies
    - **Determinant:** Any attribute whose value determines other values within a row
  - Reassign corresponding dependent attributes
- Table is in 3NF when it:
  - Is in 2NF
  - Contains no transitive dependencies

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

###### 2NF->3NF [cont'd]

Figure 6.5 - Third Normal Form (3NF)  
Conversion Results

![](b15cf8c50195a52cca59b4645c6f59fa_img.jpg)

#### 'Good' tables

We can create a better DB by doing the following augmentations, to the 3NF model we just created:

- evaluate PKs - create a **JOB\_CODE**
- evaluate naming conventions - eg. **JOB\_CHG\_HOUR**
- refine attr atomicity, eg. **EMP\_NAME**
- identify new attrs, eg. **EMP\_HIREDATE**
- identify new relationships, **PROJECT** can have **EMP\_NUM** as FK [to be able to record a project's (always sole) manager]
- refine PKs for data granularity, eg. **ASSIGN\_NUM**
- maintain historical accuracy [duplicate data], eg. store **JOB\_CHG\_HOUR** in **ASSIGNMENT**
- evaluate derived attrs, eg. **ASSIGN\_CHARGE**

#### Requirements for Good Normalized Set of Tables

- Evaluate PK assignments and naming conventions
- Refine attribute atomicity
  - **Atomic attribute**: Cannot be further subdivided
  - **Atomicity**: Characteristic of an atomic attribute
- Identify new attributes and new relationships
- Refine primary keys as required for data granularity
  - **Granularity**: Level of detail represented by the values stored in a table's row
- Maintain historical accuracy and evaluate using derived attributes

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

##### Final result

Here is the result of making the "extra" changes to our 3NF form:

Figure 6.6 - The Completed Database

![](15a7570852cac42d754e4a0e50b1dfbe_img.jpg)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

##### Final result [cont'd]

Figure 6.6 - The Completed Database

Table name: JOB Database name: Ch06\_ConstructCo

![](492e1e7e7e44b6d857688dfa5341dfae_img.jpg)

Table name: JOB

| JOB_CODE | JOB_DESCRIPTION       | JOB_CHG_HOUR |
| -------- | --------------------- | ------------ |
| 500      | Programmer            | 35.75        |
| 501      | Systems Analyst       | 96.75        |
| 502      | Database Designer     | 105.00       |
| 503      | Electrical Engineer   | 84.50        |
| 504      | Mechanical Engineer   | 67.90        |
| 505      | Civil Engineer        | 55.78        |
| 506      | Clerical Support      | 26.87        |
| 507      | DSS Analyst           | 45.95        |
| 508      | Applications Designer | 48.10        |
| 509      | Bio Technician        | 34.55        |
| 510      | General Support       | 18.35        |

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

##### Final result [cont'd]

Figure 6.6 - The Completed Database

Table name: ASSIGNMENT

Table name: ASSIGNMENT

| ASSIGN_NUM | ASSIGN_DATE | PROJ_NUM | EMP_NUM | ASSIGN_HOURS | ASSIGN_CHG_HOUR | ASSIGN_CHARGE |
| ---------- | ----------- | -------- | ------- | ------------ | --------------- | ------------- |
| 1001       | 04-Mar-14   | 15       | 103     | 2.6          | 84.50           | 219.70        |
| 1002       | 04-Mar-14   | 18       | 118     | 1.4          | 18.36           | 25.70         |
| 1003       | 05-Mar-14   | 15       | 101     | 2.6          | 105.00          | 278.00        |
| 1004       | 05-Mar-14   | 22       | 113     | 2.5          | 48.10           | 120.25        |
| 1005       | 05-Mar-14   | 15       | 103     | 1.9          | 84.50           | 160.55        |
| 1006       | 05-Mar-14   | 25       | 115     | 4.2          | 96.75           | 406.35        |
| 1007       | 05-Mar-14   | 22       | 102     | 2.2          | 105.00          | 246.00        |
| 1008       | 05-Mar-14   | 25       | 101     | 1.2          | 105.00          | 178.50        |
| 1009       | 05-Mar-14   | 15       | 105     | 2.0          | 105.00          | 210.00        |
| 1010       | 05-Mar-14   | 15       | 102     | 3.8          | 96.75           | 367.65        |
| 1011       | 06-Mar-14   | 22       | 104     | 2.6          | 96.75           | 251.55        |
| 1012       | 06-Mar-14   | 15       | 101     | 2.3          | 105.00          | 241.50        |
| 1013       | 06-Mar-14   | 25       | 114     | 1.8          | 48.10           | 86.58         |
| 1014       | 06-Mar-14   | 22       | 111     | 4.0          | 26.87           | 107.48        |
| 1015       | 06-Mar-14   | 25       | 114     | 3.4          | 48.10           | 163.54        |
| 1016       | 06-Mar-14   | 18       | 112     | 1.2          | 45.95           | 55.14         |
| 1017       | 06-Mar-14   | 18       | 118     | 2.0          | 18.36           | 36.72         |
| 1018       | 06-Mar-14   | 18       | 104     | 2.6          | 96.75           | 251.55        |
| 1019       | 06-Mar-14   | 15       | 103     | 3.0          | 84.50           | 253.50        |
| 1020       | 07-Mar-14   | 22       | 105     | 2.7          | 105.00          | 283.50        |
| 1021       | 08-Mar-14   | 25       | 108     | 4.2          | 96.75           | 406.35        |
| 1022       | 07-Mar-14   | 25       | 114     | 5.8          | 48.10           | 279.98        |
| 1023       | 07-Mar-14   | 22       | 108     | 2.4          | 35.75           | 85.80         |

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

##### Final result [cont'd]

Figure 6.6 - The Completed Database

Table name: EMPLOYEE Database name: Ch06\_ConstructCo

| EMP_NUM | EMP_LNAME  | EMP_FNAME | EMP_INITIAL | EMP_HIREDATE | JOB_CODE |
| ------- | ---------- | --------- | ----------- | ------------ | -------- |
| 101     | Neves      | John      | C           | 08-Nov-00    | 502      |
| 102     | Senior     | David     | H           | 12-Jul-99    | 501      |
| 103     | Arbough    | June      | E           | 01-Dec-97    | 503      |
| 104     | Ramoras    | Anne      | K           | 15-Nov-98    | 501      |
| 105     | Johanson   | Alice     | K           | 01-Feb-94    | 502      |
| 106     | Smithfield | William   |             | 22-Jun-05    | 500      |
| 107     | Alonzo     | Maria     | D           | 10-Oct-94    | 500      |
| 108     | Washington | Ralph     | B           | 22-Aug-99    | 501      |
| 109     | Smith      | Larry     | W           | 18-Jul-99    | 501      |
| 110     | Clawko     | Gerald    | A           | 11-Dec-96    | 505      |
| 111     | Wabash     | Geoff     | B           | 04-Apr-99    | 506      |
| 112     | Smithson   | Darlene   | M           | 23-Oct-95    | 507      |
| 113     | Joanbrood  | Delbert   | K           | 15-Nov-94    | 508      |
| 114     | Jones      | Annelise  |             | 23-Aug-91    | 508      |
| 115     | Bawangi    | Travis    | B           | 25-Jan-90    | 501      |
| 116     | Pratt      | Gerald    | L           | 05-Mar-95    | 510      |
| 117     | Williamson | Angie     | H           | 19-Jun-94    | 509      |
| 118     | Frommer    | James     | J           | 04-Jan-06    | 510      |

Cengage Learning © 2015

### Normalization: summary

- \* 1NF: eliminate repeating groups (partial:y, transitive:y)
- \* 2NF: eliminate redundant data (partial:n, transitive:y)
- \* 3NF: eliminate fields not dependent on key fields (partial:n, transitive:n)

---

**Here is more, on normalization.**

---

### Denormalization

### Denormalization

- Design goals
  - Creation of normalized relations
  - Processing requirements and speed
- Number of database tables expands when tables are decomposed to conform to normalization requirements
- Joining a larger number of tables:
  - Takes additional input/output (I/O) operations and processing logic
  - Reduces system speed

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

### Denormalization [cont'd]

#### Denormalization

- Defects in unnormalized tables
  - Data updates are less efficient because tables are larger
  - Indexing is more cumbersome
  - No simple strategies for creating virtual tables known as views

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

1/40 9:35:08 \*\*\*

![](1a9bc67d8c1b132176d58cd7754982b1_img.jpg)![](6e10326caf39add89e2f9358de953e4f_img.jpg)

## SQL

### Where did SQL come from?

As mentioned earlier, SQL is an implementation of Ed Codd's relational set operators:

1. SELECT [formerly known as RESTRICT]
2. PROJECT
3. JOIN
4. PRODUCT
5. UNION
6. INTERSECT
7. DIFFERENCE
8. DIVIDE

Interestingly, Ed's ideas were ignored by IBM, his employer. Only after Oracle debuted (with SQL support right off the bat!) did IBM create DB2, its first relational DB.

Here is a cool genealogy!

### SQL - cmds to define data, manipulate data

### Structured Query Language (SQL)

- Categories of SQL function
  - Data definition language (DDL)
  - Data manipulation language (DML)
- Nonprocedural language with basic command vocabulary set of less than 100 words
- Differences in SQL dialects are minor

now next page (right Arrow)

#### Table 7.1 - SQL Data Definition Command

| COMMAND OR OPTION           | DESCRIPTION                                                  |
| --------------------------- | ------------------------------------------------------------ |
| CREATE SCHEMA AUTHORIZATION | Creates a database schema                                    |
| CREATE TABLE                | Creates a new table in the user's database schema            |
| NOT NULL                    | Ensures that a column will not have null values              |
| UNIQUE                      | Ensures that a column will not have duplicate values         |
| PRIMARY KEY                 | Defines a primary key for a table                            |
| FOREIGN KEY                 | Defines a foreign key for a table                            |
| DEFAULT                     | Defines a default value for a column (when no value is given) |
| CHECK                       | Validates data in an attribute                               |
| CREATE INDEX                | Creates an index for a table                                 |
| CREATE VIEW                 | Creates a dynamic subset of rows and columns from one or more tables (see Chapter 8, Advanced SQL) |
| ALTER TABLE                 | Modifies a table's definition (adds, modifies, or deletes attributes or constraints) |
| CREATE TABLE AS             | Creates a new table based on a query in the user's database schema |
| DROP TABLE                  | Permanently deletes a table (and its data)                   |
| DROP INDEX                  | Permanently deletes an index                                 |
| DROP VIEW                   | Permanently deletes a view                                   |

Cengage Learning © 2015

[row next page \(Right Arrow\)](#)

#### Table 7.2 - SQL Data Manipulation Commands

| COMMAND OR OPTION           | DESCRIPTION                                                  |
| --------------------------- | ------------------------------------------------------------ |
| INSERT                      | Inserts row(s) into a table                                  |
| SELECT                      | Selects attributes from rows in one or more tables or views  |
| WHERE                       | Restricts the selection of rows based on a conditional expression |
| GROUP BY                    | Groups the selected rows based on one or more attributes     |
| HAVING                      | Restricts the selection of grouped rows based on a condition |
| ORDER BY                    | Orders the selected rows based on one or more attributes     |
| UPDATE                      | Modifies an attribute's values in one or more table's rows   |
| DELETE                      | Deletes one or more rows from a table                        |
| COMMIT                      | Permanently saves data changes                               |
| ROLLBACK                    | Restores data to their original values                       |
| <b>Comparison operators</b> |                                                              |
| =, <, >, <=, >=, <>         | Used in conditional expressions                              |
| <b>Logical operators</b>    |                                                              |
| AND/OR/NOT                  | Used in conditional expressions                              |
| <b>Special operators</b>    | Used in conditional expressions                              |
| BETWEEN                     | Checks whether an attribute value is within a range          |
| IS NULL                     | Checks whether an attribute value is null                    |
| LIKE                        | Checks whether an attribute value matches a given string pattern |
| IN                          | Checks whether an attribute value matches any value within a value list |
| EXISTS                      | Checks whether a subquery returns any rows                   |
| DISTINCT                    | Limits values to unique values                               |
| <b>Aggregate functions</b>  | Used with SELECT to return mathematical summaries on columns |
| COUNT                       | Returns the number of rows with non-null values for a given column |
| MIN                         | Returns the minimum attribute value found in a given column  |
| MAX                         | Returns the maximum attribute value found in a given column  |
| SUM                         | Returns the sum of all values for a given column             |
| AVG                         | Returns the average of all values for a given column         |

Cengage Learning © 2015

Here is a nice list of the most useful SQL cmds.

![](10f4e3a2f3c016555ee12a5b556ba834_img.jpg)

**NUMBER(p,s) [or NUMERIC(p,s)]** denotes a number (including negative values) with upto 'p' number of total digits, including 's' number of them after the decimal point. 'p' is referred to as precision, 's' denotes scale. Eg. NUMERIC(4,2) would range from -99.99 to 99.99, NUMERIC(3,0) would be -999 to 999.

**char vs VARCHAR (reserved for future use by SQL - so don't use!) vs VARCHAR2 [versus NVARCHAR2 (for Unicode)]:**

**[http://www.orafaq.com/faq/what\\_is\\_the\\_difference\\_between\\_varchar\\_varchar2\\_and\\_cha](http://www.orafaq.com/faq/what_is_the_difference_between_varchar_varchar2_and_char)**

#### Creating Table Structures

- Use one line per column (attribute) definition
- Use spaces to line up attribute characteristics and constraints
- Table and attribute names are capitalized
- Features of table creating command sequence
  - NOT NULL specification
  - UNIQUE specification
- Syntax to create table
  - CREATE TABLE tablename();

#### Primary Key and Foreign Key

- Primary key attributes contain both a NOT NULL and a UNIQUE specification
- RDBMS will automatically enforce referential integrity for foreign keys
- Command sequence ends with semicolon
- ANSI SQL allows use of following clauses to cover CASCADE, SET NULL, or SET DEFAULT
  - ON DELETE and ON UPDATE

##### Our example db

Figure 7.1 - The Database Model

![](15b94d74577004248532b2f4fd64f535_img.jpg)

#### Creating a table

```
CREATE TABLE PRODUCT (  
  P_CODE      VARCHAR(10)      NOT NULL      UNIQUE,  
  P_DESCRIPT  VARCHAR(35)      NOT NULL,  
  P_INDATE   DATE              NOT NULL,  
  P_QOH       SMALLINT         NOT NULL,  
  P_MIN       SMALLINT         NOT NULL,  
  P_PRICE     NUMBER(8,2)      NOT NULL,  
  P_DISCOUNT NUMBER(5,2)      NOT NULL,  
  V_CODE      INTEGER,  
  PRIMARY KEY (P_CODE),  
  FOREIGN KEY (V_CODE) REFERENCES VENDOR ON UPDATE  
  CASCADE);
```

#### SQL Constraints

##### NOT NULL

- Ensures that column does not accept nulls

##### UNIQUE

- Ensures that all values in column are unique

##### DEFAULT

- Assigns value to attribute when a new row is added to table

##### CHECK

- Validates data when attribute value is entered

**Plus: ON UPDATE CASCADE and ON DELETE CASCADE - both affect [change] a secondary table (that has an FK), when a change is made in the primary table (with the corresponding PK). ON UPDATE will update the values in the secondary table when corresp. values in the primary table are changed; ON DELETE will delete rows in the secondary table, when linked rows are deleted in the primary table.**

### Inserting data

#### Data Manipulation Commands

INSERT, SELECT, COMMIT, UPDATE, ROLLBACK, and DELETE.

#### INSERT: Command to insert data into table

- Syntax - INSERT INTO tablename VALUES();
- Used to add table rows with NULL and NOT NULL attributes

#### COMMIT: Command to save changes

- Syntax - COMMIT [WORK];
- Ensures database update integrity

```
INSERT INTO VENDOR VALUES (21225,'Bryson, Inc.,Smithson','615','223-3234','TN','Y');
```

```
INSERT INTO VENDOR VALUES (21226,'Superloo, Inc.,Flushing','904','215-8995','FL','N');
```

```
INSERT INTO PRODUCT VALUES ('11QER/31','Power painter, 15 psi., 3-nozzle','03-Nov-13',8,5,109.99,0.00,25595);
```

```
INSERT INTO PRODUCT VALUES ('13-Q2/P2','7.25-in. pwr. saw blade','13-Dec-13',32,15,14.99,0.05, 21344);
```

```
INSERT INTO PRODUCT VALUES ('BRT-345','Titanium drill bit','18-Oct-13', 75, 10, 4.50, 0.06, NULL);
```

```
INSERT INTO PRODUCT(P_CODE, P_DESCRIPT) VALUES ('BRT-345','Titanium drill bit');
```

Vaguely similar to parameter passing/matching during a function call [where arguments need to match in position, type, count].

### reading, writing (data)

#### Data Manipulation Commands

#### SELECT: Command to list the contents

- Syntax - SELECT *columnlist* FROM *tablename*;
- **Wildcard character(\*)**: Substitute for other characters/command

#### UPDATE: Command to modify data

- Syntax - UPDATE *tablename* SET *columnname* = *expression* [, *columnname* = *expression*] [WHERE *conditionlist*];

```
SELECT * FROM
PRODUCT;
```

```
SELECT    P_CODE, P_DESCRIPT, P_INDATE, P_QOH, P_MIN, P_PRICE, P_DISCOUNT,
          V_CODE
FROM      PRODUCT;
```

```
UPDATE    PRODUCT
SET        P_INDATE =
          '18-JAN-2014'
WHERE     P_CODE = '13-Q2/P2';
```

```
UPDATE    PRODUCT
SET        P_INDATE = '18-JAN-2014', P_PRICE = 17.99, P_MIN
          = 10
WHERE     P_CODE = '13-Q2/P2';
```

**SELECT** operates on 1 or more columns, and 0 or more rows from 1 or more tables - like many SQL commands, it is **set-oriented** and **non procedural**.

**UPDATE** modifies one or more columns of a table (on all rows, or on specific rows based on a condition specified by **WHERE**). Here is more.

#### Data Manipulation Commands

##### WHERE condition

- Specifies the rows to be selected

#### ROLLBACK: Command to restore the database

- Syntax - ROLLBACK;
- Undoes the changes since last COMMIT command

#### DELETE: Command to delete

- Syntax - DELETE FROM *tablename*
  - [WHERE *conditionlist*];

```
DELETE FROM    PRODUCT
WHERE          P_CODE = 'BRT-345';
```

**Another ex: DELETE FROM PRODUCT WHERE P\_MIN=5; (can be any condition on any attribute).**

**Q: what would DELETE do, if there isn't a WHERE condition?**

### 'Bulk' inserting of data

#### Inserting Table Rows with a SELECT Subquery

- Syntax
  - `INSERT INTO tablename SELECT columnlist FROM tablename`
- Used to add multiple rows using another table as source
- SELECT command - Acts as a subquery and is executed first
  - **Subquery:** Query embedded/nested inside another query

```
INSERT INTO      SELECT      FROM
tablename      columnlist  tablename;
```

### CONDITIONAL filtering - the heart of it all!

#### Selecting Rows Using Conditional Restrictions

- Following syntax enables to specify which rows to select
  - SELECT *columnlist*
  - FROM *tablelist*
  - [WHERE *conditionlist*];
- Used to select partial table contents by placing restrictions on the rows
- Optional WHERE clause
  - Adds conditional restrictions to the SELECT statement

```
SELECT    columnlist
FROM      tablelist
[WHERE    conditionlist
];
```

### Comparing values [like in standard programming]

#### Comparison Operators

- Add conditional restrictions on selected table contents
- Used on:
  - Character attributes
  - Dates

Table 7.6 - Comparison Operators

| SYMBOL   | MEANING                  |
| -------- | ------------------------ |
| =        | Equal to                 |
| <        | Less than                |
| <=       | Less than or equal to    |
| >        | Greater than             |
| >=       | Greater than or equal to |
| <> or != | Not equal to             |

Cengage Learning © 2015

#### Computed columns (an ex of 'feature engineering')

#### Comparison Operators: Computed Columns and Column Aliases

- SQL accepts any valid expressions/formulas in the computed columns
- **Alias:** Alternate name given to a column or table in any SQL statement to improve the readability
- Computed column, an alias, and date arithmetic can be used in a single query

```
SELECT      P_DESCRIPT, P_QOH, P_PRICE, P_QOH *
            P_PRICE
FROM        PRODUCT
```

| P_DESCRIPT                          | P_QOH | P_PRICE | Expr1   |
| ----------------------------------- | ----- | ------- | ------- |
| Power painter, 15 psi., 3-nozzle    | 8     | 109.99  | 879.92  |
| 7.25-in. pwr. saw blade             | 32    | 14.99   | 479.68  |
| 9.00-in. pwr. saw blade             | 18    | 17.49   | 314.82  |
| Hrd. cloth, 1/4-in., 2x50           | 15    | 39.95   | 599.25  |
| Hrd. cloth, 1/2-in., 3x50           | 23    | 43.99   | 1011.77 |
| B&D jigsaw, 12-in. blade            | 8     | 109.92  | 879.36  |
| B&D jigsaw, 8-in. blade             | 6     | 99.87   | 599.22  |
| B&D cordless drill, 1/2-in.         | 12    | 38.95   | 467.40  |
| Claw hammer                         | 23    | 9.95    | 228.85  |
| Sledge hammer, 12 lb.               | 8     | 14.40   | 115.20  |
| Rat-tail file, 1/8-in. fine         | 43    | 4.99    | 214.57  |
| Hicut chain saw, 16 in.             | 11    | 256.99  | 2826.89 |
| PVC pipe, 3.5-in., 8-ft             | 188   | 5.87    | 1103.56 |
| 1.25-in. metal screw, 25            | 172   | 6.99    | 1202.28 |
| 2.5-in. wd. screw, 50               | 237   | 8.45    | 2002.65 |
| Steel matting, 4'x8'x1/8", .5" mesh | 18    | 119.95  | 2159.10 |

```
SELECT      P_DESCRIPT, P_QOH, P_PRICE, P_QOH * P_PRICE AS TOTVALUE
FROM        PRODUCT;
```

| P_DESCRIPT                          | P_QOH | P_PRICE | TOTVALUE |
| ----------------------------------- | ----- | ------- | -------- |
| Power painter, 15 psi., 3-nozzle    | 8     | 109.99  | 879.92   |
| 7.25-in. pwvr. saw blade            | 32    | 14.99   | 479.68   |
| 9.00-in. pwvr. saw blade            | 18    | 17.49   | 314.82   |
| Hrd. cloth, 1/4-in., 2x50           | 15    | 39.95   | 599.25   |
| Hrd. cloth, 1/2-in., 3x50           | 23    | 43.99   | 1011.77  |
| B&D jigsaw, 12-in. blade            | 8     | 109.92  | 879.36   |
| B&D jigsaw, 8-in. blade             | 6     | 99.87   | 599.22   |
| B&D cordless drill, 1/2-in.         | 12    | 38.95   | 467.40   |
| Claw hammer                         | 23    | 9.95    | 228.85   |
| Sledge hammer, 12 lb.               | 8     | 14.40   | 115.20   |
| Rat-tail file, 1/8-in. fine         | 43    | 4.99    | 214.57   |
| Hicut chain saw, 16 in.             | 11    | 256.99  | 2826.89  |
| PVC pipe, 3.5-in., 8-ft             | 188   | 5.87    | 1103.56  |
| 1.25-in. metal screw, 25            | 172   | 6.99    | 1202.28  |
| 2.5-in. wd. screw, 50               | 237   | 8.45    | 2002.65  |
| Steel matting, 4'x8'x1/8", .5" mesh | 18    | 119.95  | 2159.10  |

```
SELECT      P_CODE, P_INDATE, P_INDATE + 90 AS EXPDATE
FROM        PRODUCT;
```

#### Arithmetic operators

#### Arithmetic operators

- **The Rule of Precedence:** Establish the order in which computations are completed
- Perform:
  - Operations within parentheses
  - Power operations
  - Multiplications and divisions
  - Additions and subtractions

Table 7.7 - The Arithmetic Operators

| ARITHMETIC OPERATOR | DESCRIPTION                                                  |
| ------------------- | ------------------------------------------------------------ |
| +                   | Add                                                          |
| -                   | Subtract                                                     |
| *                   | Multiply                                                     |
| /                   | Divide                                                       |
| ^                   | Raise to the power of (some applications use ** instead of ^) |

Cengage Learning © 2015

#### Logical (Boolean) operators

Figure 7.12 - Selected PRODUCT Table Attributes: The logical OR

| P_DESCRIPT                  | P_INDATE  | P_PRICE | V_CODE |
| --------------------------- | --------- | ------- | ------ |
| 7.25-in. pwr. saw blade     | 13-Dec-13 | 14.99   | 21344  |
| 9.00-in. pwr. saw blade     | 13-Nov-13 | 17.49   | 21344  |
| B&D jigsaw, 12-in. blade    | 30-Dec-13 | 109.92  | 24288  |
| B&D jigsaw, 8-in. blade     | 24-Dec-13 | 99.87   | 24288  |
| Rat-tail file, 1/8-in. fine | 15-Dec-13 | 4.99    | 21344  |
| Hicut chain saw, 16 in.     | 07-Feb-14 | 256.99  | 24288  |

Cengage Learning © 2015

```
SELECT P_DESCRIPT, P_INDATE, P_PRICE, V_CODE
FROM   PRODUCT
WHERE  V_CODE = 21344 OR V_CODE = 24288;
```

###### Figure 7.13 - Selected PRODUCT Table Attributes: The Logical AND

| P_DESCRIPTOR                | P_INDATE  | P_PRICE | V_CODE |
| --------------------------- | --------- | ------- | ------ |
| B&D cordless drill, 1/2-in. | 20-Jan-14 | 38.95   | 25595  |
| Claw hammer                 | 20-Jan-14 | 9.95    | 21225  |
| PVC pipe, 3.5-in., 8-ft     | 20-Feb-14 | 5.87    |        |
| 1.25-in. metal screw, 25    | 01-Mar-14 | 6.99    | 21225  |
| 2.5-in. w/d. screw, 50      | 24-Feb-14 | 8.45    | 21231  |

Cengage Learning © 2015

```

SELECT    P_DESCRIPTOR, P_INDATE, P_PRICE, V_CODE
FROM      PRODUCT
WHERE     P_PRICE < 50
AND       P_INDATE > '15-Jan-2014';

```

###### Figure 7.14 - Selected PRODUCT Table Attributes: The Logical AND and OR

| P_DESCRIPTOR                | P_INDATE  | P_PRICE | V_CODE |
| --------------------------- | --------- | ------- | ------ |
| B&D jigsaw, 12-in. blade    | 30-Dec-13 | 109.92  | 24288  |
| B&D jigsaw, 8-in. blade     | 24-Dec-13 | 99.87   | 24288  |
| B&D cordless drill, 1/2-in. | 20-Jan-14 | 38.95   | 25595  |
| Claw hammer                 | 20-Jan-14 | 9.95    | 21225  |
| Hicut chain saw, 16 in.     | 07-Feb-14 | 256.99  | 24288  |
| PVC pipe, 3.5-in., 8-ft     | 20-Feb-14 | 5.87    |        |
| 1.25-in. metal screw, 25    | 01-Mar-14 | 6.99    | 21225  |
| 2.5-in. w/d. screw, 50      | 24-Feb-14 | 8.45    | 21231  |

Cengage Learning © 2015

```
SELECT    P_DESCRIPT, P_INDATE, P_PRICE, V_CODE  
FROM      PRODUCT  
WHERE     (P_PRICE < 50 AND P_INDATE > '15-Jan-2014')  
OR        V_CODE = 24288;
```

### 'Special' operators

#### Special Operators

##### BETWEEN

- Checks whether attribute value is within a range

##### IS NULL

- Checks whether attribute value is null

##### LIKE

- Checks whether attribute value matches given string pattern

##### IN

- Checks whether attribute value matches any value within a value list

##### EXISTS

- Checks if subquery returns any rows

##### BETWEEN

```
SELECT      *
FROM        PRODUCT
WHERE       P_PRICE BETWEEN 50.00 AND 100.00;
```

```
SELECT      P_CODE, P_DESCRIPT, V_CODE
FROM        PRODUCT
WHERE       V_CODE IS NULL;
```

- % means any and all *following* or *preceding* characters are eligible. For example:

'J%' includes Johnson, Jones, Jernigan, July, and J-231Q.

'Jo%' includes Johnson and Jones.

'%n' includes Johnson and Jernigan.

- \_ means any *one* character may be substituted for the underscore. For example:

'\_23-456-6789' includes 123-456-6789, 223-456-6789, and 323-456-6789.

'\_23-\_56-678\_' includes 123-156-6781, 123-256-6782, and 823-956-6788.

'\_o\_es' includes Jones, Cones, Cokes, totes, and roles.

```
SELECT      V_NAME, V_CONTACT, V_AREACODE, V_PHONE
FROM        VENDOR
WHERE       V_CONTACT LIKE 'Smith%';
```

Another example for pattern-matching: load this page, and enter and execute:

```
SELECT * FROM Customers WHERE CustomerName LIKE 'C%';
```

```
SELECT      *  
FROM        PRODUCT  
WHERE       V_CODE = 21344  
OR          V_CODE = 24288;
```

```
SELECT      *  
FROM        PRODUCT  
WHERE       V_CODE IN (21344, 24288);
```

```
SELECT      V_CODE, V_NAME  
FROM        VENDOR  
WHERE       V_CODE IN (SELECT V_CODE FROM PRODUCT);
```

##### 'EXISTS'

The EXISTS clause is used with a query, and returns TRUE if the subquery results in any output (non-zero # of rows being returned), or FALSE if the subquery results in no data. The rest of the query (the 'main' query) will (or will not) run, based on EXISTS's output - if EXISTS returns false, the main query will get skipped.

You can loosely think of EXISTS as "ONLY WHEN". We use it to 'defensively' update (insert, modify, delete) parts of a table (after we determine it is updatable).

You can also think of 'WHERE EXISTS' as "such that there exists". Eg. in the first example below (SELECT \* FROM VENDOR..), it reads as "Find all vendors such that there exists records for them in the PRODUCT TABLE (via V\_CODE) where P\_QOH<=P\_MIN" [in other words, we are looking for vendors we need to re-order from].

In the second example (INSERT INTO CONTACTS..), read it as "get the supplier ID and name for all suppliers such that there exists order IDs for them, then insert them into the contacts table".

Exercise: what does #3 below (the UPDATE query) do?

```
SELECT      *
FROM        VENDOR
WHERE       EXISTS (SELECT * FROM PRODUCT WHERE P_QOH <= P_MIN);
```

```
INSERT INTO contacts
(contact_id, contact_name)
SELECT supplier_id, supplier_name
FROM suppliers
WHERE EXISTS (SELECT *
              FROM orders
              WHERE suppliers.supplier_id = orders.supplier_id);
```

```
UPDATE suppliers
SET supplier_name = (SELECT customers.name
                   FROM customers
                   WHERE customers.customer_id = suppliers.supplier_id)
WHERE EXISTS (SELECT customers.name
              FROM customers
              WHERE customers.customer_id = suppliers.supplier_id);
```

```
DELETE FROM suppliers
WHERE EXISTS (SELECT *
              FROM orders
              WHERE suppliers.supplier_id = orders.supplier_id);
```

##### A couple more (ex of EXISTS, NOT EXISTS):

```
SELECT *
FROM suppliers
WHERE EXISTS (SELECT *
              FROM orders
              WHERE suppliers.supplier_id = orders.supplier_id);
```

This SQL EXISTS condition example will return all records from the suppliers table where there is at least one record in the orders table with the same supplier\_id.

```
SELECT *
FROM suppliers
WHERE NOT EXISTS (SELECT *
                  FROM orders
                  WHERE suppliers.supplier_id = orders.supplier_id);
```

This SQL EXISTS example will return all records from the suppliers table where there are **no** records in the orders table for the given supplier\_id.

### Ways to 'do' SQL..

SQL is a data creation+manipulation language, so it's best learned HANDS ON (not just by looking at slides and reading about the syntax) - you need access to a relational database where you can **create tables, enter data in them and do queries on the data** (tables  $\leftarrow$  data  $\leftarrow$  queries).

There are three ways to get your hands on a DB: use a browser page [a server runs the DB software, you simply access it from a page]; install a DB locally on your laptop/tablet/phone; use a 'cloud-based' DB [this is similar to, but more powerful than, accessing a DB via a web page].

#### I. Browser-based SQL IDEs

An easy way to practice running SQL queries is to use browser-based interfaces (nothing to download, no login needed) to create/query databases. Here are some sites that provide this form of access:

- \* SQL Tutorial: <http://www.w3schools.com/sql/default.asp>
- \* ideone: <http://www.ideone.com>
- \* sqlfiddle: <http://sqlfiddle.com/>
- \* Code School's Try SQL: <http://campus.codeschool.com/courses/try-sql/contents>
- \* SQLZOO: <http://sqlzoo.net/> - has extensive tutorials
- \* another tutorial: <http://www.sqltutorial.org/>
- \* w3resource: <http://www.w3resource.com/sql-exercises/> - more tutorials
- \* Khan Academy: <https://www.khanacademy.org/computer-programming/new/sql>
- \* 'Online SQL interpreter': <https://sql.js.org/examples/GUI/> - JavaScript-based! [here is the source: <https://cdnjs.com/libraries/sql.js> ; more info: <https://sql.js.org/#/>]
- \* small, simple, fun examples: <https://sql-playground.wizardzines.com/> [to go with [this delightful booklet](#)]

Below are examples for three of the above links.

Bring up the w3schools Tryit Editor, enter and run the following pair of sql command sets one at a time (these commands run on a set of pre-installed (by w3schools.com) collection of tables called the Northwind database):

```
SELECT City FROM Customers  
WHERE Country="Germany";
```

```
SELECT City, CustomerID FROM Customers  
WHERE Country="Germany" AND CustomerID>60;
```

In ideone , select SQLite (for the choice of language), then enter and run this:

```
-- warmup
create table tble(str varchar(20));
insert into tble values ('Hello world!'),('SQL is fun!!');
select * from tble;
```

```
-- recipes
CREATE TABLE recipes (
  recipe_id INT NOT NULL,
  recipe_name VARCHAR(30) NOT NULL,
  PRIMARY KEY (recipe_id),
  UNIQUE (recipe_name)
);
```

```
INSERT INTO recipes
(recipe_id, recipe_name)
VALUES
(1, "Tacos"),
(2, "Tomato Soup"),
(3, "Grilled Cheese");
```

```
-- quick check
SELECT recipe_name
FROM recipes;
```

```
-- ingredients
CREATE TABLE ingredients (
  ingredient_id INT NOT NULL,
  ingredient_name VARCHAR(30) NOT NULL,
  ingredient_price INT NOT NULL,
  PRIMARY KEY (ingredient_id),
  UNIQUE (ingredient_name)
);
```

```
INSERT INTO ingredients
(ingredient_id, ingredient_name, ingredient_price)
VALUES
(1, "Beef", 5),
```

```
(2, "Lettuce", 1),
(3, "Tomatoes", 2),
(4, "Taco Shell", 2),
(5, "Cheese", 3),
(6, "Milk", 1),
(7, "Bread", 2);

-- recipe_ingredients
CREATE TABLE recipe_ingredients (
recipe_id int NOT NULL,
ingredient_id INT NOT NULL,
amount INT NOT NULL,
PRIMARY KEY (recipe_id,ingredient_id)
);

INSERT INTO recipe_ingredients
(recipe_id, ingredient_id, amount)
VALUES
(1,1,1),
(1,2,2),
(1,3,2),
(1,4,3),
(1,5,1),
(2,3,2),
(2,6,1),
(3,5,1),
(3,7,2);

SELECT *
FROM recipes
ORDER BY recipe_id;
```

Here is the recipes db table and its queries again, this time in sqlfiddle. After the page loads (with our SQL commands above, filled in!), click 'Build Schema' on the left, then click 'Run SQL' on the right [and wait for a few seconds for the output].

#### 2. Locally installed DBs

You can install Oracle on your machine, or install the light-weight but powerful DB Browser for SQLite, aka SQLite Browser. On Windows, this offers a 'notebook' environment: <https://sqlnotebook.com/> [a mix of SQL and non-SQL commands]. It is also OK to use Postgres, or MySQL; or you could use some other DB...

Here is a quickstart guide for SQLite Browser - we create a table called CosineTable, and fill it with rows containing [angle, cos(angle)] pairs. And here is another clip that shows how to create a simple sqlite DB and query it.

The second clip above, also shows that the .db file that is created, contains data in a SQLite-native binary format [which is public and well-documented]. FYI, there are sqlite API calls in multiple languages that let you access the (binary) data using functions/methods that accept SQL commands as regular strings. This is mixed-language programming that lets us accomplish a lot, because we leverage the power of Java, Python etc., as well as that of SQL. Eg. here's how it works in Python:

```
>>> for row in c.execute('SELECT * FROM stocks ORDER BY price'):
    print row # or we could email this, put it up on an LED
display, buy/sell the cheap/pricy stocks..
```

```
(u'2006-01-05', u'BUY', u'RHAT', 100, 35.14)
(u'2006-03-28', u'BUY', u'IBM', 1000, 45.0)
(u'2006-04-06', u'SELL', u'IBM', 500, 53.0)
(u'2006-04-05', u'BUY', u'MSFT', 1000, 72.0)
```

You could also write a binary reader+parser in C++, Java etc. and extract the sqlite-native data that way - in other words, you'd never lose your data if you store it in a sqlite .db file!

As you can see, sqlite is very popular :) Fun: download this 'universal binary', and open it with this sqlite db file...

#### 3. Cloud-based DBs

You can also work with a relational DB via the cloud, eg. using Amazon's RDS offering. RDS offers a way to create databases such as Amazon's own Aurora, Oracle, SQL Server, MariaDB, MySQL, Postgres. Likewise, Google has <https://cloud.google.com/sql>, Microsoft has <https://azure.microsoft.com/en-us/products/azure-sql/database>. Not to be outdone, Oracle has <https://cloud.oracle.com/database>.

The QUICKEST/EASIEST cloud solution is <https://neon.tech> - give it a try!

#### ALTER

### Advanced Data Definition Commands

- **ALTER TABLE** command: To make changes in the table structure
- Keywords use with the command
  - ADD - Adds a column
  - MODIFY - Changes column characteristics
  - DROP - Deletes a column
- Used to:
  - Add table constraints
  - Remove table constraints

#### Changing Column's Data Type

- ALTER can be used to change data type
- Some RDBMSs do not permit changes to data types unless column is empty
- Syntax –
  - ALTER TABLE *tablename* MODIFY (*columnname(datatype)*);

```
ALTER TABLE PRODUCT  MODIFY (V_CODE CHAR(5));
```

#### Changing Column's Data Characteristics

- Use ALTER to change data characteristics
- Changes in column's characteristics are permitted if changes do not alter the existing data type
- Syntax
  - ALTER TABLE *tablename* MODIFY (*columnname(characteristic)*);

```
ALTER TABLE PRODUCT  MODIFY (P_PRICE DECIMAL(9,2));
```

#### Adding Column, Dropping Column

- Adding a column
  - Use ALTER and ADD
  - Do not include the NOT NULL clause for new column
- Dropping a column
  - Use ALTER and DROP
  - Some RDBMSs impose restrictions on the deletion of an attribute

```
ALTER TABLE PRODUCT  ADD (P_SALECODE CHAR(1));
```

```
ALTER TABLE VENDOR  DROP COLUMN V_ORDER;
```

#### The UPDATE command

#### Advanced Data Updates

- UPDATE command updates only data in existing rows
- If a relationship is established between entries and existing columns, the relationship can assign values to appropriate slots
- Arithmetic operators are useful in data updates
- In Oracle, ROLLBACK command undoes changes made by last two UPDATE statements

```
UPDATE    PRODUCT
SET        P_SALECODE = '2'
WHERE      P_CODE = '1546-QQ2';
```

```
UPDATE    PRODUCT
SET        P_SALECODE = '1'
WHERE      P_CODE IN ('2232/QWE', '2232/QTY');
```

```
UPDATE    PRODUCT
SET        P_SALECODE = '1'
WHERE      P_INDATE >= '16-Jan-2014' AND P_INDATE <='10-Feb-2014';
```

```
UPDATE    PRODUCT
SET        P_PRICE = P_PRICE * 1.10
WHERE      P_PRICE < 50.00;
```

#### Table update in 'bulk'

Sometimes we can update a table, by filling it with output from a query. The table to be filled in has to exist first (so we need to create it if necessary), and have type-compatible columns that can receive values from our data-fetching query.

The table creation and updating can happen in separate steps, or even be combined for compactness of expression.

#### Copying Parts of Tables

- SQL permits copying contents of selected table columns
  - Data need not be reentered manually into newly created table(s)
- Table structure is created
- Rows are added to new table using rows from another table

```

CREATE TABLE PART(
PART_CODE           CHAR(8),
PART_DESCRIPT       CHAR(35),
PART_PRICE          DECIMAL(8,2),
V_CODE              INTEGER,
PRIMARY KEY (PART_CODE));

INSERT INTO PART      (PART_CODE, PART_DESCRIPT, PART_PRICE, V_CODE)
SELECT                P_CODE, P_DESCRIPT, P_PRICE, V_CODE FROM PRODUCT;

```

---

```

CREATE TABLE PART AS
SELECT    P_CODE AS PART_CODE, P_DESCRIPT AS
          PART_DESCRIPT, P_PRICE AS PART_PRICE,
          V_CODE
FROM      PRODUCT;

```

#### Adding Primary and Foreign Key Designations

- **ALTER TABLE** command
  - Followed by a keyword that produces the specific change one wants to make
  - Options include ADD, MODIFY, and DROP
- Syntax to add or modify columns
  - ALTER TABLE *tablename*
    - {ADD | MODIFY} ( *columnname datatype* [ {ADD | MODIFY} *columnname datatype* ] );
  - ALTER TABLE *tablename*
    - ADD *constraint* [ ADD *constraint* ] ;

```
ALTER TABLE PART  
ADD PRIMARY KEY (PART_CODE);
```

```
ALTER TABLE PART  
ADD FOREIGN KEY (V_CODE) REFERENCES VENDOR;
```

**Oftentimes the need to do this occurs when a table (eg. PART) is created via bulk-update, from another table (eg. PRODUCT).**

#### "Just drop it, okay??!!"

### Deleting a Table from the Database

- **DROP TABLE:** Deletes table from database
- Syntax - DROP TABLE tablename;
- Can drop a table only if it is not the one side of any relationship
- RDBMS generates a foreign key integrity violation error message if the table is dropped

### Ordering, unique entries, aggregate ops..

#### Additional SELECT Query Keywords

- Logical operators work well in the query environment
- SQL provides useful functions that:
  - Counts
  - Find minimum and maximum values
  - Calculate averages
- SQL allows user to limit queries to entries:
  - Having no duplicates
  - Whose duplicates may be grouped

#### ORDER BY

#### Ordering a Listing

- **ORDER BY** clause is useful when listing order is important
- Syntax - SELECT *columnlist*  
FROM *tablelist*  
[WHERE *conditionlist*]  
[ORDER BY *columnlist* [ASC | DESC]];
- **Cascading order sequence:** Multilevel ordered sequence
  - Created by listing several attributes after the ORDER BY clause

Below is an example of ORDER BY, where by default, values are listed (sorted) in ascending order. To list the values in descending order, we'd do this: ORDER BY P\_PRICE DESC;

```
SELECT      P_CODE, P_DESCRIPT, P_INDATE, P_PRICE
FROM        PRODUCT
ORDER BY    P_PRICE;
```

| P_CODE   | P_DESCRIPT                          | P_INDATE  | P_PRICE |
| -------- | ----------------------------------- | --------- | ------- |
| 54778-2T | Rat-tail file, 1/8-in. fine         | 15-Dec-13 | 4.99    |
| PVC23DRT | PVC pipe, 3.5-in., 8-ft             | 20-Feb-14 | 5.87    |
| SM-18277 | 1.25-in. metal screw, 25            | 01-Mar-14 | 6.99    |
| SW-23118 | 2.5-in. wd. screw, 50               | 24-Feb-14 | 8.45    |
| 23109-HB | Claw hammer                         | 20-Jan-14 | 9.95    |
| 20114-AA | Sledge hammer, 12 lb.               | 02-Jan-14 | 14.40   |
| 13-Q2/P2 | 7.25-in. pwr. saw blade             | 13-Dec-13 | 14.99   |
| 14-Q1/L3 | 9.00-in. pwr. saw blade             | 13-Nov-13 | 17.49   |
| 2238/QPD | B&D cordless drill, 1/2-in.         | 20-Jan-14 | 39.95   |
| 1546-QQ2 | Hrd. cloth, 14-in., 2x50            | 15-Jan-14 | 39.95   |
| 1558-QW1 | Hrd. cloth, 1/2-in., 3x50           | 15-Jan-14 | 43.99   |
| 2232/QWE | B&D jigsaw, 8-in. blade             | 24-Dec-13 | 99.67   |
| 2232/QTY | B&D jigsaw, 12-in. blade            | 30-Dec-13 | 109.92  |
| 11QER/31 | Power painter, 15 psi., 3-nozzle    | 03-Nov-13 | 109.99  |
| WR3/TT3  | Steel matting, 4'x8'x1/8", .5" mesh | 17-Jan-14 | 119.95  |
| 69-VRE-Q | Hicut chain saw, 16 in.             | 07-Feb-14 | 255.99  |

Cengage Learning © 2015

**The sequence (listing) obtained by specifying several comma-separated attributes for ORDER BY is called a cascading order sequence.**

```
SELECT      EMP_LNAME, EMP_FNAME, EMP_INITIAL, EMP_AREACODE, EMP_PHONE
FROM        EMPLOYEE
ORDER BY    EMP_LNAME, EMP_FNAME, EMP_INITIAL;
```

| EMP_LNAME  | EMP_FNAME | EMP_INITIAL | EMP_AREACODE | EMP_PHONE |
| ---------- | --------- | ----------- | ------------ | --------- |
| Brandon    | Marie     | G           | 901          | 882-0845  |
| Diante     | Jorge     | D           | 615          | 890-4567  |
| Genkazi    | Leighla   | W           | 901          | 569-0093  |
| Johnson    | Edward    | E           | 615          | 898-4387  |
| Jones      | Anne      | M           | 615          | 898-3456  |
| Kolmycz    | George    | D           | 615          | 324-5456  |
| Lange      | John      | P           | 901          | 504-4430  |
| Lewis      | Rhonda    | G           | 615          | 324-4472  |
| Saranda    | Hermine   | R           | 615          | 324-5505  |
| Smith      | George    | A           | 615          | 890-2984  |
| Smith      | George    | K           | 901          | 504-3339  |
| Smith      | Jeanine   | K           | 615          | 324-7883  |
| Smythe     | Melanie   | P           | 615          | 324-9006  |
| Vandam     | Rhett     |             | 901          | 675-8993  |
| Washington | Rupert    | E           | 615          | 890-4925  |
| Wiesenbach | Paul      | R           | 615          | 897-4358  |
| Williams   | Robert    | D           | 615          | 890-3220  |

Cengage Learning © 2015

#### DISTINCT

The 'DISTINCT' keyword is used to count unique/distinct occurrences of an attribute:

##### Listing Unique Values

- **DISTINCT** clause: Produces list of values that are unique
- Syntax - `SELECT DISTINCT columnlist`  
`FROM tablelist;`
- Access places nulls at the top of the list
  - Oracle places it at the bottom
  - Placement of nulls does not affect list contents

```
SELECT  DISTINCT V_CODE
FROM    PRODUCT;
```

| V_CODE |
| ------ |
|        |
| 21225  |
| 21231  |
| 21344  |
| 23119  |
| 24288  |
| 25595  |

Cengage Learning © 2015

#### AGGREGATE functions

COUNT, MIN, MAX, SUM, AVG are all functions that operate on a numerical attr/column, and produce a single scalar result (not a table). These are also called 'column operations'.

Table 7.8 - Some Basic SQL Aggregate Functions

| FUNCTION | OUTPUT                                                    |
| -------- | --------------------------------------------------------- |
| COUNT    | The number of rows containing non-null values             |
| MIN      | The minimum attribute value encountered in a given column |
| MAX      | The maximum attribute value encountered in a given column |
| SUM      | The sum of all values for a given column                  |
| AVG      | The arithmetic mean (average) for a specified column      |

Cengage Learning © 2015

#### Aggregate function examples

How many different vendors supply our products? How many supply cheap (PRICE < 10) products?

Note the third query below: COUNT(\*) counts the # of rows returned by a query (rows where the product costs < 10 units). In contrast, count() counts the # of non-null values of the column.

![](327ba7b8b963c7ef4bc897bc17d6b3e1_img.jpg)

```
SQL Plus

SQL> SELECT COUNT(DISTINCT U_CODE)
  2  FROM PRODUCT;

COUNT(DISTINCT U_CODE)
-----
                        6

SQL> SELECT COUNT(DISTINCT U_CODE)
  2  FROM PRODUCT
  3  WHERE P_PRICE <= 10.00;

COUNT(DISTINCT U_CODE)
-----
                        3

SQL> SELECT COUNT(*)
  2  FROM PRODUCT
  3  WHERE P_PRICE <= 10.00;

COUNT(*)
-----
        5

SQL>
```

Copyright Learning © 2015

What is the value for the most expensive item in the product table? Least expensive?

What is the most expensive item (details)? We can't do: WHERE P\_PRICE = MAX(P\_PRICE). This is because MAX() can only be used in a SELECT statement.

```

SQL> SELECT MAX(P_PRICE)
2 FROM PRODUCT;

MAX(P_PRICE)
-----
256.99

SQL> SELECT MIN(P_PRICE)
2 FROM PRODUCT;

MIN(P_PRICE)
-----
4.99

SQL> SELECT P_CODE, P_DESCRIPT, P_PRICE
2 FROM PRODUCT
3 WHERE P_PRICE = (SELECT MAX(P_PRICE) FROM PRODUCT);

P_CODE      P_DESCRIPT      P_PRICE
-----
89-WRE-Q    Hicut chain saw, 16 in.      256.99

SQL>

```

Cengage Learning © 2015

```

SELECT *
FROM PRODUCT
WHERE P_QOH * P_PRICE = (SELECT MAX(P_QOH * P_PRICE) FROM PRODUCT);

```

**Sum:**

```

SQL> SELECT SUM(CUS_BALANCE) AS TOTBALANCE FROM CUSTOMER;

TOTBALANCE
-----
2089.28

SQL> SELECT SUM(P_QOH * P_PRICE) AS TOTVALUE FROM PRODUCT;

TOTVALUE
-----
15084.52

SQL>

```

Cengage Learning © 2015

**Avg:**

![](9ce71bb1e3da44d64682f0b6f3b7a143_img.jpg)

```
SQL> SELECT AVG(P_PRICE) FROM PRODUCT;

AVG(P_PRICE)
-----
      56.42125

SQL> SELECT P_CODE, P_DESCRIPT, P_QOH, P_PRICE, U_CODE
2  FROM PRODUCT
3  WHERE P_PRICE > (SELECT AVG(P_PRICE) FROM PRODUCT)
4  ORDER BY P_PRICE DESC;

P_CODE      P_DESCRIPT                                P_QOH      P_PRICE      U_CODE
-----
89-WRE-Q    Hicut chain saw, 16 in.                   11         256.99      24288
WR3/TT3     Steel matting, 4'x8'x1/6", .5" mesh        18         119.95      25595
11QER/31    Power painter, 15 psi., 3-nozzle           8         109.99      25595
2232/QTY    B\&D jigsaw, 12-in. blade                  8         109.92      24288
2232/QWE    B\&D jigsaw, 8-in. blade                   6          99.87      24288

SQL>
```

Cengage Learning © 2015

#### GROUP BY (itemizing)

### Grouping Data

- Frequency distributions created by **GROUP BY** clause within SELECT statement
- GROUP BY can **only** be used in concert with an aggregate function
- Syntax - SELECT *columnlist*  
                   FROM *tablelist*  
                   [WHERE *conditionlist*]  
                   [GROUP BY *columnlist*]  
                   [HAVING *conditionlist*]  
                   [ORDER BY *columnlist* [ASC | DESC]];

```

SQL Plus
SQL> SELECT P_SALECODE, MIN(P_PRICE)
2 FROM PRODUCT
3 GROUP BY P_SALECODE
4 ORDER BY P_SALECODE;

P MIN(P_PRICE)
-----
1          9.95
2          4.99
           5.87

SQL> SELECT P_SALECODE, AVG(P_PRICE)
2 FROM PRODUCT
3 GROUP BY P_SALECODE
4 ORDER BY P_SALECODE;

P AVG(P_PRICE)
-----
1        107.152
2         47.88
           15.94

SQL>

```

Cengage Learning © 2015

You can think of 'GROUP BY' to mean "CATEGORIZE BY" or "ITEMIZE BY": rather than just a single MIN, MAX, SUM, COUNT or AVG, we're asking for a value PER OCCURRENCE of a GROUP BY value, eg. minimum price PER VENDOR, max GPA PER DEPARTMENT, average earnings PER MAJOR, etc. Specifically, when used with SUM(), GROUP BY is used to request subtotals.

The screenshot shows a SQL Plus window with the following content:

```

SQL> SELECT U_CODE, P_CODE, P_DESCRIPT, P_PRICE
2 FROM PRODUCT
3 GROUP BY U_CODE;
SELECT U_CODE, P_CODE, P_DESCRIPT, P_PRICE
      x
ERROR at line 1:
ORA-00979: not a GROUP BY expression

SQL> SELECT U_CODE, COUNT(DISTINCT P_CODE)
2 FROM PRODUCT
3 GROUP BY U_CODE;

  U_CODE COUNT(DISTINCTP_CODE)
-----
21225          2
21231          1
21344          3
23119          2
24288          3
25595          3
          2

7 rows selected.

SQL>

```

Oracle Learning © 2015

'GROUP BY' used without an aggregate function is meaningless, since there is no aggregate value (MIN, COUNT etc.) to itemize.

Note that grouping by multiple columns simply means grouping by all occurrences (unique combinations, NOT product) of the values in those columns. Eg. in here, there are 91 customers [<https://www.w3schools.com/sql>]:

'SELECT COUNT(CustomerName) AS CustCount FROM Customers;' will give you 91 [ie. customers buying products].

'SELECT COUNT(CustomerName) AS CustCount FROM Customers GROUP BY Country;' will give you 21 rows (there are 21 countries with customers) whose counts add up to 91.

'SELECT COUNT(CustomerName) AS CustCount FROM Customers GROUP BY Country, City;' will give you 69 rows whose counts add up to 91 [there are 69 city, country combinations].

#### Store receipt

Here is a grocery store receipt where subtotals are displayed itemized, aggregated by product types DELI, GROCERY, MIXED NUTS and PRODUCE (presumably using SUM(), together with GROUP BY):

#### SK SUPER KING MARKETS SUPER KING

Join "Royal Rewards" today  
and Start Earning Points!

2716 N. San Fernando Rd.  
Los Angeles, CA. 90065  
(323) 225-0044  
Store Hours 7 am - 9 pm  
www.SuperKingMarkets.com

Purchase \$ 8.74

PIN Used

Debit Card #SXXXXXXXXXX4428  
Auth # 568771 Payment from primary  
Lane # 06 Cashier # 766  
01/29/16 09:34 Ref/Seq # 065808  
Mrch=912871 Term=001 IC=DC  
EPS Sequence # 065808

##### DELI

SHAMROCK 2% STRAWBER 1.89 \*

##### GROCERY

DORITOS SPICY NACHO  
1 @ 2 FOR 5.00 2.50 \*

#### MIXED NUTS

FRIED RED SKIN PEANU  
0.66 lb @ 1.99/ lb 1.31 \*

#### PRODUCE

BLACKBERRIES BERRY L V 1.99 \*  
CACAHUATE QUEMADO  
0.53 lb @ 1.99/ lb 1.05 \*

BALANCE DUE 8.74

Debit Card 8.74  
Auth Code = 568771

CHANGE 0.00

Total number of items sold = 5

CASHIER NAME: JULIA P.

STORE:00002 REGISTER:006 CASHIER:0766  
TICKET#:4826 29JAN2016 9:34:32

\*ALL RETURNS AND EXCHANGES CAN ONLY BE  
ACCEPTED WITHIN 2 DAYS FROM THE DATE OF  
PURCHASE AND MUST BE WITH RECEIPT.

\*RETURNS OR EXCHANGES OF NON-FOOD ITEMS  
SHALL BE IN ORIGINAL PACKAGE \*NO CASH  
REFUND ON ITEMS PAID BY CREDIT CARD

\*NO RETURNS ON BABYFOOD AND FORMULA

ALL SALES ARE FINAL ON ALL

ALCOHOLIC BEVERAGES & TOBACCO

LA County State Tax Rate of 9.00%

![](9acd7ccc1be0bbd5af47889b01cd8f05_img.jpg)

**While you're at it, see what other DATA you can spot in the receipt! Even a single trip to the store can generate a LOT of data.**

#### HAVING

The **HAVING** clause is used to filter rows in a **GROUP BY** specification (only those rows **HAVING** met the specified condition will appear in the result).

Note that **HAVING** can only occur in a query that has a **GROUP BY**, which in turn can only occur when there is an aggregate function (**MIN**, **MAX**, **SUM**, **COUNT** or **AVG**).

#### HAVING Clause

- Extension of **GROUP BY** feature
- Applied to output of **GROUP BY** operation
- Used in conjunction with **GROUP BY** clause in second SQL command set
- Similar to **WHERE** clause in **SELECT** statement

![](b83b1eb356ecf21fc3c5af4ad6382ec9_img.jpg)

```
SQL> SELECT U_CODE, COUNT(DISTINCT P_CODE), AVG(P_PRICE)
  2  FROM PRODUCT
  3  GROUP BY U_CODE;

U_CODE COUNT(DISTINCTP_CODE) AVG(P_PRICE)
 
21225                     2         8.47
21231                     1         8.45
21344                     3        12.49
23119                     2        41.97
24288                     3   155.593333
25595                     3        89.63
                          2       10.135

7 rows selected.

SQL> SELECT U_CODE, COUNT(DISTINCT P_CODE), AVG(P_PRICE)
  2  FROM PRODUCT
  3  GROUP BY U_CODE
  4  HAVING AVG(P_PRICE) < 10;

U_CODE COUNT(DISTINCTP_CODE) AVG(P_PRICE)
 
21225                     2         8.47
21231                     1         8.45

SQL>
```

Cengage Learning © 2015

### Table joins

### Joining Database Tables

- Performed when data are retrieved from more than one table at a time
  - Equality comparison between foreign key and primary key of related tables
- Tables are joined by listing tables in FROM clause of SELECT statement
  - DBMS creates Cartesian product of every table in the FROM clause

#### Joining Tables With an Alias

- Alias identifies the source table from which data are taken
- Any legal table name can be used as alias
- Add alias after table name in FROM clause
  - FROM tablename alias, eg. 'FROM PRODUCT P'

```

SELECT      P_DESCRIPT, P_PRICE, V_NAME, V_CONTACT, V_AREACODE, V_PHONE
FROM        PRODUCT, VENDOR
WHERE       PRODUCT.V_CODE = VENDOR.V_CODE;

```

| P_DESCRIPT                          | P_PRICE | V_NAME          | V_CONTACT | V_AREACODE | V_PHONE  |
| ----------------------------------- | ------- | --------------- | --------- | ---------- | -------- |
| Claw hammer                         | 9.95    | Bryson, Inc.    | Smithson  | 615        | 223-3234 |
| 1.25-in. metal screw, 25            | 6.99    | Bryson, Inc.    | Smithson  | 615        | 223-3234 |
| 2.5-in. wd. screw, 50               | 8.45    | D&E Supply      | Singh     | 615        | 228-3245 |
| 7.25-in. pwr. saw blade             | 14.99   | Gomez Bros.     | Ortega    | 615        | 889-2546 |
| 9.00-in. pwr. saw blade             | 17.49   | Gomez Bros.     | Ortega    | 615        | 889-2546 |
| Rat-tail file, 1/8-in. fine         | 4.99    | Gomez Bros.     | Ortega    | 615        | 889-2546 |
| Hrd. cloth, 1/4-in., 2x50           | 39.95   | Randssets Ltd.  | Anderson  | 901        | 678-3998 |
| Hrd. cloth, 1/2-in., 3x50           | 43.99   | Randssets Ltd.  | Anderson  | 901        | 678-3998 |
| B&D jigsaw, 12-in. blade            | 109.92  | ORDVA, Inc.     | Hakford   | 615        | 898-1234 |
| B&D jigsaw, 8-in. blade             | 99.87   | ORDVA, Inc.     | Hakford   | 615        | 898-1234 |
| Hicut chain saw, 16 in.             | 256.99  | ORDVA, Inc.     | Hakford   | 615        | 898-1234 |
| Power painter, 15 psi., 3-nozzle    | 109.99  | Rubicon Systems | Orton     | 904        | 456-0092 |
| B&D cordless drill, 1/2-in.         | 38.95   | Rubicon Systems | Orton     | 904        | 456-0092 |
| Steel matting, 4'x8'x1/8", .5" mesh | 119.85  | Rubicon Systems | Orton     | 904        | 456-0092 |

Cengage Learning © 2015

```

ORDER BY   PRODUCT.P_PRICE;

```

```
SELECT      CUS_LNAME, INVOICE.INV_NUMBER, INV_DATE, P_DESCRIPT
FROM        CUSTOMER, INVOICE, LINE, PRODUCT
WHERE       CUSTOMER.CUS_CODE = INVOICE.CUS_CODE
AND         INVOICE.INV_NUMBER = LINE.INV_NUMBER
AND         LINE.P_CODE = PRODUCT.P_CODE
AND         CUSTOMER.CUS_CODE = 10014
ORDER BY    INV_NUMBER;
```

Joining n tables will need (n-1) join conditions.

#### 'Recursive join' example

Need different aliases for the table being queried so that we can use such aliases as namespaces for attributes.

#### Recursive Joins

- **Recursive query:** Table is joined to itself using alias
- Use aliases to differentiate the table from itself

#### Table, for self-join example

| EMP_NUM | EMP_TITLE | EMP_LNAME   | EMP_FNAME | EMP_INITIAL | EMP_DOB   | EMP_HIRE_DATE | EMP_AREACODE | EMP_PHONE | EMP_MGR |
| ------- | --------- | ----------- | --------- | ----------- | --------- | ------------- | ------------ | --------- | ------- |
| 100     | Mr.       | Kolmycz     | George    | D           | 15-Jun-42 | 15-Mar-85     | 615          | 324-5456  |         |
| 101     | Ms.       | Lewis       | Rhonda    | G           | 19-Mar-65 | 25-Apr-86     | 615          | 324-4472  | 100     |
| 102     | Mr.       | Yendam      | Rhett     |             | 14-Nov-58 | 20-Dec-90     | 901          | 675-8993  | 100     |
| 103     | Ms.       | Jones       | Anne      | M           | 16-Oct-74 | 28-Aug-94     | 615          | 898-3456  | 100     |
| 104     | Mr.       | Lange       | John      | P           | 08-Nov-71 | 20-Oct-94     | 901          | 504-4430  | 105     |
| 105     | Mr.       | vWilliams   | Robert    | D           | 14-Mar-75 | 08-Nov-96     | 615          | 890-3220  |         |
| 106     | Mrs.      | Smith       | Jeanine   | K           | 12-Feb-68 | 05-Jan-89     | 615          | 324-7003  | 105     |
| 107     | Mr.       | Dante       | Jorge     | D           | 21-Aug-74 | 02-Jul-94     | 615          | 890-4567  | 105     |
| 108     | Mr.       | vWesenbach  | Paul      | R           | 14-Feb-66 | 18-Nov-92     | 615          | 897-4358  |         |
| 109     | Mr.       | Smith       | George    | K           | 18-Jun-61 | 14-Apr-89     | 901          | 504-3339  | 108     |
| 110     | Mrs.      | Genkozi     | Leigha    | W           | 19-May-70 | 01-Dec-90     | 901          | 569-0093  | 108     |
| 111     | Mr.       | vWashington | Rupert    | E           | 03-Jan-66 | 21-Jun-93     | 615          | 890-4925  | 105     |
| 112     | Mr.       | Johnson     | Edward    | E           | 14-May-61 | 01-Dec-83     | 615          | 898-4387  | 100     |
| 113     | Ms.       | Smythe      | Melanie   | P           | 15-Sep-70 | 11-May-99     | 615          | 324-9005  | 105     |
| 114     | Ms.       | Brandon     | Marie     | G           | 02-Nov-56 | 15-Nov-79     | 901          | 882-0845  | 108     |
| 115     | Mrs.      | Saranda     | Hermine   | R           | 25-Jul-72 | 23-Apr-93     | 615          | 324-5505  | 105     |
| 116     | Mr.       | Smith       | George    | A           | 08-Nov-65 | 10-Dec-88     | 615          | 890-2984  | 108     |

Cengage Learning © 2015

#### Self-join example

```

SELECT      E.EMP_NUM, E.EMP_LNAME, E.EMP_MGR, M.EMP_LNAME
FROM        EMP E, EMP M
WHERE       E.EMP_MGR=M.EMP_NUM
ORDER BY    E.EMP_MGR;

```

| EMP_NUM | E.EMP_LNAME | EMP_MGR | M.EMP_LNAME |
| ------- | ----------- | ------- | ----------- |
| 112     | Johnson     | 100     | Kolmycz     |
| 103     | Jones       | 100     | Kolmycz     |
| 102     | Vandam      | 100     | Kolmycz     |
| 101     | Lewis       | 100     | Kolmycz     |
| 115     | Saranda     | 105     | Williams    |
| 113     | Smythe      | 105     | Williams    |
| 111     | Washington  | 105     | Williams    |
| 107     | Dante       | 105     | Williams    |
| 106     | Smith       | 105     | Williams    |
| 104     | Lange       | 105     | Williams    |
| 116     | Smith       | 108     | Wesenbach   |
| 114     | Brandon     | 108     | Wesenbach   |
| 110     | Gentkazi    | 108     | Wesenbach   |
| 109     | Smith       | 108     | Wesenbach   |

Cengage Learning © 2015

Here is how the join works:

| EMP_NUM | EMP_TITLE  | EMP_LNAME | EMP_FNAME | EMP_INITIAL | EMP_DOB   | EMP_HIRE_DATE | EMP_AREACODE | EMP_PHONE | EMP_JOB |
| ------- | ---------- | --------- | --------- | ----------- | --------- | ------------- | ------------ | --------- | ------- |
| 100 Mr. | Kolmycz    | George    | D         |             | 15-Jun-42 | 15-Mar-85 615 |              | 324-5455  | 100     |
| 101 Mr. | Lewis      | Rhonda    | O         |             | 19-Mar-85 | 25-Apr-85 615 |              | 324-4472  | 100     |
| 102 Mr. | Vandam     | Rudolf    |           |             | 14-Jul-85 | 20-Dec-92 901 |              | 676-5993  | 100     |
| 103 Ms. | Jones      | Anne      | M         |             | 16-Oct-74 | 28-Aug-94 615 |              | 698-3456  | 100     |
| 104 Mr. | Lange      | John      | P         |             | 08-Nov-71 | 20-Oct-94 901 |              | 504-4430  | 105     |
| 105 Mr. | Williams   | Robert    | D         |             | 14-Mar-75 | 05-Nov-95 615 |              | 696-3220  |         |
| 106 Ms. | Smith      | Jeanne    | K         |             | 12-Feb-85 | 05-Jun-89 615 |              | 324-7803  | 105     |
| 107 Mr. | Dante      | Jorge     | D         |             | 21-Aug-74 | 02-Jul-94 615 |              | 690-4567  | 105     |
| 108 Mr. | Wesenbach  | Paul      | R         |             | 14-Feb-66 | 18-Nov-92 615 |              | 697-4359  |         |
| 109 Mr. | Smith      | George    | K         |             | 15-Jun-61 | 14-Apr-89 901 |              | 504-3339  | 108     |
| 110 Ms. | Gentkazi   | Leigha    | W         |             | 19-May-70 | 01-Dec-92 901 |              | 699-0003  | 108     |
| 111 Mr. | Washington | Rupert    | E         |             | 03-Jun-66 | 21-Jun-93 615 |              | 690-4925  | 105     |
| 112 Mr. | Johnson    | Edward    | E         |             | 14-May-61 | 01-Dec-83 615 |              | 698-4307  | 100     |
| 113 Ms. | Smythe     | Melanie   | P         |             | 15-Sep-70 | 11-May-99 615 |              | 324-9006  | 105     |
| 114 Ms. | Brandon    | Marie     | O         |             | 02-Nov-55 | 15-Nov-79 901 |              | 682-8945  | 108     |
| 115 Ms. | Saranda    | Hermine   | R         |             | 25-Jul-72 | 23-Apr-93 615 |              | 324-5505  | 105     |
| 116 Mr. | Smith      | George    | A         |             | 08-Nov-85 | 10-Dec-88 615 |              | 690-2984  | 108     |

Cengage Learning © 2015

**E**

| EMP_NUM | EMP_TITLE  | EMP_LNAME | EMP_FNAME | EMP_INITIAL | EMP_DOB   | EMP_HIRE_DATE | EMP_AREACODE | EMP_PHONE | EMP_JOB |
| ------- | ---------- | --------- | --------- | ----------- | --------- | ------------- | ------------ | --------- | ------- |
| 100 Mr. | Kolmycz    | George    | D         |             | 15-Jun-42 | 15-Mar-85 615 |              | 324-5455  | 100     |
| 101 Mr. | Lewis      | Rhonda    | O         |             | 19-Mar-85 | 25-Apr-85 615 |              | 324-4472  | 100     |
| 102 Mr. | Vandam     | Rudolf    |           |             | 14-Jul-85 | 20-Dec-92 901 |              | 676-5993  | 100     |
| 103 Ms. | Jones      | Anne      | M         |             | 16-Oct-74 | 28-Aug-94 615 |              | 698-3456  | 100     |
| 104 Mr. | Lange      | John      | P         |             | 08-Nov-71 | 20-Oct-94 901 |              | 504-4430  | 105     |
| 105 Mr. | Williams   | Robert    | D         |             | 14-Mar-75 | 05-Nov-95 615 |              | 696-3220  |         |
| 106 Ms. | Smith      | Jeanne    | K         |             | 12-Feb-85 | 05-Jun-89 615 |              | 324-7803  | 105     |
| 107 Mr. | Dante      | Jorge     | D         |             | 21-Aug-74 | 02-Jul-94 615 |              | 690-4567  | 105     |
| 108 Mr. | Wesenbach  | Paul      | R         |             | 14-Feb-66 | 18-Nov-92 615 |              | 697-4359  |         |
| 109 Mr. | Smith      | George    | K         |             | 15-Jun-61 | 14-Apr-89 901 |              | 504-3339  | 108     |
| 110 Ms. | Gentkazi   | Leigha    | W         |             | 19-May-70 | 01-Dec-92 901 |              | 699-0003  | 108     |
| 111 Mr. | Washington | Rupert    | E         |             | 03-Jun-66 | 21-Jun-93 615 |              | 690-4925  | 105     |
| 112 Mr. | Johnson    | Edward    | E         |             | 14-May-61 | 01-Dec-83 615 |              | 698-4307  | 100     |
| 113 Ms. | Smythe     | Melanie   | P         |             | 15-Sep-70 | 11-May-99 615 |              | 324-9006  | 105     |
| 114 Ms. | Brandon    | Marie     | O         |             | 02-Nov-55 | 15-Nov-79 901 |              | 682-8945  | 108     |
| 115 Ms. | Saranda    | Hermine   | R         |             | 25-Jul-72 | 23-Apr-93 615 |              | 324-5505  | 105     |
| 116 Mr. | Smith      | George    | A         |             | 08-Nov-85 | 10-Dec-88 615 |              | 690-2984  | 108     |

Cengage Learning © 2015

**M**

Sooo... are joins 'evil'? Not really :)

### SQL is declarative, not imperative

Now that you're familiar with SQL syntax, you will appreciate knowing how it compares with a regular programming language such as C++. Shown below is such a comparison, using C# which lets us write code in an imperative (command-oriented) manner as well a declarative (result-oriented) one [this is from a book on functional programming]:

##### Listing 1.3 Imperative data processing (C#)

```
List<string> res = new List<string>();           #1
foreach(Product p in Products) {               #2
    if (p.UnitPrice > 75.0M) {
        res.Add(String.Format("{0} - ${1}",
            p.ProductName, p.UnitPrice));        #3
    }
}
return res;
#1 Create resulting list
#2 Iterate over products
#3 Add information to list of results
```

You'll probably need to read the code carefully to understand what it does, but that's not the only aspect we want to improve. The code is written as a sequence of some basic imperative commands. For example, the first statement creates new list (#1), the second iterates over all products (#2) and a later one adds element to the list (#3). However, we'd like to be able to describe the problem at a higher level. In more abstract terms, the code just filters a collection and returns some information about every returned product.

In C# 3.0, we can write the same code using query expression syntax. This version is closer to our real goal—it uses the same idea of filtering and transforming the data. You can see the code in listing 1.4.

###### Listing 1.4 Declarative data processing (C#)

```
var res = from p in Products                     #1
           where p.UnitPrice > 75.0M
           select string.Format("{0} - ${1}",
            p.ProductName, p.UnitPrice);         #2
return res;
#1 Filter products using predicate
#2 Return information about product
```

The expression that calculates the result (`res`) is composed from basic operators such as `where` or `select`. These operators take other expressions as an argument, because they need to know exactly what we want to filter or select as a result.

©Manning Publications Co.



1/25 9:35:42 \*\*\*

![](5f946b9310b589e34d571919bc96318a_img.jpg)![](6eb1d75070eca2cf2573ce42d49da140_img.jpg)

### More SQL

# Ch.8

11e

## Database Systems Design, Implementation, and Management

![](26d99c1e7a42cd8b86582a751365aa32_img.jpg)

# Chapter 8 Advanced SQL

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

### Learning Objectives

- In this chapter, the student will learn:
  - How to use the advanced SQL JOIN operator syntax
  - About the different types of subqueries and correlated queries
  - How to use SQL functions to manipulate dates, strings, and other data
  - About the relational set operators UNION, UNION ALL, INTERSECT, and MINUS

### Learning Objectives

- In this chapter, the student will learn:
  - How to use the advanced SQL JOIN operator syntax
  - About the different types of subqueries and correlated queries
  - How to use SQL functions to manipulate dates, strings, and other data
  - About the relational set operators UNION, UNION ALL, INTERSECT, and MINUS

### The 'JOIN' operation

Recall that we looked at examples of joining - entries from two tables, and entries from a single table. These joins were based on 'join conditions'.

It is also possible to join tables using the 'JOIN' keyword..

#### JOIN conditions

Note that JOINS can be based on  $\neq$  (aka  $\lt\gt$ ),  $\gt$ ,  $\lt$ ,  $\geq$  and  $\leq$  as well, in addition to equality. Eg. to list all students who will be getting a 'A' (uses two inequality comparisons indirectly):

```
//  
http://www.comp.nus.edu.sg/~ooibc/courses/sql/  
dml\_query\_join.htm  
SELECT  a.name, a.score  
FROM    student_scores a, grade_class b  
WHERE   b.grade = 'A' AND a.score BETWEEN  
b.low_end AND b.high_end;
```

#### SQL Join Operators

- Relational join operation merges rows from two tables and returns rows with one of the following
  - Natural join - Have common values in common columns
  - Equality or inequality - Meet a given join condition
  - **Outer join**: Have common values in common columns or have no matching values
- **Inner join**: Only rows that meet a given criterion are selected

#### Ways to specify JOIN conditions

Table 8.1 - SQL Join Expression Styles

| JOIN CLASSIFICATION | JOIN TYPE      | SQL SYNTAX EXAMPLE                           | DESCRIPTION                                                  |
| ------------------- | -------------- | -------------------------------------------- | ------------------------------------------------------------ |
| CROSS               | CROSS JOIN     | SELECT *<br>FROM T1, T2                      | Returns the Cartesian product of T1 and T2 (old style)       |
|                     |                | SELECT *<br>FROM T1 CROSS JOIN T2            | Returns the Cartesian product of T1 and T2                   |
| INNER               | Old-style JOIN | SELECT *<br>FROM T1, T2<br>WHERE T1.C1=T2.C1 | Returns only the rows that meet the join condition in the WHERE clause (old style); only rows with matching values are selected |
|                     | NATURAL JOIN   | SELECT *<br>FROM T1 NATURAL JOIN T2          | Returns only the rows with matching values in the matching columns; the matching columns must have the same names and similar data types |
|                     | JOIN USING     | SELECT *<br>FROM T1 JOIN T2 USING (C1)       | Returns only the rows with matching values in the columns indicated in the USING clause |
|                     | JOIN ON        | SELECT *<br>FROM T1 JOIN T2 ON T1.C1=T2.C1   | Returns only the rows that meet the join condition indicated in the ON clause |

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

5

##### Outer vs inner vs full ('both') JOINS

## Table 8.1 - SQL Join Expression Styles

| JOIN CLASSIFICATION | JOIN TYPE  | SQL SYNTAX EXAMPLE                                        | DESCRIPTION                                                  |
| ------------------- | ---------- | --------------------------------------------------------- | ------------------------------------------------------------ |
| OUTER               | LEFT JOIN  | SELECT *<br>FROM T1 LEFT OUTER JOIN T2<br>ON T1.C1=T2.C1  | Returns rows with matching values and includes all rows from the left table (T1) with unmatched values |
|                     | RIGHT JOIN | SELECT *<br>FROM T1 RIGHT OUTER JOIN T2<br>ON T1.C1=T2.C1 | Returns rows with matching values and includes all rows from the right table (T2) with unmatched values |
|                     | FULL JOIN  | SELECT *<br>FROM T1 FULL OUTER JOIN T2<br>ON T1.C1=T2.C1  | Returns rows with matching values and includes all rows from both tables (T1 and T2) with unmatched values |

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

6

##### Full (left+right outer) JOIN example

For example, the following query lists the product code, vendor code, and vendor name for all products and includes all product rows (products without matching vendors) as well as all vendor rows (vendors without matching products):

```
SELECT      P_CODE, VENDOR.V_CODE, V_NAME
FROM        VENDOR FULL JOIN PRODUCT ON VENDOR.V_CODE = PRODUCT.V_CODE;
```

The SQL code and its results are shown in Figure 8.12.

**FIGURE 8.12** FULL JOIN results

The screenshot shows the Oracle SQL\*Plus interface with a query window. The query is a FULL JOIN between the VENDOR and PRODUCT tables on the V\_CODE column. The results are displayed in a table with three columns: P\_CODE, V\_CODE, and V\_NAME. The results show 21 rows, including products without vendors (e.g., 11QER/31, 13-U2/P2) and vendors without products (e.g., 25595 Rubicon Systems, 21344 Gomez Bros.).

| P_CODE   | V_CODE | V_NAME          |
| -------- | ------ | --------------- |
| 11QER/31 | 25595  | Rubicon Systems |
| 13-U2/P2 | 21344  | Gomez Bros.     |
| 14-Q1/L9 | 21344  | Gomez Bros.     |
| 1546-UQ2 | 23119  | Randsets Ltd.   |
| 1558-QW1 | 23119  | Randsets Ltd.   |
| 2232/RTV | 24288  | ORUVA, Inc.     |
| 2232/QME | 24288  | ORUVA, Inc.     |
| 2238/QPD | 25595  | Rubicon Systems |
| 23100-H8 | 21225  | Bryson, Inc.    |
| 54778-2T | 21344  | Gomez Bros.     |
| 89-WRE-Q | 24288  | ORUVA, Inc.     |
| SM-18277 | 21225  | Bryson, Inc.    |
| SM-23116 | 21231  | D&E Supply      |
| VR3/TT3  | 25595  | Rubicon Systems |
|          | 22567  | Dane Supply     |
|          | 21226  | SuperLoe, Inc.  |
|          | 24804  | Bracknan Bros.  |
|          | 25501  | Danal Supplies  |
|          | 25443  | B&H, Inc.       |
| 23114-AA |        |                 |
| PUC23DRT |        |                 |

21 rows selected.

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

### 'SELECT' subqueries

| SELECT SUBQUERY EXAMPLES                                     | EXPLANATION                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| INSERT INTO PRODUCT<br>SELECT * FROM P;                      | Inserts all rows from Table P into the PRODUCT table. Both tables must have the same attributes. The subquery returns all rows from Table P. |
| UPDATE PRODUCT<br>SET P_PRICE = (SELECT AVG(P_PRICE)<br>FROM PRODUCT)<br>WHERE V_CODE IN (SELECT V_CODE<br>FROM VENDOR<br>WHERE V_AREACODE = '615') | Updates the product price to the average product price, but only for products provided by vendors who have an area code equal to 615. The first subquery returns the average price; the second subquery returns the list of vendors with an area code equal to 615. |
| DELETE FROM PRODUCT<br>WHERE V_CODE IN (SELECT V_CODE<br>FROM VENDOR<br>WHERE V_AREACODE = '615') | Deletes the PRODUCT table rows provided by vendors with an area code equal to 615. The subquery returns the list of vendor codes with an area code equal to 615. |

Cengage Learning © 2015

#### Subqueries and Correlated Queries

- Subquery is a query inside another query
- Subquery can return:
  - One single value - One column and one row
  - A list of values - One column and multiple rows
  - A virtual table - Multicolumn, multirow set of values
  - No value - Output of the outer query might result in an error or a null empty set

#### 'WHERE' subqueries

##### WHERE Subqueries

- Uses inner SELECT subquery on the right side of a WHERE comparison expression
- Value generated by the subquery must be of a comparable data type
- If the query returns more than a single value, the DBMS will generate an error
- Can be used in combination with joins

**FIGURE 8.13** WHERE subquery example![](754016c567b25212578018d56b4f5e74_img.jpg)

The screenshot shows the Oracle SQL\*Plus interface. The first query filters products by price relative to the average price. The second query joins customer, invoice, and product tables to find customers who have purchased a 'Claw hammer'.

```
Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT P_CODE, P_PRICE FROM PRODUCT
2  WHERE P_PRICE >= (SELECT AVG(P_PRICE) FROM PRODUCT);

P_CODE      P_PRICE
-----
11QER/31     109.99
2232/QTV     109.92
2232/QWE      99.87
89-WRE-Q     256.99
WR3/TT3      119.95

SQL> SELECT DISTINCT CUS_CODE, CUS_LNAME, CUS_FNAME
2  FROM CUSTOMER JOIN INVOICE USING (CUS_CODE)
3          JOIN LINE USING (INV_NUMBER)
4          JOIN PRODUCT USING (P_CODE)
5  WHERE P_CODE IN (SELECT P_CODE FROM PRODUCT WHERE P_DESCRIPT = 'Claw hammer');

CUS_CODE CUS_LNAME      CUS_FNAME
-----
10011 Dunne      Leona
10014 Orlando    Myron
```

##### IN, HAVING subqueries

##### IN and HAVING Subqueries

- IN subqueries
  - Used to compare a single attribute to a list of values
- HAVING subqueries
  - HAVING clause restricts the output of a GROUP BY query by applying conditional criteria to the grouped rows

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

11

**Compare against a LIST of values..**

**FIGURE  
8.14**

##### **IN subquery example**

```

Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT DISTINCT CUS_CODE, CUS_LNAME, CUS_FNAME
  2  FROM CUSTOMER JOIN INVOICE USING (CUS_CODE)
  3  JOIN LINE USING (INV_NUMBER)
  4  JOIN PRODUCT USING (P_CODE)
  5  WHERE P_CODE IN (SELECT P_CODE FROM PRODUCT
  6  WHERE P_DESCRIPT LIKE '%hammer%' OR P_DESCRIPT LIKE '%saw%');

CUS_CODE CUS_LNAME      CUS_FNAME
 
10011 Dunne          Leona
10012 Smith          Kathy
10014 Orlando        Hyron
10015 O'Brian        Any
SQL>

```

![](0e38ae54c6bdb931c90a3cc6081be47e_img.jpg)

As we saw earlier, this restricts the results of a GROUP BY clause. Eg. here's how to list all products sold, whose totals are greater than the average quantity sold:

**FIGURE  
8.15**

##### **HAVING subquery example**

```

Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT P_CODE, SUM(LINE_UNITS)
  2  FROM LINE
  3  GROUP BY P_CODE
  4  HAVING SUM(LINE_UNITS) > (SELECT AVG(LINE_UNITS) FROM LINE);

P_CODE      SUM(LINE_UNITS)
 
13-Q2/P2          8
23109-HB          5
54778-2T          6
PUC23DRT         17
SM-18277          3
WR3/TT3          3

6 rows selected.

SQL>

```

![](6f049c98cae71a6b0fa24769bd039368_img.jpg)

#### ALL, ANY (inequality comparisons)

Recall that 'IN' is an equality comparison against a list. To do **inequality comparison of a value against a list of values** (eg. need to be greater than ALL, need to be less than ANY..), use **ALL, ANY**.

#### Multirow Subquery Operators: ANY and ALL

- ALL operator
  - Allows comparison of a single value with a list of values returned by the first subquery
    - Uses a comparison operator other than equals
- ANY operator
  - Allows comparison of a single value to a list of values and selects only the rows for which the value is greater than or less than any value in the list

Eg. "which products do we own [in our store], whose value is more than ALL other products's values supplied by vendors in Florida?"

**FIGURE  
8.16**

##### **Multirow subquery operator example**

```

Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT P_CODE, P_QOH*P_PRICE
2 FROM PRODUCT
3 WHERE P_QOH*P_PRICE > ALL
4 (SELECT P_QOH*P_PRICE FROM PRODUCT
5  WHERE V_CODE IN (SELECT V_CODE FROM VENDOR WHERE V_STATE = 'FL'));

P_CODE      P_QOH*P_PRICE
-----
89-WRE-Q      2826.89

```

Note that 'greater than ALL' is eqvt to 'greater than the largest of'. 'ALL' is used to select rows [plural in general] that comparison-succeed against all values in a list.

Another powerful operator is the ANY multirow operator (the near cousin of the ALL multirow operator). The ANY operator allows you to compare a single value to a list of values, selecting only the rows for which the inventory cost is greater than any value of the list or less than any value of the list. You could use the equal to ANY operator, which would be the equivalent of the IN operator.

'ANY' is used to select rows [plural in general] that comparison-succeed with any value in a list.

Note that '= ANY(list of values)' is equivalent to the 'IN' operator (which is itself equivalent to multiple == conditions joined by ORs). So the following are all equivalent, for a given value of 'M':

```
(M==6) OR (M==8) OR (M==10)
```

```
M IN (6,8,10)
```

```
M = ANY (6,8,10)
```

**So loosely speaking, ALL is equivalent to AND, and ANY is equivalent to OR.**

#### 'FROM' subqueries

A **SELECT** query that appears in **FROM**, creates a **\*\*virtual table\*\*** against which the main query can run.

##### FROM Subqueries

- **FROM clause:**
  - Specifies the tables from which the data will be drawn
  - Can use **SELECT** subquery

###### All customers who bought both specified products

FIGURE 8.17 FROM subquery example

![](27875b8e8885121a94211923afb973d6_img.jpg)

```
Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT DISTINCT CUSTOMER.CUS_CODE, CUSTOMER.CUS_LNAME
2 FROM CUSTOMER,
3 (SELECT INVOICE.CUS_CODE
4 FROM INVOICE NATURAL JOIN LINE WHERE P_CODE = '19-Q2/P2') CP1, (SELECT INVOICE.CUS_CODE
5 FROM INVOICE NATURAL JOIN LINE WHERE P_CODE = '23109-HB') CP2
6 WHERE CUSTOMER.CUS_CODE = CP1.CUS_CODE AND
7       CP1.CUS_CODE = CP2.CUS_CODE;

CUS_CODE CUS_LNAME
-----
10014 Orlando

SQL> |
```

##### Attribute list subqueries

These subqueries determine what columns get output by the main query - they can be actual (existing) columns or computed columns or results of aggregate functions.

These are also known as 'column subqueries' or 'inline subqueries'.

##### Attribute List Subqueries

- SELECT statement uses attribute list to indicate what columns to project in the resulting set
- Inline subquery
  - Subquery expression included in the attribute list that must return one value
- Column alias cannot be used in attribute list computation if alias is defined in the same attribute list

**FIGURE 8.18** Inline subquery example

```

Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT P_CODE, P_PRICE, (SELECT AVG(P_PRICE) FROM PRODUCT) AS AVGPRICE,
2      P_PRICE-(SELECT AVG(P_PRICE) FROM PRODUCT) AS DIFF
3      FROM PRODUCT;

P_CODE          P_PRICE  AVGPRICE      DIFF
-----
11QER/31         189.99    56.42125    53.56875
13-Q2/P2         14.99     56.42125   -41.43125
14-Q1/L3         17.49     56.42125   -38.93125
1546-QQ2         39.95     56.42125   -16.47125
1558-QW1         43.99     56.42125   -12.43125
2232/QTY         189.92     56.42125    53.49875
2232/QWE         99.87     56.42125    43.44875
2238/QPD         38.95     56.42125   -17.47125
23109-HB         9.95      56.42125   -46.47125
23114-AA         14.4      56.42125   -42.02125
54778-2T         4.99      56.42125   -51.43125
89-WRE-Q        256.99     56.42125   200.56875
PUC23DRT         5.87      56.42125   -50.55125
SM-18277         6.99      56.42125   -49.43125
SW-23116         8.45      56.42125   -47.97125
WR3/TT3        119.95     56.42125    63.52875

16 rows selected.

SQL>

```

**FIGURE 8.19** Another example of an inline subquery

```

Oracle SQL*Plus
File Edit Search Options Help
SQL> SELECT P_CODE, SUM(LINE_UNITS*LINE_PRICE) AS SALES,
2      (SELECT COUNT(*) FROM EMPLOYEE) AS ECOUNT,
3      SUM(LINE_UNITS*LINE_PRICE)/(SELECT COUNT(*) FROM EMPLOYEE) AS CONTRIB
4      FROM LINE
5      GROUP BY P_CODE;

P_CODE          SALES      ECOUNT      CONTRIB
-----
13-Q2/P2        119.92         17  7.05411745
1546-QQ2         39.95         17    2.35
2232/QTY        189.92         17  6.46588235
2238/QPD         38.95         17  2.29117647
23109-HB         49.75         17  2.92647059
54778-2T         29.94         17  1.76117647
89-WRE-Q        256.99         17  15.1170588
PUC23DRT         99.79         17    5.87
SM-18277        20.97         17  1.23352941
WR3/TT3        359.85         17  21.1676471

10 rows selected.

SQL>

```

##### Correlated subqueries

##### Correlated Subquery

- Executes once for each row in the outer query
- Inner query references a column of the outer subquery
- Can be used with the EXISTS special operator

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

21

**In a correlated subquery, the inner (sub) query is repeatedly run, for each row of the outer query! The inner is said to be (co-)related with the outer query when it references a column in the outer query's table. This is in effect, like a double (nested) 'for' loop..**

```
for each row in OUTER table
  run subquery on EACH row in INNER table,
gather
results, use in outer table's query
```

**Here is the Wikipedia entry on correlated subqueries. This is the example shown there [select employees who make more than the average salary for their department]:**

```
SELECT employee_number, name  
FROM employees AS Bob  
WHERE salary > (  
    SELECT AVG(salary)  
    FROM employees  
    WHERE department = Bob.department);
```

**In the above, the outer query "passes in", for each employee (each row), the employee's dept. [which the inner query refers to as Bob.department]. The inner query selects all salaries for that dept., computes the average, compares it with the passed-in employee's salary; if the test passes, the outer query selects the employee's # and name.**

Until now, all subqueries you have learned execute independently. That is, each subquery in a command sequence executes in a serial fashion, one after another. The inner subquery executes first; its output is used by the outer query, which then executes until the last outer query executes (the first SQL statement in the code).

In contrast, a **correlated subquery** is a subquery that executes once for each row in the outer query. That process is similar to the typical nested loop in a programming language. For example:

```
FOR X = 1 TO 2
    FOR Y = 1 TO 3
        PRINT "X = "X, "Y = "Y
    END
END
```

1. It initiates the outer query.
2. For each row of the outer query result set, it executes the inner query by passing the outer row to the inner query.

That process is the opposite of that of the subqueries as you have already seen. The query is called a *correlated* subquery because the inner query is *related* to the outer query by the fact that the inner query references a column of the outer subquery.

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

To see the correlated subquery in action, suppose that you want to know all product sales in which the units sold value is greater than the average units sold value *for that product* (as opposed to the average for *all* products). In that case, the following procedure must be completed:

1. Compute the average units sold for a product.
2. Compare the average computed in Step 1 to the units sold in each sale row, and then select only the rows in which the number of units sold is greater.

The following correlated query completes the preceding two-step process:

```
SELECT  INV_NUMBER, P_CODE, LINE_UNITS
FROM    LINE LS
WHERE   LS.LINE_UNITS > (SELECT AVG(LINE_UNITS)
                        FROM LINE LA
                        WHERE LA.P_CODE = LS.P_CODE);
```

```

SQL> SELECT INU_NUMBER, P_CODE, LINE_UNITS
 2 FROM LINE LS
 3 WHERE LS.LINE_UNITS > (SELECT AVG(LINE_UNITS)
 4                         FROM LINE LA
 5                         WHERE LA.P_CODE = LS.P_CODE);

```

| INU_NUMBER | P_CODE   | LINE_UNITS |
| ---------- | -------- | ---------- |
| 1003       | 13-Q2/P2 | 5          |
| 1004       | 54778-2T | 3          |
| 1004       | 23109-HB | 2          |
| 1005       | PVC23DRT | 12         |

```

SQL> SELECT INU_NUMBER, P_CODE, LINE_UNITS,
 2         (SELECT AVG(LINE_UNITS) FROM LINE LX WHERE LX.P_CODE = LS.P_CODE) AS AVG
 3 FROM LINE LS
 4 WHERE LS.LINE_UNITS > (SELECT AVG(LINE_UNITS)
 5                         FROM LINE LA
 6                         WHERE LA.P_CODE = LS.P_CODE);

```

| INU_NUMBER | P_CODE   | LINE_UNITS | AVG         |
| ---------- | -------- | ---------- | ----------- |
| 1003       | 13-Q2/P2 | 5          | 2.666666667 |
| 1004       | 54778-2T | 3          | 2           |
| 1004       | 23109-HB | 2          | 1.25        |
| 1005       | PVC23DRT | 12         | 8.5         |

```

SQL>

```

In the top query and its result in Figure 8.14, note that the LINE table is used more than once, so you must use table aliases. In this case, the inner query computes the average units sold of the product that matches the P\_CODE of the outer query P\_CODE. That is, the inner query runs once, using the first product code found in the outer LINE table, and returns the average sale for that product. When the number of units sold in the outer LINE row is greater than the average computed, the row is added to the output. Then the inner query runs again, this time using the second product code found in the outer LINE table. The process repeats until the inner query has run for all rows in the outer LINE table. In this case, the inner query will be repeated as many times as there are rows in the outer query.

To verify the results and to provide an example of how you can combine subqueries, you can add a correlated inline subquery to the previous query. (See the second query and its results in Figure 8.14.) As you can see, the new query contains a correlated inline subquery that computes the average units sold for each product. You not only get an answer, you can also verify that the answer is correct.

**In the second query above, we have TWO correlated subqueries (that are identical), both of which need to run for every row of the main query.**

#### UNION, INTERSECTION, DIFFERENCE

#### Relational Set Operators

- SQL data manipulation commands are set-oriented
  - **Set-oriented:** Operate over entire sets of rows and columns at once
- UNION, INTERSECT, and Except (MINUS) work properly when relations are union-compatible
  - **Union-compatible:** Number of attributes are the same and their corresponding data types are alike
- UNION
  - Combines rows from two or more queries without including duplicate rows

#### Relational Set Operators

- Syntax - query UNION query
- UNION ALL
  - Produces a relation that retains duplicate rows
  - Can be used to unite more than two queries
- INTERSECT
  - Combines rows from two queries, returning only the rows that appear in both sets
  - Syntax - query INTERSECT query

**If the columns below are in two different tables, the intersection of them would list items in both (eg. History, Physics...):**

**MAJORS**

African American and Diaspora Studies  
 American Studies  
 Anthropology  
 Architecture and the Built Environment  
 Art  
 Asian Studies  
 Biochemistry and Chemical Biology  
 Biological Sciences  
 Chemistry  
 Cinema and Media Arts  
 Classical and Mediterranean Studies  
 Communication of Science and Technology  
 Communication Studies  
 Earth and Environmental Sciences  
 Ecology, Evolution, and Organismal Biology  
 Economics  
 Economics and History  
 English  
 Environmental Sociology  
 European Studies  
 European Studies: Russia and Eastern Europe  
 French  
 French and European Studies  
 Gender and Sexuality Studies  
 German Studies  
 German and European Studies  
 History  
 History of Art  
 Italian and European Studies  
 Jewish Studies  
 Latin American Studies  
 Latino and Latina Studies  
 Law, History, and Society  
 Mathematics  
 Medicine, Health, and Society  
 Molecular and Cellular Biology  
 Neuroscience  
 Philosophy  
 Physics  
 Political Science  
 Psychology  
 Public Policy Studies  
 Religious Studies  
 Russian Studies  
 Sociology  
 Spanish  
 Spanish and European Studies  
 Spanish and Portuguese  
 Theatre

**MINORS**

African American and Diaspora Studies  
 American Studies  
 Anthropology  
 Arabic Language  
 Architecture and the Built Environment  
 Art  
 Asian Studies  
 Astronomy  
 Biological Sciences  
 Brazilian Studies  
 Business\*  
 Chemistry  
 Chinese Language and Culture  
 Cinema and Media Arts  
 Communication of Science and Technology  
 Communication Studies  
 Data Science\*\*  
 Earth and Environmental Sciences  
 Economics  
 English: Creative Writing  
 English: Literary Studies  
 Environmental and Sustainability Studies  
 European Studies  
 French  
 Gender and Sexuality Studies  
 German Studies  
 History  
 History of Architecture  
 History of Art  
 Islamic Studies  
 Italian Studies  
 Japanese Language and Culture  
 Jewish Studies  
 Korean Language and Culture  
 Latin American Studies  
 Latino and Latina Studies  
 Mathematics  
 Medicine, Health, and Society  
 Mediterranean Archaeology  
 Mediterranean Studies  
 Nanoscience and Nanotechnology\*\*\*  
 Neuroscience  
 Philosophy  
 Physics  
 Political Science  
 Portuguese  
 Psychology  
 Religious Studies  
 Russian Studies  
 Scientific Computing\*\*\*  
 Sociology  
 South Asian Language and Culture  
 Spanish  
 Theatre

**50% ADD A MINOR TO THEIR PRIMARY DEGREE**

\*Jointly administered by the four undergraduate schools and Owen Graduate School of Management

\*\*Jointly administered by the four undergraduate schools

![](8bac45758dc61d93b9aa6f7f38dfe986_img.jpg)

#### Relational Set Operators

- EXCEPT (MINUS)
  - Combines rows from two queries and returns only the rows that appear in the first set
  - Syntax
    - query EXCEPT query
    - query MINUS query
- Syntax alternatives
  - IN and NOT IN subqueries can be used in place of INTERSECT

### VIEWS

#### Virtual Tables: Creating a View

- **View:** Virtual table based on a SELECT query
- **Base tables:** Tables on which the view is based
- **CREATE VIEW** statement: Data definition command that stores the subquery specification in the data dictionary
  - CREATE VIEW command
    - CREATE VIEW viewname AS SELECT query

#### Creating a Virtual Table with the CREATE VIEW Command

![](1bef24b7d805ed6e497f8681e3af9f44_img.jpg)

```
SQL> CREATE VIEW PRICEGT50 AS
  2     SELECT P_DESCRIPT, P_QOH, P_PRICE
  3     FROM PRODUCT
  4     WHERE P_PRICE > 50.00;

View created.

SQL> SELECT * FROM PRICEGT50;

P_DESCRIPT                                P_QOH    P_PRICE
-----
Power painter, 15 psi., 3-nozzle             8      109.99
B\&D jigsaw, 12-in. blade                    8      109.92
B\&D jigsaw, 8-in. blade                     6       99.87
Hicut chain saw, 16 in.                     11     256.99
Steel matting, 4'x8'x1/6", .5" mesh          18     119.95

SQL>
```

Cengage Learning © 2015

© 2015 Cengage Learning. All rights reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

#### Queries: summary

We looked at several variations of queries and subqueries (SELECT, WHERE, HAVING, IN..).

Most interestingly, a SELECT subquery can appear at the top (SELECT), middle (FROM) or bottom (WHERE) of a parent query, which provides a flexible way to express **complex logic** (since such subqueries can be recursively nested):

![](7d0d8045a2883a3db26b12404a569cda_img.jpg)

### SQL functions (built-ins)

**Functions return values...**

### SQL Functions

- Functions always use a numerical, date, or string value
- Value may be part of a command or may be an attribute located in a table
- Function may appear anywhere in an SQL statement where a value or an attribute can be used

#### SQL Functions

Date and time functions

Numeric functions

String functions

Conversion functions

#### Sequences

#### Oracle Sequences

- Independent object in the database
- Have a name and can be used anywhere a value expected
- Not tied to a table or column
- Generate a numeric value that can be assigned to any column in any table
- Table attribute with an assigned value can be edited and modified
- Can be created and deleted any time

###### Figure 8.27 - Oracle Sequence

```

SQL> CREATE SEQUENCE CUS_CODE_SEQ START WITH 20010 NOCACHE;
Sequence created.

SQL> CREATE SEQUENCE INU_NUMBER_SEQ START WITH 4010 NOCACHE;
Sequence created.

SQL> SELECT * FROM USER_SEQUENCES;

```

| SEQUENCE_NAME  | MIN_VALUE | MAX_VALUE   | INCREMENT_BY | C    | O    | CACHE_SIZE | LAST_NUMBER |
| -------------- | --------- | ----------- | ------------ | ---- | ---- | ---------- | ----------- |
| CUS_CODE_SEQ   | 1         | 1.00000E+27 | 1            | N    | N    | 0          | 20010       |
| INU_NUMBER_SEQ | 1         | 1.00000E+27 | 1            | N    | N    | 0          | 4010        |

```

SQL>

```

Cengage Learning © 2015

```

INSERT INTO CUSTOMER
VALUES (CUS_CODE_SEQ.NEXTVAL, 'Connery', 'Sean', NULL, '615', '898-2007', 0.00);

```

**NEXTVAL returns the current value, then does ++ (ie. it does 'post increment', ie. C++ as opposed to ++C); CURRVAL on the other hand, just fetches the current value (does not ++ it).**

```

SQL> INSERT INTO CUSTOMER
  2 VALUES (CUS_CODE_SEQ.NEXTVAL, 'Connery', 'Sean', NULL, '615', '898-2007', 0.00);

1 row created.

SQL> SELECT * FROM CUSTOMER WHERE CUS_CODE = 20010;

  CUS_CODE CUS_LNAME      CUS_FNAME      C CUS CUS_PHON CUS_BALANCE
 
     20010 Connery        Sean             615 898-2007           0

SQL> INSERT INTO INVOICE
  2 VALUES (INU_NUMBER_SEQ.NEXTVAL CURRVAL, 20010, SYSDATE);

1 row created.

SQL> SELECT * FROM INVOICE WHERE INU_NUMBER = 4010;

INU_NUMBER CUS_CODE INU_DATE
 
      4010    20010 25-JUL-11

SQL> INSERT INTO LINE
  2 VALUES (INU_NUMBER_SEQ.CURRVAL, 1, '13-Q2/P2', 1, 14.99);

1 row created.

SQL> INSERT INTO LINE
  2 VALUES (INU_NUMBER_SEQ.CURRVAL, 2, '23109-HB', 1, 9.95);

1 row created.

SQL> SELECT * FROM LINE WHERE INU_NUMBER = 4010;

INU_NUMBER LINE_NUMBER P_CODE   LINE_UNITS LINE_PRICE
 
      4010           1 13-Q2/P2          1      14.99
      4010           2 23109-HB          1       9.95

SQL> COMMIT;

Commit complete.

```

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

### Procedural Language SQL (PL/SQL)

PL/SQL involves extra (augmented) syntax that lets us do looping, branching, variable declaration and function declaration – these are of course not possible using 'plain' SQL.

PL/SQL can be used to create:

- **blocks of code** for one-time execution
- **triggers** - callbacks to invoke
- **stored procedures** - named procedures (no return values) for repeated calling
- **stored functions** - named functions (with return values) for repeated calling

#### Procedural SQL

- Performs a conditional or looping operation by isolating critical code and making all application programs call the shared code
  - Yields better maintenance and logic control
- **Persistent stored module (PSM)**: Block of code containing:
  - Standard SQL statements
  - Procedural extensions that is stored and executed at the DBMS server

#### Procedural SQL

- **Procedural Language SQL (PL/SQL)**
  - Use and storage of procedural code and SQL statements within the database
  - Merging of SQL and traditional programming constructs
- Procedural code is executed as a unit by DBMS when invoked by end user
- End users can use PL/SQL to create:
  - Anonymous PL/SQL blocks and triggers
  - Stored procedures and PL/SQL functions

#### Block creation example

```

SQL> BEGIN
2  INSERT INTO UENDOR
3  VALUES (25678, 'Microsoft Corp.', 'Bill Gates', '765', '546-8484', 'WA', 'N');
4  END;
5  /

PL/SQL procedure successfully completed.

SQL> SET SERVEROUTPUT ON
SQL>
SQL> BEGIN
2  INSERT INTO UENDOR
3  VALUES (25772, 'Clue Store', 'Issac Hayes', '456', '323-2009', 'UA', 'N');
4  DBMS_OUTPUT.PUT_LINE('New Vendor Added!');
5  END;
6  /
New Vendor Added!

PL/SQL procedure successfully completed.

SQL> SELECT * FROM UENDOR;

  U_CODE U_NAME                                U_CONTACT      U_A U_PHONE U_ U
-----
25678 Microsoft Corp.                        Bill Gates      765 546-8484 WA N
25772 Clue Store                             Issac Hayes     456 323-2009 UA N
21225 Bryson, Inc.                           Smithson        615 223-3234 TN Y
21226 SuperLoo, Inc.                         Flushing        904 215-8995 FL N
21231 D&E Supply                             Singh           615 228-3245 TN Y
21344 Gomez Bros.                           Ortega          615 889-2546 KY N
22567 Dome Supply                            Smith           901 678-1419 GA N
23119 Randsets Ltd.                         Anderson        901 678-3998 GA Y
24004 Brackman Bros.                        Browning        615 228-1410 TN N
24288 ORDUA, Inc.                            Hakford         615 898-1234 TN Y
25443 B&K, Inc.                             Smith           904 227-0093 FL N
25501 Damal Supplies                         Smythe          615 890-3529 TN N
25595 Rubicon Systems                       Orton           904 456-0092 FL Y

13 rows selected.

SQL>

```

ie website, in whole or in part.

### Triggers

#### Triggers

- Procedural SQL code automatically invoked by RDBMS when given data manipulation event occurs
- Parts of a trigger definition
  - Triggering timing - Indicates when trigger's PL/SQL code executes
  - Triggering event - Statement that causes the trigger to execute
  - Triggering level - **Statement-** and **row-level**
  - Triggering action - PL/SQL code enclosed between the BEGIN and END keywords

- *The triggering timing:* BEFORE or AFTER. This timing indicates when the trigger's PL/SQL code executes—in this case, before or after the triggering statement is completed.
- *The triggering event:* The statement that causes the trigger to execute (INSERT, UPDATE, or DELETE).
- *The triggering level:* The two types of triggers are statement-level triggers and row-level triggers.
  - A statement-level trigger is assumed if you omit the FOR EACH ROW keywords. This type of trigger is executed once, before or after the triggering statement is completed. This is the default case.
  - A row-level trigger requires use of the FOR EACH ROW keywords. This type of trigger is executed once for each row affected by the triggering statement. (In other words, if you update 10 rows, the trigger executes 10 times.)
- *The triggering action:* The PL/SQL code enclosed between the BEGIN and END keywords. Each statement inside the PL/SQL code must end with a semicolon ( ; ).

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

```
CREATE OR REPLACE TRIGGER trigger_name
[BEFORE / AFTER] [DELETE / INSERT / UPDATE OF column_name] ON table_name
[FOR EACH ROW]
[DECLARE]
[variable_name data type[:=initial_value]]
BEGIN
PL/SQL instructions;
.....
END;
```

![](83b97774a950a930d18b56acaf2271db_img.jpg)

The screenshot shows a SQL Plus window titled "SQL Plus". The command prompt shows the following SQL code being entered and executed:

```
SQL> CREATE OR REPLACE TRIGGER TRG_PRODUCT_REORDER
2  AFTER INSERT OR UPDATE OF P_QOH ON PRODUCT
3  BEGIN
4      UPDATE PRODUCT
5          SET P_REORDER = 1
6          WHERE P_QOH <= P_MIN;
7  END;
8  /
```

The output of the command is "Trigger created." followed by the prompt "SQL>".

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

![](594192dda931f926e12f903fdc68e896_img.jpg)

```
SQL> SELECT P_CODE, P_DESCRIPT, P_QOH, P_MIN, P_MIN_ORDER, P_REORDER
2 FROM PRODUCT
3 WHERE P_CODE = '11QER/31';

P_CODE      P_DESCRIPT                P_QOH P_MIN P_MIN_ORDER  P_REORDER
-----
11QER/31    Power painter, 15 psi., 3-nozz      8     5         25         0

SQL> UPDATE PRODUCT
2 SET P_QOH = 4
3 WHERE P_CODE = '11QER/31';

1 row updated.

SQL> SELECT P_CODE, P_DESCRIPT, P_QOH, P_MIN, P_MIN_ORDER, P_REORDER
2 FROM PRODUCT
3 WHERE P_CODE = '11QER/31';

P_CODE      P_DESCRIPT                P_QOH P_MIN P_MIN_ORDER  P_REORDER
-----
11QER/31    Power painter, 15 psi., 3-nozz      4     5         25         1

SQL>
```

Cengage Learning © 2015

Our trigger worked! [look at P\_REORDER]

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

#### Triggers

- DROP TRIGGER trigger\_name command
  - Deletes a trigger without deleting the table
- Trigger action based on DML predicates
  - Actions depend on the type of DML statement that fires the trigger

#### Stored procedures

#### Stored Procedures

- Named collection of procedural and SQL statements
- Advantages
  - Reduce network traffic and increase performance
  - Reduce code duplication by means of code isolation and code sharing

```
CREATE OR REPLACE PROCEDURE procedure_name [(argument [IN/OUT] data-type, ...)]  
    [IS/AS]  
    [variable_namedata type[:=initial_value] ]  
  
BEGIN  
    PL/SQL or SQL statements;  
    ...  
END;
```

![](4cf8a531519256450498baa217dfa98c_img.jpg)

The screenshot shows a window titled "SQL Plus" with a command prompt interface. The user has entered a series of SQL commands to create a procedure named PRC\_PROD\_DISCOUNT. The commands are: SQL> CREATE OR REPLACE PROCEDURE PRC\_PROD\_DISCOUNT, followed by a line number 2 and AS BEGIN, then line 3 with UPDATE PRODUCT, line 4 with SET P\_DISCOUNT = P\_DISCOUNT + .05, line 5 with WHERE P\_QOH >= P\_MIN \* 2;, line 6, line 7 with DBMS\_OUTPUT.PUT\_LINE ('\* \* Update finished \* \*');, line 8 with END;, and line 9 with /. The response "Procedure created." is displayed. The prompt SQL> is shown again at the bottom.

```
SQL> CREATE OR REPLACE PROCEDURE PRC_PROD_DISCOUNT  
2 AS BEGIN  
3     UPDATE PRODUCT  
4         SET P_DISCOUNT = P_DISCOUNT + .05  
5         WHERE P_QOH >= P_MIN * 2;  
6  
7     DBMS_OUTPUT.PUT_LINE ('* * Update finished * *');  
8 END;  
9 /  
  
Procedure created.  
  
SQL>
```

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

```

SQL Plus
SQL> SELECT P_CODE, P_DESCRIPT, P_QOH, P_MIN, P_DISCOUNT FROM PRODUCT;

P_CODE   P_DESCRIPT                     P_QOH P_MIN P_DISCOUNT
 
11QER/31 Power painter, 15 psi., 3-nozz    29     5       0.00
13-Q2/P2 7.25-in. pwr. saw blade           32    15       0.05
14-Q1/L3 9.00-in. pwr. saw blade           18    12       0.00
1546-QQ2 Hrd. cloth, 1/4-in., 2x50         15     8       0.00
1558-QW1 Hrd. cloth, 1/2-in., 3x50         23     5       0.00
2232/QTY B&D jigsaw, 12-in. blade           8     5       0.05
2232/QWE B&D jigsaw, 8-in. blade            6     7       0.05
2238/QPD B&D cordless drill, 1/2-in.       12     5       0.05
23109-HB Claw hammer                       23    10       0.10
23114-AA Sledge hammer, 12 lb.              8    10       0.05
54778-2T Rat-tail file, 1/8-in. fine       43    20       0.00
89-WRE-Q Hicut chain saw, 16 in.           11     5       0.05
PUC23DRT PVC pipe, 3.5-in., 8-ft          188    75       0.00
SM-18277 1.25-in. metal screw, 25         172    75       0.00
SW-23116 2.5-in. wd. screw, 50            237   100       0.00
WR3/TT3  Steel matting, 4'x8'x1/6", .5"    18     5       0.10

16 rows selected.

SQL> EXEC PRC_PROD_DISCOUNT;
* Update finished *

PL/SQL procedure successfully completed.

SQL> SELECT P_CODE, P_DESCRIPT, P_QOH, P_MIN, P_DISCOUNT FROM PRODUCT;

P_CODE   P_DESCRIPT                     P_QOH P_MIN P_DISCOUNT
 
11QER/31 Power painter, 15 psi., 3-nozz    29     5       0.05
13-Q2/P2 7.25-in. pwr. saw blade           32    15       0.10
14-Q1/L3 9.00-in. pwr. saw blade           18    12       0.00
1546-QQ2 Hrd. cloth, 1/4-in., 2x50         15     8       0.00
1558-QW1 Hrd. cloth, 1/2-in., 3x50         23     5       0.05
2232/QTY B&D jigsaw, 12-in. blade           8     5       0.05
2232/QWE B&D jigsaw, 8-in. blade            6     7       0.05
2238/QPD B&D cordless drill, 1/2-in.       12     5       0.10
23109-HB Claw hammer                       23    10       0.15
23114-AA Sledge hammer, 12 lb.              8    10       0.05
54778-2T Rat-tail file, 1/8-in. fine       43    20       0.05
89-WRE-Q Hicut chain saw, 16 in.           11     5       0.10
PUC23DRT PVC pipe, 3.5-in., 8-ft          188    75       0.05
SM-18277 1.25-in. metal screw, 25         172    75       0.05
SW-23116 2.5-in. wd. screw, 50            237   100       0.05
WR3/TT3  Steel matting, 4'x8'x1/6", .5"    18     5       0.15

16 rows selected.

SQL>

```

Cengage Learning © 2015

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

#### Stored functions

Reminder – these can RETURN a value.

#### PL/SQL Stored Functions

- **Stored function:** Named group of procedural and SQL statements that returns a value
  - As indicated by a RETURN statement in its program code
- Can be invoked only from within stored procedures or triggers

```
CREATE FUNCTION function_name (argument IN data-type, ...) RETURN data-type [IS]
BEGIN
    PL/SQL statements;
    ...
    RETURN (value or expression);
END;
```

Once such a function is defined, it can be CALLED inside triggers or in stored procedures..

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

The following is an example from  
<http://www.tutorialspoint.com/plsql>.  
Creating/defining a function:

```
FUNCTION findMax(x IN number, y IN number)
RETURN number
IS
    z number;
BEGIN
    IF x > y THEN
        z := x;
    ELSE
        z := y;
    END IF;

    RETURN z;
END;
```

#### Calling/executing/running the function:

```
DECLARE
    a number;
    b number;
    c number;
BEGIN
    a := 23;
    b := 45;

    c := findMax(a, b);
    dbms_output.put_line(' Maximum of (23,45): '
|| c);
END;
/
```

#### Result:

Maximum of (23,45): 45

### Wrap - and fut...

We went through a LOT of SQL! As you could see, SQL offers elegant ways to manipulate (create/modify/delete, and more importantly, query) structured data.

Where is this all going, "given agentic AI"? Here is a glimpse:

- <https://www.youtube.com/watch?v=skCV9BEmjbo> - TiDB in 3 min
- [a writeup](#), and a [brief](#)
- [scrshot1](#), [scrshot2](#)



![](1ced737a3eeca5ab275642da3e5b996e_img.jpg)![](57302a491521a084f79994df3ea42df7_img.jpg)

# TM[Transaction Management]

![](71e137816b04eee83d7e7d3d801c77c2_img.jpg)

**A different kind of TM :)**

## Ch.10

11e

Database Systems  
Design, Implementation, and Management

![](0a6f460089e77a95cab9f66d7624ae47_img.jpg)

Coronel | Morris

Chapter 10  
Transaction Management and  
Concurrency Control

### What is a 'transaction'?

### Transaction

- Logical unit of work that must be **entirely** completed or aborted
- Consists of:
  - SELECT statement
  - Series of related UPDATE statements
  - Series of INSERT statements
  - Combination of SELECT, UPDATE, and INSERT statements

### Transaction

- **Consistent database state:** All data integrity constraints are satisfied
  - Must begin with the database in a known consistent state to ensure consistency
- Formed by two or more database requests
  - **Database requests:** Equivalent of a single SQL statement in an application program or transaction
- Consists of a single SQL statement or a collection of related SQL statements

#### 'ACID'

'ACID' (+S) is an acronym to express the desirable properties of a transaction:

![](2de302a7002e3a73e2da68f075f39286_img.jpg)

### COMMIT, ROLLBACK

### Transaction Management with SQL

- SQL statements that provide transaction support
  - COMMIT
  - ROLLBACK
- Transaction sequence must continue until:
  - COMMIT statement is reached
  - ROLLBACK statement is reached
  - End of program is reached
  - Program is abnormally terminated

#### Tracking updates

### Transaction Log

- Keeps track of all transactions that update the database
- DBMS uses the information stored in a log for:
  - Recovery requirement triggered by a ROLLBACK statement
  - A program's abnormal termination
  - A system failure

A Transaction Log

| TRL_ID | TRX_NUM | PREV_PTR | NEXT_PTR | OPERATION | TABLE                   | ROW ID   | ATTRIBUTE    | BEFORE VALUE | AFTER VALUE |
| ------ | ------- | -------- | -------- | --------- | ----------------------- | -------- | ------------ | ------------ | ----------- |
| 341    | 101     | Null     | 352      | START     | ****Start Transaction   |          |              |              |             |
| 352    | 101     | 341      | 363      | UPDATE    | PRODUCT                 | 1558-QW1 | PROD_QOH     | 25           | 23          |
| 363    | 101     | 352      | 365      | UPDATE    | CUSTOMER                | 10011    | CUST_BALANCE | 525.75       | 615.73      |
| 365    | 101     | 363      | Null     | COMMIT    | **** End of Transaction |          |              |              |             |

↑  
 TRL\_ID = Transaction log record ID  
 TRX\_NUM = Transaction number  
 PTR = Pointer to a transaction log record ID  
 (Note: The transaction number is automatically assigned by the DBMS.)

Cengage Learning © 2015

### Concurrency - 'many at once'

### Concurrency Control

- Coordination of the simultaneous transactions execution in a multiuser database system
- Objective - Ensures serializability of transactions in a multiuser database environment

### Problems in Concurrency Control

#### Lost update

- Occurs in two concurrent transactions when:
  - Same data element is **updated**
  - One of the updates is lost

#### Uncommitted data

- Occurs when:
  - Two transactions are executed concurrently
  - First transaction is rolled back after the second transaction has already **accessed** uncommitted data

#### Inconsistent retrievals

- Occurs when a transaction **accesses** data before and after one or more other transactions finish working with such data

#### Serial transactions - never a problem!

Consider the following pair of transactions, starting with 35 units of an item:  
purchase 100 units, then sell 30 units:

| TRANSACTION            | COMPUTATION                   |
| ---------------------- | ----------------------------- |
| T1: Purchase 100 units | $PROD\_QOH = PROD\_QOH + 100$ |
| T2: Sell 30 units      | $PROD\_QOH = PROD\_QOH - 30$  |

Cengage Learning © 2015

| TIME | TRANSACTION | STEP                   | STORED VALUE |
| ---- | ----------- | ---------------------- | ------------ |
| 1    | T1          | Read PROD_QOH          | 35           |
| 2    | T1          | $PROD\_QOH = 35 + 100$ |              |
| 3    | T1          | Write PROD_QOH         | 135          |
| 4    | T2          | Read PROD_QOH          | 135          |
| 5    | T2          | $PROD\_QOH = 135 - 30$ |              |
| 6    | T2          | Write PROD_QOH         | 105          |

Cengage Learning © 2015

If the transactions T1 and T2 happen one after another (ie. serially, not concurrently), the PROD\_QOH value would/should be 105, as shown above.

Three different kinds of errors are possible, when interleaved transactions are not handled properly.

#### Error #1: lost updates

'Lost update' problem:

| TIME | TRANSACTION | STEP                         | STORED VALUE |
| ---- | ----------- | ---------------------------- | ------------ |
| 1    | T1          | Read PROD_QOH                | 35           |
| 2    | T2          | Read PROD_QOH                | 35           |
| 3    | T1          | $PROD\_QOH = 35 + 100$       |              |
| 4    | T2          | $PROD\_QOH = 35 - 30$        |              |
| 5    | T1          | Write PROD_QOH (lost update) | 135          |
| 6    | T2          | Write PROD_QOH               | 5            |

Cengage Learning © 2015

Here, instead of 105, our QOH comes out to be 5, which is incorrect.

#### Error #2: reading uncommitted data

Consider this rollback situation:

| TRANSACTION            | COMPUTATION                                 |
| ---------------------- | ------------------------------------------- |
| T1: Purchase 100 units | $PROD\_QOH = PROD\_QOH + 100$ (Rolled back) |
| T2: Sell 30 units      | $PROD\_QOH = PROD\_QOH - 30$                |

Cengage Learning © 2015

Proper rollback (with sequential transactions):

| TIME | TRANSACTION | STEP                   | STORED VALUE |
| ---- | ----------- | ---------------------- | ------------ |
| 1    | T1          | Read PROD_QOH          | 35           |
| 2    | T1          | $PROD\_QOH = 35 + 100$ |              |
| 3    | T1          | Write PROD_QOH         | 135          |
| 4    | T1          | *****ROLLBACK*****     | 35           |
| 5    | T2          | Read PROD_QOH          | 35           |
| 6    | T2          | $PROD\_QOH = 35 - 30$  |              |
| 7    | T2          | Write PROD_QOH         | 5            |

Cengage Learning © 2015

Here the total is 5, which is correct - the QOH goes from 35 to 135, gets rolled back to 35, after which the purchase (of 30 units) happens.

'Uncommitted data' problem (improper rollback):

| TIME | TRANSACTION | STEP                                     | STORED VALUE |
| ---- | ----------- | ---------------------------------------- | ------------ |
| 1    | T1          | Read PROD_QOH                            | 35           |
| 2    | T1          | $PROD\_QOH = 35 + 100$                   |              |
| 3    | T1          | Write PROD_QOH                           | 135          |
| 4    | T2          | Read PROD_QOH<br>(Read uncommitted data) | 135          |
| 5    | T2          | $PROD\_QOH = 135 - 30$                   |              |
| 6    | T1          | *****ROLLBACK*****                       | 35           |
| 7    | T2          | Write PROD_QOH                           | 105          |

Cengage Learning © 2015

Here, the total comes out to 105, when it should have been 5.

#### Error #3: improper [premature] retrieval

Consider the following fix (of a typo made earlier - an incorrect order of 10 units was placed for 1558-QW1 by mistake, instead of ordering 1546-QQ2; now we're fixing that error):

| TRANSACTION T1                       | TRANSACTION T2                                               |
| ------------------------------------ | ------------------------------------------------------------ |
| SELECT SUM(PROD_QOH)<br>FROM PRODUCT | UPDATE PRODUCT<br>SET PROD_QOH = PROD_QOH + 10<br>WHERE PROD_CODE = 1546-QQ2 |
|                                      | UPDATE PRODUCT<br>SET PROD_QOH = PROD_QOH - 10<br>WHERE PROD_CODE = 1558-QW1 |
|                                      | COMMIT;                                                      |

Cengage Learning © 2015

In the above, T1 is a transaction that sums up QOH; T2 is the 'correction' transaction (that fixes the incorrect purchasing).

Proper retrieval of modified data:

| PROD_CODE    | BEFORE<br>PROD_QOH | AFTER<br>PROD_QOH |
| ------------ | ------------------ | ----------------- |
| 11QER/31     | 8                  | 8                 |
| 13-Q2/P2     | 32                 | 32                |
| 1546-QQ2     | 15                 | (15 + 10) → 25    |
| 1558-QW1     | 23                 | (23 - 10) → 13    |
| 2232-QTY     | 8                  | 8                 |
| 2232-QWE     | 6                  | 6                 |
| <b>Total</b> | <b>92</b>          | <b>92</b>         |

Cengage Learning © 2015

The summing transaction gets proper totals for both affected products, so the total (of 92) is correct.

'Inconsistent retrievals' problem (improper ("before update") retrieval of modified data):

| TIME | TRANSACTION | ACTION                                    | VALUE | TOTAL       |
| ---- | ----------- | ----------------------------------------- | ----- | ----------- |
| 1    | T1          | Read PROD_QOH for PROD_CODE = '11QER/31'  | 8     | 8           |
| 2    | T1          | Read PROD_QOH for PROD_CODE = '13-Q2/P2'  | 32    | 40          |
| 3    | T2          | Read PROD_QOH for PROD_CODE = '1546-QQ2'  | 15    |             |
| 4    | T2          | PROD_QOH = 15 + 10                        |       |             |
| 5    | T2          | Write PROD_QOH for PROD_CODE = '1546-QQ2' | 25    |             |
| 6    | T1          | Read PROD_QOH for PROD_CODE = '1546-QQ2'  | 25    | (After) 65  |
| 7    | T1          | Read PROD_QOH for PROD_CODE = '1558-QW1'  | 23    | (Before) 88 |
| 8    | T2          | Read PROD_QOH for PROD_CODE = '1558-QW1'  | 23    |             |
| 9    | T2          | PROD_QOH = 23 - 10                        |       |             |
| 10   | T2          | Write PROD_QOH for PROD_CODE = '1558-QW1' | 13    |             |
| 11   | T2          | ***** COMMIT *****                        |       |             |
| 12   | T1          | Read PROD_QOH for PROD_CODE = '2232-QTY'  | 8     | 96          |
| 13   | T1          | Read PROD_QOH for PROD_CODE = '2232-QWE'  | 6     | 102         |

Cengage Learning © 2015

T1 should be doing 65+13 (which would be correct), but instead does 65+23 (which makes it incorrect) - in other words, T1 retrieves the correct value (25) for 1546-QQ2, but gets the incorrect value (23) for 1558-QW1.

Inconsistent retrieval is also called a 'dirty read'.

Look up: non-repeatable reads, phantom row reads.

### Concurrent, serializable schedule

### The Scheduler

- Establishes the order in which the operations are executed within concurrent transactions
  - Interleaves the execution of database operations to ensure serializability and isolation of transactions
- Based on concurrent control algorithms to determine the appropriate order
- Creates serialization schedule
  - **Serializable schedule:** Interleaved execution of transactions yields the same results as the serial execution of the transactions

A serializable schedule makes concurrency immaterial (non-issue).

### Locking methods

### Concurrency Control with Locking Methods

- Locking methods - Facilitate isolation of data items used in concurrently executing transactions
- **Lock:** Guarantees exclusive use of a data item to a current transaction
- **Pessimistic locking:** Use of locks based on the assumption that conflict between transactions is likely
- **Lock manager:** Responsible for assigning and policing the locks used by the transactions

**TRL pessimistic 'lock' situations: restrooms, RCS, Robert's Rules Of Order..**

#### Locking: granularity

#### Lock Granularity

- Indicates the level of lock use
- Levels of locking
  - Database-level lock
  - Table-level lock
  - Page-level lock
    - Page or **diskpage**: Directly addressable section of a disk
  - Row-level lock
  - Field-level lock

Figure 10.3 - Database-Level Locking Sequence

![](5f7af51e0b3ffa52311e075a23684fe3_img.jpg)

Figure 10.4 - An Example of a Table-Level Lock

![](ecc2b08e0d193ae74ff8a8241a83fb01_img.jpg)

### Figure 10.5 - An Example of a Page-Level Lock

![](b7ad33d883b9848a765e0abcc9ddc938_img.jpg)

### Figure 10.6 - An Example of a Row-Level Lock

![](e80b1f0d2748dacbe9d5fc551da02feb_img.jpg)

#### Locking: types [unlocked, locked\_read, locked\_write]

#### Lock Types

##### Binary lock

- Has two states, locked (1) and unlocked (0)
- If an object is locked by a transaction, no other transaction can use that object
- If an object is unlocked, any transaction can lock the object for its use

##### Exclusive lock

- Exists when access is reserved for the transaction that locked the object

##### Shared lock

- Exists when concurrent transactions are granted read access on the basis of a common lock

##### Three lock states

- Using the shared/exclusive concept, there are THREE lock states: unlocked, shared (read), exclusive (write)

###### Read(shared), write(exclusive) lock:

##### Shared lock

- Issued when a transaction wants to READ data, and no exclusive lock is held (on a data item)

##### Exclusive lock

- Issued when a transaction wants to WRITE data, and no lock is held (on a data item)

#### '2PL'

#### Two-Phase Locking (2PL)

- Defines how transactions acquire and relinquish locks
- Guarantees serializability but does not prevent deadlocks
- Phases
  - Growing phase - Transaction acquires all required locks without unlocking any data
  - Shrinking phase - Transaction releases all locks and cannot obtain any new lock

**The 2PL type that we are discussing, where a transaction acquires all the locks it needs before processing starts, is called 'Conservative' 2PL (or 'Static' 2PL).**

**Once all the locks are acquired, a transaction can proceed 'smoothly', ie won't 'hang' or lead to dirty reads etc.**

**As for the middle point above (unlocking can't precede locking), here is a loose analogy:**

OK:

```
{
  {
    {
      {
        .....
      }
    }
  }
}
```

Not OK (OK in programming, though!):

```
{
  {
  }
  {
    {
      {
      }
    }
  }
}
```

Figure 10.7 - Two-Phase Locking Protocol

![](491c4b332cae19f28c7e922759c0f88b_img.jpg)

#### Deadlocks..

#### Deadlocks

- Occurs when two transactions wait indefinitely for each other to unlock data
  - Known as **deadly embrace**
- Control techniques
  - Deadlock prevention
  - Deadlock detection
  - Deadlock avoidance
- Choice of deadlock control method depends on database environment

- *Deadlock prevention.* A transaction requesting a new lock is aborted when there is the possibility that a deadlock can occur. If the transaction is aborted, all changes made by this transaction are rolled back and all locks obtained by the transaction are released. The transaction is then rescheduled for execution. Deadlock prevention works because it avoids the conditions that lead to deadlocking.
- *Deadlock detection.* The DBMS periodically tests the database for deadlocks. If a deadlock is found, the "victim" transaction is aborted (rolled back and restarted) and the other transaction continues.
- *Deadlock avoidance.* The transaction must obtain all of the locks it needs before it can be executed. This technique avoids the rolling back of conflicting transactions by requiring that locks be obtained in succession. However, the serial lock assignment required in deadlock avoidance increases action response times.

Here is how/why a deadlock occurs:

Table 10.13 - How a Deadlock Condition is Created

| TIME | TRANSACTION | REPLY | LOCK STATUS |          |
| ---- | ----------- | ----- | ----------- | -------- |
| 0    |             |       | Data X      | Data Y   |
| 1    | T1:LOCK(X)  | OK    | Unlocked    | Unlocked |
| 2    | T2:LOCK(Y)  | OK    | Locked      | Unlocked |
| 3    | T1:LOCK(Y)  | WAIT  | locked      | Locked   |
| 4    | T2:LOCK(X)  | WAIT  | locked      | Locked   |
| 5    | T1:LOCK(Y)  | WAIT  | locked      | Locked   |
| 6    | T2:LOCK(X)  | WAIT  | locked      | Locked   |
| 7    | T1:LOCK(Y)  | WAIT  | locked      | Locked   |
| 8    | T2:LOCK(X)  | WAIT  | locked      | Locked   |
| 9    | T1:LOCK(Y)  | WAIT  | locked      | Locked   |
| ...  | .....       | ..... |             | .....    |
| ...  | .....       | ..... |             | .....    |
| ...  | .....       | ..... |             | .....    |
| ...  | .....       | ..... |             | .....    |

Cengage Learning © 2015

In the above, we see that T1 locks X, T2 locks Y, then deadlock occurs because T1 wants Y and T2 wants X. Maybe you are thinking - why can't each of them release what they are holding (since they might be done with it), and grab what they want next (ie. T1 would release X, T2 would release Y)? BECAUSE THEY CAN'T - they NEED to access what the other has, BEFORE they can release what they have. Eg. T1 might

need to read Y that is locked by T2, in order to update its X; T2 might need T1's X to use in an expression to compare with its Y. **They need access to each other's resources, *\*\*before\*\** they can release their own! That is what causes deadlocking.**

Note that more than two transactions can become deadlocked as well, on account of 'circular' (cyclical) waiting.

Here's a humorous take on resolving deadlocking ('impasse') that can occur in human interactions.

---

2PL **avoids** deadlocks [by using cycle detection in the lock acquisition stage, and rolling back all-but-one transactions to release conflicting locks and assigning them to one so it can finish].

In contrast, timestamping-based schemes **prevent** deadlocks (see the 'Deadlock prevention' slide that follows).

##### Deadlock occurrence in 2PL

Earlier we noted that the 2PL scheme cannot prevent deadlock creation. Here is an example of how a deadlock could occur (at the end of step 5):

An important and unfortunate property of 2PL schedulers is that they are subject to *deadlocks*. For example, suppose a 2PL scheduler is processing transactions  $T_1$  and  $T_3$

$T_1: r_1[x] \rightarrow w_1[y] \rightarrow c_1$        $T_3: w_3[y] \rightarrow w_3[x] \rightarrow c_3$

and consider the following sequence of events:

1. Initially, neither transaction holds any locks.
2. The scheduler receives  $r_1[x]$  from the TM. It sets  $rl_1[x]$  and submits  $r_1[x]$  to the DM.
3. The scheduler receives  $w_3[y]$  from the TM. It sets  $wl_3[y]$  and submits  $w_3[y]$  to the DM.
4. The scheduler receives  $w_3[x]$  from the TM. The scheduler does not set  $wl_3[x]$  because it conflicts with  $rl_1[x]$  which is already set. Thus  $w_3[x]$  is **delayed**.
5. The scheduler receives  $w_1[y]$  from the TM. As in (4),  $w_1[y]$  must be **delayed**.

##### Deadlock prevention

##### Time Stamping

- Assigns global, unique time stamp to each transaction
  - Produces explicit order in which transactions are submitted to DBMS
- Properties
  - **Uniqueness**: Ensures no equal time stamp values exist
  - **Monotonicity**: Ensures time stamp values always increases

Here is one way to get monotonically increasing GUIDs..

##### Time Stamping

- Disadvantages
  - Each value stored in the database requires two additional stamp fields
  - Increases memory needs
  - Increases the database's processing overhead
  - Demands a lot of system resources

Deadlock] prevention using T/O - timestamp ordering:

##### Wait/Die and Wound/Wait Concurrency Control Schemes

Two different schemes (Wait or Die, Wound or Wait) for requesting access.

| TRANSACTION REQUESTING LOCK | TRANSACTION OWNING LOCK  | WAIT/DIE SCHEME<br>older/younger                             | WOUND/WAIT SCHEME<br>older/younger                           |
| --------------------------- | ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| T1 (11548789)<br>older      | T2 (19562545)<br>younger | <ul style="list-style-type: none"> <li>• T1 waits until T2 is completed and T2 releases its locks.</li> </ul> | <ul style="list-style-type: none"> <li>• T1 preempts/rolls back T2.</li> <li>• T2 is rescheduled using the same time stamp.</li> </ul> |
| T2 (19562545)<br>younger    | T1 (11548789)<br>older   | <ul style="list-style-type: none"> <li>• T2 dies (rolls back).</li> <li>• T2 is rescheduled using the same time stamp.</li> </ul> | <ul style="list-style-type: none"> <li>• T2 waits until T1 is completed and T1 releases its locks.</li> </ul> |

Cengage Learning © 2015

- Top row: older transaction requests a lock
- Bottom row: newer transaction is requesting

#### Deadlock 'indifference' ['fix-it-later']

#### Optimistic Concurrency Control (OCC):

![](d019f7011b290eab4ed0293f4972df51_img.jpg)

![](852f70019b8d1837b2a15c007a780f82_img.jpg)![](dbf3fdd95bc408437e1d396d9ea8befd_img.jpg)

## Distributed DBs

**what is distributed?**

**how are transactions managed?**

**what is the architecture?**

11e

**Database Systems**  
**Design, Implementation, and Management**

![](27d093344eaf2ffba7d815d186301dc7_img.jpg)

Coronel | Morris

Chapter 12

Distributed Database Management  
Systems

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

### C vs D

'Centralized' DBs - no longer popular/useful...

![](faa19fa09003307090f38a25ece74252_img.jpg)

### Factors Affecting the Centralized Database Systems

- Globalization of business operation
- Advancement of web-based services
- Rapid growth of social and network technologies
- Digitization resulting in multiple types of data
- Innovative business intelligence through analysis of data

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

6

Two factors in particular, necessitated change:

- rapid, ad-hoc access to data was needed ['Internet speed' decision-making]
- distributed data access was needed, to serve dispersed business units [globalization]

So now we have **DDBMSs - distributed DBMSs.**

**Distributed DBs - almost ALL (web-incl-cloud-based)!**

### Evolution Database Management Systems

- **Distributed database management system (DDBMS):** Governs storage and processing of logically related data over interconnected computer systems
  - Data and processing functions are distributed among several sites
- Centralized database management system
  - Required that corporate data be stored in a single central site
  - Data access provided through dumb terminals

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

4

### Factors That Aided DDBMS to Cope With Technological Advancement

Acceptance of Internet as a platform for business

Mobile wireless revolution

Usage of application as a service

Focus on mobile business intelligence

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

7

### Advantages and Disadvantages of DDBMS

#### Advantages

- Data are located near greatest demand site
- Faster data access and processing
- Growth facilitation
- Improved communications
- Reduced operating costs
- User-friendly interface
- Less danger of a single-point failure
- Processor independence

#### Disadvantages

- Complexity of management and control
- Technological difficulty
- Security
- Lack of standards
- Increased storage and infrastructure requirements
- Increased training cost
- Costs incurred due to the requirement of duplicated infrastructure

### Distributed \*processing\* vs distributed \*databases\*

### Distributed Processing and Distributed Databases

- **Distributed processing:** Database's logical processing is shared among two or more physically independent sites via network
- **Distributed database:** Stores logically related database over two or more physically independent sites via computer network
- **Database fragments:** Database composed of many parts in distributed database system

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

10

![](6a0568674e792609ca7e6c1533614862_img.jpg)

Cengage Learning © 2015

![](d1ba2b47c5ebc10187d8e9089eacca4d_img.jpg)

**Distributed processing AND data storage -> 'fully' distributed.**

### Functions of Distributed DBMS

- Receives the request of an application
- **Validates analyzes**, and decomposes the request
- Maps the request
- Decomposes request into several I/O operations
- Searches and validates data
- Ensures consistency, security, and integrity
- Validates data for specific conditions
- Presents data in required format

![](9ec7afb8bd1d2648de277cd79293d4c1_img.jpg)

**Two fragments, two sites - but each user thinks they have a single (their own) local version (transparent access).**

### TP(TM) vs DP(DM)

### DDBMS Components

- Computer workstations or remote devices
- Network hardware and software components
- Communications media
- **Transaction processor (TP):** Software component of a system that requests data
- Known as **transaction manager (TM)** or **application processor (AP)**
- **Data processor (DP)** or **data manager (DM)**
- **Software** component on a system that stores and retrieves data from its location

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

14

![](543dbf9a0f62120aacfce4baebce2b06_img.jpg)

A set of protocols is used by the DDBMS, to enable the TPs and DPs to communicate with each other.

**TP: Transaction Processor** - receives data requests (from an application), and requests data (from a DP); also known as AP (Application Processor) or TM (Transaction Manager). A TP is what fulfills data requests on behalf of a transaction.

**DP: Data Processor** - receives data requests from a TP (in general, multiple TPs can request data from a single DP), retrieves and returns the requested data; also known as **DM (Data Manager)**.

### Data and processing distribution: 3 variations

### 12.6 LEVELS OF DATA AND PROCESS DISTRIBUTION

Current database systems can be classified on the basis of how process distribution and data distribution are supported. For example, a DBMS may store data in a single site (using a centralized DB) or in multiple sites (using a distributed DB), and may support data processing at one or more sites. Table 12.2 uses a simple matrix to classify database systems according to data and process distribution. These types of processes are discussed in the sections that follow.

**TABLE 12.2 Database Systems: Levels of Data and Process Distribution**

|                       | SINGLE-SITE DATA                             | MULTIPLE-SITE DATA                              |
| --------------------- | -------------------------------------------- | ----------------------------------------------- |
| Single-site process   | Host DBMS                                    | Not applicable<br>(Requires multiple processes) |
| Multiple-site process | File server<br>Client/server DBMS (LAN DBMS) | Fully distributed<br>Client/server DDBMS        |

#### SP/SD

#### Single-Site Processing, Single-Site Data (SPSD)

- Processing is done on a single host computer
- Data stored on host computer's local disk
- Processing restricted on end user's side
- DBMS is accessed by dumb terminals

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

15

![](96954411d4782a218972e74ed4cd4495_img.jpg)

#### MP/SD [note: no SP/MD!]

#### Multiple-Site Processing, Single-Site Data (MPSD)

- Multiple processes run on different computers sharing a single data repository
- Require network file server running conventional applications
  - Accessed through LAN
- **Client/server architecture**
  - Reduces network traffic
  - Processing is distributed
  - Supports data at multiple sites

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

17

**Not truly 'distributed' (data I/O is centralized).**

![](710a9cf1a991f4226fbe1e73ea3cb6a6_img.jpg)

#### MP/MD ['fully distributed']

- Fully distributed database management system
  - Support multiple data processors and transaction processors at multiple sites
- Classification of DDBMS depending on the level of support for various types of databases
  - **Homogeneous**: Integrate multiple instances of same DBMS over a network
  - **Heterogeneous**: Integrate different types of DBMSs
  - **Fully heterogeneous**: Support different DBMSs, each supporting different data model

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

19

"The whole enchilada!".. Comes in three varieties.

![](ce40278b52f481852760dc1d6d474569_img.jpg)

The above schematic is same as the one you saw earlier..

**In a fully distributed database, the TPs (that request data) are distributed, as are the DPs (that serve data), like so [you saw this in an earlier slide]:**

![](12b3831f83d090aaff6aecb06354f250_img.jpg)

**The DDBMS uses protocols to transport across its network, commands as well as data, from distributed DPs and TPs: it receives data requests from multiple TPs, collects/synchronizes data (needed by multiple TPs) from multiple DPs, and intelligently routes to multiple TPs, the data (collected from multiple DPs) they requested. In other words, since transactions need data, the DDBMS acts as a switch, shuttling and routing data, from multiple DPs, to multiple TPs.**

### DDBMS restrictions

### Restrictions of DDBMS

- Remote access is provided on a read-only basis
- Restrictions on the number of remote tables that may be accessed in a single transaction
- Restrictions on the number of distinct databases that may be accessed
- Restrictions on the database model that may be accessed

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

20

**DDBMs span the spectrum from homegenous to fully heterogenous, and tend to come with restrictions.**

### Distributed concurrency control

#### Distributed Concurrency Control

- Concurrency control is important in distributed databases environment
  - Due to multi-site multiple-process operations that create inconsistencies and deadlocked transactions

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

26

**TP must ensure that all parts of a transaction (across sites) are completed, before doing a COMMIT.**

#### Problem!

![](4628881725ec2d73799a0521cb4036c5_img.jpg)

Can't COMMIT the entire transaction, can't ROLLBACK it either! Solution: **2PC**.

### Two-phase commit ("2PC") protocol

#### Two-Phase Commit Protocol (2PC)

- Guarantees if a portion of a transaction operation cannot be committed, all changes made at the other sites will be undone
  - To maintain a consistent database state
- Requires that each DP's transaction log entry be written before database fragment is updated
- **DO-UNDO-REDO protocol**: Roll transactions back and forward with the help of the system's transaction log entries

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

28

#### Two-Phase Commit Protocol (2PC)

- **Write-ahead protocol**: Forces the log entry to be written to permanent storage before actual operation takes place
- Defines operations between **coordinator** and **subordinates**
- Phases of implementation
  - Preparation
  - The final COMMIT

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

29

#### 2PC: steps

The following is the sequence of steps (phase I, phase2) that are used to effect a complete distributed transaction (keep clicking on the >| button):

Click anywhere to show/hide controls:  
 \* <<, >>: first/last frame  
 \* <\*1, >\*1: play once from curr, rev/fwd  
 \* <, >: play (loop) rev/fwd  
 \* <|, >|: prev/next frame  
 \* fps -/+ : decr/incr fps  
 \* ??: HUD toggle  
 \* ||: halt  
 Note — fps steps: 0.125,0.25,0.5,1,5,7,10,12,15,18,20,24,28,30

![](24798c5a4bf2c6cc826162e3668c4252_img.jpg)

And here's how a transaction is aborted, when one of the participating nodes is unable to commit a sub-transaction:

Click anywhere to show/hide controls:  
 \* <<, >>: first/last frame  
 \* <\*1, >\*1: play once from curr, rev/fwd  
 \* <, >: play (loop) rev/fwd  
 \* <|, >|: prev/next frame  
 \* fps -/+ : decr/incr fps  
 \* ??: HUD toggle  
 \* ||: halt  
 Note — fps steps: 0.125,0.25,0.5,1,5,7,10,12,15,18,20,24,28,30

![](4839b8dd9d072ebd0ca746f0f3fef8f9_img.jpg)

In the two phase commit protocol, as the name implies, there are two phases:

- phase I: commit request phase, aka 'voting' phase: coordinator sends a 'commit or abort?' (aka 'query to commit' or 'prepare to commit') message to each participating transaction node; each node responds (votes), with a 'can commit' (aka 'ready') or 'need to abort' (aka 'abort') message
- phase 2: commit phase, aka 'completion' phase:
  - if in phase I, all nodes responded with 'can commit', the coordinator sends a 'commit' phase to each node; each node commits, and sends an

- acknowledgment to the coordinator**
- **or, if in phase I, any node responded with 'need to abort', the coordinator sends an 'abort' message to each node; each node aborts, and sends an acknowledgment to the coordinator**

**The devil's in the details - all sorts of variations/refinements exist in implementations, but the above is the overall (simple, robust) idea.**

**It's an all-or-nothing scheme - either all nodes of a distributed transaction locally commit (in which case the overall transaction is successful), or all of them locally abort so that the DB is not left in an inconsistent state unlike in the 'Problem!' slide (in which case the overall transaction fails and needs to be redone).**

**FYI, this is yet another description :)**

### "What distribution? We have NO distribution!"

![](34921caa1996eef32dd520e93a1e64b8_img.jpg)

DDBMSs are designed to HIDE distribution specifics - this feature is called 'transparency', and can be classified into different kinds.

![](5f445e5f4b652a887cab7ede472eba7d_img.jpg)

**Fragmentation transparency:** end user does not know that the data is fragmented.

**Location transparency:** end user does not know where fragments are located.

**Location mapping transparency:** end user does not know how fragments are mapped.

**Distrib. transparency** is supported via a distributed data dictionary (DDD) [aka DDC], which contains the distributed global schema which local TPs use to translate user requests for processing by DPs.

### Performance and Failure Transparency

- **Performance transparency:** Allows a DDBMS to perform as if it were a centralized database
- **Failure transparency:** Ensures the system will operate in case of network failure
- Considerations for resolving requests in a distributed data environment
  - Data distribution
  - Data replication
    - **Replica transparency:** DDBMS's ability to hide multiple copies of data from the user

### Performance and Failure Transparency

- Network and node availability
  - **Network latency:** delay imposed by the amount of time required for a data packet to make a round trip
  - **Network partitioning:** delay imposed when nodes become suddenly unavailable due to a network failure

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

31

**We also need to take into account, network delay and network failure ("partitioning") when planning for or evaluating transparency.**

### Transaction Transparency

- Ensures database transactions will maintain distributed database's integrity and consistency
- Ensures transaction completed only when all database sites involved complete their part
- Distributed database systems require complex mechanisms to manage transactions

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

24

### Distributed DB design

## Distributed Database Design

- Data fragmentation**
  - How to partition database into fragments
- Data replication**
  - Which fragments to replicate
- Data allocation**
  - Where to locate those fragments and replicas

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

32

**Partition (divide), replicate (copy)? Where to store the partitions/copies?**

### Fragmentation (partitioning)

#### Data Fragmentation

- Breaks single object into many segments
  - Information is stored in distributed data catalog (DDC)
- Strategies
  - **Horizontal fragmentation:** Division of a relation into subsets (fragments) of tuples (rows)
  - **Vertical fragmentation:** Division of a relation into attribute (column) subsets
  - **Mixed fragmentation:** Combination of horizontal and vertical strategies

#### Replication

#### Data Replication

- Data copies stored at multiple sites served by a computer network
- **Mutual consistency rule:** Replicated data fragments should be identical
- Styles of replication
  - Push replication
  - Pull replication
- Helps restore lost data

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

34

#### Data Replication Scenarios

##### Fully replicated database

- Stores multiple copies of each database fragment at multiple sites

##### Partially replicated database

- Stores multiple copies of some database fragments at multiple sites

##### Unreplicated database

- Stores each database fragment at a single site

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

35

You can read more about replication, [here](#).

#### Storage of fragments/replicas

### Data Allocation Strategies

#### Centralized data allocation

- Entire database stored at one site

#### Partitioned data allocation

- Database is divided into two or more disjointed fragments and stored at two or more sites

#### Replicated data allocation

- Copies of one or more database fragments are stored at several sites

### The CAP 'theorem' [2 out of 3; 1 out of 2]

#### The CAP Theorem

- CAP stands for:
  - Consistency
  - Availability
  - Partition tolerance
- **Basically available, soft state, eventually consistent (BASE)**
  - Data changes are not immediate but propagate slowly through the system until all replicas are consistent

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

37

**Consistency:** always correct data.

**Availability:** requests are always filled.

**Partition ("outage") tolerance:** continue to operate even if (some/most) nodes fail.

The CAP theorem 'used to say' that in a networked (distributed) DB system, at most 2 out of 3 of the above are achievable [PC, CA, or PA]. But CA means low P, that means that we can't even operate, which makes CA a moot point! In other words, **CA doesn't exist**, ie. a low P is not an option! So now we think of it differently: in the event of a network partition (P has occurred), only one of availability or consistency is achievable. You can read more [here](#).

In the 'ACID' (Atomicity, Consistency, Isolation, Durability) world of older relational DBs, the CAP Theorem was a reminder that it is usually difficult to achieve C,A,P all at once, and that consistency is more important than availability.

In today's 'BASE' (Basically Available, Soft\_state, Eventually\_consistent) model of non-relational (eg. NoSQL) DBs, we prefer to sacrifice consistency in favor of availability.

| DBMS TYPE              | CONSISTENCY                                                 | AVAILABILITY | PARTITION TOLERANCE | TRANSACTION MODEL | TRADE-OFF                                     |
| ---------------------- | ----------------------------------------------------------- | ------------ | ------------------- | ----------------- | --------------------------------------------- |
| Centralized DBMS       | High                                                        | High         | N/A                 | ACID              | No distributed data processing                |
| Relational DDBMS (2PC) | High                                                        | Relaxed      | High                | ACID              |                                               |
|                        | Sacrifices availability to ensure consistency and isolation |              |                     |                   |                                               |
| NoSQL DDBMS            | Relaxed                                                     | High         | High                | BASE              | Sacrifices consistency to ensure availability |

Cengage Learning © 2015

Eric Brewer came up with CAP - here is his 2000 presentation on it [look at the slide on page 4!], and here is his update on it more than a decade later.

See this, and this for more.

### Date's '12 commandments' for distributed DBMSs

| RULE NUMBER | RULE NAME                                 | RULE EXPLANATION                                             |
| ----------- | ----------------------------------------- | ------------------------------------------------------------ |
| 1           | <i>Local-site independence</i>            | Each local site can act as an independent, autonomous, centralized DBMS. Each site is responsible for security, concurrency control, backup, and recovery. |
| 2           | <i>Central-site independence</i>          | No site in the network relies on a central site or any other site. All sites have the same capabilities. |
| 3           | <i>Failure independence</i>               | The system is not affected by node failures. The system is in continuous operation even in the case of a node failure or an expansion of the network. |
| 4           | <i>Location transparency</i>              | The user does not need to know the location of data to retrieve those data. |
| 5           | <i>Fragmentation transparency</i>         | Data fragmentation is transparent to the user, who sees only one logical database. The user does not need to know the name of the database fragments to retrieve them. |
| 6           | <i>Replication transparency</i>           | The user sees only one logical database. The DDBMS transparently selects the database fragment to access. To the user, the DDBMS manages all fragments transparently. |
| 7           | <i>Distributed query processing</i>       | A distributed query may be executed at several different DP sites. Query optimization is performed transparently by the DDBMS. |
| 8           | <i>Distributed transaction processing</i> | A transaction may update data at several different sites, and the transaction is executed transparently. |
| 9           | <i>Hardware independence</i>              | The system must run on any hardware platform.                |
| 10          | <i>Operating system independence</i>      | The system must run on any operating system platform.        |
| 11          | <i>Network independence</i>               | The system must run on any network platform.                 |
| 12          | <i>Database independence</i>              | The system must support any vendor's database product.       |

Think of these more as checklist items, rather than commandments.

1/12 9:36:11 \*\*\*

![](0a1144412c3d8c3cebb87477007b84eb_img.jpg)![](aadfab5cbe068adc0353a761a185ff6b_img.jpg)

## Database connectivity

## Ch.14

11e

**Database Systems**  
**Design, Implementation, and Management**

![](2b39cfde3d5d5b789d8be1e2a0e372a2_img.jpg)

Coronel | Morris

Chapter 14  
Database Connectivity and Web  
Technologies

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

## Learning Objectives

- In this chapter, students will learn:
  - About various database connectivity technologies
  - How Web-to-database middleware is used to integrate databases with the Internet
  - About Web browser plug-ins and extensions
  - What services are provided by Web application servers
  - What Extensible Markup Language (XML) is and why it is important for Web database development
  - About cloud computing and how it enables the database-as-a-service model

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

2

### Early days

### Database Connectivity

- **Database middleware:** Provides an interface between the application program and the database
- Data repository/source - Data management application (eg. Oracle RDBMS) that is used to store data generated by an application program

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

3

### Various connectivity options

- Native SQL (provided by vendors)
- M'soft: ODBC, DAO+JET, RDO
- M'soft: OLE-DB
- M'soft: ADO.NET
- JDBC (from Sun)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

4

### Native SQL Connectivity

- Connection interface provided by database vendors, which is unique to each vendor
- Interfaces are optimized for particular vendor's DBMS
- Maintenance is a burden for the programmer

### Microsoft: UDA, ODBC

#### 'UDA'

**Microsoft's Universal Data Access (UDA):** Collection of technologies used to access any type of data source and manage the data through a common interface

ODBC, OLE-DB and ADO.NET form the backbone of the MS UDA architecture

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

5

[and this is a contemporary 'UDA' :)]

#### ODBC, DAO+Jet, RDO

- **Open Database Connectivity (ODBC):** Microsoft's implementation of a superset of SQL Access Group **Call Level Interface (CLI)** standard for database access
  - Widely supported database connectivity interface
  - Allows Windows application to access relational data sources by using SQL via standard **application programming interface (API)**
  - Too much of a 'low level' API, so need something more

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

7

#### ODBC, DAO+Jet, RDO

- **Data Access Objects (DAO):** Object-oriented API used to access MS Access, MS FoxPro, and dBase databases from Visual Basic programs
  - Provides an optimized interface that expose functionality of **Jet** data engine to programmers
  - DAO interface can be used to access other relational style data sources as well

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

8

**JET: 'Joint Engine Technology', later became ACE.**

#### ODBC, DAO+Jet, RDO

- **Remote Data Objects (RDO)**
  - Higher-level object-oriented application interface used to access remote database servers
- **Dynamic-link libraries (DLLs)**
  - Implements ODBC, DAO, and RDO as shared code that is dynamically linked to the Windows operating environment

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

9

#### Components of ODBC Architecture

- High-level ODBC API through which application programs access ODBC functionality
- Driver manager that is in charge of managing all database connections
- ODBC driver that communicates directly to DBMS

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

10

## Figure 14.2 - Using ODBC, DAO, and RDO to access databases

![](5d18e168996dc3ae3f595f348261e80e_img.jpg)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

11

### Microsoft: OLE-DB

#### Object Linking and Embedding for Database (OLE-DB)

- Database middleware that adds object-oriented functionality for access to data
- Series of COM objects provides low-level database connectivity for applications
- Types of objects based on functionality
  - Consumers (request data)
  - Providers (produce data – from data sources)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

13

#### Object Linking and Embedding for Database (OLE-DB)

- Does not provide support for scripting languages
- **ActiveX Data Objects (ADO)**: Provides:
  - High-level application-oriented interface to interact with OLE-DB, DAO, and RDO
  - Unified interface to access data from any programming language that uses the underlying OLE-DB objects

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

14

**COM was modeled after OMG's CORBA... Here is more...**

# Figure 14.5 - OLE-DB Architecture

![](1f94fa97697122830275fb74bbe6f718_img.jpg)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

15

### Microsoft: ADO.NET;

#### ADO.NET

- Data access component of Microsoft's .NET application development framework (improves on the ADO + OLE-DB functionality)
- **Microsoft's .NET framework**
  - Component-based platform for developing distributed, heterogeneous, interoperable applications
  - Manipulates any type of data using any combination of network, operating system, and programming language

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

16

#### ADO.NET

- Features critical for the development of distributed applications
  - **DataSet**: Disconnected memory-resident representation of database
  - **XML support**
    - DataSet is internally stored in XML format
    - Data in DataSet could be made persistent as XML documents

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

17



#### Not-Microsoft: JDBC

#### Java Database Connectivity (JDBC)

- **Java:** Object-oriented programming language that runs on top of web browser software, on smartphones, on the desktop and on servers
- **JDBC:** Application programming interface that allows a Java program to interact with a wide range of data sources – a simple URL is all is needed to connect to a db

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

19

#### Advantages of JDBC

- Company can leverage existing technology and personnel training
- Allows direct access to database server or access via database middleware
- Allows programmers to use their SQL skills to manipulate the data in the company's databases
- Provides a way to connect to databases through an ODBC driver

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

20

Figure 14.7 - JDBC Architecture

![](470b612d7c5c8f18f60ddf220b78e272_img.jpg)

© 2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

23

Here is some sample code that uses the JDBC API:

```
public class HW2 {
    private Connection conn=null;
    private final String connection;
    private final String username;
    private final String password;
    private Statement stmt = null;

    HW2(String username,String password,String connection) {
        this.username = username;
        this.password = password;
        this.connection = connection;
    }

    void getDBConnection() {
        try {
            DriverManager.registerDriver(new oracle.jdbc.OracleDriver());
        } catch (SQLException ex) {
            System.out.println("Please install Oracle Driver.");
            return;
        }
        try {
            conn = DriverManager.getConnection(connection, username, password);
        } catch (SQLException e) {
            System.out.println(e);
            return;
        }
        if (conn != null) {
            System.out.println("Connection Succeeded.");
        } else {
            System.out.println("Connection failed.");
        }
    }

    public static void main(String[] args) {
        HW2 obj = new HW2("<Username>", "<Password>", "jdbc:oracle:thin:@localhost:1522:orcl");
        obj.getDBConnection();
        System.out.println("Test Exit.");
    }
}
```

© 2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

After we create a connection, we can create a statement, execute a query, get back a result set and iterate through it:

```
// create a connection via DriverManager.getConnection()
// ...

Statement myStmt = myConn.createStatement();

ResultSet myRslt= myStmt.executeQuery("....");
```

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

**Here is a complete example.**

### Internet connectivity! [aka 'full stack']

#### Database Internet Connectivity

- Allows new innovative services that:
  - Permit rapid response by bringing new services and products to market quickly
  - Increase customer satisfaction through creation of web-based support services
  - Allow anywhere, anytime data access using mobile smart devices via the Internet
  - Yield fast and effective information dissemination through universal access

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.24

**Why? One word: "e-Commerce" :)**

**Full stack encompasses:**

- **Frontend: UI**
- **Middleware: web server and associated components**
- **Backend: DB**

### Middleware

#### Web-to-Database Middleware

- Web server is the main hub through which Internet services are accessed
- **Server-side extension:** Program that interacts directly with the web server
  - Also known as **web-to-database middleware**
  - Provides its services to the web server in a way that is totally transparent to the client browser

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

27

#### Web-to-Database Middleware

![](136dccf3666a75086068fdbbf4a72c58_img.jpg)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

28



#### Middleware: server-adj.

Figure 14.9 - Web Server CGI and API Interfaces

![](4141e32339a99ae82b6360896250e1fc_img.jpg)

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

29

Here is Perl 'CGI' script to interface w/ a DB.

Here are notes on using CORBA to interface a webserver with a DB. These can also be used: JSP, ASP.

In addition to CGI scripts and APIs, server side includes (SSIs) can also be used for DB connectivity.

As an FYI note, Java provides very many ways to connect a client to a DB via a webserver: applets, sockets, servlets, RMI, CORBA, agents..

#### Middleware: stdalone

### Web Application Servers

- Middleware application that expands the functionality of web servers by linking them to a wide range of services
- Uses
  - Connect to and query database from web page
  - Create dynamic web search pages
  - Enforce referential integrity

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

32

**A 'web application server' is a specialized server that interfaces with web services such as databases, search engines. The client (eg browser) can query these data sources and have results generated dynamically.**

#### Features of Web Application Servers

- Security and user authentication
- Access to multiple services
- Integrated development environment
- Computational languages
- Automation generation of HTML pages
- Performance and fault - tolerant features
- Database access with transaction management capabilities

©2015 Cengage Learning. All Rights Reserved. May not be scanned, copied or duplicated, or posted to a publicly accessible website, in whole or in part.

33

**Examples of web application servers: WebLogic, ColdFusion/JRun, WebSphere Application Server, WebObjects, IIS, WildFly (JBoss), Tomcat, Jetty..**

**Each web application server (WAS) offers its own programming environment. Eg. CFML can be used to consume web services and present results for the end user (likewise for DB result sets).**

**Here is a ColdFusion syntax sample, and roundtrip dataflow:**



### Modern connectivity

**'MCC' [Microservices (including 'serverless'), Containers, Cloud] - is where things are [INCLUDING LLM-based apps!]. This makes the Internet a fully-distributed computing platform - via function calls that are chained across servers.**

**'WebAssembly' is also part of this vision.**

### Modern architecture styles:

Top 6 Most Popular API Architecture Styles

ByteByteGo.com

| Style     | Illustration | Use Cases                                    |
| --------- | ------------ | -------------------------------------------- |
| SOAP      |              | XML-based for enterprise applications        |
| RESTful   |              | Resource-based for web servers               |
| GraphQL   |              | Query language reduce network load           |
| gRPC      |              | High performance for microservices           |
| WebSocket |              | Bi-directional for low-latency data exchange |
| Webhook   |              | Asynchronous for event-driven application    |

Alex Xu • Following

Follow me for system design & ...

1h • Edited •

Top 6 most popular API architecture styles.

With billions of API calls made every day, understanding API architecture styles has never been more important. In this video, we take a closer look at these styles. They are the backbone of our interconnected digital world. We will talk about:

- SOAP
- RESTful
- GraphQL
- gRPC
- WebSocket
- Webhook

Watch & subscribe here: <https://lnkd.in/e2Jwg9w8>

...

Subscribe to our weekly newsletter to get a Free System Design PDF (158 pages): <https://bit.ly/42Ex9oZ>

#systemdesign #coding #interviewtips

![](7e8207b282f35e6bd6035d8fe543a775_img.jpg)

ByteByteGo  
230,288 followers  
2d •

What is GraphQL? Is it a replacement for the REST API?

The diagram below shows the quick comparison between REST and GraphQL.

- ◆ GraphQL is a query language for APIs developed by Meta. It provides a complete description of the data in the API and gives clients the power to ask for exactly what they need.
- ◆ GraphQL servers sit in between the client and the backend services.
- ◆ GraphQL can aggregate multiple REST requests into one query. GraphQL server organizes the resources in a graph.
- ◆ GraphQL supports queries, mutations (applying data modifications to resources), and subscriptions (receiving notifications on schema modifications).

### REST v.s. GraphQL

[blog.bytebytego.com](https://blog.bytebytego.com)

![](ea32354ab94fb7e4fdb2e08cb39b1846_img.jpg)

REST

![](746339de60a18834270b45f3928c3e8a_img.jpg)

GraphQL

![](3dfd0a5f4b8b5b87052f927cfda939dc_img.jpg)

Vladimir Romanov

#### Most Utilized API Architectures

![](a8e2aac7919c9dda82a304bfacc58dc8_img.jpg)

MQTT is a lightweight, publish-subscribe protocol optimized for low-bandwidth or unstable networks, often used in IoT applications.

![](e70285b7d75f2ab0c351640618082c0d_img.jpg)

SOAP is a protocol using XML for web services communication, typically over HTTP or SMTP.

![](b9416a482697626c9fdfb87263256c2c_img.jpg)

GraphQL uses one flexible endpoint for client-specified data, minimizes excess fetching, and provides structured results with schemas.

![](6aff6f81d7404196a8fb5521d5662aca_img.jpg)

A Webhook API enables real-time data communication by sending automated messages or payloads to specified URLs in response to events or triggers.

![](51c35ae4c2ca74c7fcbe9a0db1893dd5_img.jpg)

REST API is a set of conventions for building web services using standard HTTP methods, emphasizing stateless communication and resource-oriented URLs.

![](98daa92e8115229e723dab8e8ec5dbc6_img.jpg)

A WebSocket API allows for real-time, two-way communication between a client and server over a single, long-lived connection.

The top-3 cloud vendors (plus Oracle, IBM) offer a variety of (micro)services upon which businesses run:

![](603738e78a489658732e33631dd15f17_img.jpg)

Hot off the press: MCP.