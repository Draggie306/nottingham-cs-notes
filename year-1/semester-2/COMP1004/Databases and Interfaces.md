COMP1004 ~ University of Nottingham - Spring Semester, Year 1

**Module Convenors**
Dr Armaghan Moemeni (Magan) (C10B)
Dr Kai Xu (B83) - teaching second half.

# Introduction

## Learning Objectives
- Conduct a general requirement analysis for a database
- Design a data storage storage solution using a DBMS
- Use SQLite
- Build and query a relational database using SQL (first few weeks)
Second half (5 weeks):
- Design a web-based frontend with HTML, CSS and JS.
- Integrate front-end with a DBMS backend - online database
- Complete end-to-end web solution for data

Learning time: 100 hours of study time, 11 weeks of teaching with 22hrs lecture and 22hrs labs and practical.

New content weekly:
- Exercises and worksheets from moodle
- Labs and practicals on Tues 3-5pm (**not week 1**); some weeks have exercises and worksheets
- Courseworks to be done in the lab time, 
- 2hours of lectures a week on Mon 11am.

1970s content - can review A Level notes for this.
## Schedule
Weeks:
2. Relational Model - DBMS
3. Entity Relationship Diagram and Normalisation
4. Relational Algebra
5. Basics of SQL
6. Data Manipulation Language
> There will be an exam “mini quiz” here
7. HTML
8. CSS
9. JavaScript
10. Database
11. Testing

Fundamental module for CS, so understand the basics

## Assessment
Moodle quiz: 50% done in a lab slot in Week 6. This is on database system including relational database design and SQL. Closed-book - POTENTIALLY on Moodle with the Moodle content

Coursework: 50%. A database + web interfaced, released on week 7 and submitted in Week 12. This is manually marked. Feedback can be obtained *but not after submission or on the last few days*.
### Resources
- For SQLite - DB Browser for SQLite.
- Modern Database Management (Jefferey Hoffer)
- A Practical Approach to Design, Implementation and Management (Connolly, T.M.)
- Mozilla Development Network (MDN Web Docs). 

## About the module
### Databases
Databases are systems that are used to store data. The Relational Database Model was introduced in the 1970s. It has tables (relations), columns and rows, keys and operations. It also includes how to design, build and query/search for specific elements in the relational databases.


Database systems give a set of transferrable tools for storing, searching and managing information - they are a core concept in computer science software engineering. 
We need to store data and query it appropriately, and create a front-end application for users to access that data.

### Interfaces
Important to be able to be able to make native apps etc. across languages and platforms.


## Lecture 2
Originally, data storage was a completely file-based system. Each program had its own file format, and each program can read, write and manage its data. Any other program using the file has to know the format. 

It was realised that a **middleware** was a better solution to this, with a database program (such as SQLite, MySQL) that can coordinate access, without the need to write new storage & retrieval code for each application. Applications could thus communicate with the DBMS rather than the raw data directly.

> Database: a shared collection of logically related data and a description of the data designed to meet the needs of an organisation.
 
> Database management system: a software system that enables front-end users to define, create, maintain and access the database.

> Application programming interface (API): a program that interacts with to database through the DBMS with an appropriate request.

Just like with algorithms design, we need to design databases for different applications - a hospital database will be very different to a social media database.

We need to understand the data and data types, but we do not need to know how to implement the code to store/retrieve it.

### Relational data structure
The relational model was introduced by E.F. Codd in the paper “A relational model of data for large shared databanks”. This is the foundational model for most database systems. 
Information is stored as records in relations (tables). 

The model covers: 
- structure
- integrity
- manipulation (scripting languages with SQL)

- Data is stored in relations (tables).
- Relations are made of attributes (columns).
	- Each column has a domain - a set from which all possible values for that column can come from, e.g. the set of all first names from CS students
- Data takes the form of tuples (rows)
	- Tuples specify values for each attribute in a relation.
	- of which, there is no duplicate tuple and the order is not important

This could be seen as similar to OOP/java: each relation is a class. The entity is the instance.

> The **degree of a relation** is how long each tuple is/how many columns the table has.

> The **cardinality of a relation** is how many different tuples there are, or how many rows a table has.

> Attributes are the named columns in a relation.
> The heading/attributes for a relation is known as the **schema**.

A relation is therefore a set of tuples with the same schema.

### Keys
A set of attributes in a relation is a candidate key if, and only if:
- every tuple has a unique value for that set of attributes (**uniqueness**)
- no proper subset of the set has the uniqueness property (**minimality**)

To choose candidate keys, it is not a written rule to always use an ID, but this typically satisfies the rule of uniqueness and minimality.

One candidate key is usually chosen to identify tuples in a relation. This is called the Primary Key or just Key. Often, the rule of thumb is that a special attribute “ID” is used as the primary key.

