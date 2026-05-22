# Aletheia — “Vibe Coding” Context & OOP Implementation Guide

Use this as the development mindset and engineering guide for the whole project.

---

# Aletheia Engineering Philosophy

## Core Rule

> “Simple systems survive longer.”

The goal is NOT to build the most advanced library system.

The goal is to build:

* understandable code
* stable architecture
* maintainable features
* predictable behavior
* scalable foundations

Every feature should feel:

```text
clean
intentional
modular
easy to extend
```

---

# Development Vibe

## Think Like a Librarian System Designer

Every object represents a real-world concept.

The codebase should read like the domain itself.

---

# GOOD

```text
User borrows Book
Book has availability
Reservation waits in queue
BorrowRecord tracks due date
```

---

# BAD

```text
MegaManager handles everything
Utils class does random magic
Controllers contain business logic
```

---

# Engineering Priorities

Always prioritize in this order:

## 1. Correctness

The system behaves according to business rules.

## 2. Readability

The codebase remains understandable for future developers.

## 3. Stability

Features behave consistently without unexpected side effects.

## 4. Maintainability

New features can be added safely without breaking existing functionality.

## 5. Optimization

Optimization happens only after the system is stable and correct.

---

# OOP Mindset for Aletheia

---

# 1. Model Real-World Objects Properly

The system revolves around domain objects.

---

## Core Domain Objects

```text
User
Book
BorrowRecord
Reservation
AuthSession
Notification
```

Each object owns its own responsibility.

---

# GOOD EXAMPLE

## Book

Responsible for:

* availability
* quantity tracking
* metadata

NOT responsible for:

* authentication
* sending emails
* generating reports

---

# 2. Every Class Should Feel Predictable

Every class has a clearly defined responsibility.

The purpose of the class must be immediately understandable.

---

# GOOD

```text
BookService
```

Responsibilities:

* borrow validation
* availability checks
* inventory updates

---

# BAD

```text
BookService
```

Unrelated responsibilities:

* sends OTPs
* validates JWTs
* exports PDFs

---

# 3. Thin Controllers, Smart Services

---

# Controller Vibe

Controllers are:

```text
traffic managers
```

Controllers:

* receive requests
* validate request structure
* call services
* return responses

Controllers never contain business logic.

---

# NEVER

```java
@PostMapping("/borrow")
public ResponseEntity<?> borrowBook() {

    // 200 lines of business logic
}
```

---

# ALWAYS

```java
@PostMapping("/borrow")
public ResponseEntity<?> borrowBook() {
    return borrowService.borrowBook();
}
```

---

# Service Vibe

Services contain:

* business rules
* validations
* workflows
* domain coordination

---

# 4. Protect Your Domain

Entities are protected from invalid modification.

---

# GOOD

```java
private int availableCopies;
```

Modified through controlled methods only.

---

# BAD

```java
public int availableCopies;
```

This creates invalid states and unpredictable behavior.

---

# 5. Business Rules First, Technology Second

The system focuses on business rules before implementation details.

---

# Borrowing Rules

```text
cannot borrow unavailable books
max 5 borrowed books
due date is 14 days
overdue books must be tracked
```

Implementation follows these rules directly.

---

# 6. Avoid “Magic”

Code behavior remains explicit and self-explanatory.

---

# BAD

```java
processBookState();
```

---

# GOOD

```java
markBookAsReturned();
updateAvailableCopies();
validateBorrowLimit();
```

Explicit naming is mandatory.

---

# 7. Services Should Read Like Stories

Service methods follow readable sequential workflows.

---

# GOOD FLOW

```java
validateUser();

validateBorrowLimit();

findBook();

validateAvailability();

createBorrowRecord();

reduceAvailableCopies();

sendNotification();
```

Readable business logic is preferred over clever abstractions.

---

# 8. Avoid Massive Classes Early

Classes remain small and focused.

Classes with:

* unrelated logic
* excessive methods
* giant file sizes

must be split immediately.

---

# GOOD SPLIT

```text
AuthService
BookService
BorrowService
ReservationService
NotificationService
```

---

# 9. Prefer Explicitness Over Abstraction

The system avoids premature abstraction.

---

# BAD

```text
UniversalManagerFactoryHandlerProcessor
```

---

# GOOD

```text
BorrowService
```

Simple naming is preferred.

---

# 10. Database Design Should Reflect Reality

Relationships model real-world borrowing behavior.

---

# GOOD RELATIONSHIPS

```text
User -> BorrowRecord -> Book
```

---

# BAD RELATIONSHIPS

