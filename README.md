# blank_python_project

## Overview

A Python project template with pre-configured development tools, logging with rotation, and code quality checks.

## Features

- **Structured Project Layout**: Organized source code with separate modules for configuration, helpers, and models
- **Logging with Rotation**: Centralized logging system with automatic file rotation (10MB per file, 5 backups)
- **Pre-commit Hooks**: Automated code formatting and quality checks using isort, black, ruff, and pylint
- **Type Hints**: Full type annotation support throughout the codebase
- **Environment-based Configuration**: Development and production configurations
- **Main Entry Point**: Ready-to-use application entry point with proper error handling

## Setup

### 1. Clone the Repository

Begin by cloning the repository to your local machine:

```bash
git clone https://github.com/sergeychernyakov/blank_python_project.git
cd blank_python_project
```

### 2. Create a Virtual Environment

It's recommended to use a virtual environment to manage dependencies:

```bash
python3 -m venv .venv
```

### 3. Activate the Virtual Environment

Activate the virtual environment before installing dependencies.

- **Linux/MacOS:**

    ```bash
    source .venv/bin/activate
    ```

- **Windows:**

    ```bash
    .venv\Scripts\activate
    ```

### 4. Install Dependencies

Install the required packages using `pip`:

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

The application relies on environment variables for configuration. Create a `.env` file in the root directory with the following content:

```env
APP_ENV=development
```

- Ensure that the `.env` file is **not** committed to version control to protect sensitive information.

### 6. Export Installed Packages (Optional)

If you add new dependencies during development, update the `requirements.txt` file:

```bash
pip freeze > requirements.txt
```

## Pre-commit Hooks

This project uses pre-commit hooks to ensure code quality:

### Tools Used:
- **isort**: Sorts and organizes imports
- **black**: Formats code to a consistent style
- **ruff**: Fast Python linter
- **pylint**: Code quality checker (minimum score: 10.0)
- **pytest**: Runs tests with coverage requirement (90%+)

### Setup:
```bash
pip install pre-commit
pre-commit install
```

### Manual Run:
```bash
pre-commit run --all-files
```

Pre-commit will automatically run on every commit to ensure code quality.


## Usage

### Running the Application

To run the main application:

```bash
python main.py
```

The application will:
1. Initialize the logging system with rotation
2. Run the main application logic
3. Handle graceful shutdown on interruption (Ctrl+C)
4. Log all activities to both console and file (`tmp/logs/`)

### Using the Logger

Import and use the logger in your modules:

```python
from src.helpers.logger import get_logger

logger = get_logger(__name__)
logger.info("Starting process")
logger.error("An error occurred", exc_info=True)
```

## Project Structure

```
.
├── README.md
├── CLAUDE.md              # AI assistant instructions
├── PYTHON_STYLE_GUIDE.md  # Python coding standards
├── main.py                # Application entry point
├── media/                 # Media assets
├── requirements.txt       # Python dependencies
├── src/
│   ├── __init__.py
│   ├── config/           # Configuration module
│   │   ├── __init__.py
│   │   └── settings.py   # Environment-based settings
│   ├── helpers/          # Utility modules
│   │   ├── __init__.py
│   │   └── logger.py     # Logging with rotation
│   └── models/           # Data models
│       ├── __init__.py
│       ├── base.py       # Base model with validation
│       └── enums.py      # Enumerations
├── tests/                # Unit tests
│   └── __init__.py
└── tmp/
    └── logs/             # Application logs with rotation
```

### Directory Breakdown

- **`main.py`**: Main application entry point with error handling and logging
- **`media/`**: Contains input and output files, and other media assets
- **`src/`**: Source code organized into subdirectories:
  - **`config/`**: Configuration management with environment-based settings
  - **`helpers/`**: Utility modules including the logger with rotation
  - **`models/`**: Data models with Pydantic base model and enumerations
- **`tests/`**: Unit tests for various components
- **`tmp/logs/`**: Log files with automatic rotation (10MB limit, 5 backups)

## Logging

Logs are stored in the `tmp/logs/` directory with automatic rotation:
- Each module logs to its own file (e.g., `__main__.log`, `module_name.log`)
- Log files rotate when they reach 10MB in size
- Up to 5 backup files are kept (`.log.1` through `.log.5`)
- Logging level is DEBUG in development, INFO in production
- Logs output to both console and file simultaneously

## Testing

Unit tests are located in the `tests/` directory. To run the tests, execute:

```bash
pytest
```

