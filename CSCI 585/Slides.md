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

##### Partial dependency, transitive dependency:

##### Types of Functional Dependencies

- **Partial dependency:** Functional dependence in which the determinant is only part of the primary key
  - Assumption - One candidate key
  - Straight forward
  - Easy to identify
- **Transitive dependency:** An attribute functionally depends on another nonkey attribute

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

In other words, "fill in the blanks" so that there are no nulls. Now we have an actual relation (table) [with a value in each cell - no more blanks].

Further, identify the PK! In our example, it is (PROJ\_NUM,EMP\_NUM).

##### ONF->INF [cont'd]

##### Conversion to First Normal Form

- **Dependency diagram:** Depicts all dependencies found within given table structure
  - Helps to get an overview of all relationships among table's attributes
  - Makes it less likely that an important dependency will be overlooked

**Create a **dependency diagram**, showing relationships (dependencies) between the attributes - this will help us systematically normalize the table.**

##### Dependency diagram

Indicate full dependencies on the top, and partial and transitive dependencies on the bottom. "Top good, bottom bad". Also, color the PK components in a different color (and underline them). Result:

<img src="Slides.assets/Screenshot 2026-06-09 at 4.11.22 PM.png" style="zoom:80%;" />

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

###### 1NF → 2NF: remove partial dependencies

##### Conversion to Second Normal Form

- Steps
  - Make new tables to eliminate partial dependencies
  - Reassign corresponding dependent attributes
- Table is in 2NF when it:
  - Is in 1NF
  - Includes no partial dependencies

###### 1NF->2NF [cont'd]

We eliminate partial dependencies by creating separate tables of such dependencies, and removing the dependent attributes from the starter table.

<img src="Slides.assets/Screenshot 2026-06-09 at 4.12.05 PM.png" style="zoom:80%;" />

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

###### 2NF->3NF [cont'd]

Figure 6.5 - Third Normal Form (3NF)  
Conversion Results

<img src="Slides.assets/Screenshot 2026-06-09 at 4.13.26 PM.png" style="zoom:80%;" />

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

##### Final result

Here is the result of making the "extra" changes to our 3NF form:

Figure 6.6 - The Completed Database

<img src="Slides.assets/Screenshot 2026-06-09 at 4.14.52 PM.png" style="zoom:80%;" />

##### Final result [cont'd]

Figure 6.6 - The Completed Database

<img src="Slides.assets/Screenshot 2026-06-09 at 4.15.37 PM.png" style="zoom:80%;" />





##### Final result [cont'd]

Figure 6.6 - The Completed Database

<img src="Slides.assets/Screenshot 2026-06-09 at 6.13.50 PM.png" alt="Screenshot 2026-06-09 at 6.13.50 PM" style="zoom:80%;" />

##### Final result [cont'd]

Figure 6.6 - The Completed Database

<img src="Slides.assets/Screenshot 2026-06-09 at 6.14.08 PM.png" alt="Screenshot 2026-06-09 at 6.14.08 PM" style="zoom:80%;" />

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

### Denormalization [cont'd]

#### Denormalization

- Defects in unnormalized tables
  - Data updates are less efficient because tables are larger
  - Indexing is more cumbersome
  - No simple strategies for creating virtual tables known as views

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.15.33 PM.png" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.15.57 PM.png" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.18.21 PM.png" alt="Screenshot 2026-06-09 at 6.18.21 PM" style="zoom:50%;" />

```
SELECT      P_DESCRIPT, P_QOH, P_PRICE, P_QOH * P_PRICE AS TOTVALUE
FROM        PRODUCT;
```
<img src="Slides.assets/Screenshot 2026-06-09 at 6.18.49 PM.png" alt="Screenshot 2026-06-09 at 6.18.49 PM" style="zoom:50%;" />

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

#### Logical (Boolean) operators

Figure 7.12 - Selected PRODUCT Table Attributes: The logical OR

<img src="Slides.assets/Screenshot 2026-06-09 at 6.19.28 PM.png" alt="Screenshot 2026-06-09 at 6.19.28 PM" style="zoom:50%;" />

```
SELECT P_DESCRIPT, P_INDATE, P_PRICE, V_CODE
FROM   PRODUCT
WHERE  V_CODE = 21344 OR V_CODE = 24288;
```

###### Figure 7.13 - Selected PRODUCT Table Attributes: The Logical AND

<img src="Slides.assets/Screenshot 2026-06-09 at 6.19.40 PM.png" alt="Screenshot 2026-06-09 at 6.19.40 PM" style="zoom:50%;" />

```
SELECT    P_DESCRIPTOR, P_INDATE, P_PRICE, V_CODE
FROM      PRODUCT
WHERE     P_PRICE < 50
AND       P_INDATE > '15-Jan-2014';
```

###### Figure 7.14 - Selected PRODUCT Table Attributes: The Logical AND and OR