Duplicated book and user data across unrelated tables.

---

# 11. DTOs Are API Contracts

Entities are internal database models.

DTOs are external API contracts.

Entities are never exposed directly to frontend clients.

---

# GOOD

```text
BookEntity
```

Internal database model.

---

```text
BookResponseDTO
```

Frontend response model.

---

# DTO PURPOSE

DTOs prevent:

* leaking sensitive fields
* frontend dependency on database structure
* accidental API breaking changes

---

# 12. Avoid Premature Complexity

The MVP remains simple and focused.

---

# DO NOT ADD YET

* microservices
* Kafka
* CQRS
* event sourcing
* AI recommendations
* websocket systems

---

# MVP CORE PROBLEM

```text
track books and borrowing
```

The system solves this first before adding advanced features.

---

# 13. Build Features Vertically

Features are completed fully before starting unrelated modules.

---

# DEVELOPMENT ORDER

## Authentication

Completed fully before proceeding.

Then:

## Book Management

Completed fully before proceeding.

Then:

## Borrowing

Completed fully before proceeding.

---

# BAD DEVELOPMENT FLOW

Simultaneous unfinished development of:

* authentication
* analytics
* recommendations
* notifications

---

# 14. Keep Frontend Components Focused

React components remain small reusable UI units.

---

# GOOD COMPONENTS

```text
BookCard
BorrowButton
SearchBar
ReturnModal
```

---

# BAD COMPONENT

```text
MegaDashboardComponent
```

with unrelated responsibilities and excessive complexity.

---

# 15. State Should Be Predictable

Frontend state remains simple and explicit.

---

# GOOD

```text
authState
bookList
borrowedBooks
searchQuery
```

---

# BAD

Deeply nested global state structures with mixed responsibilities.

---

# 16. Backend Should Own Business Truth

The backend is the single source of truth.

Frontend applications never decide:

* borrow limits
* due dates
* permissions

All business rules are enforced by backend services.

---

# 17. Make Errors Human-Friendly

Error responses remain understandable.

---

# BAD

```text
500 Internal Server Error
```

---

# GOOD

```json
{
  "message": "Book is currently unavailable"
}
```

---

# 18. Use Transactions for Critical Operations

Critical workflows use transactional safety.

---

# Borrow Workflow

Borrowing performs:

* create borrow record
* reduce available copies

Both operations succeed together or fail together.

---

# REQUIRED

```java
@Transactional
```

---

# 19. Design APIs Around Actions

REST APIs remain explicit and action-oriented.

---

# GOOD

```text
POST /borrow/{bookId}
POST /return/{borrowId}
```

---

# BAD

```text
/processBookOperation
```

Ambiguous endpoints are prohibited.

---

# 20. Build for Future Extensions Without Overengineering

The architecture supports future expansion while remaining simple.

---

# FUTURE EXTENSIONS

```text
penalties
mobile app
analytics
recommendations
```

These additions must not require rewriting the core architecture.

---

# Recommended Architecture Vibe

# Backend

```text
Controller
↓
Service
↓
Repository
↓
Database
```

---

# Frontend

```text
Pages
↓
Components
↓
API Services
↓
Backend
```

---

# Recommended Coding Standards

---

# Naming

## Classes

```text
PascalCase
```

Example:

```text
BorrowService
```

---

## Methods

```text
camelCase
```

Example:

```text
validateBorrowLimit()
```

---

## Constants

```text
UPPER_CASE
```

Example:

```text
MAX_BORROW_LIMIT
```

---

# Recommended Backend Folder Structure

```text
auth/
book/
borrow/
reservation/
user/
common/
security/
exception/
config/
```

Feature-based organization is mandatory.

---

# Recommended React Structure

```text
pages/
components/
services/
hooks/
types/
layouts/
context/
```

---

# Recommended Development Flow

# Phase 1 — Foundation

Build:

* Spring Boot setup
* PostgreSQL
* JWT authentication
* Email verification
* MFA

---

# Phase 2 — Core Library System

Build:

* books
* search
* availability

---

# Phase 3 — Borrowing

Build:

* borrow logic
* return logic
* due dates
* overdue detection

---

# Phase 4 — Reservations

Build:

* reservation queue
* notification integration

---

# Phase 5 — UI Polish

Improve:

* responsiveness
* UX
* accessibility
* dashboards

---

# Final Engineering Rule

The system rejects solutions that are:

* confusing
* overabstracted
* difficult to explain
* unnecessarily clever

Good OOP systems feel:

```text
boring
predictable
clean
stable
easy to reason about
```

That is what scales.
