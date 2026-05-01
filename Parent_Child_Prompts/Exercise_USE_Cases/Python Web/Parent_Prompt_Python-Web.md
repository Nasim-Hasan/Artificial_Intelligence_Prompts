##### Python Development Framework: Development Guidelines Parent Prompt

Version: 0.10.0

Last Updated: 04-Sep-2025

###### 1\. Key Responsibilities

1\.1. Application Development

* Develop robust RESTful APIs and backend services using modern asynchronous frameworks
* Implement data processing pipelines, ETL jobs, and automation scripts
* Build scalable microservices and integrate with message brokers and caches
* Create data models and interact with various database systems using ORMs and drivers
* Write scripts for DevOps, infrastructure management, and testing

1\.2. Code Quality & Modularity

* Adhere strictly to PEP 8 style guidelines and Pythonic principles
* Design with modularity in mind, using a clear separation of concerns (e.g., MVC, Service-Repository patterns)
* Write reusable functions and classes to avoid code duplication
* Use type hints (PEP 484) to improve code clarity, enable static analysis, and facilitate better IDE support
* Ensure compatibility with the defined project structure and dependency management

1\.3. Performance & Efficiency

* Write efficient algorithms optimized for time and space complexity
* Leverage asynchronous programming (asyncio) for I/O-bound operations to maximize concurrency
* Utilize multiprocessing for CPU-bound tasks to leverage multiple cores
* Implement proper connection pooling for databases and external services
* Profile code to identify and rectify bottlenecks

1\.4. Documentation

* Write comprehensive docstrings following PEP 257 (Google or NumPy style)
* Use inline comments to explain complex logic or "why" something is done, not "what" is done
* Maintain clear and updated README.md files for projects and modules
* Use README.rst and setup.py for packaging and publishing libraries
* Document API endpoints automatically using OpenAPI (FastAPI) or similar

###### 2\. Project Context

**2\.1. Primary Application Types**

* The Python ecosystem is versatile and supports a wide range of applications:
* Web APIs & Backends - High-performance REST and GraphQL APIs
* Data Science & Machine Learning - Data analysis, model training, and inference pipelines
* Automation & Scripting - DevOps scripts, system administration, and task automation
* Microservices - Small, focused services within a larger architecture
* Data Processing - ETL (Extract, Transform, Load) jobs and data streaming

**2\.2. Technical Stack**

The project leverages a modern Python ecosystem:

Language: Python 3.10+ (Utilizing modern features like structural pattern matching, union operators, etc.)

Web Frameworks:

* FastAPI (Preferred for new projects: async, automatic OpenAPI docs, high performance)
* Django (Batteries-included for monolithic applications, ORM, admin panel)
* Flask (Lightweight, for simpler services or micro-frameworks)
* Async Framework: asyncio with async/await

Data & ORM:

* SQLAlchemy (Powerful ORM and SQL toolkit)
* Alembic (Database migrations)
* Django ORM (If using Django)
* Pandas (Data manipulation and analysis)
* Redis Py (Redis client)

API Clients: httpx (async), requests (sync)

Message Brokers: aiokafka (async Kafka), pika (RabbitMQ)

Testing:

* pytest (Test framework)
* unittest (Standard library module)
* factory_boy (Test fixtures)
* pytest-asyncio (Async tests)

Linting & Formatting:

* flake8 or ruff (Linting)
* black (Code formatting)
* isort (Import sorting)
* mypy (Static type checking)

Dependency Management: poetry (Preferred) or pip with requirements.txt/pipenv

Containerization: Docker, Docker Compose

Config Management: pydantic (For settings management), .env files, python-dotenv

**2\.3. System Architecture**

A typical Python service follows a layered architecture:

2\.3.1. API Layer (Controller)

FastAPI Routers / Django Views / Flask Blueprints

Handles HTTP requests/responses, validation, authentication

2\.3.2. Service Layer

Contains core business logic

Orchestrates interactions between repositories, external APIs, and other services

Stateless and framework-agnostic where possible

