# The Sql Surgeons Project 2

Cas van Ruijven [Cas van Ruijven](https://github.com/casvanruijven/the_sql_surgeons_project_2)\
Nathan Riggle [Nathan Riggle](https://github.com/nathanriggle/the_sql_surgeons_project_2)\
Max Weaver [Max Weaver](https://github.com/MaxWeaver7/the_sql_surgeons_project_2)\
Sam Holtzclaw [Sam Holtzclaw](https://github.com/holtzclawsam/the_sql_surgeons_project_2)\
Jack Beal [Jack Beal](https://github.com/Jhbeal03/the_sql_surgeons_project_2)

## Description
This gym database efficiently manages fitness center operations, including memberships, payments, classes, equipment, and feedback. It tracks member and employee details, supports mentorships, and organizes class schedules with prerequisites and attendance records. Feedback from members about classes and employees can be logged and responded to. Equipment usage and maintenance are monitored, ensuring availability and safety. The database links memberships, payments, classes, and feedback, providing a streamlined system for managing daily activities. While comprehensive for operational needs, it does not handle advanced business functions like payroll or marketing, focusing instead on improving efficiency and the overall member experience.

![Gym Database Model](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Gym_system_2.png)

- Employee: Stores employee details, including their supervisor and certification level.
- Member: Contains member information like contact details and the date they joined.
- Member has mentor: Indicates whether a member is assigned zero, one or more mentors.
- Membership: Tracks the type of membership, price, and access level.
- Payments: Logs payment records, linking members to their membership plans.
- Class and Class_Schedule: Tracks fitness classes, including schedule details and employee instructors.
- Class has prerequisite: Specifies if completing one class is required before enrolling in another.
- Feedback: Records feedback given by members about classes or employees.
- Feedback has response: Indicates whether feedback provided by a member has received responses.
- Equipment and Equipment_Usage: Monitors gym equipment and its usage in classes, with associated maintenance requests.
- Attendance: Captures class attendance information for members.
- Maintenance_Request: Logs equipment maintenance needs.

## Data Dictionary

#### Member
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| member_id        | INT            | Unique identifier for each member (Primary Key) |
| first_name       | VARCHAR(45)    | Member’s first name                          |
| last_name        | VARCHAR(45)    | Member’s last name                           |
| date_of_birth    | DATE           | Member’s date of birth                       |
| email            | VARCHAR(45)    | Contact email for the member                 |
| phone_number     | VARCHAR(45)    | Member’s contact number                      |
| join_date        | DATE           | Date when the member joined                  |

#### Member_has_Mentor
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| member_id        | INT            | Unique identifier for each member (Primary Key) |
| mentor_member_id | INT            | Unique identifier for each mentor (Primary Key) |

#### Membership
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| membership_id    | INT            | Unique identifier for each membership (Primary Key) |
| membership_name   | VARCHAR(45)   | Name of the membership plan                   |
| price            | DECIMAL(6,2)   | Cost of the membership                        |
| duration         | INT            | Duration of the membership in months         |
| access_level     | INT            | Level of access granted by the membership     |
| parent_membership_id     | INT    | References the membership_id of a parent membership plan |

#### Employee
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| employee_id      | INT            | Unique identifier for each employee (Primary Key) |
| first_name       | VARCHAR(45)    | Employee’s first name                        |
| last_name        | VARCHAR(45)    | Employee’s last name                         |
| specialization    | VARCHAR(45)    | Area of expertise for the employee            |
| certification_level | INT          | Level of certification held by the employee   |
| email            | VARCHAR(45)    | Contact email for the employee               |
| phone_number     | VARCHAR(45)    | Employee’s contact number                    |
| supervised_by    | INT            | Employee ID of the supervisor                 |

#### Class
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| class_id         | INT            | Unique identifier for each class (Primary Key) |
| class_name       | VARCHAR(45)    | Name of the class                            |
| description      | VARCHAR(255)   | Description of the class                     |
| intensity_level   | INT            | Intensity level of the class                 |
| max_capacity     | INT            | Maximum number of participants allowed       |
| duration         | INT            | Duration of the class in minutes             |

#### Class_has_prerequisite
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| class_id         | INT            | Unique identifier for each class (Primary Key) |
| prerequisite_class_id  | INT  | References the class_id of a prerequisite class that must be completed  |

#### Class_Schedule
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| class_schedule_id | INT            | Unique identifier for each class schedule (Primary Key) |
| employee_id      | INT            | ID of the employee conducting the class      |
| class_id         | INT            | ID of the class scheduled                    |
| start_date_time  | DATETIME       | Date and time when the class starts         |
| end_date_time    | DATETIME       | Date and time when the class ends           |
| location         | VARCHAR(45)    | Location where the class is held             |

#### Attendance
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| attendance_id    | INT            | Unique identifier for each attendance record (Primary Key) |
| class_schedule_id | INT            | ID of the scheduled class                    |
| member_id        | INT            | ID of the member attending                   |
| ShowedUp         | TINYINT        | Indicator of whether the member showed up (1 for Yes, 0 for No) |

#### Payments
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| payment_id       | INT            | Unique identifier for each payment (Primary Key) |
| member_id        | INT            | ID of the member making the payment         |
| membership_id    | INT            | ID of the membership being paid for         |
| payment_date     | DATE           | Date when the payment was made              |
| payment_amount   | DECIMAL(5,2)   | Amount paid                                  |
| payment_method    | VARCHAR(45)    | Method of payment (e.g., Credit Card, Cash) |

#### Feedback
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| feedback_id      | INT            | Unique identifier for each feedback entry (Primary Key) |
| member_id        | INT            | ID of the member providing feedback         |
| employee_id      | INT            | ID of the employee receiving feedback       |
| class_id         | INT            | ID of the class related to the feedback     |
| feedback_text    | VARCHAR(255)   | Text of the feedback provided                |
| rating           | INT            | Rating given by the member (e.g., 1 to 5)   |
| feedback_date    | DATE           | Date when the feedback was submitted         |

#### Feedback_Response
| Column Name      | Data Type  | Description                                  |
|------------------|------------|----------------------------------------------|
| feedback_id      | INT        | Unique identifier for each feedback entry (Primary Key) |
| feedback_response_id | INT    | Unique identifier for each response to feedback, linking it to a specific feedback |

#### Equipment
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| equipment_id     | INT            | Unique identifier for each piece of equipment (Primary Key) |
| equipment_name   | VARCHAR(45)    | Name of the equipment                        |
| purchase_date    | DATE           | Date when the equipment was purchased       |
| maintenance_due_date | DATE       | Date when the next maintenance is due      |
| status           | VARCHAR(45)    | Current status of the equipment (e.g., Good, Needs Repair) |
| location         | VARCHAR(45)    | Location of the equipment within the facility |

#### Equipment_Usage
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| equipment_id     | INT            | ID of the equipment used                    |
| class_schedule_id | INT            | ID of the class schedule using the equipment |
| (Composite Key)  |                | Combination of equipment_id and class_schedule_id serves as the primary key |

#### Maintenance_Request
| Column Name      | Data Type      | Description                                  |
|------------------|----------------|----------------------------------------------|
| maintenance_request_id | INT      | Unique identifier for each maintenance request (Primary Key) |
| equipment_id     | INT            | ID of the equipment requiring maintenance    |
| request_date      | DATE           | Date when the maintenance request was made  |
| request_status    | VARCHAR(45)    | Current status of the maintenance request    |
| completed_date    | DATE           | Date when the maintenance was completed      |

## Queries

| Database information                   | Query 1 | Query 2 | Query 3 | Query 4 | Query 5 |
|----------------------------------------|---------|---------|---------|---------|---------|
| **Multiple table join**                |    x    |         |         |    x    |    x    |
| **Create view**                        |    x    |    x    |         |         |         |
| **Group by, Aggregation**              |         |    x    |         |         |    x    |
| **Join**                               |    x    |    x    |    x    |    x    |    x    |

#### 1
Enables quick identification of active memberships and their pricing, which is crucial for pricing strategy, promotions, or member retention analysis.

![Picture1](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture1.png)
![Picture2](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture2.png)

#### 2
Management can track how well each class is performing based on feedback and average ratings, which is crucial for quality assurance.

![Picture3](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture3.png)
![Picture4](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture4.png)
![Picture5](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture5.png)

#### 3
It directly connects each employee with their supervisor, allowing management to see the reporting structure within the organization. This is crucial for understanding team dynamics and accountability.

![Picture6](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture6.png)
![Picture7](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture7.png)

#### 4
This query is beneficial for management because it provides a clear view of mentor-mentee relationships within the organization.

![Picture8](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture8.png)
![Picture9](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture9.png)

#### 5
This query would help management to see areas that are lacking engagement as well as what classes are in high demand. Management can brainstorm ways to improve efficiency and optimize resources.

![Picture10](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture10.png)
![Picture11](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Picture11.png)

## Tableau visualizations

![Tableau](https://github.com/casvanruijven/the_sql_surgeons_project_2/blob/main/Tableau.png)

### Total Revenue by Membership Type:

- Purpose: This chart displays the total revenue generated for each membership type.
- Relevance: Helps identify which membership tier is the most lucrative, aiding in strategic decisions such as pricing adjustments or marketing focus.

### Total Payments by Membership Type:

- Purpose: Shows the count of payments made by members across different membership types.
- Relevance: Highlights engagement levels per membership category, offering insight into user behavior and potential opportunities for increased interaction or retention.

### Average Feedback Rating by Membership Type:

- Purpose: Illustrates the average feedback or satisfaction rating for each membership type.
- Relevance: Indicates member satisfaction and helps prioritize improvements in customer experience for specific membership categories.
