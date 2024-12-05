# Hospital Management System Database

This project is a comprehensive Hospital Management System Database designed to manage hospital operations efficiently. The database is implemented in SQL and includes tables for doctors, patients, appointments, departments, billing, and more. It supports functionalities like patient registration, appointment scheduling, billing, and medical records management.

## Features

- Doctor Management: Store and manage information about doctors, including specialization, contact details, and salary.
- Patient Management: Keep records of patients, their medical history, and associated doctors.
- Appointment Scheduling: Schedule and track patient appointments with doctors.
- Billing System: Manage billing details, including payment status and methods.
- Departmental Management: Organize hospital departments and their heads.
- Data Relationships: Establish meaningful relationships between patients, doctors, and appointments using foreign keys.

## Database Structure
This document outlines the database structure for the Hospital Management System (HMS). The database includes tables for managing patients, doctors, appointments, medical records, billing, and staff.

## Database Tables

### 1. **Patients Table**
This table stores information about patients.

| Column Name       | Data Type       | Constraints              |
|-------------------|-----------------|--------------------------|
| `patient_id`      | INT             | PRIMARY KEY, AUTO_INCREMENT |
| `first_name`      | VARCHAR(50)     | NOT NULL                |
| `last_name`       | VARCHAR(50)     | NOT NULL                |
| `gender`          | ENUM('Male', 'Female', 'Other') | NOT NULL |
| `date_of_birth`   | DATE            | NOT NULL                |
| `phone`           | VARCHAR(15)     | UNIQUE, NOT NULL        |
| `email`           | VARCHAR(100)    | UNIQUE                  |
| `address`         | TEXT            | NULL                    |
| `created_at`      | DATETIME        | DEFAULT CURRENT_TIMESTAMP |

### 2. **Doctors Table**
This table stores information about doctors.

| Column Name       | Data Type       | Constraints              |
|-------------------|-----------------|--------------------------|
| `doctor_id`       | INT             | PRIMARY KEY, AUTO_INCREMENT |
| `first_name`      | VARCHAR(50)     | NOT NULL                |
| `last_name`       | VARCHAR(50)     | NOT NULL                |
| `specialization`  | VARCHAR(100)    | NOT NULL                |
| `phone`           | VARCHAR(15)     | UNIQUE, NOT NULL        |
| `email`           | VARCHAR(100)    | UNIQUE                  |
| `address`         | TEXT            | NULL                    |
| `created_at`      | DATETIME        | DEFAULT CURRENT_TIMESTAMP |

### 3. **Appointments Table**
This table stores information about patient appointments with doctors.

| Column Name       | Data Type       | Constraints              |
|-------------------|-----------------|--------------------------|
| `appointment_id`  | INT             | PRIMARY KEY, AUTO_INCREMENT |
| `patient_id`      | INT             | FOREIGN KEY REFERENCES `Patients(patient_id)` ON DELETE CASCADE |
| `doctor_id`       | INT             | FOREIGN KEY REFERENCES `Doctors(doctor_id)` ON DELETE CASCADE |
| `appointment_date`| DATETIME        | NOT NULL                |
| `reason`          | TEXT            | NULL                    |
| `status`          | ENUM('Scheduled', 'Completed', 'Cancelled') | DEFAULT 'Scheduled' |

### 4. **Medical Records Table**
This table stores the medical records for each patient.

| Column Name       | Data Type       | Constraints              |
|-------------------|-----------------|--------------------------|
| `record_id`       | INT             | PRIMARY KEY, AUTO_INCREMENT |
| `patient_id`      | INT             | FOREIGN KEY REFERENCES `Patients(patient_id)` ON DELETE CASCADE |
| `doctor_id`       | INT             | FOREIGN KEY REFERENCES `Doctors(doctor_id)` ON DELETE CASCADE |
| `diagnosis`       | TEXT            | NOT NULL                |
| `prescription`    | TEXT            | NULL                    |
| `record_date`     | DATETIME        | DEFAULT CURRENT_TIMESTAMP |

### 5. **Billing Table**
This table stores billing information for appointments.

| Column Name       | Data Type       | Constraints              |
|-------------------|-----------------|--------------------------|
| `bill_id`         | INT             | PRIMARY KEY, AUTO_INCREMENT |
| `appointment_id`  | INT             | FOREIGN KEY REFERENCES `Appointments(appointment_id)` ON DELETE CASCADE |
| `amount`          | DECIMAL(10, 2)  | NOT NULL                |
| `payment_status`  | ENUM('Pending', 'Paid') | DEFAULT 'Pending' |
| `payment_date`    | DATETIME        | NULL                    |

## Relationships Between Tables:
- **Patients** can book **Appointments** with **Doctors**.
- **Appointments** may have associated **Medical Records** and **Billing**.

## Sample Data
The database includes sample data for testing and demonstration:
- Doctors: 15 records.
- Patients: 40 records.
- Appointments: 30 records.
- Departments: 5 records.
- Billing: 10 records.

## Prerequisites
- MySQL or any compatible database system.
- SQL client to run the scripts (e.g., MySQL Workbench, phpMyAdmin, or command-line tools).

## Future Enhancements
- Add more detailed patient records such as emergency contacts.
- Implement security features like access control.
- Create a front-end application to interact with the database.


