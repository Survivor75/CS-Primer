## Database Management System

 1. Overview
 2. Components of DBMS
 3. DBMS Architecture
 4. Database Models
 5. ER Model
 6. ER Diagrams
 7. Generalization and Specialization
 8. Database Normalization
 9. Transactions 

 ### Overview
 
 **What is Data?**

**Data**  is nothing but facts and statistics stored or free flowing over a network, generally it's raw and unprocessed. For example: When you visit any website, they might store you IP address, that is data, in return they might add a cookie in your browser, marking you that you visited the website, that is data, your name, it's data, your age, it's data.

Data becomes  **information**  when it is processed, turning it into something meaningful. Like, based on the cookie data saved on user's browser, if a website can analyse that generally men of age 20-25 visit us more, that is information, derived from the data collected.

----------

**What is a Database?**

A  **Database**  is a collection of related data organised in a way that data can be easily accessed, managed and updated. Database can be software based or hardware based, with one sole purpose, storing data.

During early computer days, data was collected and stored on tapes, which were mostly write-only, which means once data is stored on it, it can never be read again. They were slow and bulky, and soon computer scientists realised that they needed a better solution to this problem.

**Larry Ellison**, the co-founder of  **Oracle**  was amongst the first few, who realised the need for a software based Database Management System.

----------

**What is DBMS?**

A  **DBMS**  is a software that allows creation, definition and manipulation of database, allowing users to store, process and analyse data easily. DBMS provides us with an interface or a tool, to perform various operations like creating database, storing data in it, updating data, creating tables in the database and a lot more.

DBMS also provides protection and security to the databases. It also maintains data consistency in case of multiple users.

Here are some examples of popular DBMS used these days:

-   MemSql
-   SQL Server
-   MongoDB
-   PostgreSQL
-   DynamoDB

----------

**Characteristics of Database Management System**

A database management system has following characteristics:

1.  **Data stored into Tables:**  Data is never directly stored into the database. Data is stored into tables, created inside the database. DBMS also allows to have relationships between tables which makes the data more meaningful and connected. You can easily understand what type of data is stored where by looking at all the tables created in a database.
2.  **Reduced Redundancy:**  In the modern world hard drives are very cheap, but earlier when hard drives were too expensive, unnecessary repetition of data in database was a big problem. But DBMS follows  **Normalisation**  which divides the data in such a way that repetition is minimum.
3.  **Data Consistency:**  On Live data, i.e. data that is being continuosly updated and added, maintaining the consistency of data can become a challenge. But DBMS handles it all by itself.
4.  **Support Multiple user and Concurrent Access:**  DBMS allows multiple users to work on it(update, insert, delete data) at the same time and still manages to maintain the data consistency.
5.  **Query Language:**  DBMS provides users with a simple Query language, using which data can be easily fetched, inserted, deleted and updated in a database.
6.  **Security:**  The DBMS also takes care of the security of data, protecting the data from un-authorised access. In a typical DBMS, we can create user accounts with different access permissions, using which we can easily secure our data by restricting user access.
7.  DBMS supports  **transactions**, which allows us to better handle and manage data integrity in real world applications where multi-threading is extensively used.

### Components of DBMS

The database management system can be divided into five major components, they are:

1.  Hardware
2.  Software
3.  Data
4.  Procedures
5.  Database Access Language

Let's have a simple diagram to see how they all fit together to form a database management system.

