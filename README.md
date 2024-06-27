create database Town_Mangement;
use Town_Mangement;
drop  database Town_Mangement;

CREATE TABLE Citizens (
    citizen_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    phone VARCHAR(15),
    address VARCHAR(200),
    date_of_birth DATE
);
CREATE TABLE Services (
    service_id INT PRIMARY KEY AUTO_INCREMENT,
    service_name VARCHAR(100),
    description TEXT,
    category VARCHAR(50)
);

CREATE TABLE Service_Requests (
    request_id INT PRIMARY KEY  AUTO_INCREMENT,
    citizen_id INT,
    service_id INT ,
    request_date DATE,
    status VARCHAR(50),
    FOREIGN KEY (citizen_id) REFERENCES Citizens(citizen_id),
    FOREIGN KEY (service_id) REFERENCES Services(service_id)
);
drop table Service_Requests;

CREATE TABLE Employees (
    employee_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    position VARCHAR(50),
    department VARCHAR(50)
);

CREATE TABLE Departments (
    department_id INT PRIMARY KEY AUTO_INCREMENT,
    department_name VARCHAR(100),
    description TEXT
);

CREATE TABLE Resources (
    resource_id INT PRIMARY KEY AUTO_INCREMENT,
    resource_name VARCHAR(100),
    quantity INT,
    location VARCHAR(100)
);

DELIMITER //
CREATE PROCEDURE InsertCitizen (
    IN first_name VARCHAR(50),
    IN last_name VARCHAR(50),
    IN email VARCHAR(100),
    IN phone VARCHAR(15),
    IN address VARCHAR(200),
    IN date_of_birth DATE
)
BEGIN
    INSERT INTO Citizens (first_name, last_name, email, phone, address, date_of_birth)
    VALUES (first_name, last_name, email, phone, address, date_of_birth);
END //
DELIMITER ;

DELIMITER //
CREATE PROCEDURE InsertService (
    IN service_name VARCHAR(100),
    IN description TEXT,
    IN category VARCHAR(50)
)
BEGIN
    INSERT INTO Services (service_name, description, category)
    VALUES (service_name, description, category);
END //
DELIMITER ;

DELIMITER //
CREATE PROCEDURE InsertServiceRequest (
    IN citizen_id INT,
    IN service_id INT,
    IN request_date DATE,
    IN status VARCHAR(50)
)
BEGIN
    INSERT INTO Service_Requests (citizen_id, service_id, request_date, status)
    VALUES (citizen_id, service_id, request_date, status);
END //
DELIMITER ;

DELIMITER //

CREATE PROCEDURE InsertEmployee (
    IN first_name VARCHAR(50),
    IN last_name VARCHAR(50),
    IN position VARCHAR(50),
    IN department VARCHAR(50)
)
BEGIN
    INSERT INTO Employees (first_name, last_name, position, department)
    VALUES (first_name, last_name, position, department);
END //

DELIMITER ;

DELIMITER //

CREATE PROCEDURE InsertDepartment (
    IN department_name VARCHAR(100),
    IN description TEXT
)
BEGIN
    INSERT INTO Departments (department_name, description)
    VALUES (department_name, description);
END //

DELIMITER ;

DELIMITER //

CREATE PROCEDURE InsertResource (
    IN resource_name VARCHAR(100),
    IN quantity INT,
    IN location VARCHAR(100)
)
BEGIN
    INSERT INTO Resources (resource_name, quantity, location)
    VALUES (resource_name, quantity, location);
END //

DELIMITER ;

DELIMITER //

CREATE PROCEDURE GetAllCitizens()
BEGIN
    SELECT * FROM Citizens;
END //

DELIMITER ;

DELIMITER //

CREATE PROCEDURE GetAllServices()
BEGIN
    SELECT * FROM Services;
END //

DELIMITER ;
DELIMITER //

CREATE PROCEDURE GetAllServiceRequests()
BEGIN
    SELECT * FROM Service_Requests;
END //

DELIMITER ;
-- Insert sample citizens
CALL InsertCitizen('Ali', 'Hamza', 'AliHamza@gmail.com', '+1234567890', '123 Elm Street', '1980-01-01');
CALL InsertCitizen('Ali', 'Haider', 'Ali@gmail.com', '+1234567891', '456 Oak Avenue', '1990-02-02');

-- Insert sample services
CALL InsertService('Garbage Collection', 'Weekly garbage collection service', 'Sanitation');
CALL InsertService('Water Supply', 'Daily water supply service', 'Utilities');

-- Insert sample service requests
CALL InsertServiceRequest(1, 1, '2024-06-01', 'Pending');
CALL InsertServiceRequest(2, 2, '2024-06-02', 'Completed');

-- Insert sample employees
CALL InsertEmployee('Ali', 'Brown', 'Manager', 'Sanitation');
CALL InsertEmployee('Haroon', 'White', 'Technician', 'Utilities');

-- Insert sample departments
CALL InsertDepartment('Sanitation', 'Handles waste management and recycling services');
CALL InsertDepartment('Utilities', 'Manages water, electricity, and other utilities');

-- Insert sample resources
CALL InsertResource('Truck', 5, 'Garage 1');
CALL InsertResource('Water Pump', 10, 'Storage Facility');

-- Verify citizens
SELECT * FROM Citizens;

-- Verify services
SELECT * FROM Services;

-- Verify service requests
SELECT * FROM Service_Requests;

-- Verify employees
SELECT * FROM Employees;

-- Verify departments
SELECT * FROM Departments;

-- Verify resources
SELECT * FROM Resources;