A foreign key is used to link two or more relations.
A set of attributes in the first relation is a foreign key if its value matches a primary/candidate key in a second relation. This is called referential integrity.

When relations are updated, ref integ may be violated - when a referenced tuple is updated or deleted.
To solve this:
- RESTRICT: stop any updates to it
- CASCADE: let changes flow, dangerous but powerful
- SET NULL: make the referenced values NULL
- SET DEFAULT: make the referenced values the default for their column.

### NULLs
Missing/blank/empty data can be represented using NULL. This indicates a missing or unknown value - not the same as 0 or blank space. *Primary keys must not contain NULL - this is entity integrity, as it contradicts the rules.*

## Database Design — todo: recap this!!
Entity/Relationship modelling is used for conceptual design. 
- Entities are objects or items of interest. They can be physical or abstract.
- Attributes are properties of an entity
- Relationships are the links between entities.
The models and diagrams give a conceptual view of the database and can help identify problems in a design. They are independent of the DBMS.


Relationships have a name, set of entities that partake in them

The cardinality ratio is how many relationships the entity has. Each entity can participate in zero, one, or more than one instance of that relationship.

One-to-one: each lecturer has a unique office and offices are single occupancy.
One-to-many: each tutor tutors many students; each student has one tutor.
Many-to-many: each student takes many modules, and each module can be chosen by many students.

Many-to many databases require data entry, which is more costly. Similarly, one-to-one relations are avoided too as they can usually be combined into 1-to-many.

> When working out the cardinality in E/R diagrams, think about whether it makes sense to link from BOTH SIDES. For example, many departments can have many courses, but many courses cannot have many departments. Many courses can be offered by one department; one department offers many courses.


### Turning ER diagrams into relations
Each regular entity can be transformed into a relation of the same type’s name. Equally, the attributes of the entity become one of the relation. The entity type’s identifier becomes the primary key of the relation.

#### Handling multivalued attributes
When a regular entity contains a multivalued attribute, two new relations are created. The first contains all the attributes except the multivalued attribute. The second relation contains only 2 attributes: the primary key from the first relation and the multivalued attribute name.

#### Weak entities
A weak entity is one that can only exist under another entity and cannot therefore be identified by its attributes - there is no primary key. 

Therefore, for each type of a weak entity, create a new relation (table) and include all its simple attributes as the relation’s attributes. The primary key of the identifying (parent) relation will be used as a foreign key in the new relation. 

## Normalisation
Normalisation in database management refers to a set of rules that reorganises relations in a way that reduces redundancy and improves data integrity.

### Removing many-to-many relationships
Many-to-many relationships are difficult to represent in a database and (alongside one-to-ones) will cause many more lookups than the optimal amount.


https://cdn.discordapp.com/attachments/1243582890185326616/1346472280280273037/COMP1004_mergedSolutions.pdf?ex=67c84f87&is=67c6fe07&hm=2eb53d60e38f4b3c0425c427f310cf56891e831da5d6536281600476dbe53967&

## Finding mistakes
When reviewing an ER diagram for potential improvements, it helps to use a systematic checklist. Below are several key aspects you should verify along with some examples drawn from your questions:

### 1. **Entity Completeness and Association**

- **Check for Missing Entities:**  
    Ensure that all real-world objects and their interactions are modeled. If there are many-to-many relationships that involve additional attributes or if business rules imply an intermediary, you might need an associative entity.  
    _Example:_ The suggestion that “there are at least two missing associate entities” means you should review if any relationships (e.g., between staff and location) require a separate linking entity to capture additional details.

### 2. **Relationship Cardinality and Participation**

- **Define Cardinality Clearly:**  
    Verify that every relationship has a clearly defined cardinality (one-to-one, one-to-many, or many-to-many). Missing cardinalities can lead to ambiguity.  
    _Examples:_
    
    - The missing cardinality between “Location” and “Librarian” suggests that you need to decide whether the relationship is one-to-one, one-to-many, or many-to-many.
    - The possibility that “the relationship between ‘Item’ and ‘Location’ should be one-to-one” requires you to reassess the business rules behind that relationship.
- **Review Participation Constraints:**  
    Check if entities are required to participate in a relationship (mandatory vs. optional) to enforce business rules accurately.
    

### 3. **Attribute Assignment and Correctness**

- **Appropriate Attribute Placement:**  
    Each attribute should logically belong to the entity that best represents it.  
    _Examples:_
    - If “Aisle” is a characteristic that uniquely identifies a property of an “Item” (or its placement), it might belong as an attribute of “Item” rather than as a standalone entity.
    - If “Weight” is a property of a physical location (like a storage facility’s capacity or the weight limit of items it can hold), then it should be part of “Location” rather than “Item.”

### 4. **Primary Keys and Foreign Keys**

