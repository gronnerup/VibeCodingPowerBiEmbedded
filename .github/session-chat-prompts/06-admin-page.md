# Prompt 06: Admin Page

## User Request

Add an admin page where administrators can manage reports. Create a reports table in the database and add CRUD operations for managing which reports are available.

## Expected Outcome

- Admin page only accessible to users with admin role
- Reports table in database
- UI to view, add, edit, delete reports
- List showing report ID, name, workspace ID
- Protection to prevent non-admins from accessing

## Database Schema

Reports table with:
- id (primary key)
- reportId (Power BI report ID)
- reportName (display name)
- workspaceId (Power BI workspace ID)
