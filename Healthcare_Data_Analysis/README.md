# Hospital_Project_Sql

📘 Hospital Management SQL Project

This project is a SQL-based Hospital Management Database that manages patients, hospitals, diseases, visit history, and billing information.
It includes 50+ SQL queries using JOINs, GROUP BY, aggregate functions, views, date functions, and window functions.

📌 Project Objective

To design and analyze a hospital management system using SQL by:

Storing patient and hospital information

Tracking visit details and bills

Mapping diseases to hospital specializations

Performing analytical reporting for insights

🗂 Database Tables Used

patient_master – Patient personal and medical details

hospital_master – Hospital name, location, rating, specialization

visit_record – Visit date, bill amount, PatientID, HospitalID

disease_hospital_map – Disease and specialization mapping

patient_ratings – Patient feedback and ratings

🛠 Tools & Technologies

MySQL / MariaDB

SQL Workbench / DBeaver

SQL (DDL + DML)

📊 SQL Concepts Covered

SELECT, WHERE, ORDER BY

DISTINCT, GROUP BY, HAVING

INNER JOIN, LEFT JOIN

Aggregation (COUNT, SUM, AVG, MIN, MAX)

Window Functions (RANK, ROW_NUMBER)

Views

Date Functions

📈 Key Features of the Project

List of patients, hospitals, and diseases

Count hospitals, patients, and visits

Most common disease among patients

Hospitals with highest/lowest ratings

Total revenue generated per hospital

Month-wise patient visit growth

Patients who visited multiple hospitals

Hospitals treating more than one disease

TOP 3 hospitals per disease (Window Function)

View for patient–hospital–bill summary

📝 Example Query (Revenue Analysis)
SELECT h.HospitalName, SUM(v.TotalBill) AS Revenue
FROM hospital_master h
JOIN visit_record v ON h.HospitalID = v.HospitalID
GROUP BY h.HospitalName
ORDER BY Revenue DESC;

🧾 View Created in Project
CREATE VIEW patient_details AS
SELECT p.Name, h.HospitalName, v.VisitDate, v.TotalBill
FROM patient_master p
JOIN visit_record v ON p.PatientID = v.PatientID
JOIN hospital_master h ON v.HospitalID = h.HospitalID;
