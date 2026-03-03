# SQL Joins & Set Operations Practice Guide

This repository contains a practice database and a set of exercises designed to test your knowledge of SQL Joins, Set Operations, and Subqueries. It is optimized for PostgreSQL and is perfect for technical exam preparation (such as the Administrateur 2ème grade IT concour).

## 🚀 Setup Instructions

Run the following SQL script in pgAdmin (or your preferred PostgreSQL client) to create the practice environment. The scenario tracks candidates who took a written IT exam and those who advanced to the oral interview.

```sql
-- Table 1: Candidates who passed the Written IT Exam
CREATE TABLE written_exam (
    candidate_id INT,
    full_name VARCHAR(50),
    specialty VARCHAR(50)
);

INSERT INTO written_exam (candidate_id, full_name, specialty) VALUES
(1, 'Lamine Yamal', 'Frontend Dev'),
(2, 'Pedri', 'Backend Dev'),
(3, 'Anas Bouteffah Touiki', 'Data Engineering'),
(4, 'Magnus Carlsen', 'AI & Data Science');

-- Table 2: Candidates who passed the Oral Interview
CREATE TABLE oral_exam (
    candidate_id INT,
    full_name VARCHAR(50),
    interview_room VARCHAR(10)
);

INSERT INTO oral_exam (candidate_id, full_name, interview_room) VALUES
(2, 'Pedri', 'Room A'),
(3, 'Anas Bouteffah Touiki', 'Room B'),
(5, 'Gavi', 'Room C'),
(6, 'Hikaru Nakamura', 'Room A');
```

## 🧠 Practice Exercises

Attempt to write the query for each goal before expanding the answer block to check your work.

### 1. INNER JOIN

**Goal:** Find the candidates who passed both the written and oral exams. The result should include their ID, name, specialty, and interview room.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT w.candidate_id, w.full_name, w.specialty, o.interview_room
FROM written_exam AS w
INNER JOIN oral_exam AS o
ON w.candidate_id = o.candidate_id;

or 

select t1.candidate_id, t1.full_name , specialty , interview_room 
from public.oral_exam as t1 inner join public.written_exam as t2 using (candidate_id)
```

</details>

### 2. LEFT JOIN

**Goal:** List all candidates who took the written exam. If they also made it to the oral exam, show their room. If they didn't, the room column should display NULL.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT w.candidate_id, w.full_name, w.specialty, o.interview_room
FROM written_exam AS w
LEFT JOIN oral_exam AS o
ON w.candidate_id = o.candidate_id;
```

</details>

### 3. RIGHT JOIN

**Goal:** List all candidates who took the oral exam. If they also took the written exam, show their specialty. Otherwise, show NULL.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT o.candidate_id, o.full_name, o.interview_room, w.specialty
FROM written_exam AS w
RIGHT JOIN oral_exam AS o
ON w.candidate_id = o.candidate_id;
```

</details>

### 4. UNION vs. UNION ALL

**Goal A:** Generate a single-column list of every unique name that appears in either table.
**Goal B:** Generate the same list, but allow duplicate names to appear.

<details>
<summary><b>💡 Click to reveal answers</b></summary>

```sql
-- Goal A: UNIQUE names (UNION)
SELECT full_name FROM written_exam
UNION
SELECT full_name FROM oral_exam;

-- Goal B: Includes DUPLICATES (UNION ALL)
SELECT full_name FROM written_exam
UNION ALL
SELECT full_name FROM oral_exam;
```

</details>

### 5. INTERSECT

**Goal:** Using a set operation (do not use a join), find the names of people who exist in both tables.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT full_name FROM written_exam
INTERSECT
SELECT full_name FROM oral_exam;
```

</details>

### 6. EXCEPT

**Goal:** Find the names of candidates who passed the written exam but not the oral exam.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT full_name FROM written_exam
EXCEPT
SELECT full_name FROM oral_exam;
```

</details>

### 7. SEMI JOIN (Using Subqueries)

**Goal:** A semi-join chooses records in the first table where a condition is met in the second table, without adding columns from the second table. Use a subquery with IN to find all data from the written_exam table for candidates who also took the oral exam.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT * FROM written_exam 
WHERE candidate_id IN (
    SELECT candidate_id FROM oral_exam
);
```

</details>

### 8. ANTI JOIN (Using Subqueries)

**Goal:** An anti-join chooses records in the first table that do not find a match in the second. Use a subquery with NOT IN to find the written candidates who were rejected before the oral interview.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT * FROM written_exam 
WHERE candidate_id NOT IN (
    SELECT candidate_id FROM oral_exam
);
```

</details>

### 9. CROSS JOIN

**Goal:** The database administrator needs to test scheduling combinations. Create a Cartesian product that pairs every single written candidate with every single oral interview room.

<details>
<summary><b>💡 Click to reveal answer</b></summary>

```sql
SELECT w.full_name AS written_candidate, o.interview_room
FROM written_exam AS w
CROSS JOIN oral_exam AS o;
```

</details>