- **Verify Key Constraints:**  
    Ensure that every entity has a primary key and that relationships are supported by appropriate foreign keys.  
    _Example:_
    - The note that “Locationid is missing in ‘Item’” suggests that you should confirm that the foreign key linking an item to its location is present to enforce referential integrity.

### 5. **Mapping of Organizational or Assignment Relationships**

- **Identify Relationship Clarity:**  
    Sometimes, the ER diagram must capture not just the existence of entities but also which entity instances are related in specific contexts.  
    _Example:_
    - “From the ERD it cannot be identified which staff member will be working at which location.” This indicates a potential oversight where a linking relationship or an associative entity (possibly with additional attributes like work schedule) is required.

### 6. **Normalization and Reducing Redundancy**

- **Avoid Data Redundancy:**  
    Check that the ER diagram adheres to normalization rules, ensuring that data is stored efficiently and that updates don’t lead to inconsistencies.  
    _Example:_
    - If the “Location” and “Librarian” relationship is many-to-many (as suggested), then breaking it down into an associative entity can prevent redundancy and support additional attributes about the assignment.

### 7. **Business Rule Conformance and Logical Consistency**

- **Validate Against Business Requirements:**  
    Confirm that the model accurately reflects business rules. Ask questions such as:
    - Should an “Item” always be located in one place (one-to-one) or can it be available at multiple locations (one-to-many or many-to-many)?
    - How is responsibility assigned to staff or librarians relative to locations?Each answer to these questions will drive whether the current structure meets the needs or requires adjustments.

---

**In summary:**  
When evaluating an ER diagram, you should verify that all entities and relationships are present and correctly defined, attributes are appropriately assigned, key constraints are maintained, and that the model fully captures business rules without ambiguity. By systematically checking for missing associative entities, ambiguous cardinalities, misassigned attributes, and unclear relationships (especially in staff-location mappings), you can identify potential areas of improvement and ensure a robust, logically consistent database design.


### Constraints
`AUTOINCREMENT`
- A very useful constraint to add (especially to primary keys) to ensure there is a unique value generated


`check` function
- can use any arithmetic operator in the function

> alert (not alter)

`ALTER TABLE`
SQLite can only perform limited functionality of the ALTER TABLE statement.
- **Rename** a table: `ALTER TABLE x RENAME TO y`
- **Add** a new table: `ALTER TABLE x ADD COLUMN y`
- **Rename** a column: `ALTER TABLE x RENAME COLUMN y TO z`
- **Drop** column: `ALTER TABLE x DROP COLUMN y`

The `DELETE` keyword can delete 

`UPDATE`
- Can `SET` the values to anything e.g. `SET AGE = 20 WHERE name=“S”`


### SELECT
Is the most important keyword in any database.
- Using `SELECT DISTINCT x FROM y` restricts the output to remove duplicate results (ALL instead retains the duplicates, and is implied by default)

columnExpression \[ AS newName ]
FROM TableName \[, …]

There is a sequence
- `FROM` the table(s) to be used
- `WHERE` comparision/arithmetic/pattern condition to filter rows subject to a condition
- `GROUP BY` forms groups of rows with the same column value or subject to a condition
- `HAVING` filters by a specific condition
- `SELECT` the columns to appear in the output
- `ORDER BY` specifies the order of the output


### WHERE
Search conditions can include a comparison, range, set membership, pattern match or nullity.

#### Comparison (operators)
Includes operators `=`, `!=`, `<`, `>`, `<=`, `>=`.
```sql
SELECT *
FROM customer
WHERE age > 25 or phone is not null
```

####  Range (IN)

```sql
SELECT *
FROM customer
WHERE price IN (20, 26);
-- IN is particularly efficient for large datasets
-- OR:
-- WHERE (price >= 20) AND (price <= 26)
```

#### Pattern match (LIKE)
It has many uses, including searches for content of the text/string values, including the date.
It is not as strict as a strict equality `=`, so allows us to search things like name abbreviations, certain email providers, dates only in 2025, etc.

The keyword is `LIKE`.
```sql
SELECT *
FROM bouquet
WHERE bouquet_name LIKE “H%”;
-- WHERE bouquet_name LIKE “H___”;
-- WHERE bouquet_name LIKE “%h%”;
```
`LIKE “H%”` matches House, Home, Harry, etc.
`LIKE “H___”` matches Home, Hack, Hall

The wildcards are `%` and `_`, where % means any sequence of 0 or more characters and `_` is a specific single character. 

![[Pasted image 20250303122509.png]]


#### LIMIT
To only show a given number of rows, we can use a LIMIT to limit the data amount returned bu the WHERE statement.

```sql
SELECT x FROM y WHERE z LIMIT 3;
```


