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
### US-01 As a receptionist, I want to send reminders to patients about their appointments, so they do not forget to come.
### US-02 As a doctor, I want to share medical records of my patients with other doctors, so I can get help from them.
### US-03 As an administrator, I want to be able to update or cancel appointments, so I can help patients when the receptionist is not here.
### US-04 As a receptionist, I want to register a patient, so we can see their information before an appointment
### US-05 As a receptionist, I want to search and view patients, so I can quickly find their data
### US-06 As an administrator, I want to manage doctors, so they can be enabled to use the system
### US-07 As a receptionist, I want double booking to be prevented, so I dont make any mistakes
### US-08 As a doctor, I want to export data as pdf, so I can use it for lab testing or reporting.

## 5. Process and ceremonies
The sprint length will be 2 weeks, I chose this because the threat from doctors trying to hack into other roles will be low as is their cyber security knowledge, so security is not the main issue. Also the data that we manage is purely text, can be pdf, should be easy to transfer from application to the server.

Sprint plan:
Sprint 1: Doctor record sharing, Doctors can view records sent from other doctors, but only if allowed by them, and no doctor should be able to edit other records
Sprint 2: Appointment reminder sending, Receptionists can send a reminder, but they can not see the contact info of the patient, only the patient should be able to call back if interested.

Ceremonies: Sprint planning will happen each start of the sprint, where duties are spread over the team, and sprint review will happen each end of the sprint, so we can see if something needs to be reviewed or redone.

Backlog refinement triggers: A story is too large for one sprint, A story is unclear, Priorities have changed


## 6. Epics

### EP-01 Managing patients
Register, search, view, edit, and deactivate patients

### Ep-02 Managing doctors
Register, search, view, edit, and deactivate doctors

### EP-03 Managing appointments
Register, search, view, edit, and deactivate appointments

### EP-04 Medical records
Register, search, view, edit medical records

### EP-05 Authentication and access control
Auchenticate users and stabilize who can do what

### EP-06 Reports
Allow doctors to download patient data as pdf

### EP-07 Reminders
Allow receptionists to send reminders to patients and doctors about their appointments

### EP-08 DevOps
Regulate automated testing, versioning, containeraisation before deploying

## 7. Story points and estimation

| Meaning                              | Story points | 
|-----------------------------------------|--------------|
| Small change | 1 |
| Small change with minimal complexity | 2 |
| Small feature, requires testing | 2 |
| Medium feature, requires multiple components | 4 |
| Large feature, requires integration and testing | 5 |
| Very large feature that should be split into multiple stories | 6 |

### Anchor story
The anchor story is US - 04 : Managing a patient, which is estimated at 3 points
Here, we must create the data model for the patient, validate input fields and test everything.

### Procut backlog estimates

| ID    | User story summary                                           | Story points |
| ----- | ------------------------------------------------------------ | -----------: |
| US-01 | Send  reminders                                   |            5 |
| US-02 | Share medical records securely between doctors               |            4 |
| US-03 | Allow administrators to update or cancel appointments        |            3 |
| US-04 | Register a patient                                           |            3 |
| US-05 | Search, view and edit patient records                        |            3 |
| US-06 | Manage doctor records and availability                       |            3 |
| US-07 | Schedule appointments                                        |            3|
| US-08 | Prevent appointment double-booking                           |            4 |
| US-09 | Record diagnoses and visit notes                             |            3 |
| US-10 | Export authorised data to CSV                                |            2 |
| US-11 | Authenticate users and enforce role permissions              |            5 |
| US-12 | Deactivate patients while preserving historical appointments |           2 |
| US-13 | Run automated unit and end-to-end tests in CI                |            5 |
| US-14 | Build and publish container images through CI/CD             |            3 |
| US-15 | Expose application metrics and configure a dashboard         |            4 |
| US-16 | Configure container restart and application health checks    |            4 |

## 9. Technology Stack

### Backend
Python - FastAPI provides automatic validation

### Database
PostgreSQL - good integrity possible between patients and appointments

### Containterizing 
Docker - possible to enable automatic image publishing upon a rapository update

### CI/CD
Github actions - runs testing on every request automatically

### Metrics
Grafana with Prometheus - expose metrics on dashboards
