# 🏅 Sports Inventory Management System (SIMS)

A backend DBMS project developed using **Oracle SQL** and **PL/SQL**, designed for managing sports items, student performance, and automated shortlisting for competitions. This project simulates a real-world inventory and student evaluation workflow in a college sports department.

---

## 📘 Project Overview

This system ensures:
- Students can **issue any number of items on the same day**
- On the **next day**, students **cannot issue more items unless previous ones are returned**
- A **fine of ₹10 per day** is calculated if items are **not returned on the due date**
- Staff members **evaluate student performance**; students with **rating > 8** are **auto-shortlisted**
- Shortlisted students are recommended for competitions
- Various **stored procedures, triggers, and cursors** are used for real-time data handling and reporting

---

## 🛠️ Tech Stack

- **Oracle SQL**
- **PL/SQL** — Procedures, Triggers, Sequences, Cursors
- **SQL Developer** — Execution & Testing
- **GitHub** — Version control and documentation

---

## ✨ Key Features

### 🎓 Student Equipment Issuing
- Students can issue **multiple items** in one day
- Cannot issue new items next day **unless all previously issued items are returned**
- Logic implemented using **procedure + validations**

### 📆 Fine Calculation Logic
- If item is **not returned by due date**, system adds **₹10 fine per extra day**
- Fine is automatically inserted in the **Fine_Payment** table with `UNPAID` status
- Another procedure handles **fine payment marking**

### 📈 Performance Evaluation + Shortlisting
- Staff assign **ratings** to students in specific sports
- If **skill_rating > 8**, student is **auto-added to the shortlist**
- If rating drops below 8 later, student is **removed** from shortlist
- This logic is implemented using a **trigger**

### 📊 Dynamic Reports with Cursors
You can run a procedure `run_named_cursor()` with the following options:
- `OVERDUE_STUDENTS` — Students who didn’t return items on time
- `LOW_STOCK_ITEMS` — Items with low availability
- `UNPAID_FINES` — Pending fine payments
- `MOST_USED_ITEMS` — Most frequently issued items
- `STUDENT_ISSUE_HISTORY` — Item-wise issue-return history
- `SHORTLISTED_STUDENTS` — Currently shortlisted students
- `PERFORMANCE_LOG` — All performance ratings
- `ALL_ITEMS` — Inventory overview

---

## 🧱 Entity List

- `Student`, `Staff`, `Item`, `Issue_Record`, `Return_Record`, `Fine_Payment`
- `Performance_Log`, `Shortlist`, `Sports_Type`
- `Student_Phone`, `Staff_Phone`

---

## 📁 Files Included

| File | Description |
|------|-------------|
| `dbms_code.txt` | Full SQL + PL/SQL code (tables, procedures, triggers, cursors) |
| `SIMS_Report.pdf` | Final report with diagrams, use-case explanation, and logic flow |

---

## 👨‍💻 Developed By

> **Team — Thapar Institute of Engineering & Technology**  
> - Harshit Katyal  
> - Bhavish Pushkarna
> - Shubham Goyal
> - Aryan Bindra

---

## 🚀 Sample Calls

```sql
-- Add student
BEGIN
  add_new_student_with_phones(101, 'Harshit', 'Katyal', 'harshit@example.com', 'CSE', '9876543210', '8765432109');
END;

-- Issue item
BEGIN
  issue_item_to_student(p_student_id => 101, p_item_id => 201);
END;

-- Return item
BEGIN
  return_item_from_student(p_issue_id => 1001);
END;

-- Evaluate student (rating > 8 will trigger shortlist)
BEGIN
  add_or_update_performance_log(101, 'Football', 302, 9.2, 12);
END;

-- Display students who didn’t return items on time
BEGIN
  run_named_cursor('OVERDUE_STUDENTS');
END;