#### Aggregate Functions
These include COUNT, SUM, AVG, MIN and MAX. They operate on a single column and return a single value.
- All of these apart from COUNT eliminates nulls and operates only on the remaining non-null values.
COUNT counts all the rows of a table including duplicates and NULLs (use distinct to remove these).


```sql
SELECT COUNT(cust_id) AS “Customer Count”
SUM(salary) AS “Salary”
FROM customer
WHERE name LIKE “%s%”

-- outputs Customer Count: 7 and Salary: 46
-- 
```

### Relational algebra

Database problems can be expressed in 3 different main ways:
- English
	- “list all staff with a salary greater than £50,000”
- Relational Algebra
	- “sigma salary > 10000 (Staff)”
- SQL
	- `SELECT * FROM Staff WHERE Salary > 10000`


Relational algebra  has two different sets of operations: unary and binary.

Unary operations work on on a single table
- projection
- selection works on criteria or condition

Binary operations
This is similar to set theory, but instead of sets, there are tables.
- Cartesian product (x)
- Union
- Intersection
- Difference
- Join

### Selection
The selection operation works on a single relation/table R and defines a relation that contains only those tuples of R that satisfy the specified condition (predicate).
Multiple predicates or rules can be applied - AND & ORs can be very useful.

The final table - the result of the selection - is a subset of the original table.

“list all staff whose salaries are above £10k”


### Projection
This operation works on a single relation R and gets the values of specified attributes. *In algebraic representation, duplicates are removed too; this is not the case for SQL.*

Projection can be combined with selection to project attributes from a given table, but with added ”filters”.

==Project ”city” attribute from table “country”==

To speed up the database interaction, we use projections (but keeping the foreign key) to project the right attribute based on the right question/statement.

### Union
Between two relations R and S, the result of the union of them is those included in either/both of the input relations, with duplicates removed. 

> Union compatibility: given two tables, the first job is to ensure that both tables have the same domain with the same number of attributes (column). If they are not, we need to make corrections.


### Set Difference
The tuples in R but not in S is R-S.
Union compatibility must be upheld.

### Intersection
Opposite to the union. The operation defines a new relation, consisting of the set of all tuples in **BOTH** R and S. ONLY what is shared between both input relations. 

`R ∩ S = R - (R-S)`

### Cartesian product
This operation defines a relation that is the concatenation of every tuple of relation R with every tuple of relation S. 

For example:
```
A 1
B 2 
```
becomes:
```
A 1
A 2
B 1
B 2
```

There should be a common attribute - the foreign key - repeated once between the two tables

### Natural join
This is a join of the two relations R and S over a common attribute, the key. One occurrence of the common attribute is removed from the result.
This is used by the ⋈ operator.

## SQL
Allows us to access and manipulate databases. It is a standard of ANSI - but whilst it is so, its support amongst DBMS is different and not supported in the exact same way.


DDL - Data definition language
- Used for creating and modifying database object objects such as tables.
- DDL statements define the **structure** and organisation of data in the database - e.g, setting data types

DML - data manipulation language
- Used for inserting into, retrieving and manipulating data in a database. 

DCL - data control language
- Used for controlling security and access to a database
- Commands for creating/dropping accounts, updating permissions

A static type system is one that has a column declared with a specific data type, and only those with that data type can be added to it.

#### Storage Classes
There are 5 main storage classes (broader than just data types):
- NULL
- Integer
- Real
- Text
- Blob

#### Constraints
It is important to have constraints in tables. These are usually defined when using the `CREATE TABLE` syntax.

- NOT NULL
	- must not be empty.
- DEFAULT
	- a default value used if not provided with one when inserting new data. this could be e.g. having a default semester of 1 for all new students.
- UNIQUE
	- ensures all values in a column are different - each value must have a different key number
- CHECK
	- Can restrict certain values to meet certain criteria (e.g. `check(age > 10)`)
- PRIMARY KEY
	- Uniquely identifies each record in a table.
	- (by default is unique)
	- If the primary key is a combination of two or multiple columns, we can specify this as `PRIMARY KEY(id_1, id_2)`
- FOREIGN KEY
	- Is important to specify this to reduce the chances of operations destroying references between tables
	- Uniquely identifies a given tuple/row



### Averages & comparison
Example:
```sql
SELECT staffid AS 'Staff ID', positionname AS 'Position', salary AS 'Annual Salary', salary -(SELECT AVG(salary) FROM staff) AS 'Salary Difference'

FROM staff,staff_positions
WHERE staff.position = staff_positions.positionid AND salary > (SELECT AVG(salary) FROM staff)
ORDER BY positionname;
```


### Joining
The default `JOIN` is an inner join - selects and joins record that have matching values in both tables.

`SELECT x FROM y`

`JOIN table_to_combine_rows ON existing_table.primarykey = table_to_combine_rows.primarykey`

> the resulting existing_table all the columns as the table_to_combine_rows, based on whether each row has a matching primarykey.
