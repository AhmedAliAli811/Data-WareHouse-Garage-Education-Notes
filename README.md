# Data Warehouse Notes
* All notes taken from the [Big Data Engineering in depth Course](https://youtube.com/playlist?list=PLxNoJq6k39G_m6DYjpz-V92DkaQEiXxkF&si=kw2CJj5jUw2oNcej)  

****Table of Content****


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
9. Shrunken Rollup Dimension.
10. Swappable Dimension.
11. Heterogenous Dimensions.
12. Multi-valued dimensions.

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