2\.3.3. Repository Layer (Data Access)

Abstracts data access using SQLAlchemy sessions or Django QuerySets

Isolates persistence logic from business logic

2\.3.4. Model Layer

SQLAlchemy ORM models, Pydantic models, or Django models

Defines data structures and validation rules

2\.3.5. Integration Layer

Clients for external services (HTTP, gRPC)

Producers/consumers for message brokers (Kafka, RabbitMQ)

Cache clients (Redis)

3\. Project Structure & Configuration

3\.1. Standard Project Structure

my_project/

├── .github/                         # GitHub Actions workflows

│   └── workflows/

├── app/                             # Main application package

│   ├── \__init_\_.py

│   ├── main.py                      # FastAPI app factory/entry point

│   ├── api/                         # API Layer (Controller)

│   │   ├── \__init_\_.py

│   │   ├── v1/                      # API version namespace

│   │   │   ├── \__init_\_.py

│   │   │   ├── endpoints/

│   │   │   │   ├── \__init_\_.py

│   │   │   │   ├── items.py         # Router for /items/\*

│   │   │   │   └── users.py         # Router for /users/\*

│   │   │   └── router.py            # Includes all v1 endpoints

│   │   └── dependencies.py          # FastAPI dependencies (auth, DB session)

│   ├── core/                        # Core configuration and setup

│   │   ├── \__init_\_.py

│   │   ├── config.py                # Pydantic settings model

│   │   └── security.py              # Auth functions (JWT, etc.)

│   ├── models/                      # Model Layer (Pydantic & ORM)

│   │   ├── \__init_\_.py

│   │   ├── pydantic_models.py       # Request/Response schemas

│   │   └── orm_models.py            # SQLAlchemy/Django ORM models

│   ├── schemas/                     # (Alternative to models/) Pydantic schemas

│   ├── services/                    # Service Layer

│   │   ├── \__init_\_.py

│   │   ├── item_service.py

│   │   └── user_service.py

│   ├── repositories/                # Repository Layer (Data Access)

│   │   ├── \__init_\_.py

│   │   ├── item_repository.py

│   │   └── user_repository.py

│   ├── database/                    # Database connection and utils

│   │   ├── \__init_\_.py

│   │   ├── session.py               # SQLAlchemy session factory

│   │   └── base.py                  # SQLAlchemy Base class

│   └── utils/                       # Utility functions/classes

│       ├── \__init_\_.py

│       └── loggers.py

├── tests/                           # Test package

│   ├── \__init_\_.py

│   ├── conftest.py                  # Pytest fixtures

│   ├── api/

│   │   └── v1/

│   ├── services/

│   └── repositories/

├── migrations/                      # Alembic migrations (generated)

├── scripts/                         # Helper scripts (e.g., seed DB)

├── Dockerfile

├── docker-compose.yml

├── pyproject.toml                   # Poetry/packaging config (preferred)

├── requirements.txt                 # (if not using Poetry)

├── .env.example                     # Example environment variables

├── .pre-commit-config.yaml          # Pre-commit hooks

└── README.md

3\.1.1. Key Configuration Files & Concepts

* pyproject.toml (Poetry): Defines project dependencies, build system, and tool configurations (black, isort, mypy)
* requirements.txt: Lists project dependencies for pip
* .env: Contains environment-specific variables (API keys, database URLs)
* Dockerfile: Instructions to build the application container
* docker-compose.yml: Defines multi-container applications (app, DB, redis)
* Pydantic BaseSettings: For type-safe, validated application settings loaded from environment variables
* Routers (FastAPI): Organize API endpoints into modular units
* Dependency Injection (FastAPI): Used for providing database sessions, service classes, and auth dependencies

**3\.1.2. Configuration Examples**

3\.1.2.1. Main Application Entry Point (app/main.py)

from fastapi import FastAPI

from app.api.v1.router import api_router

from app.core.config import settings

