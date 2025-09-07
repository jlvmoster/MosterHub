### Minimize Historical Data

### Stateful Operations (INSERT, UPDATE, DELETE)

### Third Normal Form (3NF) or Higher

Incoming data is detailed and real-time, so the best practice in storing this type of data is by normalizing the structure in terms of entity model (e.g. student, professor, course, etc.).

#### Example

Imagine a table named "Students" with the following columns: `Student_ID`, `Student_Name`, `Course`, `Course_Instructor`. In this table, `Course_Instructor` depends on `Course`, which in turn depends on `Student_ID`. This creates a transitive dependency.

To achieve 3NF, the "Students" table can be split into two tables:

- **"Students" table:** Contains `Student_ID`, `Student_Name`
- **"Courses" table:** Contains `Course_ID`, `Course_Name`, `Course_Instructor`

#### Benefits of 3NF Normalization

**Reduced Redundancy:** By storing course information in a separate table, data redundancy is minimized. For example, a course's instructor is only stored once, not for each student enrolled.

**Data Integrity:** Updates to course information (e.g., instructor) only need to be made in one place, preventing inconsistencies.

**Improved Data Management:** This structure allows for easier management of student and course data, as they are separated into distinct entities.
