# Design Patterns in Aletheia

This document describes the main design patterns used in Aletheia based on the current backend and frontend implementation.

## Backend Patterns

### 1. Layered Architecture / Service Layer Pattern
- **What it means:** The application is split into clearly separated layers: controllers, services, and repositories.
- **What it does:** Controllers handle HTTP requests and responses, services contain business logic, and repositories handle database access.
- **Why used:** This separation makes the application easier to maintain, test, and evolve.
- **Where:** `com.jhy.aletheia.*.controller`, `com.jhy.aletheia.*.service`, and `com.jhy.aletheia.*.repository` packages.

### 2. Repository Pattern
- **What it means:** Data access is abstracted behind repository interfaces.
- **What it does:** Repositories encapsulate all database operations and provide a persistent storage API.
- **Why used:** It decouples business logic from persistence details and enables Spring Data JPA to generate queries automatically.
- **Where:** `UserRepository`, `BookRepository`, `BorrowRepository`, `ReservationRepository`, `AuditLogRepository`, etc.

### 3. DTO Pattern
- **What it means:** Data Transfer Objects are used to separate API payloads from internal entities.
- **What it does:** DTOs define request and response shapes for the HTTP API without exposing the database model directly.
- **Why used:** This improves security, avoids leaking internal fields, and makes API contracts explicit.
- **Where:** DTO packages like `com.jhy.aletheia.auth.dto`, `com.jhy.aletheia.book.dto`, `com.jhy.aletheia.borrow.dto`, `com.jhy.aletheia.reservation.dto`, and `com.jhy.aletheia.admin.dto`.

### 4. Builder Pattern
- **What it means:** A builder API is used to construct complex objects in a readable way.
- **What it does:** It allows response objects to be created with named properties instead of large constructors.
- **Why used:** It reduces constructor overload, improves readability, and makes response assembly easier.
- **Where:** Lombok `@Builder` is used in DTOs such as `BookResponse`, `PaginatedBookResponse`, `BorrowResponse`, `ReservationResponse`, `AdminDashboardResponse`, and others.

### 5. Dependency Injection / Inversion of Control
- **What it means:** Dependencies are provided to classes by the framework rather than created manually.
- **What it does:** Spring injects service, repository, and component instances via annotations like `@Service`, `@Component`, and `@RequiredArgsConstructor`.
- **Why used:** It improves testability, reduces coupling, and makes it easier to replace or mock implementations.
- **Where:** Backend classes like `AuthService`, `BookService`, `JwtAuthenticationFilter`, and `AuthenticatedUserService`.

### 6. Security Filter / Pipeline Pattern
- **What it means:** Incoming HTTP requests are processed through a filter chain before reaching controllers.
- **What it does:** `JwtAuthenticationFilter` validates JWT tokens, extracts user details, and establishes authentication context.
- **Why used:** It centralizes authentication logic and ensures security checks happen consistently for protected endpoints.
- **Where:** `com.jhy.aletheia.security.jwt.JwtAuthenticationFilter`.

### 7. Global Exception Handling Pattern
- **What it means:** Cross-cutting error handling is centralized in one place.
- **What it does:** `GlobalExceptionHandler` catches validation errors, custom exceptions, unauthorized access, and unexpected exceptions.
- **Why used:** It keeps controllers clean and ensures consistent API error responses.
- **Where:** `com.jhy.aletheia.exception.GlobalExceptionHandler`.

## Frontend Patterns

### 1. Component-Based UI Pattern
- **What it means:** User interface is built from reusable React components.
- **What it does:** Small UI pieces like `Sidebar`, `AdminSidebar`, and `DashboardCard` are reused across pages.
- **Why used:** It improves maintainability, reusability, and keeps page code simpler.
- **Where:** `Aletheia/Frontend/src/components`, `Aletheia/Frontend/src/pages`.

### 2. Route Guard Pattern
- **What it means:** Navigation is protected by a wrapper that checks authentication before rendering a page.
- **What it does:** The `ProtectedRoute` component checks for a valid token and redirects unauthenticated users to `/login`.
- **Why used:** It prevents unauthorized access to dashboard and profile routes.
- **Where:** `Aletheia/Frontend/src/routes/ProtectedRoute.tsx` and `Aletheia/Frontend/src/App.tsx`.

### 3. Service Layer / API Abstraction Pattern
- **What it means:** Frontend pages call service functions instead of using raw fetch logic inline.
- **What it does:** The imported service functions group related API calls for authentication, books, borrowing, reservations, and profile data.
- **Why used:** It separates network logic from UI logic and makes the code easier to maintain.
- **Where:** `Aletheia/Frontend/src/pages/*` imports functions from `../services/*` APIs.

### 4. Typed Contract Pattern
- **What it means:** TypeScript interfaces define the shape of data flowing through the UI.
- **What it does:** Interfaces such as `Book`, `User`, `Reservation`, `BorrowedBook`, and `Profile` document expected API data structures.
- **Why used:** It improves developer confidence, catches type errors early, and keeps frontend data consistent.
- **Where:** `Aletheia/Frontend/src/types/*`.

## Why these patterns were chosen
- They support a clean separation of concerns between HTTP handling, business rules, and persistence.
- They make the project easier to extend and maintain as new features are added.
- They enforce consistent API contracts and reduce accidental coupling between layers.
- They improve developer productivity by making object construction, dependency wiring, and error handling more declarative.

## Summary
Aletheia uses a modern architecture built around Spring Boot and React. The backend emphasizes layered separation, DTO-based APIs, and Spring-managed components. The frontend uses reusable components, route protection, service abstraction, and typed data contracts.