<img src="Slides.assets/Screenshot 2026-06-09 at 6.20.20 PM.png" alt="Screenshot 2026-06-09 at 6.20.20 PM" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.23.09 PM.png" alt="Screenshot 2026-06-09 at 6.23.09 PM" style="zoom:80%;" />

**The sequence (listing) obtained by specifying several comma-separated attributes for ORDER BY is called a cascading order sequence.**

```
SELECT      EMP_LNAME, EMP_FNAME, EMP_INITIAL, EMP_AREACODE, EMP_PHONE
FROM        EMPLOYEE
ORDER BY    EMP_LNAME, EMP_FNAME, EMP_INITIAL;
```

<img src="Slides.assets/Screenshot 2026-06-09 at 6.23.38 PM.png" alt="Screenshot 2026-06-09 at 6.23.38 PM" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.24.02 PM.png" alt="Screenshot 2026-06-09 at 6.24.02 PM" style="zoom:50%;" />

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

#### Aggregate function examples

How many different vendors supply our products? How many supply cheap (PRICE < 10) products?

Note the third query below: COUNT(\*) counts the # of rows returned by a query (rows where the product costs < 10 units). In contrast, count() counts the # of non-null values of the column.

<img src="Slides.assets/Screenshot 2026-06-09 at 6.24.30 PM.png" style="zoom:50%;" />

What is the value for the most expensive item in the product table? Least expensive?

What is the most expensive item (details)? We can't do: WHERE P\_PRICE = MAX(P\_PRICE). This is because MAX() can only be used in a SELECT statement.

<img src="Slides.assets/Screenshot 2026-06-09 at 6.25.46 PM.png" alt="Screenshot 2026-06-09 at 6.25.46 PM" style="zoom:50%;" />

**Sum:**

<img src="Slides.assets/Screenshot 2026-06-09 at 6.26.27 PM.png" alt="Screenshot 2026-06-09 at 6.26.27 PM" style="zoom:50%;" />

**Avg:**

<img src="Slides.assets/Screenshot 2026-06-09 at 6.26.40 PM.png" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.27.04 PM.png" alt="Screenshot 2026-06-09 at 6.27.04 PM" style="zoom:50%;" />

You can think of 'GROUP BY' to mean "CATEGORIZE BY" or "ITEMIZE BY": rather than just a single MIN, MAX, SUM, COUNT or AVG, we're asking for a value PER OCCURRENCE of a GROUP BY value, eg. minimum price PER VENDOR, max GPA PER DEPARTMENT, average earnings PER MAJOR, etc. Specifically, when used with SUM(), GROUP BY is used to request subtotals.

The screenshot shows a SQL Plus window with the following content:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.27.22 PM.png" alt="Screenshot 2026-06-09 at 6.27.22 PM" style="zoom:50%;" />

'GROUP BY' used without an aggregate function is meaningless, since there is no aggregate value (MIN, COUNT etc.) to itemize.

Note that grouping by multiple columns simply means grouping by all occurrences (unique combinations, NOT product) of the values in those columns. Eg. in here, there are 91 customers [<https://www.w3schools.com/sql>]:

'SELECT COUNT(CustomerName) AS CustCount FROM Customers;' will give you 91 [ie. customers buying products].

'SELECT COUNT(CustomerName) AS CustCount FROM Customers GROUP BY Country;' will give you 21 rows (there are 21 countries with customers) whose counts add up to 91.

'SELECT COUNT(CustomerName) AS CustCount FROM Customers GROUP BY Country, City;' will give you 69 rows whose counts add up to 91 [there are 69 city, country combinations].

#### Store receipt

Here is a grocery store receipt where subtotals are displayed itemized, aggregated by product types DELI, GROCERY, MIXED NUTS and PRODUCE (presumably using SUM(), together with GROUP BY):

<img src="Slides.assets/Screenshot 2026-06-09 at 6.28.35 PM.png" alt="Screenshot 2026-06-09 at 6.28.35 PM" style="zoom:50%;" />

**While you're at it, see what other DATA you can spot in the receipt! Even a single trip to the store can generate a LOT of data.**

#### HAVING

The **HAVING** clause is used to filter rows in a **GROUP BY** specification (only those rows **HAVING** met the specified condition will appear in the result).

Note that **HAVING** can only occur in a query that has a **GROUP BY**, which in turn can only occur when there is an aggregate function (**MIN**, **MAX**, **SUM**, **COUNT** or **AVG**).

#### HAVING Clause

- Extension of **GROUP BY** feature
- Applied to output of **GROUP BY** operation
- Used in conjunction with **GROUP BY** clause in second SQL command set
- Similar to **WHERE** clause in **SELECT** statement

<img src="Slides.assets/Screenshot 2026-06-09 at 6.28.56 PM.png" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.29.23 PM.png" alt="Screenshot 2026-06-09 at 6.29.23 PM" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.29.53 PM.png" alt="Screenshot 2026-06-09 at 6.29.53 PM" style="zoom:80%;" />

#### Self-join example

<img src="Slides.assets/Screenshot 2026-06-09 at 6.30.25 PM.png" alt="Screenshot 2026-06-09 at 6.30.25 PM" style="zoom:80%;" />

Here is how the join works:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.30.35 PM.png" alt="Screenshot 2026-06-09 at 6.30.35 PM" style="zoom:80%;" />

Sooo... are joins 'evil'? Not really :)

