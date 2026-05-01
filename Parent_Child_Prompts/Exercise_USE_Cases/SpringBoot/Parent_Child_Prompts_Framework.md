📚 Parent Prompt: General Guidelines for E-Commerce Project
1. Project Structure
Architecture:
Implement a layered architecture:
Presentation Layer
Application Layer
Domain Layer
Infrastructure Layer
Framework:
Use Spring Boot with Spring MVC for RESTful services.
Database:
Utilize PostgreSQL or MySQL with JPA/Hibernate for data management.
Frontend:
Integrate Thymeleaf or connect with a third-party frontend framework like Angular or React.
2. Key Modules
User Management: Features such as registration, login, and profile management.
Product Catalog: CRUD operations on products, categories, and inventory.
Shopping Cart: Manage cart items with add, update, and remove functionality.
Ordering System: Process orders with payment integration, track order history.
Security: Implement authentication using JWT and role-based authorization.
💡 Child Prompt: User Management Module
1. Task Requirements
Feature Set

Register users with email verification.
Enable logins secured with JWT.
Allow profile updates for users.
Implementation Details

Controller: Define endpoints for user registration and login.
Service Layer: Include business logic for registration, login, and profile updates.
Repository Layer: Utilize Spring Data JPA for accessing user data.
Security: Protect endpoints with Spring Security using JWT.
Testing

Perform unit tests for the service layer.
Conduct integration tests for API endpoints.
💡 Child Prompt: Product Catalog Module
1. Task Requirements
Feature Set

Implement CRUD operations for products and categories.
Enable product search and filtering by name, category, and price.
Implementation Details

Controller: Manage product and category API endpoints.
Service Layer: Handle business logic for product management.
Repository Layer: Use JPA repositories for database operations.
Testing

Execute unit tests for product logic.
Perform integration tests on API endpoints.
💡 Child Prompt: Shopping Cart Module
1. Task Requirements
Feature Set

Add, update, and remove items from the cart.
Display cart contents to users.
Implementation Details

Controller: Define endpoints for cart operations.
Service Layer: Manage cart business logic.
Session Management: Use HTTP sessions or a database for maintaining cart state.
Testing

Test cart functionality and associated business rules.
💡 Child Prompt: Ordering System
1. Task Requirements
Feature Set

Facilitate order processing with payment gateway integration.
Provide interfaces for viewing order history and details.
Implementation Details

Controller: Set up endpoints for order placement and history viewing.
Service Layer: Focus on business logic for processing orders.
Payments: Integrate a payment gateway such as Stripe or PayPal.
Testing

Validate ordering workflows through comprehensive tests.
💡 Child Prompt: Security Implementation
1. Task Requirements
Feature Set

Authenticate REST APIs using JWT.
Implement role-based access controls on various endpoints.
Implementation Details

Security Configurations: Configure within WebSecurityConfigurerAdapter.
JWT Utilities: Develop utility classes for token generation and validation.
Testing

Test authentication mechanisms and role-based access control functionalities.