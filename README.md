# Data Normalization and Entity-Relationship Diagramming

An assignment to normalize the structure of data and establish a set of Entity-Relationship Diagrams for the data.

## the Original Table
| assignment_id | student_id | due_date | professor | assignment_topic                | classroom | grade | relevant_reading    | professor_email   |
| :------------ | :--------- | :------- | :-------- | :------------------------------ | :-------- | :---- | :------------------ | :---------------- |
| 1             | 1          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 80    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 2             | 7          | 18.11.21 | Logston   | Single table queries            | 60FA 314  | 25    | Dümmlers Chapter 11 | e.logston@foo.edu |
| 1             | 4          | 23.02.21 | Melvin    | Data normalization              | WWH 101   | 75    | Deumlich Chapter 3  | l.melvin@foo.edu  |
| 5             | 2          | 05.05.21 | Logston   | Python and pandas               | 60FA 314  | 92    | Dümmlers Chapter 14 | e.logston@foo.edu |
| 4             | 2          | 04.07.21 | Nevarez   | Spreadsheet aggregate functions | WWH 201   | 65    | Zehnder Page 87     | i.nevarez@foo.edu |
| ...           | ...        | ...      | ...       | ...                             | ...       | ...   | ...                 | ...               |

## Reasons of Not 4NF
Because the current/original table has data redundancy, the repetition of facts in multiple places within the data.
Also, because it violetes the requirement of 4NF, it has two more independent multi-valued fact about an enity. For example, A single professor who teachs multiple sections, or a single student who does multiple assignments (two independent multi-valued facts about them) might erroneously be represented with two or more independent multi-valued fact fields.
Also, it violets the requirement of 3NF. All non-key field are not about the fact of the primary key, like the professor email belongs to professor not student about the place/address rather than the users, and the relevant readings, assigment topics belong tp assignment as well. 

# Tables in 4NF
## Create a table for Assignment
| STUDENT_ID | ASSIGNMENT_ID | ASSIGNMENT_TOPIC                | DUE_DATE | READINGS            |
|------------|---------------|---------------------------------|----------|---------------------|
| 1          | 1             | Data Normalization              | 23.02.21 | Deumlich Chapter 3  |
| 7          | 2             | Single Table Queries            | 18.11.21 | Dümmlers Chapter 11 |
| 4          | 1             | Data Normalization              | 23.02.21 | Deumlich Chapter 3  |
| 2          | 5             | Python and Pandas               | 05.05.21 | Dümmlers Chapter 14 |
| 2          | 4             | Spreadsheet Aggregate Functions | 04.07.21 | Zehnder Page 87     |
| ...        | ...           | ...                             | ...      | ...                 |

## Create a table for Professor
| STUDENT_ID | PROFESSOR_NAME | PROFESSOR_EMAIL   |
|------------|----------------|-------------------|
| 1          | Melvin         | l.melvin@foo.edu  |
| 7          | Logston        | e.logston@foo.edu |
| 4          | Melvin         | l.melvin@foo.edu  |
| 2          | Logston        | e.logston@foo.edu |
| 2          | Nevarez        | i.nevarez@foo.edu |
| ...        | ...            | ...               |
## Create a table for section
| STUDENT_ID | CLASSROOM |
|------------|-----------|
| 1          | WWH 101   |
| 7          | 60FA 314  |
| 4          | WWH 101   |
| 2          | 60FA 314  |
| 2          | WWH 201   |
| ...        | ...       |

## Create a table for grade
| STUDENT_ID | ASSIGNMENT_ID | GRADE |
|------------|---------------|-------|
| 1          | 1             | 80    |
| 7          | 2             | 25    |
| 4          | 1             | 75    |
| 2          | 5             | 92    |
| 2          | 4             | 65    |
| ...        | ...           | ...   |

# ERD 
![ E-R Diagram](./images/images_.svg)

# Description of the changes
I made 4 tables in order to let the original dataset table to be in 4NF. Since some of them should be dependent from each other, I splited the data up into multiple tables. I created a table for assignment, the assignment ID, assignment topic, relavant readings and due date are in this table, they are dependent upon the other, then it works for 4NF. The assignment has relationship with students and grades. Then, I created a table for grades, which means students do assignments and assignments have grade. So, they are dependent upon each other and no longer independent.
Then, I made tables for professor and sections. Each professor have their names and emails and the students they teach; the table section has the classroom. Since professor has sections and students attend sections, they are dependent upon each other as well. Thus, these 4 tables' formats are allowed in 4NF. 