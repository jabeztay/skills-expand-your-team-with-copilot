# Development Guide

## Initial Setup

This project is best developed using GitHub Codespaces, which provides a consistent development environment with all the necessary tools pre-configured.

### Setting up your development environment

1. Open the repository in a codespace
2. Wait for the container to finish building and installing dependencies
3. Install Python dependencies by running:

   ```bash
   python -m pip install -r requirements.txt
   ```

### Dependencies

The project requires the following Python packages:

- FastAPI - Modern web framework for building APIs
- Uvicorn - ASGI server implementation for running the FastAPI application
- PyMongo - MongoDB driver for Python
- Argon2 - Password hashing library for secure authentication

These dependencies will be installed when you run `pip install -r requirements.txt`

## Debugging

### Running the website locally

1. From VS Code's Run and Debug view (Ctrl+Shift+D), select "Launch Mergington WebApp" from the launch configuration dropdown
2. Press F5 or click the green play button to start debugging
3. The website will be available at `http://localhost:8000`
4. The API documentation will be available at `http://localhost:8000/docs`

### Debugging tips

- FastAPI's auto-reload feature will automatically restart the server when you make code changes
- Use the interactive API documentation at `/docs` to test your endpoints

## Getting Started

1. Install the dependencies:

   ```bash
   pip install -r src/requirements.txt
   ```

2. Ensure MongoDB is running locally on port 27017

3. Run the application from the src directory:

   ```bash
   cd src
   uvicorn app:app --reload
   ```

4. Open your browser and go to:
   - Main application: http://localhost:8000
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## Usage

### API Endpoints

#### Activities

| Method | Endpoint                                      | Description                                                          |
| ------ | --------------------------------------------- | -------------------------------------------------------------------- |
| GET    | `/activities`                                 | Get all activities with optional filtering by day and time           |
| GET    | `/activities/days`                            | Get a list of all days that have activities scheduled                |
| POST   | `/activities/{activity_name}/signup`          | Register a student for an activity (requires teacher authentication) |
| POST   | `/activities/{activity_name}/unregister`      | Unregister a student from an activity (requires teacher authentication) |

**Query Parameters for `/activities`:**
- `day` (optional): Filter activities by day (e.g., 'Monday', 'Tuesday')
- `start_time` (optional): Filter activities starting at or after this time (24-hour format, e.g., '14:30')
- `end_time` (optional): Filter activities ending at or before this time (24-hour format, e.g., '17:00')

**Query Parameters for signup/unregister:**
- `email` (required): Student email address
- `teacher_username` (required): Username of the authenticated teacher

#### Authentication

| Method | Endpoint                 | Description                                      |
| ------ | ------------------------ | ------------------------------------------------ |
| POST   | `/auth/login`            | Login with teacher credentials                   |
| GET    | `/auth/check-session`    | Validate a user session                          |

**Default Teacher Accounts:**
- Username: `mrodriguez`, Password: `art123` (Ms. Rodriguez)
- Username: `mchen`, Password: `chess456` (Mr. Chen)
- Username: `principal`, Password: `admin789` (Principal Martinez)

> [!IMPORTANT]
> All data is stored in MongoDB. The database is automatically initialized with sample activities and teacher accounts on first run.
