# Hospital-management
CREATE TABLE Patients (
    patient_id INT PRIMARY KEY,
    patient_name VARCHAR(50),
    age INT,
    gender VARCHAR(10),
    doctor_id INT
);


CREATE TABLE Doctors (
    doctor_id INT PRIMARY KEY,
    doctor_name VARCHAR(50),
    department VARCHAR(50)
);



CREATE TABLE Bills (
    bill_id INT PRIMARY KEY,
    patient_id INT,
    bill_amount DECIMAL(10,2)
);
INSERT INTO Doctors (doctor_id, doctor_name, department)
VALUES
(1, 'Dr. Sharma', 'Cardiology'),
(2, 'Dr. Reddy', 'Neurology'),
(3, 'Dr. Kumar', 'Orthopedics');

INSERT INTO Patients (patient_id, patient_name, age, gender, doctor_id)
VALUES
(101, 'Ravi', 35, 'Male', 1),
(102, 'Priya', 28, 'Female', 2),
(103, 'Rahul', 45, 'Male', 3),
(104, 'Anjali', 32, 'Female', 2),
(105, 'Kiran', 60, 'Male', 1);

INSERT INTO Bills (bill_id, patient_id, bill_amount)
VALUES
(1, 101, 25000.00),
(2, 102, 40000.00),
(3, 103, 18000.00),
(4, 104, 35000.00),
(5, 105, 50000.00);

-- ==========================
-- 3. QUERIES USING JOINS
-- ==========================

-- Query 1: Patient Name and Doctor Name
SELECT
    p.patient_name,
    d.doctor_name
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id;

-- Query 2: Patient, Doctor and Department
SELECT
    p.patient_name,
    d.doctor_name,
    d.department
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id;

-- Query 3: Patient and Bill Amount
SELECT
    p.patient_name,
    b.bill_amount
FROM Patients p
JOIN Bills b
ON p.patient_id = b.patient_id;

-- Query 4: Complete Report (3 Table Join)
SELECT
    p.patient_name,
    p.age,
    d.doctor_name,
    d.department,
    b.bill_amount
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id
JOIN Bills b
ON p.patient_id = b.patient_id;

-- Query 5: Patients Whose Bill is Greater Than 30000
SELECT
    p.patient_name,
    d.department,
    b.bill_amount
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id
JOIN Bills b
ON p.patient_id = b.patient_id
WHERE b.bill_amount > 30000;

-- Query 6: Department-wise Total Revenue
SELECT
    d.department,
    SUM(b.bill_amount) AS total_revenue
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id
JOIN Bills b
ON p.patient_id = b.patient_id
GROUP BY d.department;

-- Query 7: Average Bill by Department
SELECT
    d.department,
    AVG(b.bill_amount) AS average_bill
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id
JOIN Bills b
ON p.patient_id = b.patient_id
GROUP BY d.department;

-- Query 8: Highest Bill with Doctor Details
SELECT
    p.patient_name,
    d.doctor_name,
    d.department,
    b.bill_amount
FROM Patients p
JOIN Doctors d
ON p.doctor_id = d.doctor_id
JOIN Bills b
ON p.patient_id = b.patient_id
ORDER BY b.bill_amount DESC
LIMIT 1;
