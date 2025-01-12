# Data Warehouse Notes
* All notes taken from the [Big Data Engineering in depth Course](https://youtube.com/playlist?list=PLxNoJq6k39G_m6DYjpz-V92DkaQEiXxkF&si=kw2CJj5jUw2oNcej)  

****Table of Content****


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
1. **Source System Layer**: This layer consists of various data sources, such as databases, applications, and external systems, that provide raw data to the data warehouse.

2. **Extraction Layer**: This layer handles the process of retrieving data from the source systems and preparing it for further processing.

3. **Staging Area**: A temporary storage area where extracted data is cleaned, validated, and transformed before being loaded into the data warehouse.

4. **Data Modeling**: This layer involves designing the data structure, including schemas and relationships, to optimize data organization and retrieval.

5. **ETL Layer**: The Extract, Transform, Load (ETL) layer processes data by extracting it from sources, transforming it as per business rules, and loading it into the warehouse.

6. **Storage Layer**: The storage layer is where the processed and structured data is securely stored for analysis and reporting purposes.

7. **Reporting (UI) Layer**: This layer provides tools and interfaces for users to visualize, query, and analyze the data in the warehouse.

8. **Metadata Layer**: The metadata layer stores information about the data's structure, sources, transformations, and usage to enable efficient management and understanding of the warehouse.

9. **System Operations Layer**: This layer oversees the operational aspects of the data warehouse, including monitoring, scheduling, and maintaining system performance.