# alx-backend-user-data

## Table of Contents
- [Project Overview](#project-overview)
- [Learning Objectives](#learning-objectives)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
- [Features](#features)
  - [0. Regex-ing](#0-regex-ing)
  - [1. Log Formatter](#1-log-formatter)
  - [2. Create Logger](#2-create-logger)
  - [3. Connect to Secure Database](#3-connect-to-secure-database)
  - [4. Read and Filter Data](#4-read-and-filter-data)
- [Resources](#resources)
- [License](#license)

## Project Overview
This project focuses on managing **Personally Identifiable Information (PII)** securely in backend applications using Python. The goal is to demonstrate skills in handling sensitive data, logging, encryption, and secure database connections. The implementation ensures sensitive information is obfuscated in logs, passwords are securely hashed, and database connections are protected using environment variables.

## Learning Objectives
By the end of this project, you will be able to:
- Identify examples of Personally Identifiable Information (PII).
- Implement a log filter that obfuscates PII fields.
- Encrypt passwords and verify their validity.
- Authenticate and connect to a database using environment variables for security.

## Requirements
- **OS**: Ubuntu 18.04 LTS
- **Python Version**: Python 3.7
- **Coding Style**: [Pycodestyle](https://pypi.org/project/pycodestyle/) (version 2.5)
- Your code files should be executable and include documentation.
- Ensure each Python file starts with `#!/usr/bin/env python3`.
- **Database**: MySQL (using `mysql-connector-python` for database connections)

## Setup Instructions

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/martinnyemba/alx-backend-user-data.git
    cd alx-backend-user-data/0x00-personal_data
    ```

2. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Set up Environment Variables**:
    ```bash
    export PERSONAL_DATA_DB_USERNAME='root'
    export PERSONAL_DATA_DB_PASSWORD='root'
    export PERSONAL_DATA_DB_HOST='localhost'
    export PERSONAL_DATA_DB_NAME='my_db'
    ```

4. **Database Setup**:
    ```sql
    CREATE DATABASE IF NOT EXISTS my_db;
    CREATE USER IF NOT EXISTS 'root'@'localhost' IDENTIFIED BY 'root';
    GRANT ALL PRIVILEGES ON my_db.* TO 'root'@'localhost';
    ```

5. **Run the Project**:
    ```bash
    ./main.py
    ```

## Features

### 0. Regex-ing
- **Task**: Implement `filter_datum()` function to obfuscate specific PII fields in a log message.
- **Usage**:
    ```python
    fields = ["password", "date_of_birth"]
    message = "name=John Doe;email=johndoe@example.com;password=secret123;date_of_birth=01/01/2000;"
    print(filter_datum(fields, 'xxx', message, ';'))
    # Output: name=John Doe;email=johndoe@example.com;password=xxx;date_of_birth=xxx;
    ```

### 1. Log Formatter
- **Task**: Extend the `RedactingFormatter` class to obfuscate sensitive data in logs.
- **Example**:
    ```python
    formatter = RedactingFormatter(fields=("email", "password"))
    message = "email=johndoe@example.com; password=my_secret_password;"
    log_record = logging.LogRecord("logger", logging.INFO, None, None, message, None, None)
    print(formatter.format(log_record))
    # Output: email=***; password=***;
    ```

### 2. Create Logger
- **Task**: Implement a `get_logger()` function to return a configured logger instance.
- **PII Fields**: `name`, `email`, `phone`, `ssn`, `password`
- **Usage**:
    ```python
    logger = get_logger()
    logger.info("User login attempt")
    ```

### 3. Connect to Secure Database
- **Task**: Implement `get_db()` function to securely connect to MySQL using environment variables.
- **Dependencies**: Ensure `mysql-connector-python` is installed.
- **Usage**:
    ```python
    db = get_db()
    cursor = db.cursor()
    cursor.execute("SELECT * FROM users;")
    for row in cursor:
        print(row)
    cursor.close()
    db.close()
    ```

### 4. Read and Filter Data
- **Task**: Implement a `main()` function to fetch and display obfuscated user data from the database.
- **Example Output**:
    ```
    [HOLBERTON] user_data INFO: name=***; email=***; phone=***; ssn=***; password=***;
    ```

## Resources
- [What Is PII, non-PII, and Personal Data?](https://www.csoonline.com/article/3444488/what-is-pii.html)
- [Python `logging` Documentation](https://docs.python.org/3/library/logging.html)
- [Python `bcrypt` Package](https://pypi.org/project/bcrypt/)
- [Logging to Files, Setting Levels, and Formatting](https://realpython.com/python-logging/)

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
