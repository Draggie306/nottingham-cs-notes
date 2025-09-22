A database is a shared collection of logically related data designed to meet the needs of an organisation.

### DBMS
Originally, each program had its own structure, file type etc. to store data. A Database Management System is a program in the middle of the application and the storage file to coordinate, define, create, maintain and access the database. Includes PostgreSQL, MS Access, etc.

### The Relational Model
A database is made of relations (tables). In each, there are attributes (named columns) and data itself, known as tuples (rows). The order is not important but there must not be duplicate tuples.
Each attribute/column has a domain - the set of all possible values allowed. This could be age, from 1 to 100.
The **degree** of the relation is how many attributes are in a table. The **cardinality** is how many entries/tuples there are.
A schema defines the relation’s attributes. It is typically the header row in a relation.

This can be written thus:
\{ ( Name, Joe ), ( Age, 23 ) }

A set of tuples in the same schema is the relation.
#### Keys
> … or Caius?

An attribute is a candidate key if it is unique for each tuple. These keys can consist of multiple/combined columns. 

It is difficult to determine these from a relation — the domain is much larger than the given values. Real-world knowledge is required.
To uniquely identify one tuple, we use one of the candidate keys, the primary key, often an ID.

NULL values indicate missing/unknown values. A candidate key cannot be null.

Foreign keys link data across relations. An employee may have a primary key of their ID, and another attribute of their department ID. This department ID can be linked to another relation that has Department ID as its primary key, with e.g. its name.

### Integrity
When referenced tuples are updated/deleted, referential integrity (dependency of a foreign key on primary key) may be violated. There are some options that can be used:
- RESTRICT - stops the action
- CASCADE - delete tuple attributes referencing it automatically
- SET NULL - set tuple attributes referencing it to NULL
- SET DEFAULT - set tuple attributes referencing it to the default attribute value.

### E-R Modelling
These are concepts, often drawn as diagrams, that give a view of entities (tuples), their attributes, and how they link (relationships). This makes it easy to see problems, such as many-to-many relationships, before implementing in the DBMS. 

An entity is represented as a box with rounded edges, with the name of the class. 
Attributes are represented as ovals linked to an entity, with the attribute name. These are the smallest “units”, i.e. cannot be broken down into more attributes, and belongs to a parent entity.
Relationships are an association between entities.

Once the ER diagram has been finalised, it is developed into schemas.

If an entity type has composite attributes (e.g. an `Address` - made of `Street`, `City`, etc.), only the components of the composite attribute are included in the new relation.

If there is a multivalued attribute - one that allows for several values in an attribute (e.g. `PersonInterests`, `UploadName`), two relations are created: the first containing all attributes of the original entity type except the multivalued attribute; and the second having the primary key of the first relation, and the multivalued attribute name.

A weak entity is one that does not have enough data or attributes to be identified with a primary key. To include them, a new relation should be created with the primary key of the identifying parent relation used as a foreign key. 

#### Cardinality Ratios
Each entity can participate in any number of instances of relationships.

- A 1:1 relationship means that each entity has one of another entity, like a lecturer and office.
- A 1:M relationship means one entity has many of another entity (but **not** the other way), like a lecturer and students they tutor.
- A M:M relationship means many entities all have many other entities, like students and modules.

In an E-R diagram, these relationships are shown in diamonds, with the end of the line showing cardinality. 

Ideally, M:M relationships should be removed - they duplicate data, slow down queries and can complicate referential integrity, resulting in mismatched data. To do this, two 1:M relationships can be made instead, joined with an associative entity in the middle. This makes computing and representing the data much easier.

#### Making a model
Given a description, entities and attributes can be identified as nouns (lecturer, student, module) and relationships are typically verbs (teaches, takes, enrols in).


### Normalisation
Normalisation is a set of rules to restructure relations, in order to reduce redundancy and to improve efficiency and integrity. Each relation should have a single purpose.

Anomalies in a database are inconsistencies, caused by when there is too much redundancy: making changes to one record may not update the record in another relation. There are three anomaly types: insertion (all details must be entered, else inconsistency/entity integrity violation), deletion (all details will be lost for a tuple even if something else depends on it) and modification (changes made in one relation must be made to others).

**Functional dependency**: when one attribute determines another - i.e. A -> B, every A value  determines every B value. *For example, a BuildingName may be functionally dependent on BuildingID — if BuildingID is 1, then BuildingName will always be the same, and only change if BuildingID is also changed.*

A full functional dependency is when one candidate key and no subset of it fully determines another - if BuildingID is the only thing that dictates BuildingName, then BuildingName is fully functionally dependent on BuildingID. 

> A is known as the determinant. 

**Transitive dependency**: when attributes depend on another, but through another attribute -- if A -> B and B -> C, and A does not functionally depend on B or C, then C transitively depends on A.
*For example, given BuildingID -> BuildingName, OwnerName, BranchNumber, and BranchNumber -> BranchAddress, then the transitive dependency BranchNumber -> BranchAddress exists on BuildingID, via BranchAddress, and also as BranchAddress/BranchNumber does not functionally determine BuildingID.* 


#### 1NF
Repeating groups/multivalued attributes are removed. This mean that each tuple can only have 1 of each attribute - e.g. `UploadName` can only have 1 value.