def create_application() -> FastAPI:

    application = FastAPI(

        title=settings.PROJECT_NAME,

        debug=settings.DEBUG,

        version=settings.VERSION,

    )

 

    # Include API router

    application.include_router(api_router, prefix=settings.API_V1_STR)

 

    # Add event handlers

    application.add_event_handler("startup", create_db_tables)

 

    return application

app = create_application()

\# For running with uvicorn directly

if \__name_\_ == "\__main_\_":

    import uvicorn

    uvicorn.run(app, host="0.0.0.0", port=8000)

**3\.1.2.2. Pydantic Settings Configuration (app/core/config.py)**

from pydantic import BaseSettings, PostgresDsn, validator

from typing import Optional

class Settings(BaseSettings):

    PROJECT_NAME: str = "My Awesome API"

    VERSION: str = "1.0.0"

    API_V1_STR: str = "/api/v1"

    DEBUG: bool = False

    # Database

    DATABASE_URL: PostgresDsn

    SYNC_DATABASE_URL: Optional\[PostgresDsn] = None

    @validator("SYNC_DATABASE_URL", pre=True)

    def set_sync_database_url(cls, v, values):

        if v is not None:

            return v

        # Create a synchronous connection URL from the async one (for Alembic)

        if "DATABASE_URL" in values:

            return values\["DATABASE_URL"].replace("+asyncpg", "")

        return v

    # Secrets

    SECRET_KEY: str

    ALGORITHM: str = "HS256"

    ACCESS_TOKEN_EXPIRE_MINUTES: int = 30

    class Config:

        case_sensitive = True

        env_file = ".env"

settings = Settings()

**3\.1.2.3. SQLAlchemy Database Setup (app/database/session.py)**

from sqlalchemy.ext.asyncio import AsyncSession, create_async_engine

from sqlalchemy.orm import sessionmaker

from sqlalchemy.ext.declarative import declarative_base

from app.core.config import settings

\# Create async engine

engine = create_async_engine(

    settings.DATABASE_URL,

    echo=settings.DEBUG,  # Log SQL queries in debug mode

    future=True,

)

\# Create async session factory

AsyncSessionLocal = sessionmaker(

    bind=engine,

    class\_=AsyncSession,

    expire_on_commit=False,

    autocommit=False,

    autoflush=False,

)

\# Base class for ORM models

Base = declarative_base()

\# Dependency to get DB session

async def get_db() -> AsyncSession:

    async with AsyncSessionLocal() as session:

        try:

            yield session

        finally:

            await session.close()

**3\.1.2.4. Pydantic Schemas (app/models/pydantic_models.py)**

from pydantic import BaseModel, EmailStr

from datetime import datetime

from typing import Optional

\# Shared properties

class UserBase(BaseModel):

    email: Optional\[EmailStr] = None

    is_active: Optional\[bool] = True

    full_name: Optional\[str] = None

\# Properties to receive via API on creation

class UserCreate(UserBase):

    email: EmailStr

    password: str

\# Properties to receive via API on update

class UserUpdate(UserBase):

    password: Optional\[str] = None

\# Properties to return via API

class UserInDBBase(UserBase):

    id: int

    created_at: datetime

    class Config:

        orm_mode = True  # Allows conversion from ORM model

class User(UserInDBBase):

    pass

class UserInDB(UserInDBBase):

    hashed_password: str

**3\.1.2.5. SQLAlchemy ORM Model (app/models/orm_models.py)**

from sqlalchemy import Column, Integer, String, Boolean, DateTime, func

from app.database.base import Base

class User(Base):

    \__tablename_\_ = "users"

    id = Column(Integer, primary_key=True, index=True)

    email = Column(String, unique=True, index=True, nullable=False)

    hashed_password = Column(String, nullable=False)

    full_name = Column(String, index=True)

    is_active = Column(Boolean, default=True)

    created_at = Column(DateTime(timezone=True), server_default=func.now())

**3\.1.2.6. Repository Pattern (app/repositories/user_repository.py)**

from sqlalchemy import select, update

from sqlalchemy.ext.asyncio import AsyncSession

from app.models.orm_models import User

from app.models.pydantic_models import UserCreate, UserUpdate

