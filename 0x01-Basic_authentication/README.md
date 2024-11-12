# Basic Authentication API

## Overview
This project implements a Basic Authentication system for a simple REST API. The implementation walks through each step of the authentication mechanism for learning purposes, although in production environments you should use established authentication frameworks.

## Project Structure
```
0x01-Basic_authentication/
├── api/
│   └── v1/
│       ├── auth/
│       │   ├── __init__.py
│       │   ├── auth.py
│       │   └── basic_auth.py
│       ├── views/
│       │   └── index.py
│       └── app.py
├── models/
│   └── user.py
└── requirements.txt
```

## Environment Setup
- Ubuntu 18.04 LTS
- Python 3.7
- Style: pycodestyle 2.5

## Installation
1. Clone the repository
2. Install dependencies:
```bash
pip3 install -r requirements.txt
```

## Running the Server
```bash
API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
```

For Basic Authentication:
```bash
API_HOST=0.0.0.0 API_PORT=5000 AUTH_TYPE=basic_auth python3 -m api.v1.app
```

## Features

### Authentication System
- Base Authentication Class (`Auth`)
- Basic Authentication Implementation (`BasicAuth`)
- Custom error handlers for 401 and 403 responses
- Base64 encoding/decoding for authentication headers
- User credential extraction and validation

### API Endpoints

#### Status Endpoints
- `GET /api/v1/status/`: Get API status
- `GET /api/v1/unauthorized/`: Test 401 error
- `GET /api/v1/forbidden/`: Test 403 error

#### Protected Routes
- `GET /api/v1/users`: Get list of users (requires authentication)

### Error Handling
- 401 Unauthorized: `{"error": "Unauthorized"}`
- 403 Forbidden: `{"error": "Forbidden"}`

## Authentication Flow
1. Client sends request with Basic Auth header
2. Server extracts and validates Base64 encoded credentials
3. Credentials are checked against user database
4. If valid, access is granted; if invalid, appropriate error is returned

## Testing
Test the API using curl:

```bash
# Test status endpoint
curl "http://0.0.0.0:5000/api/v1/status"

# Test unauthorized access
curl "http://0.0.0.0:5000/api/v1/unauthorized"

# Test with invalid auth
curl "http://0.0.0.0:5000/api/v1/users" -H "Authorization: Basic invalid_token"

# Test with valid auth
curl "http://0.0.0.0:5000/api/v1/users" -H "Authorization: Basic <valid_token>"
```

## Development Requirements
- All files must be executable
- Documentation required for modules, classes, and methods
- All modules should have documentation: `python3 -c 'print(__import__("my_module").__doc__)'`
- All functions (inside and outside a class) should have documentation

## Authors
Nyemba Martin

## Setup

```
$ pip3 install -r requirements.txt
```

## Run

```
$ API_HOST=0.0.0.0 API_PORT=5000 python3 -m api.v1.app
```

