# Data Warehouse Notes
* All notes taken from the [Big Data Engineering in depth Course](https://youtube.com/playlist?list=PLxNoJq6k39G_m6DYjpz-V92DkaQEiXxkF&si=kw2CJj5jUw2oNcej)  



<!-- Start Document Outline -->

* [Chapter One: Data Management](#chapter-one-data-management)
	* [What is Data Management ?](#what-is-data-management-)
	* [Data Management Life Cycle](#data-management-life-cycle)
	* [What is Data Abstraction?](#what-is-data-abstraction)
		* [Physical Level (Lowest Level , Internal)](#physical-level-lowest-level--internal)
		* [Logical Level (Intermediate Level , Conceptual)](#logical-level-intermediate-level--conceptual)
		* [View Level (Highest Level , External)](#view-level-highest-level--external)
* [Chapter Two: Data Warehouse Components](#chapter-two-data-warehouse-components)
	* [What is Data Warehousing?](#what-is-data-warehousing)
	* [Transactions DB VS Data WareHouse](#transactions-db-vs-data-warehouse)
	* [Types of Data Warehouse](#types-of-data-warehouse)
	* [Multi-temperature Storage](#multi-temperature-storage)
		* [What is the multi-temperature data management model?](#what-is-the-multi-temperature-data-management-model)
		* [Why do we need the multi-temperature data management model?](#why-do-we-need-the-multi-temperature-data-management-model)
		* [How to implement the multi-temperature data management model?](#how-to-implement-the-multi-temperature-data-management-model)
	* [What is DWH Characteristics?](#what-is-dwh-characteristics)
	* [Data WareHouse Architecture](#data-warehouse-architecture)
	* [Data Modeling](#data-modeling)
		* [What is data model?](#what-is-data-model)
		* [Purpose of Data Models](#purpose-of-data-models)
		* [Data Model Elements](#data-model-elements)
		* [Dimensional Data Model Elements](#dimensional-data-model-elements)
		* [Dimensional model life cycle](#dimensional-model-life-cycle)
		* [Dimensions Types](#dimensions-types)
		* [Conformed Dimension](#conformed-dimension)
		* [Degenerate Dimension](#degenerate-dimension)
		* [Junk Dimension (Garbage Dimension)](#junk-dimension-garbage-dimension)
		* [Role-playing dimensions (Re-usable Dimension)](#role-playing-dimensions-re-usable-dimension)
		* [Outrigger Dimensions](#outrigger-dimensions)
		* [Snowflake Dimensions](#snowflake-dimensions)
		* [Slowly changing dimensions](#slowly-changing-dimensions)
		* [Fast changing dimensions (rapidly changing dimensions , Mini Dimensions )](#fast-changing-dimensions-rapidly-changing-dimensions--mini-dimensions-)
		* [Shrunken Rollup Dimension.](#shrunken-rollup-dimension)
		* [Multi-Valued Dimensions](#multi-valued-dimensions)
		* [Swappable Dimensions (Hot-Swappable Dimensions / Profile Tables)](#swappable-dimensions-hot-swappable-dimensions--profile-tables)
		* [Heterogeneous Dimensions](#heterogeneous-dimensions)
	* [Fact Tables](#fact-tables)
		* [1. What is a Fact Table?](#1-what-is-a-fact-table)
		* [Key Characteristics](#key-characteristics)
		* [2. How to Design a Fact Table](#2-how-to-design-a-fact-table)
		* [3. Fact Table Grain (Granularity)](#3-fact-table-grain-granularity)
	* [4. Fact Table Types](#4-fact-table-types)
		* [4.1 Transaction Fact Table](#41-transaction-fact-table)
		* [4.2 Periodic Snapshot Fact Table](#42-periodic-snapshot-fact-table)
		* [4.3 Accumulating Snapshot Fact Table](#43-accumulating-snapshot-fact-table)
	* [5. Fact Table Types Comparison](#5-fact-table-types-comparison)
	* [6. Fact Types](#6-fact-types)
		* [6.1 Additive Facts](#61-additive-facts)
		* [6.2 Semi-Additive Facts](#62-semi-additive-facts)
		* [6.3 Non-Additive Facts](#63-non-additive-facts)
		* [6.4 Derived Facts](#64-derived-facts)
		* [6.5 Textual Facts](#65-textual-facts)
		* [6.6 Pseudo Facts](#66-pseudo-facts)
		* [6.7 Factless Fact Tables](#67-factless-fact-tables)
	* [7. Identifying Facts](#7-identifying-facts)
	* [8. Conformed Facts](#8-conformed-facts)
	* [9. Year-to-Date (YTD) Facts](#9-year-to-date-ytd-facts)
	* [10. Event Fact Tables](#10-event-fact-tables)
	* [11. Composite Primary Key Design](#11-composite-primary-key-design)
	* [12. Fact Table Sizing and Growth](#12-fact-table-sizing-and-growth)
	* [Business-Based Estimation](#business-based-estimation)
	* [Technical-Based Estimation](#technical-based-estimation)
	* [13. Best Practices](#13-best-practices)
	* [Schema Types](#schema-types)
		* [1. Schema Types Overview](#1-schema-types-overview)
		* [2. Star Schema](#2-star-schema)
		* [3. Snowflake Schema](#3-snowflake-schema)
		* [4. Star Schema vs Snowflake Schema (Enhanced)](#4-star-schema-vs-snowflake-schema-enhanced)
	* [5. Additional Notes](#5-additional-notes)
	* [Factless Fact Tables](#factless-fact-tables)
	* [Pseudo-Facts](#pseudo-facts)
	* [Choosing a Schema](#choosing-a-schema)
	* [Real-World Example](#real-world-example)

<!-- End Document Outline -->







## Chapter One: Data Management 

### What is Data Management ?
Data Management is The process of collecting, organizing, protecting, and storing an organization's data so it can be analyzed for business decisions.  

### Data Management Life Cycle

![Data Management Life Cycle](Images/Data%20Management%20Cycle.png)
1. **Idea**: The service you have to provide or the problem you have to solve. 
2. **Identify**: Obtain all data sources and identify their types.
3. **Document**: Documenting all steps and all details throughout the cycle.
4. **DevOps**: Identifying Tools and Processes 
5. **Architecture**: Establishing principles of modeling and data processing
6. **ETL**: **Extracting** information from data sources, **transforming** and processing it, and then **loading** it into the target source.
7. **Business Intelligence BI**: Data Analysis, Reporting or Discovery
8. **Integration**: How the data will integrate with other teams and how we will publish it.
9. **Archiving**: How will we archive data after a long time and what is the retention policy?


### What is Data Abstraction? 
Data Abstraction is The process of hiding irrelevant details from layer to another layer.

* ex. DBMS hides some information from the developers and the developers hide some information from the end user. 

* There are 3 layers of Data Abstraction.
    
   1. Physical Level
   2. Logical/Conceptual Level.
   3. View Level.
   
   ![Data Layers](Images/Data%20Layers.png)
   

#### Physical Level (Lowest Level , Internal) 
   1. It describes **How** data is stored also describes data structure.
   2. Allows you to modify the physical part without any change in the logical schema.
   
  * **Important Example**
  
    Database contains product information.
    
    The physical layer describes: 
    
    * The storage mechanism and blocks (bytes, gigabytes, terabytes, etc.).     
    
    * The amount of memory used. 
    
    * **This layer is usually abstracted from programmers.** 
    
#### Logical Level (Intermediate Level , Conceptual) 
    
   1. It describes **What** data is stored also describes the relationship between tables.
   2. Allows you to change the logical view without altering the external view.
   
  * **Important Example**
  
    Database contains product information.
    
    The Logical layer describes: 
    
    * The product fields and their data types.     
    
    * How this product interact with other entities in the database. 
    
    * **The programmers’ design this level based on business knowledge and the requirements.** 
    
#### View Level (Highest Level , External)
    
   1. It Views the stored data.
   2. It's the final interface for the user     
   
  * **Important Example**
  
    Database contains product information.
    
    The View layer Shows: 
    
    * It could be designed to show the sales of the product in a specific region.     
    
    * We might hide information about some products based on the teams or users. 
    
 
 
 
## Chapter Two: Data Warehouse Components
 

Some challenges are facing the people who work on data management backend.
* Performance.
* Integration.
* Applying analytical functions.

So Vendors who are working on solving the above challenges are creating their product of DWH. **Their ultimate goal is to optimize the above points.**

### What is Data Warehousing?
A DWH is a technique for collecting and managing data from varied sources to **provide meaningful business insights**. It is a blend of technologies and components which aids the strategic use of data.

Some Important Facts About DWH
* The DWH is **not a product** but an environment.
* It is a process of transforming data into information and make it available to users in a **timely manner** to make a difference.
* It is an architectural construct of an information system that provides users with current and historical decision support information which is difficult to access or present in the traditional operational data store.
* The DWH is the core of the BI system built for data analysis and reporting.

### Transactions DB VS Data WareHouse 

| Metric | TransactionsDB | DWH |
|:--------:|:----------------:|:-----:|
| Volume | GB/TB | TB/PB |
| Historical | Short-term | Long-Term |
| Rows | <100M | 100M> |
| Orientation | Product | Subject or multiple products |
| Business Units | Product team | Multi-organizational units |
| Normalization | Normalized | Not required (De-normalized in many use cases) |
| Data Model | Relational | Star Schema or Multi-dim |
| Intelligence | Reporting | Advanced reporting and Machine Learning |
| Use Cases | Online transactions & operations | Centralized storage (360°) |
  
 
### Types of Data Warehouse

1. **Enterprise Data Warehouse (EDWH) For batch**: It provides decision support service across the enterprise. It offers a unified approach for organizing and representing data (DWH Model). It offers data classifications according to the subject with privileges policy.  
  
2. **Operational Data Store (ODS) for Real Time**: is a central database that provides an up-to-date (real-time) data from multiple transnational systems for operational reporting into a single DWH.
3. **Data Mart (Subset of Date Warehouse)**:: A data mart is a subset of the data warehouse. It specially designed for a particular line of business, such as sales, finance, sales or finance. In an independent data mart, data can collect directly from sources.  



| Metric | DWH | ODS | Data Mart |
|:--------:|:-----:|:-----:|:-----------:|
| Latency | Day -1 | Real-time | Day -1  |
| Data level | Transnational | Transnational | Summary |
| Historical | Long-term | Snapshot | Aggregated Long-Term |
| Size | TB/PB | GB | GB/TB | 
| Orientation | Multi sources | Multi sources | Product |
| Business Units | Multi organizational units | Product team | Business team |

### Multi-temperature Storage
#### What is the multi-temperature data management model?
It is a data classification design which allows us to have the following characteristics:  
   * (high performance) access on the frequent data **(Hot data)**. 
   * Good (average performance) access to less-frequently data **(warm data)**.
   * Availability to access rarely accessed data **(cold data)**.

#### Why do we need the multi-temperature data management model?
* Cost reduction. 
* Performance.

#### How to implement the multi-temperature data management model?  

Before implementation, we need to know the following Question's Answers: 
1. What is the Frequency of access ?
2. What is the Data change rate?

Then Identify which storage type is suitable for the project 
* **Hot data** stored on the fast storage system.
* **Warm data** (usual) stored on slightly slower storage.
* **Cold data** stored on the slowest storage.

### What is DWH Characteristics?
* Integrated: DWH is an integrated environment which allows us to integrate different source systems.

* Time-Variant: Data modeled (organized) based on periods (hourly, daily, weekly, monthly, quarterly, yearly).

* Subject-oriented: DWH main target is to support business needs for the whole organization including (decision-makers, departments, and specific user requirements).

* Non-Volatile: It refers to the data that erased or deleted (It could be archived and retrieved when needed).


### Data WareHouse Architecture 


![](Images/DWH%20Arch.png)

DWH architecture contains the following layers:
1. **Source System Layer**: This layer consists of various data sources, such as databases, applications, and external systems, that provide raw data to the data warehouse and identifying the stakeholders and deliver data analysis document.

2. **Extraction Layer**: This layer handles the process of retrieving data from the source systems and preparing it with minimal data cleansing for staging layer.

3. **Staging Area**: A temporary storage area where extracted data is cleaned, validated, and transformed before being loaded into the data warehouse [Learn more about staging layer](https://www.geeksforgeeks.org/what-is-a-data-staging-area-in-data-warehouse/).

4. **Data Modeling**: This layer involves designing the data structure, including schemas and relationships, to optimize data organization and retrieval.

5. **ETL Layer**: The Extract, Transform, Load (ETL) layer processes data by extracting it from sources, transforming it as per business rules, and loading it into the warehouse.

6. **Storage Layer**: The storage layer is where the processed and structured data is securely stored for analysis and reporting purposes.

7. **Reporting (UI) Layer**: This layer provides tools and interfaces for users to visualize, query, and analyze the data in the warehouse.

8. **Metadata Layer**: The metadata layer stores information about the data's structure, sources, transformations, and usage to enable efficient management and understanding of the warehouse.

9. **System Operations Layer**: This layer oversees the operational aspects of the data warehouse, including monitoring, scheduling, and maintaining system performance.

### Data Modeling 

#### What is data model?

A data model is an abstract representation that outlines how data is organized, interconnected, and utilized within a system. It represents the key elements, such as entities and their characteristics, and defines the rules governing their interactions. By offering a clear blueprint, it ensures data is consistently stored, retrieved, and interpreted, aligning with the system's goals. Data models also describe the logical flow and processes of a business or application, helping to translate real-world scenarios into a structured digital format for efficient handling and analysis.

Data Model Concepts

| **Is not a** | **Is a**|
|:----------:|:-------------:|
|a science.|a general concept that leads to build full architecture.|
|a static design for each organization.|an engineering design practices.|
|a type of database.|different based on the use case and the database type.|
|a new invention which needs to be done for each project.|customizable, and we can utilize some of the ready built architecture.|
|           |affecting information reporting performance.|


Data Model Also is 

* The first part before starting integration with any new source system.

* The connection layer between business requirements and technical design.

* It is also the translation between logical and physical layer.

* It is unified across all systems and has the same patterns and practices.

* It engaged with any source systems integration from the early stages.
 
* This stage output is a data model design document or mapping sheet


#### Purpose of Data Models
- Used to capture and present information.
- Applied in two forms:
  - **Operational Form**: For OLTP (Online Transaction Processing) applications.
  - **Informational Form**: For data warehouses.
  
**E/R Diagram (Entity-Relationship Diagram)**
- A traditional data modeling method.
- Focuses on capturing relationships between entities.
- Acts as a communication tool between data modelers and business analysts.
- Helps analyze business requirements and design data structures.

**Dimensional Modeling**
- Focused on the business perspective.
- Helps business analysts visualize abstract questions and utilize data effectively.
- Facilitates easy navigation of data structures for ad hoc queries and analysis.
- Represents data as an abstraction of business activities, resources, and results.

**Comparison of E/R and Dimensional Models**

| **E/R Models**| **Dimensional Models**|
|:-------------:|:---------------------:|
|Normalized structure.| Denormalized structure.|
| Ideal for OLTP systems.| Ideal for data warehouses.|
| Focuses on efficient data insertion, updating, and deletion. | Focuses on efficient data retrieval (Select). |
| Best for reporting and fixed queries.| Best for ad hoc queries and analysis.|

**When to Use Each Approach**
- **E/R Modeling**: Use for highly transaction-oriented OLTP applications, reporting, and fixed queries.
- **Dimensional Modeling**: Use for data warehousing applications with ad hoc querying and analysis.

**Core Goals of Data Models**
- **OLTP Applications**: Efficiently manage data (Insert, Update, Delete).
- **Data Warehouses**: Efficiently retrieve data (Select).

**Role of Data Models in Data Warehousing**
- Organize the structure and contents of data in the warehouse.
- Essential for understanding and managing business processes.

**Key Distinction**
- All dimensional models are technically E/R models.
- **E/R Models**: Normalized structure.
- **Dimensional Models**: Denormalized structure.
----
#### Data Model Elements

1. Facts: are the measurements/metrics or facts from the business process.

2. Dimensions: provide the context surrounding a business process event. In simple terms, they give who, what, where the fact.

3. Attributes: are the various characteristics of the dimension.

---
#### Dimensional Data Model Elements
1. Fact Table: is a primary table in a dimensional model.A Fact Table contains (Measurements/facts and Foreign key to dimension table).

2. Dimension table: contains dimensions of a fact and business reference data. They are joined to fact table via a foreign key. Dimension tables are de-normalized tables.

---
#### Dimensional model life cycle

**1. Gathering Requirements (Source Driven, Business/User Driven).**

This phase involves selecting a specific business process to model. The selection is based on its importance to the organization, the quality of data available in the source systems, and the feasibility or complexity of the process.

**2. Identify granularity of the facts**

The grain defines the level of detail at which the data is captured. If a process has multiple grains, separate fact tables should be created for each. It is important to design the grain at the most detailed (atomic) level to allow flexibility for future additions and modifications without major redesigns.


**3. Identify the dimensions**

Dimensions are descriptive attributes of the data that provide context to the facts. In this step, the relevant dimensions for the chosen grain are identified.


**4. Identify the facts**

Facts represent measurable data points associated with the chosen grain. This step involves identifying the relevant facts and classifying them (e.g., additive, semi-additive, or non-additive). Default aggregation rules for these facts are also determined.

**5. Verify the Model**

Before moving forward, the dimensional model is validated against business requirements. If the model fails to meet requirements, the grain or other elements may need to be revisited and adjusted.

**6. Physical Design Considerations**

Once the model is designed, focus shifts to performance optimization. Techniques such as data partitioning, indexing, and aggregation are applied to enhance query efficiency and support real-world operational demands.


----
#### Dimensions Types

1. [Conformed Dimension.](#conformed-dimension)
2. [Degenerate Dimension](#degenerate-dimension).
3. [Junk Dimension (Garbage Dimension)](#junk-dimension-garbage-dimension).
4. [Role-Playing Dimension](#role-playing-dimensions-re-usable-dimension).
5. [Outrigger Dimension](#outrigger-dimensions).
6. [Snowflake Dimension](#snowflake-dimensions).
7. [Slowly changing Dimension](#slowly-changing-dimensions).
8. [Fast Changing Dimension (Mini Dimension)](#fast-changing-dimensions-rapidly-changing-dimensions--mini-dimensions-).
9. [Shrunken Rollup Dimension](#shrunken-rollup-dimension).
10. [Multi-valued dimensions](#multi-valued-dimensions).
11. [Swappable Dimension](#swappable-dimensions-hot-swappable-dimensions--profile-tables).
12. [Heterogenous Dimensions](#heterogeneous-dimensions).

---
#### Conformed Dimension

**What are conformed dimensions?**

Conformed dimensions are shared dimensions that have the same meaning across all fact tables they are joined with. They may share some or all attributes drawn from the same domain. A conformed dimension can also contain a subset of attributes from a primary dimension.

**Purpose of Conformed Dimensions**

Conformed dimensions are referenced by multiple fact tables or dimensional models, ensuring consistency across the enterprise data warehouse. They are used to avoid redundancy and support integration across different business processes.

**Examples of Conformed Dimensions**

* Date as a Key: if we have a date column across many facts, we could use the date as key in all tables. So, it should be a unified format.

* Product-Id as a Key: if we have a product name which could vary between systems ex: (upper/lower) We can create a dimension table for the product details and use product id unified across fact tables.

**Identifying Conformed Dimensions**

* First, check if the required dimension already exists in the enterprise data warehouse. If it does, use the existing dimension instead of redesigning it.

* If the required dimension does not exist, design a new dimension with long-term cross-enterprise usage in mind. During this process, interact with various business units to ensure the new dimension aligns with anticipated future requirements.


---
#### Degenerate Dimension

**What is a degenerate dimension?**

A Dimension without any attributes. They are not typical dimensions, It is a transaction-based number which resides in the fact table. There
may be more than one degenerate dimension inside a fact table.

* Dimension Key without corresponding dimension table.
* Stored in fact table.
* It used to provide a grouping for business cases.

**How to Identify a Degenerate Dimension**

* It is a transaction-related number present in the OLTP system.
* It does not have associated descriptive attributes that need to be stored separately.
* The transaction number still provides value by allowing tracking and lookup of details related to a specific fact table row.
* All descriptive information related to it is already extracted into other dimensions (e.g., date, time, product, customer).
  
**Example of a Degenerate Dimension**

![](Images/Degenerate%20DIm.png)

Consider a retail store sales transaction:

* A Bill Number# 0405001 exists in the sales system.
* The Bill Number# represents a purchase transaction.
* All details of this transaction (date, time, products purchased, price, quantity) are already stored in separate dimensions.
* The Bill Number# itself does not require a separate dimension table but remains in the fact table as a degenerate dimension.


---
#### Junk Dimension (Garbage Dimension)

**What is a Junk dimension?**

A garbage dimension, also called a junk dimension, is a dimension that stores low-cardinality attributes such as codes, indicators, statuses, and flags. These attributes do not belong to a hierarchy and are grouped together to reduce the number of dimensions and minimize columns in the fact table.

* It used to reduce the number of dimensions (low-cardinality columns) in the dimensional model and reduce the number of columns in the fact table. It is a collection of random transnational codes, flags, or text attributes.

* It optimizes space as fact tables should not include low-cardinality or text fields. It mainly includes measures, foreign keys, and degenerate dimension keys.

**Junk Dimension Example**

![](Images/junk%20dim.png)

**How to Calculate Total Size of a Garbage Dimension?**

* We must split the Junk dimension into more dimensions in case the size grows by the time.

* It is easy to calculate the expected number of rows as it is the total number of combinations between the low-cardinality attributes; 3 columns each have 3 values total = 3 * 3 = 9.


---
#### Role-playing dimensions (Re-usable Dimension)

**What is a Role-playing dimension?**

A single physical dimension helps to reference multiple times in a fact table as each reference linking to a logically distinct role for the dimension.

**Role-playing Dimension Example**

a dimensional model designed for an order management business process. There are two date entities (order and received date) at the same day grain involved.

![](Images/role-playing%201.png)

Instead of using two separate date tables, Order_Date and Received Date with the same details, we can use just one date table and refer to it multiple times.

![](Images/role-playing%202.png)


**Conformed vs Role-Playing Dimension**

* Conformed is the same dimension used in different facts and has the **same meaning** ex: CustomerID.

* Role-Playing is the same dimension which used multiple times within the same fact but with **different meanings** ex: Date.

---


#### Outrigger Dimensions

**What is a Outrigger Dimensions?**

A dimension which has a reference to another dimension table. The secondary dimension called outrigger dimension.

**Outrigger Dimensions Example**

![](Images/Outrigger%20.png)
  
---  
  
#### Snowflake Dimensions

**What is Snowflake Dimension?**

Snowflake Dimension is a dimension that has a hierarchy of attributes. This attribute is normalized, and each dimension has a relationship with another hierarchy dimension table.

**When to Use Snowflaking?**

* When a dimension contains attributes of different grains (levels of detail).
* When attributes come from different source systems, making updates more manageable.
* For performance optimization in aggregate tables, where certain hierarchical data can be separated for faster queries.

**Why NOT to Use Snowflaking**

* Reduces query performance due to increased joins.
* Increases complexity, making the schema harder to understand.
* Minimal space savings, as dimension tables are small compared to fact tables.


**Snowflake Dimension Example**

![](Images/snowflake%20dim.png)

---

#### Slowly changing dimensions

**What are slowly changing dimensions?**  

A slowly changing dimension is a dimension whose attributes for a record (row) change slowly over time.

**Types of slowly changing dimension**
1. Type 0 (Fixed Dimension): We don’t change the current even the source changes.
![](Images/slowly%20type%200.png)
2. Type 1 (No History): No history is maintained only the latest replace the current.
![](Images/slowly%20type%201.png)
3. Type 2 (History): Series of history of records are maintained.
![](Images/slowly%20type%202.png)
4. Type 3 (Hybrid): Only the last Change and the Current new change is stored
![](Images/slowly%20type%203.png)
5. Type 4 : We split the data into two tables, first the current record and second is the historical (most common usage).
![](Images/slowly%20type%204.png)

**Important Note**
There are some other types which is a combination between the above similar than type 3 combined between 1 | 2.| You can check the chapter resources for more information about the other types.

**Type 1 approach**

**When to use the Type-1 change handling approach ?**
* This may be the best approach to use if the attribute change is simple, such as a correction in
spelling. And, if the old value was wrong, it may not be critical that history is not maintained.

* It is also appropriate if the business does not need to track changes for specific attributes of a particular dimension.

**Advantages of the Type-1 change handling approach**
* It is the easiest and most simple to implement.
* It is extremely effective in those situations requiring the correction of bad data.
* No change is needed to the structure of the dimension table.


**Disadvantages of the Type-1 change handling approach**
* All history may be lost if this approach is used inappropriately. It is typically not possible to trace history.
* All previously made aggregated tables need to be rebuilt.


**Type 2 approach**

**When to use the Type-2 change handling approach ?**
* When there is need to track an unknown number of historical changes to dimensional attributes.


**Advantages of the Type-2 change handling approach**
* Enables tracking of all historical information accurately and for an infinite number of changes.


**Disadvantages of the Type-2 change handling approach**
* Causes the size of the dimension table to grow fast. In cases where the number of rows being inserted is very high, then storage and performance of the dimensional model may be affected.

* Complicates the ETL process needed to load the dimensional model. ETL-related activities that are required in the type-2 approach include maintenance of effective and expiration date attributes in the staging area.

**Impact on existing dimension table structure**
* No change to dimensional structure needed.
* Additional columns for effective and expiration dates are not needed in the dimension table.

**Impact on preexisting aggregations**
* There is no impact on the preaggregated tables. The aggregated tables are not required to be rebuilt as with the type-1 approach.

**Impact on database size**
* Yes, accelerates the dimensional table growth because with each change in a dimensional attribute, a new row is inserted into the dimension table.

**Adding effective and expiration dates to dimension tables**
* No. This is not necessary in the dimension tables.




**Type 3 approach**

**When to use the type-3 change handling approach?**
* Should only be used when it is necessary for the data warehouse to track historical changes, and when such changes will only occur for a finite number of times. If the number of changes can be predicted, then the dimension table can be modified to place additional columns to track the changes.


**Advantages of the type-3 change handling approach**
* Does not increase the size of the table as compared to the type-2 approach, since new information is updated.
* Allows us to keep part of history. This is equivalent to the number of changes we can predict. Such prediction helps us modify the dimension table to accommodate new columns.

**Disadvantages of the type-3 change handling approach**
* Does not maintain all history when an attribute is
changed more often than the number in the
predicted range, because the dimension table is
designed to accommodate a finite number of
changes.

* If we designed a dimension table assuming a
fixed number of changes, then needed more,
then we would have to redesign or risk losing
history.

        
**Impact on existing dimension table structure**
* The dimension table is modified to add columns.
* The number of columns added depends on the
number of changes to be tracked.

**Impact on preexisting aggregations**
* You may be required to rebuild the
preaggregated tables.

**Impact on database size**
* No impact is there since data is only updated.

---

#### Fast changing dimensions (rapidly changing dimensions , Mini Dimensions )

**What are fast changing dimensions?**
what happens when the rate of change in these slowly changing dimensions speeds up? If a
dimension attribute changes very quickly on a daily, weekly, or monthly basis,
then we are no longer dealing with a slowly changing dimension that can be
handled by using the Type-1, Type-2, or Type-3 approach.

**Why Fast Changing Dimensions?**
* When we have a dimension with one or more of its attributes changing very fast.
* It causes a performance issue if we tried to handle this case similar SCD Type 2 because of the rapidly changing in this dimension and the table will includes a lot of rows for this dimension


**How to handle fast changing dimensions?**

The best approach for handling very fast changing dimensions is to separate the
fast changing attributes into one or more separate dimensions which are called
**mini-dimensions**. 

The fact table then has two or more foreign keys—one for the
primary dimension table and another for the one or more mini-dimensions
(consisting of fast changing attributes). The primary dimension table and all its
mini-dimensions are associated with one another every time we insert a row in
the fact table.


**What is a mini-dimension?** 

A mini-dimension is a dimension that usually contains fast changing attributes of
a larger dimension table. This is to improve accessibility to data in the fact table.
Rows in mini-dimensions are fewer than rows in large dimension tables because
we try to restrict the rows in mini-dimensions by using the band range value
concept.


**Solving the Fast-Changing Dimensions Problem**

- **Step 1: Identify constantly changing attributes**, such as:
  - Age, income, test score, credit history score, customer account status, weight.

- **Step 2: Convert each changing attribute into band ranges**:
  - This limits the number of possible values by forcing attributes into discrete categories.
  
- **Example**:
  - If 7 attributes each have 10 possible values, the mini-dimension table would have 10⁷ = 1 million rows.

- **Step 3: Create a Customer Mini-Dimension table**:
  - Contains only banded values of fast-changing attributes.
  - Reduces volatility in the main dimension table.
  
- **Result**:
  - The fast-changing attributes now take fixed band-range values.
  - This prevents constant changes and simplifies tracking.


**Before FCD**

![](Images/before%20fcd.png)


**After FCD**

![](Images/after%20fcd.png)


**Why not use Snowflaking?**


![](Images/why%20not%20snow.png)


**Snowflaking Does Not Solve the Fast-Changing Dimension Problem**

- **Scenario**:
  - A Customer dimension is split by creating a **Customer Mini-Dimension**.
  - The mini-dimension is **snowflaked** and attached as a **foreign key** to the Customer dimension.

- **Issue with this design**:
  - Although it may seem logical, **snowflaking the mini-dimension is a bad design** for handling fast-changing dimensions.
  - This design still introduces the **fast-changing dimension problem**.

- **Example**:
  - Customer **Stanislav Vohnik** is initially linked to the 1st row in the `Customer_Mini_Dimension`.

- **Change scenario**:
  - In one year, Stanislav's profile changes 5 times.
  - Now, he is associated with **5 different rows** in the mini-dimension.

- **Scale of the issue**:
  - If there are **10 million customers**, and each has an average of **5 profile changes per year**:
    - The mini-dimension would grow to approximately **50 million rows**.

**Recommended Solution**

- Instead of snowflaking, attach the **primary key of the `Customer_Mini_Dimension` table directly to the `Retail_Sales` fact table**.

- **Why this works**:
  - Each fact table record is associated with the **correct profile** of the customer **at the time of transaction**.
  - The `Customer` table retains **only one record** for each customer (e.g., Stanislav Vohnik).
  - **Profile changes** are tracked in the fact table using the appropriate reference to the mini-dimension.

- **Result**:
  - The fact table handles the changes efficiently.
  - No need to replicate the customer in the main dimension for each change.
  - The solution avoids bloating the dimension tables and provides a scalable approach to track fast-changing attributes.



#### Shrunken Rollup Dimension.

**What is Shrunken Rollup dimension?**

Shrunken Rollup dimension is used for developing aggregate (higher level of summary) fact tables.
  
  
* It required that the data model has a lower level of granularity.

* We have a daily usage fact table, and we need to have a higher level of monthly usage.  So, we use the monthly dimension to get a summary of the daily.

* We have a daily usage fact table aggregated on area-id, and we need to create another summary table aggregate* d based on city id. So, the new grain level here is the new dimension for the city.

##### Example  

![](Images/Shrunken%20dim.png)

**Original Date Dimension**
- Date
- Day
- Month
- Quarter
- Year

**Shrunken Rollup Date Dimension**
- Month
- Quarter
- Year

Used when one fact table is at the **daily level** and another is at the **monthly level**.

##### Why It’s Used
- Improves query performance
- Simplifies the data model
- Avoids unnecessary joins
- Preserves conformed dimensions across fact tables

###### Key Characteristics
- Subset of a larger dimension
- Higher granularity
- Fewer attributes
- Reused across fact tables

##### When to Use It
- Fact tables with different grains
- Detailed attributes are not needed
- Need consistency in reporting


#### Multi-Valued Dimensions

##### What Is a Multi-Valued Dimension?
A **multi-valued dimension** occurs when one fact record relates to **more than one dimension member**.

##### Common Examples
- Multiple insured persons under one insurance policy
- Multiple customers associated with a single bank account
- Multiple diagnoses for one patient
- Multiple sales representatives contributing to one order

---

##### Why It Is a Modeling Challenge
Including a multi-valued dimension directly in the fact table:
- Violates the **grain** of the fact table
- Causes incorrect aggregations
- Leads to data duplication and inaccurate analysis

If the grain is defined as *one row per policy account per month*, adding individual customers directly would break this rule when multiple people are associated with the same policy.

---

##### Bridge Table Solution

##### What Is a Bridge Table?
A **bridge table** is used to resolve a **many-to-many relationship** between:
- A fact table (or dimension), and
- A multi-valued dimension

##### Typical Contents
- Foreign key to the first table (Fact or Dimension)
- Foreign key to the multi-valued Dimension
- Optional **weighting factor**

---

##### Insurance Example
- Policy Account Number: `963276`
- Insured Persons: John (primary), Lisa, Dave
- Monthly premium is charged once for the entire family

##### Fact Table Grain
- One row per **policy account per month**

##### Solution
- Create an **Account–Insured_Person bridge table**
- Associate multiple insured persons with one policy account
- Preserve the fact table grain

---

##### Weighting Factor

##### Definition
A **weighting factor** is a numeric value stored in the bridge table that allocates additive facts across multiple dimension members.

##### Rules
- Weighting factors for a single group must **sum to 1**
- Used to correctly distribute metrics such as revenue or premiums

##### Example
| Insured Person | Weight |
|---------------|--------|
| John          | 0.50   |
| Lisa          | 0.30   |
| Dave          | 0.20   |
| **Total**     | **1.00** |

---

##### Approaches to Handling Multi-Valued Dimensions

##### 1. Choose One Value and Ignore Others
- Simplest approach
- Often results in incomplete or misleading analysis

##### 2. Create Fixed Multiple Dimension Columns
- Not scalable
- Lacks flexibility when number of values varies

##### 3. Use a Bridge Table (Best Practice)
- Scalable and flexible
- Preserves grain integrity
- Supports accurate aggregation

---

##### Bridge Table Placement Options

##### 1. Between Fact and Dimension
Example: Orders ↔ Sales Representatives  
- Each contributor gets a weighting factor based on contribution

##### 2. Between Two Dimensions
Example: Account ↔ Insured Person  
- Fact table remains unchanged
- Bridge table captures many-to-many relationship

---

##### Why Multi-Valued Dimensions Are Important
- Accurately model real-world complexity
- Enable advanced analytics without corrupting data
- Maintain clean and reliable dimensional models

---

#### Swappable Dimensions (Hot-Swappable Dimensions / Profile Tables)

##### Definition
A **swappable dimension** is a dimension that has **multiple alternate versions** of itself that can be **swapped at query time**. Each version of the hot swappable dimension can have **different structures**, including incompatible attribute names and different hierarchies.  

**Key Characteristics:**
- Alternate versions may be **completely different** in structure.  
- All versions access the **same fact table** but produce **different outputs**.  
- Unlike relational databases, OLAP systems make hot swappable dimensions **more complicated**, as joins cannot always be defined at query time.  

---

##### Implementation Approaches

1. **Separate Physical Dimensions**
   - Create **physical subsets** of the primary dimension with only relevant **columns and rows**.  
   - Swap the subset dimension at runtime by **joining its key** to the fact table’s foreign key.  
   - The **fact table remains the same** across all dimension versions.

2. **Views Based on the Primary Dimension**
   - Create **one or more views** from the primary dimension.  
   - Swap these views at runtime instead of the original dimension table.  

3. **Direct Join with Runtime Filter**
   - Join the **fact table directly** to a generalized dimension containing all versions.  
   - Use a **runtime filter** (e.g., `ProfileType` or `PartyType`) to select the relevant version.  
   - Some columns may be **empty or NULL** depending on the version being used.  

---


- **Dimensional Model Example:**  
  - In an **order management system**, dimensions such as **Product, Customer, Supplier, and Sales_Channel** can have swappable dimensions.  
  - All business users still use the same fact table (**Sales_Fact**) stored in a single place, but they may **swap different versions of dimensions at query time**.  

- **Heterogeneous Products Note:**  
  - If the company is selling **heterogeneous products to completely different customers**, these products would usually belong to **separate data marts** or **data warehouses**.  

- **Benefits:**  
  - Improves **performance** of the dimensional model.  
  - Helps create **more secure dimensions**.  
  - Provides **flexibility** to analyze the same facts from **different perspectives** without duplicating the fact table.  

- **Summary:**  
  - Swappable dimensions allow multiple **perspectives of the same entity**.  
  - They support **dynamic analysis** without duplicating facts.  
  - Implementation can be via **physical dimension subsets**, **views**, or **direct joins with runtime filters**.  
  - Useful in **complex OLAP systems** to handle **different business needs**, **performance optimization**, and **security management**.

---


#### Heterogeneous Dimensions

##### Definition
A **heterogeneous dimension** occurs when different types of entities share a common fact table, but each type has **different sets of attributes**.  

- Each type has unique attributes not shared with others.  
- This allows analysis of different types in a shared context while managing structural differences.  

**Illustrative Example (Products):**  
- An insurance company sells **home insurance** and **car insurance**.  
- Attributes for home insurance (e.g., property value, number of rooms) differ from car insurance (e.g., vehicle type, license plate).  
- Modeling both under the same dimension requires special handling — this is a case of heterogeneous dimensions.  

---

##### Implementation Approaches

##### 1. Separate Dimensions
- **Description:** Create a **dimension table for each type** and optionally separate fact tables.  
- **Example:**  
  - Home Insurance Dimension & Fact Table  
  - Car Insurance Dimension & Fact Table  
- **Pros:**  
  - Detailed, type-specific analysis.  
  - Smaller, manageable tables.  
- **Cons:**  
  - Cross-type analysis requires combining multiple tables.  

##### 2. Merge Attributes
- **Description:** Combine all attributes from all types into **one table**.  
- **Example:**  
  - A single Insurance Dimension table with columns for both home and car insurance; irrelevant columns are **NULL** for each type.  
- **Pros:** Single table for all types.  
- **Cons:**  
  - Table can grow very large.  
  - Performance and maintenance issues.  
- **Recommendation:** Only feasible if attribute differences are small; generally **not recommended**.  

##### 3. Generic Design
- **Description:** Include only **common attributes** across types in a single dimension table.  
- **Example:**  
  - A generic Insurance Dimension table with shared attributes like customer ID, policy number, and transaction amount.  
- **Pros:** Allows comparison across types.  
- **Cons:**  
  - Only common attributes are analyzable.  
  - Detailed insights require separate tables.  

---

##### Key Insights
- Heterogeneous dimensions handle **diverse entity types** in a shared fact context.  
- **Implementation choice depends on analysis needs:**  
  - **Separate dimensions** → Detailed, type-specific analysis  
  - **Generic design** → High-level cross-type metrics  
  - **Avoid merge attributes** → For highly diverse types due to performance and maintenance issues


### Fact Tables

#### 1. What is a Fact Table?
A **Fact Table** is the **core and foundation of a Data Warehouse**.  
It stores **measurable business data (facts)** related to a specific **business process**.

#### Key Characteristics
- Contains **numeric measurements (facts)** and **foreign keys** to dimension tables
- Represents business activities such as **sales, calls, orders, or claims**
- Located at the **center of the Star Schema**
- Main target of **analytical queries and reports**
- Optimized for **aggregation and analysis**

---

#### 2. How to Design a Fact Table
1. **Choose the business process**  
   (Sales, Billing, Calls, Claims, etc.)
2. **Identify the grain**
3. **Identify the dimensions**
4. **Identify the facts**

---

#### 3. Fact Table Grain (Granularity)
The **grain** defines what a **single row** in the fact table represents.

###### Key Points
- Describes the **physical business event** being measured
- Controls which dimensions and facts are valid
- Not always time-based
- **Best practice:** design at the **lowest possible grain**

##### Example Grains
- One transaction
- One call
- One line item on a bill
- One process instance

---

### 4. Fact Table Types
There are **three main types** of fact tables:

---

#### 4.1 Transaction Fact Table
- **Grain:** one row per transaction
- New row for every transaction
- Grows very fast
- No updates after insert

**Use Cases**
- Sales transactions
- Telecom calls
- Payments

---

#### 4.2 Periodic Snapshot Fact Table
- One row per entity per **fixed time period**
- Aggregated from transaction data
- Loaded periodically (daily, monthly, yearly)
- Not updated after load

**Use Cases**
- Daily sales summary
- Monthly call totals
- Inventory snapshots

---

#### 4.3 Accumulating Snapshot Fact Table
- One row represents the **entire lifecycle** of a process
- Tracks **milestones/stages**
- Rows are **updated** as stages complete
- Used to analyze **time between events**

**Use Cases**
- Order lifecycle
- Insurance claims processing
- Hiring process

---

### 5. Fact Table Types Comparison

| Feature | Transaction | Periodic Snapshot | Accumulating Snapshot |
|------|------------|------------------|----------------------|
| Grain | One transaction | One time period | Process stages |
| Date usage | Lowest granularity | End-of-period | Multiple dates |
| Facts | Transaction metrics | Period aggregates | Lifecycle metrics |
| Table size | Largest | Medium | Smallest |
| Updates | No | No | Yes |

---

### 6. Fact Types

#### 6.1 Additive Facts
- Can be summed across **all dimensions**
- Most flexible type

**Examples**
- Sales amount
- Quantity sold
- Total cost

---

#### 6.2 Semi-Additive Facts
- Can be aggregated across **some dimensions but not all**
- Usually not additive across time

**Examples**
- Account balance
- Inventory quantity
- Headcount

---

#### 6.3 Non-Additive Facts
- Cannot be summed across any dimension
- Usually ratios or percentages

**Examples**
- Profit margin
- Discount rate

---

#### 6.4 Derived Facts
- Calculated from other facts
- May or may not be stored

**Example**
```text
Total Sales = Quantity × (Unit Price − Discount)
```
#### 6.5 Textual Facts
- Contain text values (flags, indicators)
- Should be avoided in fact tables
- Better placed in dimension tables

#### 6.6 Pseudo Facts
- Numeric but meaningless when summed
- Mainly used for counting events

#### 6.7 Factless Fact Tables
- Contain only foreign keys
- No numeric facts
- Used to record events

---

### 7. Identifying Facts
- Facts must be true to the grain
- Identified from:
  - Grain definition
  - Source E/R models
  - Line-item analysis
- Avoid storing Year-To-Date (YTD) facts at atomic grain

---

### 8. Conformed Facts
- Shared facts across multiple data marts
- Same definition and calculation logic
- Enable cross-mart analysis

---

### 9. Year-to-Date (YTD) Facts
- Aggregated totals from start of year to current date
- Non-additive
- Prefer calculating in:
  - OLAP tools
  - SQL views
  - Reporting layer

---

### 10. Event Fact Tables
- Used to record events (clicks, attendance, logins)
- Often contain:
  - Pseudo facts
  - Or no facts (factless)
- Mainly used for counting

---

### 11. Composite Primary Key Design
- Fact tables usually use a composite primary key
- Built from:
  - Dimension foreign keys
  - Degenerate dimensions (e.g., Bill Number)
- Grain definition determines uniqueness

---

### 12. Fact Table Sizing and Growth

### Business-Based Estimation
- Based on business volume (e.g., revenue ÷ average price)

### Technical-Based Estimation
- Based on dimension cardinality and row size
- Used to estimate maximum growth

---

### 13. Best Practices
- Always define grain first
- Design at the lowest possible granularity
- Prefer additive facts
- Avoid textual facts
- Handle YTD and derived facts in reporting layer
- Validate model with business users

### Schema Types

#### 1. Schema Types Overview
In **Data Warehousing (DWH)**, schemas define how **fact tables** and **dimension tables** are structured.  

The two most common schema types are:

- **Star Schema** – optimized for simplicity and query performance  
- **Snowflake Schema** – optimized for storage efficiency and normalization  

Other less common schema types (for context):

- **Galaxy / Fact Constellation Schema** – multiple fact tables sharing dimensions, often used for complex enterprise DWH.  
- **Constellation Schema** – similar to galaxy, supports multiple business processes in one warehouse.

---

#### 2. Star Schema

##### Definition
A **Star Schema** is a **central fact table** connected to **denormalized dimension tables**, forming a star-like shape.  

It is **highly intuitive** and widely used in business intelligence.

---

###### Main Characteristics of Star Schema

1. **Simplicity**
   - Straightforward design
   - Easy for developers, analysts, and BI tools to understand

2. **Query Effectiveness**
   - Minimal joins needed for queries
   - High performance for large datasets  
   - Ideal for OLAP queries and reporting

3. **Data Redundancy & Storage**
   - Dimension tables are **de-normalized**, leading to **redundant data**  
   - Can require **more disk space**  
   - Updates may be harder due to repeated data

4. **Wide Support**
   - Most BI tools, ETL pipelines, and reporting frameworks support it natively

---

##### Structural Characteristics

- **Dimensions:** One table per dimension  
- **Fact Table:** Contains foreign keys and numeric measures  
- **Joins:** Dimension tables **do not join to each other**  
- **Data Integrity:** Not strictly enforced, de-normalization can cause inconsistencies  

---

##### Advantages of Star Schema
- Faster query performance  
- Easier for non-technical users to understand  
- Simplifies reporting and dashboards  
- Good for **data marts** with simple business processes  

##### Disadvantages
- High data redundancy  
- Large disk space requirements  
- Maintenance can be more challenging (updates propagate to multiple rows)

---

##### When to Use Star Schema
- Simple **1:1** or **1:many** relationships  
- Datamarts for **sales, finance, or marketing reporting**  
- Scenarios prioritizing **query speed over storage efficiency**

---

#### 3. Snowflake Schema

##### Definition
A **Snowflake Schema** is an **extension of the Star Schema**, where **dimension tables are normalized** into multiple related tables.  

This creates a more **complex, hierarchical structure**, often resembling a snowflake.

---

##### Main Characteristics of Snowflake Schema

1. **Normalized Dimensions**
   - Dimension tables split into multiple related tables  
   - Reduces data redundancy  
   - Improves data consistency

2. **Storage Efficiency**
   - Requires **less disk space**  
   - Smaller tables can improve certain query operations (less data scanned)

3. **Query Complexity**
   - Queries require **more joins**  
   - Slightly slower performance compared to Star Schema  

4. **Maintainability**
   - Easier to maintain due to normalized structure  
   - Changes propagate without redundancy issues  

---

##### Structural Characteristics

- Fact table is surrounded by **dimension hierarchies**  
- Each dimension may expand into **multiple related tables**  
- Better supports **complex relationships** and large enterprises

---

##### Advantages of Snowflake Schema
- Low data redundancy  
- Easier maintenance and updates  
- Efficient storage usage  
- Supports **many-to-many relationships**  

##### Disadvantages
- Slower query performance due to multiple joins  
- More complex to design and understand  
- Harder for casual users to write queries manually  

---

##### When to Use Snowflake Schema
- Core **enterprise data warehouses**  
- Complex hierarchies and many-to-many relationships  
- Storage efficiency is critical  
- OLAP queries that can tolerate additional joins

---

#### 4. Star Schema vs Snowflake Schema (Enhanced)

| Feature | Star Schema | Snowflake Schema |
|---------|------------|----------------|
| Dimension Structure | One table per dimension | Multiple normalized tables per dimension |
| Fact Table | Surrounded by dimension tables | Surrounded by dimension hierarchies |
| Joins | Few joins | Many joins |
| Design Complexity | Simple | Complex |
| Data Structure | De-normalized | Normalized |
| Data Redundancy | High | Low |
| Maintenance | More difficult | Easier |
| Storage Efficiency | Lower | Higher |
| Query Performance | High | Moderate to low |
| Best Use Case | Simple datamarts, OLAP | Enterprise DWH, complex relationships |

---

### 5. Additional Notes

### Factless Fact Tables
- Contain only foreign keys (no numeric measures)  
- Used to **record events or relationships**  

### Pseudo-Facts
- Numeric values **not additive** (e.g., counts, flags)  
- Cannot be summed meaningfully across dimensions  

### Choosing a Schema
- **Star Schema:** Focus on **query performance**, **simplicity**, and **reporting speed**  
- **Snowflake Schema:** Focus on **data integrity**, **storage efficiency**, and **maintainability**  
- Hybrid approach is sometimes used: **star schema for reporting, snowflake for storage**  

### Real-World Example
- **Retail Data Mart:** Star schema with `Sales_Fact` and dimensions like `Customer`, `Product`, `Time`  
- **Enterprise DWH:** Snowflake schema with `Product` dimension normalized into `Category` → `Subcategory` → `Product` tables  

---

    
