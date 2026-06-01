# 📊 Team Changelog

### Project and Repository creation - 05/12/26

### Project Requirements, Context and Rules - 05/22/26
- Personal md and teamchangelog creation <br>
- All three members contributed to the project requirements, context-rules, and additional rules

### Backend Foundation Setup [2026-05-25] 

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

### Authentication Module MVP [2026-05-25] 

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


### Book Module Foundation [2026-05-27]

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

### Borrowing Module Foundation [2026-05-27]

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

### Reservation Module Foundation [2026-05-27]

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

### JWT Security Integration Foundation [2026-05-28]

CHANGES:
- Added JWT authentication filter
- Added secured API flow
- Added authenticated request handling
- Added Spring Security integration
- Added UserDetails implementation

SECURITY:
- APIs now require JWT authentication
- Stateless session management enabled
- Authorization header validation implemented

TECHNICAL:
- Added SecurityContext authentication flow
- Added authenticated user extraction foundation

TEST STATUS:
- JWT authentication manually tested

### Role-Based Authorization Foundation [2026-05-28]

CHANGES:
- Added role-based endpoint security
- Added librarian/admin-only APIs
- Added student-safe API access
- Added authorization rules for borrowing/reservations

SECURITY:
- Restricted inventory management endpoints
- Protected admin/librarian functionality
- Added authority-based endpoint access

TECHNICAL:
- Added role-aware authentication response
- Connected Spring Security authorization to Role enum

TEST STATUS:
- Manual authorization testing completed

### Book Search + Pagination Foundation [2026-05-28]

CHANGES:
- Added searchable book APIs
- Added pagination support
- Added sorting support
- Added title/author/ISBN filtering
- Added pageable backend responses

TECHNICAL:
- Added Spring Pageable integration
- Added paginated response DTOs
- Added scalable repository query methods

TEST STATUS:
- Manual search testing completed


### Overdue Detection + Return Management Foundation [2026-05-28]

CHANGES:
- Added borrow lifecycle statuses
- Added return book workflow
- Added overdue detection
- Added borrow history APIs
- Added returned date tracking
- Added inventory restoration logic

BUSINESS RULES:
- Borrow status lifecycle implemented
- Overdue validation added
- Returned books tracked properly

TECHNICAL:
- Added BorrowStatus enum
- Added overdue status updater
- Added borrow lifecycle architecture

TEST STATUS:
- Manual return/overdue testing completed

### Reservation Queue + Auto Availability Foundation [2026-05-28]

CHANGES:
- Added FIFO reservation queue
- Added reservation lifecycle statuses
- Added reservation cancellation
- Added automatic reservation activation
- Added queue position tracking
- Added reservation timing tracking

BUSINESS RULES:
- FIFO reservation ordering implemented
- Auto availability handoff implemented
- Duplicate reservation prevention added

TECHNICAL:
- Added ReservationStatus enum
- Added queue reordering logic
- Added reservation activation workflow

TEST STATUS:
- Manual queue workflow testing completed

### Admin Library Management Foundation [2026-05-28]

CHANGES:
- Added admin-only inventory management
- Added book archival workflow
- Added inventory recalculation logic
- Added admin management APIs
- Added role-protected admin endpoints

SECURITY:
- Admin APIs restricted to ADMIN/LIBRARIAN roles
- Archived books hidden from public operations

TECHNICAL:
- Added AdminService
- Added AdminController
- Added soft delete foundation
- Added inventory update workflows

TEST STATUS:
- Manual RBAC and inventory testing completed

That's all for now sa susunod na po yung iba pang changelog T^T
