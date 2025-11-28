# Prompt 02: Database and Authentication

## User Request

Set up a database to store users and implement login/logout functionality with JWT tokens. Create a few demo users with different roles (admin and regular user).

## Expected Outcome

- sql.js database initialized
- Users table with username, password (hashed), role, email
- Login endpoint that returns JWT token
- Logout functionality
- Middleware to protect routes
- Seed data with admin and demo users

## Sample Users

- admin / admin123 (role: admin)
- demo / demo123 (role: user)
