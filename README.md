# Data Warehouse Notes
* All notes taken from the [Big Data Engineering in depth Course](https://youtube.com/playlist?list=PLxNoJq6k39G_m6DYjpz-V92DkaQEiXxkF&si=kw2CJj5jUw2oNcej)  



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
    
 
 
 
## Chapter Two: Intro to Data Warehouse 

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