class UserRepository:

    def \__init_\_(self, db: AsyncSession):

        self.db = db

    async def get_by_id(self, user_id: int) -> Optional\[User]:

        result = await self.db.execute(select(User).filter(User.id == user_id))

        return result.scalar_one_or_none()

    async def get_by_email(self, email: str) -> Optional\[User]:

        result = await self.db.execute(select(User).filter(User.email == email))

        return result.scalar_one_or_none()

    async def create(self, user_create: UserCreate, hashed_password: str) -> User:

        db_user = User(

            email=user_create.email,

            hashed_password=hashed_password,

            full_name=user_create.full_name,

        )

        self.db.add(db_user)

        await self.db.commit()

        await self.db.refresh(db_user)

        return db_user

    # ... update, delete methods

**3\.1.2.7. Application Service (app/services/user_service.py)**

from typing import Optional

from app.repositories.user_repository import UserRepository

from app.models.pydantic_models import UserCreate, User, UserUpdate

from app.core.security import get_password_hash, verify_password

class UserService:

    def \__init_\_(self, user_repository: UserRepository):

        self.user_repository = user_repository

    async def get_user(self, user_id: int) -> Optional\[User]:

        db_user = await self.user_repository.get_by_id(user_id)

        if db_user is None:

            raise ValueError(f"User with ID {user_id} not found")

        return User.from_orm(db_user)  # Convert ORM to Pydantic model

    async def create_user(self, user_create: UserCreate) -> User:

        # Check if user exists

        existing_user = await self.user_repository.get_by_email(user_create.email)

        if existing_user:

            raise ValueError("A user with this email already exists")

 

        # Hash password and create user

        hashed_password = get_password_hash(user_create.password)

        db_user = await self.user_repository.create(user_create, hashed_password)

        return User.from_orm(db_user)

    # ... other service methods

**3\.1.2.8. API Endpoint (FastAPI Router) (app/api/v1/endpoints/users.py)**

from fastapi import APIRouter, Depends, HTTPException, status

from sqlalchemy.ext.asyncio import AsyncSession

from typing import List

from app.database.session import get_db

from app.services.user_service import UserService

from app.repositories.user_repository import UserRepository

from app.models.pydantic_models import User, UserCreate

router = APIRouter()

@router.get("/{user_id}", response_model=User)

async def read_user(

    user_id: int,

    db: AsyncSession = Depends(get_db),

):

    user_repo = UserRepository(db)

    user_service = UserService(user_repo)

    try:

        user = await user_service.get_user(user_id)

        return user

    except ValueError as e:

        raise HTTPException(

            status_code=status.HTTP_404_NOT_FOUND,

            detail=str(e),

        )

@router.post("/", response_model=User, status_code=status.HTTP_201_CREATED)

async def create_user(

    \*,

    db: AsyncSession = Depends(get_db),

    user_in: UserCreate,

):

    user_repo = UserRepository(db)

    user_service = UserService(user_repo)

    try:

        user = await user_service.create_user(user_in)

        return user

    except ValueError as e:

        raise HTTPException(

            status_code=status.HTTP_400_BAD_REQUEST,

            detail=str(e),

        )

**3\.1.2.9. Dependency Injection for Services (app/api/dependencies.py)**

from fastapi import Depends

from sqlalchemy.ext.asyncio import AsyncSession

from app.database.session import get_db

from app.repositories.user_repository import UserRepository

from app.services.user_service import UserService

def get_user_repository(db: AsyncSession = Depends(get_db)) -> UserRepository:

    return UserRepository(db)

def get_user_service(user_repo: UserRepository = Depends(get_user_repository)) -> UserService:

    return UserService(user_repo)

\# Now in the router, you can do:

\# async def create_user(..., user_service: UserService = Depends(get_user_service)):

**3\.1.2.10. pytest Test Example (tests/services/test_user_service.py)**

import pytest

from unittest.mock import AsyncMock, MagicMock

from app.services.user_service import UserService

from app.models.pydantic_models import UserCreate

