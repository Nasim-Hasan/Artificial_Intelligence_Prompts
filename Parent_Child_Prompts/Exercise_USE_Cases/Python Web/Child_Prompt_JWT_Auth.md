#### Child Prompt: JWT Authentication \& Refresh Flow



Objective: Generate a minimal, secure JWT auth system for the existing User model, integrated into the parent's FastAPI/SQLAlchemy structure.



Requirements:

* Schemas (pydantic\_models.py):
* Token: access\_token, token\_type, refresh\_token.
* TokenRefresh: refresh\_token.
* TokenPayload: Core JWT claims.



Security Utilities (security.py):

* verify\_password(plain, hashed) -> bool (using passlib/bcrypt).
* get\_password\_hash(password) -> str.
* create\_access\_token(data, expires\_delta) -> str.
* decode\_token(token) -> TokenPayload.
* Service Layer (user\_service.py):
* Extend UserService with authenticate\_user(email, password) -> User.



API Endpoints (auth.py):

* POST /auth/login: Accepts credentials, returns tokens.
* POST /auth/refresh: Accepts refresh token, returns new tokens.
* GET /users/me (protected): Returns current user.



Dependencies (dependencies.py):

get\_current\_user(token) -> User: Validates JWT and fetches user.



Key Constraints:

* Use settings from config.py for SECRET\_KEY, ALGORITHM, ACCESS\_TOKEN\_EXPIRE\_MINUTES.
* Hash passwords with bcrypt. Never return passwords.
* Short-lived access token, longer-lived refresh token.
* Raise HTTPException in routes, ValueError in services.



Generate the concise code implementing the above.

