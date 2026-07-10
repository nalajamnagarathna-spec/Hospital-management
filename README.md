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
