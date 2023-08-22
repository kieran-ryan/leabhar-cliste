# Database

## Database requirements collection & analysis

Database designers understand & **document** the data **requirements** of the database users.

Resulting data requirements must be written concisely and briefly - yet contains every detail.

Functional requirements must also be captured.

- Consists of user-defined operations

### Conceptual Design

Create conceptual schema using a high-level or conceptual data model - provides concepts close to the way how users see data.

- conceptual schema -> concise description of the data requirements & detailed description of the entity types, relationships and constraints
  - Do not contain implementation details

### Logical Design

**Actual implementation** of the database, using commercial DBMS.
Transform high-level conceptual design into the implementation data model - also known as 'data model mapping'.
Results in a DB schema in the implementation data model of the DBMS.

### Physical Design

Last step. Specify internal storage structures, indexes and access paths.
Along with these activities, application programs are designed, implemented as transactions corresponding to high-level transaction specification.

#### Weak Entity Types

Entity Types **do not have key attributes** of their own.
They are identified by relating to another entity type called the identifying or the **owner entity type**.
Identifying relationship -> relationship between weak entity type to its owner

#### Relationship

Association among 2+ entities.

Degree of relationship -> Number of entity types that participate in a relationship

- Unary -> Association with only one entity
- Binary -> Association among two entities
- Ternary -> Association among three entities

##### Relationship Constraints

- Cardinality Ratio -> Maximum number of relationship instances an entity can participate in
- Participation Constraints -> Specifies whether existence of an entity depends on its being related to another entity
  - Total participation -> represented by double line
  - Partial participation ->

## Other

Implement models with appropriate data validation

Define type of database best suited to the data requirements and associated software to use e.g. relational database, NoSQL, etc.

- Define most appropriate database software e.g. relational PostgreSQL and MySQL; NoSQL: MongoDB, Apache Cassandra; etc.

Define database infrastructure requirements

- Consistency level - strict (data is available to all readers on each save) or eventual (delay between writes and when data is available to reader)
- Consider whether more read or write operations are required
- Consider whether database requires sharding
  - Consider whether to shard by:
    - Feature:
    - Value e.g. user base in different countries
    - Hash - can be scaled through 'consistent hashing'
- Consider data replication requirements

Define cache to place in front of database to optimise performance - select most appropriate software e.g Redis, Memecached, etc.
