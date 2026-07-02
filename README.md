# Smart-Library-Request-Workflow-in-ServiceNow


## Project Overview

The Smart Library Request Workflow is a ServiceNow-based application designed to automate library book request and management processes. It introduces role-based access control, workflow automation, and real-time data validation.

This system allows students to request books, librarians to approve or reject requests, automatic updating of book availability, and reporting for most borrowed books.

---

## Problem Statement

Traditional library systems lack automation and proper access control, leading to duplicate or invalid book requests, no real-time tracking of book availability, manual workload for librarians, and poor reporting.

This project addresses these issues using ServiceNow workflows and structured data management.

---

## Technologies and Skills Used

* ServiceNow Platform
* Flow Designer
* Access Control Lists (ACLs)
* UI Policies
* Data Modeling (Tables and Fields)
* Reference Qualifiers
* Reporting

---

## Project Milestones and Implementation

### Milestone 1: Role Creation

Roles created:

* student
* librarian

Students can request books. Librarians can manage books and requests.

---

### Milestone 2: Table Creation

Tables created:

1. Book Table

   * Name: u_book

2. Borrow Request Table

   * Name: u_borrow_request

Relationship:

* Borrow Request contains a reference field to Book.

---

### Milestone 3: Book Table Fields

Fields:

* Title (String)
* Author (String)
* ISBN (String)
* Status (Choice)

Status values:

* Available (default)
* Issued
* Lost

---

### Milestone 4: Borrow Request Fields

Fields:

* Requested By (Reference to User)
* Book (Reference to Book)
* Request Date (Date/Time)
* Status (Choice)

Status values:

* Requested (default)
* Approved
* Rejected
* Returned

---

### Milestone 5: Related List

Borrow Request is added as a related list in the Book form to track all requests associated with a book.

---

### Milestone 6: Reference Qualifier

Condition used:

```
status=Available
```

This ensures only available books can be selected in requests.

---

### Milestone 7: Flow Designer Automation

Flow Name: Issue Book Flow

Trigger:

* When Borrow Request status changes to Approved

Action:

* Update Book status to Issued

Optional:

* Send notification email to requester

---

### Milestone 8: UI Policy

Condition:

* Status is Approved

Actions:

* Make Book field read-only
* Make Requested By field read-only
* Make Request Date field read-only

---

### Milestone 9: Access Control (ACLs)

Book Table:

* Read: student, librarian
* Create: librarian
* Write: librarian
* Delete: librarian

Borrow Request Table:

* Create: student
* Read: student (own records), librarian
* Write: librarian
* Delete: librarian

Condition for student read access:

```
requested_by = current user
```

---

### Milestone 10: Report – Most Borrowed Books

Configuration:

* Table: Borrow Request
* Group by: Book
* Aggregation: Count
* Sort: Descending
* Limit: Top 5

---

## Key Features

* Role-based access control
* Automated book issuing workflow
* Data validation for requests
* Improved user interface
* Reporting and insights

---

## Conclusion

This project demonstrates how ServiceNow can be used to develop a structured and automated library management system. It improves efficiency, ensures proper access control, and provides meaningful insights through reporting.

---

## Future Enhancements

* Due date tracking
* Fine calculation
* Email reminders
* Mobile interface
* External system integration

---

## Author

Pooja R
B.Tech Artificial Intelligence and Data Science
