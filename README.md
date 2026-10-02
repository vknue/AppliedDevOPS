# Hospital Management — DevOps Project

## 1. Project overview
## 2. Requirement analysis
### 2.1 Functional requirements
PATIENTS Register, search, view, edit. Deactivate a record while preserving past appointments.
DOCTORS Register, view, update, deactivate. Track specialisation and availability.
APPOINTMENTS Create with patient, doctor, date, time and reason. Status: scheduled, completed, cancelled. No double-booking.
MEDICAL RECORDS A doctor records visit date, diagnosis and notes. Records are retained and readable by authorised staff.
AUTHENTICATION Users log in before reaching protected functionality. The system distinguishes three roles.
ACCESS AND EXPORT Functionality restricted by role. A doctor exports authorised data as a CSV report.
### 2.2 Non-functional requirements
Performance Requests processed within two seconds under the expected demonstration workload.
Availability Available during normal operation; recovers automatically from an application or container failure.
Security — storage Passwords must not be stored in plain text.
Security — access Authentication before protected functionality; role permissions enforced.
Deployability A change on the main branch produces a published container image without manual steps.
Testability Automated unit and end-to-end tests run in CI on every pull request.
Observability Application and system metrics exposed and visible on a dashboard.
Maintainability A documented branching strategy and a versioning scheme for artefacts
## 3. Roles and access control
A receptionist can access all patient data and edit them, including appointments, but should not be able to access their medical records.
Doctors are able to view and edit appointments, and read and edit medical records of their own patients.
Administrators can manage rols, patient data but not their medical records.

| Capability                              | Receptionist | Doctor   | Administrator |   
|-----------------------------------------|--------------|----------|---------------|
| Register, search and edit a patient     | Y            | N        | Y             |   
| Deactivate a patient record             | Y            | N        | Y             |   
| Register, update or deactivate a doctor | N            | N        | Y             |   
| Schedule an appointment                 | Y            | N        | Y             |   
| View appointments                       | ALL          | OWN ONLY | ALL           |   
| Update or cancel an appointment         | Y            | Y        | N             |   
| Record diagnosis and visit notes        | N            | Y        | N             |   
| Read a patient's medical history        | N            | OWN ONLY | N             |   
| Export authorised data to CSV           | N            | Y        | N             |   
| Manage user accounts and roles          | N            | N        | Y             |   

Patients are NOT system users.
## 4. Product backlog
US-01 As a receptionist, I want to send reminders to patients about their appointments, so they do not forget to come.
US-02 As a doctor, I want to share medical records of my patients with other doctors, so I can get help from them.
US-03 As an administrator, I want to be able to update or cancel appointments, so I can help patients when the receptionist is not here.
## 5. Process and ceremonies