### SQL is declarative, not imperative

Now that you're familiar with SQL syntax, you will appreciate knowing how it compares with a regular programming language such as C++. Shown below is such a comparison, using C# which lets us write code in an imperative (command-oriented) manner as well a declarative (result-oriented) one [this is from a book on functional programming]:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.31.00 PM.png" alt="Screenshot 2026-06-09 at 6.31.00 PM" style="zoom:80%;" />

### More SQL

# Chapter 8 Advanced SQL

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.33.21 PM.png" alt="Screenshot 2026-06-09 at 6.33.21 PM" style="zoom:80%;" />

##### Outer vs inner vs full ('both') JOINS

## Table 8.1 - SQL Join Expression Styles

<img src="Slides.assets/Screenshot 2026-06-09 at 6.33.39 PM.png" alt="Screenshot 2026-06-09 at 6.33.39 PM" style="zoom:80%;" />

##### Full (left+right outer) JOIN example

<img src="Slides.assets/Screenshot 2026-06-09 at 6.33.55 PM.png" alt="Screenshot 2026-06-09 at 6.33.55 PM" style="zoom:80%;" />

### 'SELECT' subqueries

<img src="Slides.assets/Screenshot 2026-06-09 at 6.34.32 PM.png" alt="Screenshot 2026-06-09 at 6.34.32 PM" style="zoom:50%;" />

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

**FIGURE 8.13** WHERE subquery example

<img src="Slides.assets/Screenshot 2026-06-09 at 6.34.52 PM.png" alt="Screenshot 2026-06-09 at 6.34.52 PM" style="zoom:50%;" />



##### IN, HAVING subqueries

##### IN and HAVING Subqueries

- IN subqueries
  - Used to compare a single attribute to a list of values
- HAVING subqueries
  - HAVING clause restricts the output of a GROUP BY query by applying conditional criteria to the grouped rows

**Compare against a LIST of values..**

<img src="Slides.assets/Screenshot 2026-06-09 at 6.37.34 PM.png" alt="Screenshot 2026-06-09 at 6.37.34 PM" style="zoom:50%;" />

As we saw earlier, this restricts the results of a GROUP BY clause. Eg. here's how to list all products sold, whose totals are greater than the average quantity sold:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.38.02 PM.png" alt="Screenshot 2026-06-09 at 6.38.02 PM" style="zoom:50%;" />

#### ALL, ANY (inequality comparisons)

Recall that 'IN' is an equality comparison against a list. To do **inequality comparison of a value against a list of values** (eg. need to be greater than ALL, need to be less than ANY..), use **ALL, ANY**.

#### Multirow Subquery Operators: ANY and ALL

- ALL operator
  - Allows comparison of a single value with a list of values returned by the first subquery
    - Uses a comparison operator other than equals
- ANY operator
  - Allows comparison of a single value to a list of values and selects only the rows for which the value is greater than or less than any value in the list

Eg. "which products do we own [in our store], whose value is more than ALL other products's values supplied by vendors in Florida?"

##### <img src="Slides.assets/Screenshot 2026-06-09 at 6.38.45 PM.png" alt="Screenshot 2026-06-09 at 6.38.45 PM" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.39.24 PM.png" alt="Screenshot 2026-06-09 at 6.39.24 PM" style="zoom:67%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.40.46 PM.png" alt="Screenshot 2026-06-09 at 6.40.46 PM" style="zoom:67%;" /><img src="Slides.assets/Screenshot 2026-06-09 at 6.45.36 PM.png" alt="Screenshot 2026-06-09 at 6.45.36 PM" style="zoom:67%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 6.46.54 PM.png" alt="Screenshot 2026-06-09 at 6.46.54 PM" style="zoom:80%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 6.47.18 PM.png" alt="Screenshot 2026-06-09 at 6.47.18 PM" style="zoom:67%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.48.53 PM.png" alt="Screenshot 2026-06-09 at 6.48.53 PM" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.49.23 PM.png" style="zoom:50%;" />

#### Queries: summary

We looked at several variations of queries and subqueries (SELECT, WHERE, HAVING, IN..).

Most interestingly, a SELECT subquery can appear at the top (SELECT), middle (FROM) or bottom (WHERE) of a parent query, which provides a flexible way to express **complex logic** (since such subqueries can be recursively nested):

<img src="Slides.assets/Screenshot 2026-06-09 at 6.49.48 PM.png" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.50.24 PM.png" alt="Screenshot 2026-06-09 at 6.50.24 PM" style="zoom:50%;" />

**NEXTVAL returns the current value, then does ++ (ie. it does 'post increment', ie. C++ as opposed to ++C); CURRVAL on the other hand, just fetches the current value (does not ++ it).**

<img src="Slides.assets/Screenshot 2026-06-09 at 6.50.48 PM.png" alt="Screenshot 2026-06-09 at 6.50.48 PM" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.51.23 PM.png" alt="Screenshot 2026-06-09 at 6.51.23 PM" style="zoom:50%;" />

### Triggers

#### Triggers

- Procedural SQL code automatically invoked by RDBMS when given data manipulation event occurs
- Parts of a trigger definition
  - Triggering timing - Indicates when trigger's PL/SQL code executes
  - Triggering event - Statement that causes the trigger to execute
  - Triggering level - **Statement-** and **row-level**
  - Triggering action - PL/SQL code enclosed between the BEGIN and END keywords

<img src="Slides.assets/Screenshot 2026-06-09 at 6.51.57 PM.png" alt="Screenshot 2026-06-09 at 6.51.57 PM" style="zoom:50%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 6.52.13 PM.png" style="zoom:50%;" />



<img src="Slides.assets/Screenshot 2026-06-09 at 6.52.51 PM.png" alt="Screenshot 2026-06-09 at 6.52.51 PM" style="zoom:50%;" />

Our trigger worked! [look at P\_REORDER]

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.53.13 PM.png" style="zoom:67%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 6.54.16 PM.png" alt="Screenshot 2026-06-09 at 6.54.16 PM" style="zoom:80%;" />

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

# TM[Transaction Management]

## Ch.10 Transaction Management and Concurrency Control

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.56.34 PM.png" style="zoom:67%;" />

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

 <img src="Slides.assets/Screenshot 2026-06-09 at 6.57.13 PM.png" alt="Screenshot 2026-06-09 at 6.57.13 PM" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 6.58.34 PM.png" alt="Screenshot 2026-06-09 at 6.58.34 PM" style="zoom:80%;" />

If the transactions T1 and T2 happen one after another (ie. serially, not concurrently), the PROD\_QOH value would/should be 105, as shown above.

Three different kinds of errors are possible, when interleaved transactions are not handled properly.

#### Error #1: lost updates

'Lost update' problem:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.59.01 PM.png" alt="Screenshot 2026-06-09 at 6.59.01 PM" style="zoom:67%;" />

Here, instead of 105, our QOH comes out to be 5, which is incorrect.

#### Error #2: reading uncommitted data

Consider this rollback situation:

<img src="Slides.assets/Screenshot 2026-06-09 at 6.59.27 PM.png" alt="Screenshot 2026-06-09 at 6.59.27 PM" style="zoom:80%;" />

Proper rollback (with sequential transactions):

<img src="Slides.assets/Screenshot 2026-06-09 at 6.59.38 PM.png" alt="Screenshot 2026-06-09 at 6.59.38 PM" style="zoom:80%;" />

Cengage Learning © 2015

Here the total is 5, which is correct - the QOH goes from 35 to 135, gets rolled back to 35, after which the purchase (of 30 units) happens.

'Uncommitted data' problem (improper rollback):

<img src="Slides.assets/Screenshot 2026-06-09 at 6.59.54 PM.png" alt="Screenshot 2026-06-09 at 6.59.54 PM" style="zoom:80%;" />

Here, the total comes out to 105, when it should have been 5.

#### Error #3: improper [premature] retrieval

