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