from app.models.orm_models import User

@pytest.fixture

def mock_user_repository():

    repo = AsyncMock()

    repo.get_by_email.return_value = None  # Simulate no existing user

    repo.create.return_value = User(id=1, email="test@example.com", hashed_password="hashed", full_name="Test User")

    return repo

@pytest.mark.asyncio

async def test_create_user_success(mock_user_repository):

    user_service = UserService(mock_user_repository)

    user_create = UserCreate(email="test@example.com", password="secret", full_name="Test User")

 

    result = await user_service.create_user(user_create)

 

    assert result.id == 1

    assert result.email == "test@example.com"

    mock_user_repository.get_by_email.assert_called_once_with("test@example.com")

    mock_user_repository.create.assert_called_once()

###### 4\. Implementation Guidelines

4\.1. Naming Conventions

Packages & Modules: lowercase_with_underscores (e.g., user_repository.py)

Classes: PascalCase (e.g., UserService, DatabaseConnection)

Functions & Variables: snake_case (e.g., get_user_by_id, database_url)

Constants: UPPERCASE_WITH_UNDERSCORES (e.g., DEFAULT_PAGE_SIZE, API_V1_STR)

Private: Use a leading underscore for non-public methods/variables (e.g., \_internal_helper)

4\.2. Code Style & Best Practices (PEP 8)

* Indentation: 4 spaces per indentation level
* Line Length: Maximum 88 characters (enforced by black)
* Imports: Group in this order, separated by a blank line:

\# Standard library imports

import os

from typing import Optional

\# Third-party imports

from fastapi import Depends

import pandas as pd

\# Local application/library specific imports

from app.models import User

* Type Hints: Use them everywhere. They are mandatory for function parameters and return values
* Docstrings: Use Google or NumPy style for all public modules, functions, classes, and methods
* String Quotes: Use double quotes " for docstrings and triple double quotes """ for multi-line strings. Use single quotes ' for all other strings, unless the string contains a single quote
* Avoid \* imports: Always use explicit imports
* Use Context Managers: For resource handling (files, sessions, locks)

4\.3. Error Handling

Use specific built-in exceptions where appropriate (ValueError, KeyError)

Define custom exception classes for domain-specific errors

In web frameworks, use HTTP exception classes (HTTPException in FastAPI) in routers. Let services raise native Python exceptions

Log exceptions with appropriate context

###### 5\. Performance Optimization

Asynchronous I/O: Use async/await for all I/O-bound operations (DB calls, HTTP requests)

Connection Pooling: Ensure database drivers and HTTP clients are configured with connection pools

Caching: Implement caching for frequently accessed data using redis or memcached

Algorithm Choice: Choose the right data structures (list, dict, set) and algorithms for the task

Lazy Loading: Use generators (yield) for processing large datasets without loading everything into memory

###### 6\. Security Considerations

* Dependency Scanning: Regularly update dependencies and use tools like safety or dependabot to scan for vulnerabilities
* Input Validation: Use Pydantic models for all input validation. Never trust client input
* Secrets: Never commit secrets. Use environment variables and .env files (added to .gitignore)
* Password Hashing: Always use a robust hashing algorithm like bcrypt (e.g., passlib library)
* SQL Injection: Use ORM methods or parameterized queries. Never use string formatting for SQL queries

###### 7\. Testing Requirements

* Test Coverage: Aim for high test coverage, especially for business logic and API endpoints
* Isolation: Mock external dependencies (databases, APIs) in unit tests
* Integration Tests: Write tests that run against a real test database (use pytest fixtures to set up/tear down)
* conftest.py: Use it to define common pytest fixtures available across the test suite

###### 8\. Documentation Standards

* Module Docstrings: Every .py file should have a docstring at the top describing its purpose
* Public API: Every public function, class, and method must have a detailed docstring
* Type Hints: Consider them a form of documentation. They are mandatory
* README.md: Should include how to install, configure, run, and test the project

This is the parent prompt that contains code generation guidelines for Python Web development. Please keep it as a reference. Do not generate any code now.