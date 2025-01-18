# ALX Backend User Authentication Service

## Project Overview
This project implements a user authentication service using Flask, SQLAlchemy, and bcrypt. It demonstrates core concepts of user authentication including registration, login, session management, and password hashing.

## Prerequisites
- Ubuntu 18.04 LTS
- Python 3.7
- SQLAlchemy 1.3.x
- Flask
- bcrypt

## Installation
```bash
# Clone the repository
git clone https://github.com/[username]/alx-backend-user-data.git

# Install dependencies
pip3 install bcrypt
pip3 install SQLAlchemy==1.3.x
pip3 install Flask
```

## Project Structure
```
0x03-user_authentication_service/
├── app.py             # Flask application
├── auth.py            # Authentication logic
├── db.py              # Database operations
├── user.py            # User model
└── README.md
```

## Features
1. User Management:
   - User registration
   - Password hashing
   - Session management
   - Profile retrieval

2. Authentication:
   - Login/Logout functionality
   - Session creation/destruction
   - Password validation
   - Session ID handling

3. API Endpoints:
   - POST /users - Register new user
   - POST /sessions - Login user
   - DELETE /sessions - Logout user
   - GET /profile - Get user profile
   - GET / - Basic welcome route

## API Routes

### User Registration
```bash
POST /users
data: email, password
```

### User Login
```bash
POST /sessions
data: email, password
```

### User Logout
```bash
DELETE /sessions
```

### User Profile
```bash
GET /profile
requires: session_id cookie
```

## Testing
```bash
# Run the Flask application
python3 app.py

# Test registration
curl -XPOST localhost:5000/users -d 'email=test@test.com' -d 'password=mypass'

# Test login
curl -XPOST localhost:5000/sessions -d 'email=test@test.com' -d 'password=mypass'
```

## Development Guidelines
1. Follow PEP 8 style guide (pycodestyle 2.5)
2. All files should use shebang `#!/usr/bin/env python3`
3. Include docstrings for all modules, classes, and functions
4. Implement type annotations for all functions
5. Flask app should only interact with Auth class, not DB directly
6. Use only public methods of Auth and DB outside these classes

## Author
Martin Nyemba

## License
Copyright © 2025 ALX, All rights reserved.