#### 2NF
Partial dependencies are removed. There should only be 1 candidate key (a primary key) that everything is fully functionally dependent on - e.g. `UserID, UploadID, UploadName` is split into two relations: one with `UserID, UploadID` and the other `UploadID, UploadName`.

#### 3NF
Transitive dependencies are removed. Every attribute for an entity must depend on nothing but the primary key. Let's say there is a `StudentID, StudentName, StudentCounty, StudentCity` - here, `StudentID -> StudentCounty` and `StudentCounty -> StudentCity` so `StudentCity` transitively depends on `StudentID` through `StudentCounty`. The `StudentCity` should be moved to another table, linked with the `StudentCounty` foreign key to the parent table.


### Relational algebra

Unary operators
- σ = select. σ ClockSpeedGHZ > 4 and CoreCount < 6 (CPUs) = select all from CPUs where ClockSpeedGHZ is above 4 and has less than 6 cores.
- Projection (Π). Only show the given fields (ΠClockSpeed(CPUs)). Also removes duplicates, unlike SQL statements

Binary operators:
- Union (∪) - a new table that contains all tuples from X and Y. Tuples must have the same number of attributes and be from the same domain. Duplicates are removed.
- Intersection (∩) - a new relation that consists of only tuples in both X and Y.
- Set Difference (-) - a new relation that contains all in X but not Y.
- Cartesian product (×) - a new relation that is the combination of all tuples in X and Y.
- Natural Join (⨝ / bowtie) - a new set of both relations X and Y, combining data from both tuples id they have common attribute(s).

All operators can be combined with inner brackets, which are evaluated from the inside out.

## SQL
SQL = structured query language.

SQLite uses a dynamic type system: types are dependent on the value added, not the column/attribute. There are 5 storage classes: NULL, INTEGER (1 to 8 bytes; not 7), REAL, TEXT and BLOB. Dates can be stored in YYYY-MM-DD, days since Nov 24 4714 B.C or seconds since 1970

The two mandatory clauses when writing a SQL query are `SELECT x FROM y`

```sql
CREATE TABLE tableName
(
	attribute1 blob NOT NULL,
	attribute2 real NOT NULL UNIQUE,
	attribute3 text DEFAULT "hello world",
	attributeId integer PRIMARY KEY AUTOINCREMENT,
	FOREIGN KEY(attributeId) REFERENCES otherTable(itemId) ON UPDATE CASCADE ON DELETE SET RESTRICT
);
```

You can use common sense to determine whether some things should be null or not.


- SELECT COUNT(\*) AS "Number of Items" - creates a new attribute named "Number of Items" with value of the number of tuples in a relation
- GROUP BY - forms groups of rows/tuples with the same attribute value, given it
- HAVING - filters groups subject to a condition

# Interfaces


### img

img src = "relative/absolute url" alt="alt text

```html
<figure>
	<img src ="..." alt="..." width="200" height="300" />
	<figcaption>
	caption here
	</figcaption>
</figure>
```


Images have licenses: 
- all rights reserved/closed copyright means you must have permission, pay the license fee or only use for fair use.
- permissive (Creative Commons) - no need to pay or ask permission, but may need credit, have derivative works under the same license, not use for commercial purposes.
- public domain: CC0 - no copyright applies to it, anyone can use it, no conditions.


### video

```html
<video src="file.webm" controls>
	<p>you cannot play this</p>
</video>


<video controls>
	<source src="file.mp4" type="video/mp4" />
	<source src="file.webm" type="video/webm" />
	<p>you cannot play this</p>
</video>
```

Audio works the same way.


### graphics

Vector and raster graphics can be used. THe img tag adds raster graphics, but the svg tag adds vector graphics. Vector graphics are instantly scalable. SVG is an XML-based language to describe vector images.

```html
<svg width="300" height="200">
	<rect width="100%" height="100%" fill="green" />
</svg>
```


### CSS

applied in an external stylesheet: 

```html
<link rel="stylesheet" href="styles.css" />
```

... or in an internal style tag...

```html
<html>
	<head>
		<style>
		h1 {
			color: pink;
			border: 1px solid yellow;
		}
		</style>
	...

```


... or inline

```html
<p style="color: pink;background-color: orange">
	hello
</p>
```


## Selectors
```css
/* All P elements with class yellowClass */
p.yellowClass { 
	color: yellow;
}

/* All em that must be within a li element */
li em {
	color: black;
}

/* Next sibling combinator: only a paragraph directly after a h2 */
h2 + p {
	background-color: red;
}


/* All 'embolden' class elements, in a p tag immediately after a h2, in the body */
body h2 + p .embolden {
	color: green;
	padding: 5px;
}

/* all p elements that are the child of body */
body > p {
	color: purple;
}
```


Specificity: element -> class -> id -> inline -> !important


### inlines
An element that is `inline` will not break onto a new line


Margin -> Border -> Padding -> Content

### functions


Mathematical operations can be performed for dynamic sizing of elements:
`width: calc(80% - 10px);`


### at rules

Imports another stylesheet:
```css
@import "anotherstyle.css";
```

The following rules only apply for screens below 500px:
`@media (max-width: 499px) `