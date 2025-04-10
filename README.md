# COVID Patient Management System

This is a simple C++ console-based application for managing COVID patient records. The system allows users to perform various operations such as adding new patients, viewing patient details by ID, and updating patient records.

## Features

- **Add New Patient**: Add a new patient's details such as name, address, age, gender, symptoms, tests, treatment, and status.
- **View Patient by ID**: View the details of a patient by entering their unique ID.
- **Update Patient by ID**: Update a patient's details by providing their unique ID.
- **Exit**: Exit the application.

## Classes and Design

### 1. `Corona` Class (Composition)
The `Corona` class represents the patient's health details. It includes attributes like:
- Name
- Address
- Age
- Gender
- Symptoms
- Tests
- Treatment
- Status

### 2. `PatientDetails` Class (Aggregation)
The `PatientDetails` class aggregates the `Corona` class, associating each patient with a unique ID. This class provides functions to:
- Display patient details
- Access and modify patient health information through the `Corona` object

### Data Structure
- **In-memory storage**: All patients' records are stored in a vector `patients` as `PatientDetails` objects.

## Usage

### 1. Add New Patient
- Enter a unique patient ID and other personal details such as name, address, age, gender, symptoms, tests, treatment, and status.

### 2. View Patient by ID
- Enter the patient's unique ID to view all details related to the patient.

### 3. Update Patient by ID
- Enter the patient's unique ID and modify any details such as name, address, age, symptoms, or treatment.

### 4. Exit
- Exit the application.

## Example Interaction

```plaintext
----- COVID Patient Management System -----
1. Add New Patient
2. View Patient by ID
3. Update Patient by ID
4. Exit
Enter choice:
