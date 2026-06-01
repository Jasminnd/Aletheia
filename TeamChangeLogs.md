# 📊 Team Changelog

### Project and Repository creation - 05/12/26

### Project Requirements, Context and Rules - 05/22/26
- Personal md and teamchangelog creation <br>
- All three members contributed to the project requirements, context-rules, and additional rules

### [2026-05-25] 

FEATURE 1:
- Backend Foundation Setup

CHANGES:
- Initialized Spring Boot backend
- Configured PostgreSQL integration
- Added layered package structure
- Added global exception handling
- Added validation setup
- Added security foundation
- Added health endpoint
- Added BaseEntity auditing support

TESTS:
- Added application context tests
- Added health endpoint tests


FEATURE 2:
- Authentication Module MVP

CHANGES:
- Added UserEntity
- Added JWT authentication
- Added login/register APIs
- Added password hashing
- Added NU email validation
- Added role foundation

TESTS:
- Registration validation tests
- Login authentication tests


### [2026-05-27]

FEATURE:
- Book Module Foundation

CHANGES:
- Added BookEntity
- Added book persistence
- Added book creation API
- Added book retrieval APIs
- Added inventory tracking
- Added availability logic
- Added ISBN uniqueness validation

BUSINESS RULES:
- ISBN must be unique
- availableCopies initialized from totalCopies
- Books cannot start with invalid inventory

TEST STATUS:
- Manual API testing completed


FEATURE:
- Borrowing Module Foundation

CHANGES:
- Added borrowing workflow
- Added return workflow
- Added due date tracking
- Added borrow limit validation
- Added inventory synchronization
- Added overdue-ready logic

BUSINESS RULES:
- Max borrow limit = 5
- Borrow duration = 14 days
- Cannot borrow unavailable books
- Returning restores inventory

TECHNICAL:
- Added transactional borrow operations
- Added relational mapping between users/books

TEST STATUS:
- Manual borrowing tests completed


FEATURE:
- Reservation Module Foundation

CHANGES:
- Added reservation workflow
- Added FIFO reservation queue logic
- Added duplicate reservation prevention
- Added reservation retrieval API
- Added queue position tracking

BUSINESS RULES:
- Cannot reserve available books
- Cannot duplicate reservations
- Reservations ordered by reservation timestamp

TECHNICAL:
- Added relational mapping between users/books/reservations
- Added reservation queue foundation

TEST STATUS:
- Manual reservation testing completed