Consider the following fix (of a typo made earlier - an incorrect order of 10 units was placed for 1558-QW1 by mistake, instead of ordering 1546-QQ2; now we're fixing that error):

<img src="Slides.assets/Screenshot 2026-06-09 at 7.00.19 PM.png" alt="Screenshot 2026-06-09 at 7.00.19 PM" style="zoom:80%;" />

Cengage Learning © 2015

In the above, T1 is a transaction that sums up QOH; T2 is the 'correction' transaction (that fixes the incorrect purchasing).

Proper retrieval of modified data:

<img src="Slides.assets/Screenshot 2026-06-09 at 7.00.33 PM.png" alt="Screenshot 2026-06-09 at 7.00.33 PM" style="zoom:80%;" />

The summing transaction gets proper totals for both affected products, so the total (of 92) is correct.

'Inconsistent retrievals' problem (improper ("before update") retrieval of modified data):

<img src="Slides.assets/Screenshot 2026-06-09 at 7.59.26 PM.png" alt="Screenshot 2026-06-09 at 7.59.26 PM" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 7.59.51 PM.png" style="zoom:80%;" />

Figure 10.4 - An Example of a Table-Level Lock

<img src="Slides.assets/Screenshot 2026-06-09 at 8.00.02 PM.png" style="zoom:80%;" />

### Figure 10.5 - An Example of a Page-Level Lock

<img src="Slides.assets/Screenshot 2026-06-09 at 8.00.11 PM.png" style="zoom:80%;" />

### Figure 10.6 - An Example of a Row-Level Lock

<img src="Slides.assets/Screenshot 2026-06-09 at 8.00.20 PM.png" style="zoom:80%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.00.49 PM.png" style="zoom:80%;" />

#### Deadlocks..

#### Deadlocks

- Occurs when two transactions wait indefinitely for each other to unlock data
  - Known as **deadly embrace**
- Control techniques
  - Deadlock prevention
  - Deadlock detection
  - Deadlock avoidance
- Choice of deadlock control method depends on database environment
- <img src="Slides.assets/Screenshot 2026-06-09 at 8.01.30 PM.png" alt="Screenshot 2026-06-09 at 8.01.30 PM" style="zoom:80%;" />

Here is how/why a deadlock occurs:

Table 10.13 - How a Deadlock Condition is Created

<img src="Slides.assets/Screenshot 2026-06-09 at 8.01.15 PM.png" alt="Screenshot 2026-06-09 at 8.01.15 PM" style="zoom:80%;" />

In the above, we see that T1 locks X, T2 locks Y, then deadlock occurs because T1 wants Y and T2 wants X. Maybe you are thinking - why can't each of them release what they are holding (since they might be done with it), and grab what they want next (ie. T1 would release X, T2 would release Y)? BECAUSE THEY CAN'T - they NEED to access what the other has, BEFORE they can release what they have. Eg. T1 might

need to read Y that is locked by T2, in order to update its X; T2 might need T1's X to use in an expression to compare with its Y. **They need access to each other's resources, *\*\*before\*\** they can release their own! That is what causes deadlocking.**

Note that more than two transactions can become deadlocked as well, on account of 'circular' (cyclical) waiting.

Here's a humorous take on resolving deadlocking ('impasse') that can occur in human interactions.

---

2PL **avoids** deadlocks [by using cycle detection in the lock acquisition stage, and rolling back all-but-one transactions to release conflicting locks and assigning them to one so it can finish].

In contrast, timestamping-based schemes **prevent** deadlocks (see the 'Deadlock prevention' slide that follows).

##### Deadlock occurrence in 2PL

Earlier we noted that the 2PL scheme cannot prevent deadlock creation. Here is an example of how a deadlock could occur (at the end of step 5):

<img src="Slides.assets/Screenshot 2026-06-09 at 8.06.15 PM.png" alt="Screenshot 2026-06-09 at 8.06.15 PM" style="zoom:67%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.06.41 PM.png" alt="Screenshot 2026-06-09 at 8.06.41 PM" style="zoom:80%;" />

- Top row: older transaction requests a lock
- Bottom row: newer transaction is requesting

#### Deadlock 'indifference' ['fix-it-later']

#### Optimistic Concurrency Control (OCC):

<img src="Slides.assets/Screenshot 2026-06-09 at 8.08.57 PM.png" style="zoom:50%;" />

## Distributed DBs

**what is distributed?**

**how are transactions managed?**

**what is the architecture?**

Distributed Database Management  
Systems

### C vs D

'Centralized' DBs - no longer popular/useful...

<img src="Slides.assets/Screenshot 2026-06-09 at 8.17.58 PM.png" style="zoom:67%;" />

### Factors Affecting the Centralized Database Systems

- Globalization of business operation
- Advancement of web-based services
- Rapid growth of social and network technologies
- Digitization resulting in multiple types of data
- Innovative business intelligence through analysis of data

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

### Factors That Aided DDBMS to Cope With Technological Advancement

Acceptance of Internet as a platform for business

Mobile wireless revolution

Usage of application as a service

Focus on mobile business intelligence

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.18.49 PM.png" style="zoom:67%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 8.19.03 PM.png" style="zoom:67%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.19.19 PM.png" style="zoom:67%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.19.29 PM.png" style="zoom:50%;" />

A set of protocols is used by the DDBMS, to enable the TPs and DPs to communicate with each other.

**TP: Transaction Processor** - receives data requests (from an application), and requests data (from a DP); also known as AP (Application Processor) or TM (Transaction Manager). A TP is what fulfills data requests on behalf of a transaction.

**DP: Data Processor** - receives data requests from a TP (in general, multiple TPs can request data from a single DP), retrieves and returns the requested data; also known as **DM (Data Manager)**.

### Data and processing distribution: 3 variations

<img src="Slides.assets/Screenshot 2026-06-09 at 8.19.47 PM.png" alt="Screenshot 2026-06-09 at 8.19.47 PM" style="zoom:50%;" />

#### SP/SD

#### Single-Site Processing, Single-Site Data (SPSD)

- Processing is done on a single host computer
- Data stored on host computer's local disk
- Processing restricted on end user's side
- DBMS is accessed by dumb terminals

<img src="Slides.assets/Screenshot 2026-06-09 at 8.20.16 PM.png" style="zoom:50%;" />

#### MP/SD [note: no SP/MD!]

#### Multiple-Site Processing, Single-Site Data (MPSD)

- Multiple processes run on different computers sharing a single data repository
- Require network file server running conventional applications
  - Accessed through LAN
- **Client/server architecture**
  - Reduces network traffic
  - Processing is distributed
  - Supports data at multiple sites

**Not truly 'distributed' (data I/O is centralized).**

<img src="Slides.assets/Screenshot 2026-06-09 at 8.20.34 PM.png" style="zoom:50%;" />

#### MP/MD ['fully distributed']

- Fully distributed database management system
  - Support multiple data processors and transaction processors at multiple sites
- Classification of DDBMS depending on the level of support for various types of databases
  - **Homogeneous**: Integrate multiple instances of same DBMS over a network
  - **Heterogeneous**: Integrate different types of DBMSs
  - **Fully heterogeneous**: Support different DBMSs, each supporting different data model

"The whole enchilada!".. Comes in three varieties.

<img src="Slides.assets/Screenshot 2026-06-09 at 8.20.46 PM.png" style="zoom:67%;" />

The above schematic is same as the one you saw earlier..

**In a fully distributed database, the TPs (that request data) are distributed, as are the DPs (that serve data), like so [you saw this in an earlier slide]:**

<img src="Slides.assets/Screenshot 2026-06-09 at 8.20.59 PM.png" style="zoom:50%;" />

**The DDBMS uses protocols to transport across its network, commands as well as data, from distributed DPs and TPs: it receives data requests from multiple TPs, collects/synchronizes data (needed by multiple TPs) from multiple DPs, and intelligently routes to multiple TPs, the data (collected from multiple DPs) they requested. In other words, since transactions need data, the DDBMS acts as a switch, shuttling and routing data, from multiple DPs, to multiple TPs.**

### DDBMS restrictions

### Restrictions of DDBMS

- Remote access is provided on a read-only basis
- Restrictions on the number of remote tables that may be accessed in a single transaction
- Restrictions on the number of distinct databases that may be accessed
- Restrictions on the database model that may be accessed

**DDBMs span the spectrum from homegenous to fully heterogenous, and tend to come with restrictions.**

### Distributed concurrency control

#### Distributed Concurrency Control

- Concurrency control is important in distributed databases environment
  - Due to multi-site multiple-process operations that create inconsistencies and deadlocked transactions

**TP must ensure that all parts of a transaction (across sites) are completed, before doing a COMMIT.**

#### Problem!

<img src="Slides.assets/Screenshot 2026-06-09 at 8.21.21 PM.png" style="zoom:50%;" />

Can't COMMIT the entire transaction, can't ROLLBACK it either! Solution: **2PC**.

### Two-phase commit ("2PC") protocol

#### Two-Phase Commit Protocol (2PC)

- Guarantees if a portion of a transaction operation cannot be committed, all changes made at the other sites will be undone
  - To maintain a consistent database state
- Requires that each DP's transaction log entry be written before database fragment is updated
- **DO-UNDO-REDO protocol**: Roll transactions back and forward with the help of the system's transaction log entries

#### Two-Phase Commit Protocol (2PC)

- **Write-ahead protocol**: Forces the log entry to be written to permanent storage before actual operation takes place
- Defines operations between **coordinator** and **subordinates**
- Phases of implementation
  - Preparation
  - The final COMMIT

#### 2PC: steps

The following is the sequence of steps (phase I, phase2) that are used to effect a complete distributed transaction (keep clicking on the >| button):

<img src="Slides.assets/Screenshot 2026-06-09 at 8.21.49 PM.png" alt="Screenshot 2026-06-09 at 8.21.49 PM" style="zoom:50%;" />

And here's how a transaction is aborted, when one of the participating nodes is unable to commit a sub-transaction:

<img src="Slides.assets/Screenshot 2026-06-09 at 8.22.09 PM.png" style="zoom:50%;" />

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

<img src="Slides.assets/Screenshot 2026-06-09 at 8.22.33 PM.png" style="zoom:50%;" />

DDBMSs are designed to HIDE distribution specifics - this feature is called 'transparency', and can be classified into different kinds.

<img src="Slides.assets/Screenshot 2026-06-09 at 8.22.42 PM.png" style="zoom:50%;" />

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

**We also need to take into account, network delay and network failure ("partitioning") when planning for or evaluating transparency.**

### Transaction Transparency

- Ensures database transactions will maintain distributed database's integrity and consistency
- Ensures transaction completed only when all database sites involved complete their part
- Distributed database systems require complex mechanisms to manage transactions

### Distributed DB design

## Distributed Database Design

- Data fragmentation**
  - How to partition database into fragments
- Data replication**
  - Which fragments to replicate
- Data allocation**
  - Where to locate those fragments and replicas

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

#### Data Replication Scenarios

##### Fully replicated database

- Stores multiple copies of each database fragment at multiple sites

##### Partially replicated database

- Stores multiple copies of some database fragments at multiple sites

##### Unreplicated database

- Stores each database fragment at a single site

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

**Consistency:** always correct data.

**Availability:** requests are always filled.

**Partition ("outage") tolerance:** continue to operate even if (some/most) nodes fail.

The CAP theorem 'used to say' that in a networked (distributed) DB system, at most 2 out of 3 of the above are achievable [PC, CA, or PA]. But CA means low P, that means that we can't even operate, which makes CA a moot point! In other words, **CA doesn't exist**, ie. a low P is not an option! So now we think of it differently: in the event of a network partition (P has occurred), only one of availability or consistency is achievable. You can read more [here](#).

In the 'ACID' (Atomicity, Consistency, Isolation, Durability) world of older relational DBs, the CAP Theorem was a reminder that it is usually difficult to achieve C,A,P all at once, and that consistency is more important than availability.

In today's 'BASE' (Basically Available, Soft\_state, Eventually\_consistent) model of non-relational (eg. NoSQL) DBs, we prefer to sacrifice consistency in favor of availability.

<img src="Slides.assets/Screenshot 2026-06-09 at 8.23.55 PM.png" alt="Screenshot 2026-06-09 at 8.23.55 PM" style="zoom:50%;" />

Eric Brewer came up with CAP - here is his 2000 presentation on it [look at the slide on page 4!], and here is his update on it more than a decade later.

See this, and this for more.

### Date's '12 commandments' for distributed DBMSs

<img src="Slides.assets/Screenshot 2026-06-09 at 8.24.14 PM.png" alt="Screenshot 2026-06-09 at 8.24.14 PM" style="zoom:50%;" />

Think of these more as checklist items, rather than commandments.

## Database connectivity

## Ch.14

**Database Systems**  
**Design, Implementation, and Management**

Chapter 14 
Database Connectivity and Web Technologies

## Learning Objectives

- In this chapter, students will learn:
  - About various database connectivity technologies
  - How Web-to-database middleware is used to integrate databases with the Internet
  - About Web browser plug-ins and extensions
  - What services are provided by Web application servers
  - What Extensible Markup Language (XML) is and why it is important for Web database development
  - About cloud computing and how it enables the database-as-a-service model

### Early days

### Database Connectivity

- **Database middleware:** Provides an interface between the application program and the database
- Data repository/source - Data management application (eg. Oracle RDBMS) that is used to store data generated by an application program

### Various connectivity options

- Native SQL (provided by vendors)
- M'soft: ODBC, DAO+JET, RDO
- M'soft: OLE-DB
- M'soft: ADO.NET
- JDBC (from Sun)

### Native SQL Connectivity

- Connection interface provided by database vendors, which is unique to each vendor
- Interfaces are optimized for particular vendor's DBMS
- Maintenance is a burden for the programmer

### Microsoft: UDA, ODBC

#### 'UDA'

**Microsoft's Universal Data Access (UDA):** Collection of technologies used to access any type of data source and manage the data through a common interface

ODBC, OLE-DB and ADO.NET form the backbone of the MS UDA architecture

**[and this is a contemporary 'UDA' :)]**

#### ODBC, DAO+Jet, RDO

- **Open Database Connectivity (ODBC):** Microsoft's implementation of a superset of SQL Access Group **Call Level Interface (CLI)** standard for database access
  - Widely supported database connectivity interface
  - Allows Windows application to access relational data sources by using SQL via standard **application programming interface (API)**
  - Too much of a 'low level' API, so need something more

#### ODBC, DAO+Jet, RDO

- **Data Access Objects (DAO):** Object-oriented API used to access MS Access, MS FoxPro, and dBase databases from Visual Basic programs
  - Provides an optimized interface that expose functionality of **Jet** data engine to programmers
  - DAO interface can be used to access other relational style data sources as well

**JET: 'Joint Engine Technology', later became ACE.**

#### ODBC, DAO+Jet, RDO

- **Remote Data Objects (RDO)**
  - Higher-level object-oriented application interface used to access remote database servers
- **Dynamic-link libraries (DLLs)**
  - Implements ODBC, DAO, and RDO as shared code that is dynamically linked to the Windows operating environment

#### Components of ODBC Architecture

- High-level ODBC API through which application programs access ODBC functionality
- Driver manager that is in charge of managing all database connections
- ODBC driver that communicates directly to DBMS

## Figure 14.2 - Using ODBC, DAO, and RDO to access databases

<img src="Slides.assets/Screenshot 2026-06-09 at 9.58.45 PM.png" style="zoom:75%;" />

### Microsoft: OLE-DB

#### Object Linking and Embedding for Database (OLE-DB)

- Database middleware that adds object-oriented functionality for access to data
- Series of COM objects provides low-level database connectivity for applications
- Types of objects based on functionality
  - Consumers (request data)
  - Providers (produce data – from data sources)

#### Object Linking and Embedding for Database (OLE-DB)

- Does not provide support for scripting languages
- **ActiveX Data Objects (ADO)**: Provides:
  - High-level application-oriented interface to interact with OLE-DB, DAO, and RDO
  - Unified interface to access data from any programming language that uses the underlying OLE-DB objects

**COM was modeled after OMG's CORBA... Here is more...**

# Figure 14.5 - OLE-DB Architecture

<img src="Slides.assets/Screenshot 2026-06-09 at 9.59.16 PM.png" style="zoom:50%;" />

### Microsoft: ADO.NET;

#### ADO.NET

- Data access component of Microsoft's .NET application development framework (improves on the ADO + OLE-DB functionality)
- **Microsoft's .NET framework**
  - Component-based platform for developing distributed, heterogeneous, interoperable applications
  - Manipulates any type of data using any combination of network, operating system, and programming language

#### ADO.NET

- Features critical for the development of distributed applications
  - **DataSet**: Disconnected memory-resident representation of database
  - **XML support**
    - DataSet is internally stored in XML format
    - Data in DataSet could be made persistent as XML documents

<img src="Slides.assets/Screenshot 2026-06-09 at 9.59.58 PM.png" alt="Screenshot 2026-06-09 at 9.59.58 PM" style="zoom:50%;" />

#### Not-Microsoft: JDBC

#### Java Database Connectivity (JDBC)

- **Java:** Object-oriented programming language that runs on top of web browser software, on smartphones, on the desktop and on servers
- **JDBC:** Application programming interface that allows a Java program to interact with a wide range of data sources – a simple URL is all is needed to connect to a db

#### Advantages of JDBC

- Company can leverage existing technology and personnel training
- Allows direct access to database server or access via database middleware
- Allows programmers to use their SQL skills to manipulate the data in the company's databases
- Provides a way to connect to databases through an ODBC driver

Figure 14.7 - JDBC Architecture

<img src="Slides.assets/Screenshot 2026-06-09 at 10.00.27 PM.png" style="zoom:50%;" />

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

After we create a connection, we can create a statement, execute a query, get back a result set and iterate through it:

```
// create a connection via DriverManager.getConnection()
// ...

Statement myStmt = myConn.createStatement();

ResultSet myRslt= myStmt.executeQuery("....");
```

**Here is a complete example.**

### Internet connectivity! [aka 'full stack']

#### Database Internet Connectivity

- Allows new innovative services that:
  - Permit rapid response by bringing new services and products to market quickly
  - Increase customer satisfaction through creation of web-based support services
  - Allow anywhere, anytime data access using mobile smart devices via the Internet
  - Yield fast and effective information dissemination through universal access

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

#### Web-to-Database Middleware

<img src="Slides.assets/Screenshot 2026-06-09 at 10.01.09 PM.png" style="zoom:50%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 10.01.22 PM.png" style="zoom:67%;" />

#### Middleware: server-adj.

Figure 14.9 - Web Server CGI and API Interfaces

<img src="Slides.assets/Screenshot 2026-06-09 at 10.01.55 PM.png" alt="Screenshot 2026-06-09 at 10.01.55 PM" style="zoom:67%;" />

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

**A 'web application server' is a specialized server that interfaces with web services such as databases, search engines. The client (eg browser) can query these data sources and have results generated dynamically.**

#### Features of Web Application Servers

- Security and user authentication
- Access to multiple services
- Integrated development environment
- Computational languages
- Automation generation of HTML pages
- Performance and fault - tolerant features
- Database access with transaction management capabilities

**Examples of web application servers: WebLogic, ColdFusion/JRun, WebSphere Application Server, WebObjects, IIS, WildFly (JBoss), Tomcat, Jetty..**

**Each web application server (WAS) offers its own programming environment. Eg. CFML can be used to consume web services and present results for the end user (likewise for DB result sets).**

**Here is a ColdFusion syntax sample, and roundtrip dataflow:**

<img src="Slides.assets/Screenshot 2026-06-09 at 10.02.33 PM.png" alt="Screenshot 2026-06-09 at 10.02.33 PM" style="zoom:50%;" />

### Modern connectivity

**'MCC' [Microservices (including 'serverless'), Containers, Cloud] - is where things are [INCLUDING LLM-based apps!]. This makes the Internet a fully-distributed computing platform - via function calls that are chained across servers.**

**'WebAssembly' is also part of this vision.**

### Modern architecture styles:

<img src="Slides.assets/Screenshot 2026-06-09 at 10.02.48 PM.png" alt="Screenshot 2026-06-09 at 10.02.48 PM" style="zoom:50%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 10.03.13 PM.png" alt="Screenshot 2026-06-09 at 10.03.13 PM" style="zoom:80%;" />

<img src="Slides.assets/Screenshot 2026-06-09 at 10.05.38 PM.png" alt="Screenshot 2026-06-09 at 10.05.38 PM" style="zoom:80%;" />

The top-3 cloud vendors (plus Oracle, IBM) offer a variety of (micro)services upon which businesses run:

<img src="Slides.assets/Screenshot 2026-06-09 at 10.04.10 PM.png" style="zoom:75%;" />

Hot off the press: MCP.