![components of database management system](https://www.studytonight.com/dbms/images/components-of-dbms.png)

**DBMS Components: Hardware**

When we say Hardware, we mean computer, hard disks, I/O channels for data, and any other physical component involved before any data is successfully stored into the memory.

When we run Oracle or MySQL on our personal computer, then our computer's Hard Disk, our Keyboard using which we type in all the commands, our computer's RAM, ROM all become a part of the DBMS hardware.

----------

**DBMS Components: Software**

This is the main component, as this is the program which controls everything. The DBMS software is more like a wrapper around the physical database, which provides us with an easy-to-use interface to store, access and update data.

The DBMS software is capable of understanding the Database Access Language and intrepret it into actual database commands to execute them on the DB.

----------

**DBMS Components: Data**

Data is that resource, for which DBMS was designed. The motive behind the creation of DBMS was to store and utilise data.

In a typical Database, the user saved Data is present and  **meta data**  is stored.

**Metadata**  is data about the data. This is information stored by the DBMS to better understand the data stored in it.

**For example:**  When I store my  **Name**  in a database, the DBMS will store when the name was stored in the database, what is the size of the name, is it stored as related data to some other data, or is it independent, all this information is metadata.

----------

**DBMS Components: Procedures**

Procedures refer to general instructions to use a database management system. This includes procedures to setup and install a DBMS, To login and logout of DBMS software, to manage databases, to take backups, generating reports etc.

----------

**DBMS Components: Database Access Language**

Database Access Language is a simple language designed to write commands to access, insert, update and delete data stored in any database.

A user can write commands in the Database Access Language and submit it to the DBMS for execution, which is then translated and executed by the DBMS.

User can create new databases, tables, insert data, fetch stored data, update data and delete the data using the access language.

----------

**Users**

-   **Database Administrators:**  Database Administrator or DBA is the one who manages the complete database management system. DBA takes care of the security of the DBMS, it's availability, managing the license keys, managing user accounts and access etc.
-   **Application Programmer or Software Developer:**  This user group is involved in developing and desiging the parts of DBMS.
-   **End User:**  These days all the modern applications, web or mobile, store user data. How do you think they do it? Yes, applications are programmed in such a way that they collect user data and store the data on DBMS systems running on their server. End users are the one who store, retrieve, update and delete data.

### DBMS Architecture

A Database Management system is not always directly available for users and applications to access and store data in it. A Database Management system can be  **centralised**(all the data stored at one location),  **decentralised**(multiple copies of database at different locations) or  **hierarchical**, depending upon its architecture.

**1-tier DBMS**  architecture also exist, this is when the database is directly available to the user for using it to store data. Generally such a setup is used for local application development, where programmers communicate directly with the database for quick response.

Database Architecture is logically of two types:

1.  2-tier DBMS architecture
2.  3-tier DBMS architecture

**2-tier DBMS Architecture**

2-tier DBMS architecture includes an  **Application layer**  between the user and the DBMS, which is responsible to communicate the user's request to the database management system and then send the response from the DBMS to the user.

An application interface known as  **ODBC**(Open Database Connectivity) provides an API that allow client side program to call the DBMS. Most DBMS vendors provide ODBC drivers for their DBMS.

![2-tier dbms architecture](https://www.studytonight.com/dbms/images/2-tier-dbms.png)

Such an architecture provides the DBMS extra security as it is not exposed to the End User directly. Also, security can be improved by adding security and authentication checks in the Application layer too.

**3-tier DBMS Architecture**

3-tier DBMS architecture is the most commonly used architecture for web applications.

![3-tier dbms architecture](https://www.studytonight.com/dbms/images/3-tier-dbms.png)

It is an extension of the 2-tier architecture. In the 2-tier architecture, we have an application layer which can be accessed programatically to perform various operations on the DBMS. The application generally understands the Database Access Language and processes end users requests to the DBMS.

In 3-tier architecture, an additional Presentation or GUI Layer is added, which provides a graphical user interface for the End user to interact with the DBMS.


### Database Models

A Database model defines the logical design and structure of a database and defines how data will be stored, accessed and updated in a database management system. While the  **Relational Model**  is the most widely used database model, there are other models too:

-   Hierarchical Model
-   Network Model
-   Entity-relationship Model
-   Relational Model

----------

**Hierarchical Model**

This database model organises data into a tree-like-structure, with a single root, to which all the other data is linked. The heirarchy starts from the  **Root**  data, and expands like a tree, adding child nodes to the parent nodes.

In this model, a child node will only have a single parent node.

This model efficiently describes many real-world relationships like index of a book, recipes etc.

In hierarchical model, data is organised into tree-like structure with one one-to-many relationship between two different types of data, for example, one department can have many courses, many professors and of-course many students.

![Hierarchical Model of database](https://www.studytonight.com/dbms/images/hierarchical-dbms-model.png)

**Network Model**

This is an extension of the Hierarchical model. In this model data is organised more like a graph, and are allowed to have more than one parent node.

In this database model data is more related as more relationships are established in this database model. Also, as the data is more related, hence accessing the data is also easier and fast. This database model was used to map many-to-many data relationships.

This was the most widely used database model, before Relational Model was introduced.

![Network Model of database](https://www.studytonight.com/dbms/images/network-dbms-model.png)

**Entity-relationship Model**

In this database model, relationships are created by dividing object of interest into entity and its characteristics into attributes.

Different entities are related using relationships.

E-R Models are defined to represent the relationships into pictorial form to make it easier for different stakeholders to understand.

This model is good to design a database, which can then be turned into tables in relational model(explained below).

Let's take an example, If we have to design a School Database, then  **Student**  will be an  **entity**  with  **attributes**  name, age, address etc. As  **Address**  is generally complex, it can be another  **entity**  with  **attributes**  street name, pincode, city etc, and there will be a relationship between them.

![E-R Model of database](https://www.studytonight.com/dbms/images/attribute-example.jpg)

**Relational Model**

In this model, data is organised in two-dimensional  **tables**  and the relationship is maintained by storing a common field.

This model was introduced by E.F Codd in 1970, and since then it has been the most widely used database model, infact, we can say the only database model used around the world.

The basic structure of data in the relational model is tables. All the information related to a particular type is stored in rows of that table.

Hence, tables are also known as  **relations**  in relational model.

![Relational Model of database](https://www.studytonight.com/dbms/images/relational-dbms-model.png)

### ER Model

As we described in the tutorial Database models, Entity-relationship model is a model used for design and representation of relationships between data.

The main data objects are termed as Entities, with their details defined as attributes, some of these attributes are important and are used to identity the entity, and different entities are related using relationships.

In short, to understand about the ER Model, we must understand about:

-   Entity and Entity Set
-   What are Attributes? And Types of Attributes.
-   Keys
-   Relationships

Let's take an example to explain everything. For a  **School Management Software**, we will have to store  **Student**  information,  **Teacher**  information,  **Classes**,  **Subjects**  taught in each class etc.

----------

**ER Model: Entity and Entity Set**

Considering the above example,  **Student**  is an entity,  **Teacher**  is an entity, similarly,  **Class**,  **Subject**  etc are also entities.

An Entity is generally a real-world object which has characteristics and holds relationships in a DBMS.

If a Student is an Entity, then the complete dataset of all the students will be the  **Entity Set**

----------

**ER Model: Attributes**

If a Student is an Entity, then student's  **roll no.**, student's  **name**, student's  **age**, student's  **gender**  etc will be its attributes.

An attribute can be of many types, here are different types of attributes defined in ER database model:

1.  **Simple attribute:**  The attributes with values that are atomic and cannot be broken down further are simple attributes. For example, student's  **age**.
2.  **Composite attribute:**  A composite attribute is made up of more than one simple attribute. For example, student's  **address**  will contain,  **house no.**,  **street name**,  **pincode**  etc.
3.  **Derived attribute:**  These are the attributes which are not present in the whole database management system, but are derived using other attributes. For example,  _average age of students in a class_.
4.  **Single-valued attribute:**  As the name suggests, they have a single value.
5.  **Multi-valued attribute:**  And, they can have multiple values.

----------

**ER Model: Keys**

If the attribute  **roll no.**  can uniquely identify a student entity, amongst all the students, then the attribute  **roll no.**  will be said to be a key.

Following are the types of Keys:

1.  Super Key
2.  Candidate Key
3.  Primary Key

----------

**ER Model: Relationships**

When an Entity is related to another Entity, they are said to have a relationship. For example, A  **Class**  Entity is related to  **Student**  entity, becasue students study in classes, hence this is a relationship.

Depending upon the number of entities involved, a  **degree**  is assigned to relationships.

For example, if 2 entities are involved, it is said to be  **Binary relationship**, if 3 entities are involved, it is said to be  **Ternary**  relationship, and so on.

### ER Diagrams

ER Diagram is a visual representation of data that describes how data is related to each other. In ER Model, we disintegrate data into entities, attributes and setup relationships between entities, all this can be represented visually using the ER diagram.

For example, in the below diagram, anyone can see and understand what the diagram wants to convey:  _Developer develops a website, whereas a Visitor visits a website_.

![example of er-diagram](https://www.studytonight.com/dbms/images/er-diagram.jpg)

----------

**Components of ER Diagram**

Entitiy, Attributes, Relationships etc form the components of ER Diagram and there are defined symbols and shapes to represent each one of them.

Let's see how we can represent these in our ER Diagram.

**Entity**

Simple rectangular box represents an Entity.

![Entity in ER diagram](https://www.studytonight.com/dbms/images/er-entity.png)

  

**Relationships between Entities - Weak and Strong**

Rhombus is used to setup relationships between two or more entities.

![Relationships in ER diagram](https://www.studytonight.com/dbms/images/er-relationship.png)

  

**Attributes for any Entity**

Ellipse is used to represent attributes of any entity. It is connected to the entity.

![Attribute in ER diagram](https://www.studytonight.com/dbms/images/er-attributes.png)

  

**Weak Entity**

A weak Entity is represented using double rectangular boxes. It is generally connected to another entity.

![Weak Entity in ER diagram](https://www.studytonight.com/dbms/images/er-weak-entity.png)

  

**Key Attribute for any Entity**

To represent a Key attribute, the attribute name inside the Ellipse is underlined.

![Key Attribute in ER diagram](https://www.studytonight.com/dbms/images/er-key-attr.png)

  

**Derived Attribute for any Entity**

Derived attributes are those which are derived based on other attributes, for example, age can be derived from date of birth.

To represent a derived attribute, another dotted ellipse is created inside the main ellipse.

![Derived Attribute in ER diagram](https://www.studytonight.com/dbms/images/er-derived-attr.png)

  

**Multivalued Attribute for any Entity**

Double Ellipse, one inside another, represents the attribute which can have multiple values.

![Multivalued Attribute in ER diagram](https://www.studytonight.com/dbms/images/er-multi-attr.png)

  

**Composite Attribute for any Entity**

A composite attribute is the attribute, which also has attributes.

![Composite Attribute in ER diagram](https://www.studytonight.com/dbms/images/er-composite-attr.png)

----------

**ER Diagram: Entity**

An  **Entity**  can be any object, place, person or class. In ER Diagram, an  **entity**  is represented using rectangles. Consider an example of an Organisation- Employee, Manager, Department, Product and many more can be taken as entities in an Organisation.

![Entity example ER Diagram](https://www.studytonight.com/dbms/images/entity-example.jpg)

The yellow rhombus in between represents a relationship.

----------

**ER Diagram: Weak Entity**

Weak entity is an entity that depends on another entity. Weak entity doesn't have anay key attribute of its own. Double rectangle is used to represent a weak entity.

![weak Entity example ER diagram](https://www.studytonight.com/dbms/images/weak-entity-example.jpg)

----------

**ER Diagram: Attribute**

An  **Attribute**  describes a property or characterstic of an entity. For example,  **Name**,  **Age**,  **Address**  etc can be attributes of a  **Student**. An attribute is represented using eclipse.

![attribute example](https://www.studytonight.com/dbms/images/attribute-example.jpg)

----------

**ER Diagram: Key Attribute**

Key attribute represents the main characterstic of an Entity. It is used to represent a Primary key. Ellipse with the text underlined, represents Key Attribute.

![key attribute example er diagram](https://www.studytonight.com/dbms/images/key-attribute-example.jpg)

----------

**ER Diagram: Composite Attribute**

An attribute can also have their own attributes. These attributes are known as  **Composite**  attributes.

![composite attribute example](https://www.studytonight.com/dbms/images/composite-attribute-example.jpg)

----------

**ER Diagram: Relationship**

A Relationship describes relation between  **entities**. Relationship is represented using diamonds or rhombus.

![relationship example er diagram](https://www.studytonight.com/dbms/images/relationship-example.jpg)

There are three types of relationship that exist between Entities.

1.  Binary Relationship
2.  Recursive Relationship
3.  Ternary Relationship

----------

**ER Diagram: Binary Relationship**

Binary Relationship means relation between two Entities. This is further divided into three types.

  

**One to One Relationship**

This type of relationship is rarely seen in real world.

![one-to-one relationship example er diagram](https://www.studytonight.com/dbms/images/one-to-one-example.jpg)

The above example describes that one student can enroll only for one course and a course will also have only one Student. This is not what you will usually see in real-world relationships.

  

**One to Many Relationship**

The below example showcases this relationship, which means that 1 student can opt for many courses, but a course can only have 1 student. Sounds weird! This is how it is.

![one-to-many example](https://www.studytonight.com/dbms/images/one-to-many-example.jpg)

  

**Many to One Relationship**

It reflects business rule that many entities can be associated with just one entity. For example, Student enrolls for only one Course but a Course can have many Students.

![one-to-many example](https://www.studytonight.com/dbms/images/many-to-one.jpg)

  

**Many to Many Relationship**

![many-to-many example](https://www.studytonight.com/dbms/images/many-to-many-example.jpg)

The above diagram represents that one student can enroll for more than one courses. And a course can have more than 1 student enrolled in it.

----------

**ER Diagram: Recursive Relationship**

When an Entity is related with itself it is known as  **Recursive**  Relationship.

![recursive relationship example ER diagram](https://www.studytonight.com/dbms/images/recursive-relationship.jpg)

----------

**ER Diagram: Ternary Relationship**

Relationship of degree three is called Ternary relationship.

A Ternary relationship involves three entities. In such relationships we always consider two entites together and then look upon the third.

![ternary relationship example ER diagram](https://www.studytonight.com/dbms/images/ternary-relationship.png)

For example, in the diagram above, we have three related entities,  **Company**,  **Product**  and  **Sector**. To understand the relationship better or to define rules around the model, we should relate two entities and then derive the third one.

A  **Company**  produces many  **Products**/ each product is produced by exactly one company.

A  **Company**  operates in only one  **Sector**  / each sector has many companies operating in it.

Considering the above two rules or relationships, we see that although the complete relationship involves three entities, but we are looking at two entities at a time.

### Generalization and Specialization

As the complexity of data increased in the late 1980s, it became more and more difficult to use the traditional ER Model for database modelling. Hence some improvements or enhancements were made to the existing ER Model to make it able to handle the complex applications better.

Hence, as part of the  **Enhanced ER Model**, along with other improvements, three new concepts were added to the existing ER Model, they were:

1.  Generalization
2.  Specialization
3.  Aggregration

Let's understand what they are, and why were they added to the existing ER Model.

----------

**Generalization**

**Generalization**  is a bottom-up approach in which two lower level entities combine to form a higher level entity. In generalization, the higher level entity can also combine with other lower level entities to make further higher level entity.

It's more like Superclass and Subclass system, but the only difference is the approach, which is bottom-up. Hence, entities are combined to form a more generalised entity, in other words, sub-classes are combined to form a super-class.

![generalization in ER model](https://www.studytonight.com/dbms/images/generalization.jpg)

For example,  **Saving**  and  **Current**  account types entities can be generalised and an entity with name  **Account**  can be created, which covers both.

----------

**Specialization**

**Specialization**  is opposite to Generalization. It is a top-down approach in which one higher level entity can be broken down into two lower level entity. In specialization, a higher level entity may not have any lower-level entity sets, it's possible.

![Specialization in ER Model](https://www.studytonight.com/dbms/images/specialization.jpg)

----------

**Aggregration**

Aggregration is a process when relation between two entities is treated as a  **single entity**.

![aggregration](https://www.studytonight.com/dbms/images/aggregration.jpg)

In the diagram above, the relationship between  **Center**  and  **Course**  together, is acting as an Entity, which is in relationship with another entity  **Visitor**. Now in real world, if a Visitor or a Student visits a Coaching Center, he/she will never enquire about the center only or just about the course, rather he/she will ask enquire about both.

### Database Normalization

Database Normalization is a technique of organizing the data in the database. Normalization is a systematic approach of decomposing tables to eliminate data redundancy(repetition) and undesirable characteristics like Insertion, Update and Deletion Anomalies. It is a multi-step process that puts data into tabular form, removing duplicated data from the relation tables.

Normalization is used for mainly two purposes,

-   Eliminating redundant(useless) data.
-   Ensuring data dependencies make sense i.e data is logically stored.

**Normalization Rule**

Normalization rules are divided into the following normal forms:

1.  First Normal Form
2.  Second Normal Form
3.  Third Normal Form
4.  BCNF
5.  Fourth Normal Form


**First Normal Form (1NF)**

For a table to be in the First Normal Form, it should follow the following 4 rules:

1.  It should only have single(atomic) valued attributes/columns.
2.  Values stored in a column should be of the same domain
3.  All the columns in a table should have unique names.
4.  And the order in which data is stored, does not matter.

----------

**Second Normal Form (2NF)**

For a table to be in the Second Normal Form,

1.  It should be in the First Normal form.
2.  And, it should not have Partial Dependency.

----------

**Third Normal Form (3NF)**

A table is said to be in the Third Normal Form when,

1.  It is in the Second Normal form.
2.  And, it doesn't have Transitive Dependency.

----------

**Boyce and Codd Normal Form (BCNF)**

**Boyce and Codd Normal Form**  is a higher version of the Third Normal form. This form deals with certain type of anomaly that is not handled by 3NF. A 3NF table which does not have multiple overlapping candidate keys is said to be in BCNF. For a table to be in BCNF, following conditions must be satisfied:

-   R must be in 3rd Normal Form
-   and, for each functional dependency ( X → Y ), X should be a super Key.

----------

**Fourth Normal Form (4NF)**

A table is said to be in the Fourth Normal Form when,

1.  It is in the Boyce-Codd Normal Form.
2.  And, it doesn't have Multi-Valued Dependency.


### Transactions


A transaction is a way of representing a state change. Transactions ideally have four properties, commonly known as ACID:

-   Atomic (if the change is committed, it happens in one fell swoop; you can never see "half a change")
-   Consistent (the change can only happen if the new state of the system will be valid; any attempt to commit an invalid change will fail, leaving the system in its previous valid state)
-   Isolated (no-one else sees any part of the transaction until it's committed)
-   Durable (once the change has happened - if the system says the transaction has been committed, the client doesn't need to worry about "flushing" the system to make the change "stick")

**Serializability**

When multiple transactions are being executed by the operating system in a multiprogramming environment, there are possibilities that instructions of one transactions are interleaved with some other transaction.

-   **Schedule**  − A chronological execution sequence of a transaction is called a schedule. A schedule can have many transactions in it, each comprising of a number of instructions/tasks.
    
-   **Serial Schedule**  − It is a schedule in which transactions are aligned in such a way that one transaction is executed first. When the first transaction completes its cycle, then the next transaction is executed. Transactions are ordered one after the other. This type of schedule is called a serial schedule, as transactions are executed in a serial manner.
    

In a multi-transaction environment, serial schedules are considered as a benchmark. The execution sequence of an instruction in a transaction cannot be changed, but two transactions can have their instructions executed in a random fashion. This execution does no harm if two transactions are mutually independent and working on different segments of data; but in case these two transactions are working on the same data, then the results may vary. This ever-varying result may bring the database to an inconsistent state.

To resolve this problem, we allow parallel execution of a transaction schedule, if its transactions are either serializable or have some equivalence relation among them.

**Equivalence Schedules**

An equivalence schedule can be of the following types −

**Result Equivalence**

If two schedules produce the same result after execution, they are said to be result equivalent. They may yield the same result for some value and different results for another set of values. That's why this equivalence is not generally considered significant.

**View Equivalence**

Two schedules would be view equivalence if the transactions in both the schedules perform similar actions in a similar manner.

For example −

-   If T reads the initial data in S1, then it also reads the initial data in S2.
    
-   If T reads the value written by J in S1, then it also reads the value written by J in S2.
    
-   If T performs the final write on the data value in S1, then it also performs the final write on the data value in S2.
    

**Conflict Equivalence**

Two schedules would be conflicting if they have the following properties −

-   Both belong to separate transactions.
-   Both accesses the same data item.
-   At least one of them is "write" operation.

Two schedules having multiple transactions with conflicting operations are said to be conflict equivalent if and only if −

-   Both the schedules contain the same set of Transactions.
-   The order of conflicting pairs of operation is maintained in both the schedules.

**Note**  − View equivalent schedules are view serializable and conflict equivalent schedules are conflict serializable. All conflict serializable schedules are view serializable too.

**States of Transactions**

A transaction in a database can be in one of the following states −

![Transaction States](https://www.tutorialspoint.com/dbms/images/transaction_states.png)

-   **Active**  − In this state, the transaction is being executed. This is the initial state of every transaction.
    
-   **Partially Committed**  − When a transaction executes its final operation, it is said to be in a partially committed state.
    
-   **Failed**  − A transaction is said to be in a failed state if any of the checks made by the database recovery system fails. A failed transaction can no longer proceed further.
    
-   **Aborted**  − If any of the checks fails and the transaction has reached a failed state, then the recovery manager rolls back all its write operations on the database to bring the database back to its original state where it was prior to the execution of the transaction. Transactions in this state are called aborted. The database recovery module can select one of the two operations after a transaction aborts −
    
    -   Re-start the transaction
    -   Kill the transaction
-   **Committed**  − If a transaction executes all its operations successfully, it is said to be committed. All its effects are now permanently established on the database system.
