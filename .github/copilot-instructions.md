# OBJECTIVE

These instructions guide you (Copilot) in helping me build a complete Power BI Customer Portal with authentication, administration, and Azure deployment.

# PROJECT GOAL

Build a customer portal that:
- Embeds Power BI reports with authentication
- Has user login/logout functionality
- Includes admin features for managing users and reports
- Uses a simple database for user/report data
- Deploys successfully to Azure App Service

# RESPONSE RULES

**When I ask to create files:**
- Provide complete, ready-to-use code
- Use sql.js for all database operations
- Include proper error handling
- Add helpful console.log statements
- **Download JavaScript libraries locally** - never use CDN links
- Place all `.js` library files in `/public` folder
- Reference libraries with relative paths (e.g., `<script src="powerbi.min.js"></script>`)

**When I ask about Power BI:**
- Use context7 for all Power BI embedded, Power BI javascript and Power BI REST API questions.
- Use the Power BI JavaScript SDK (powerbi-client)
- Implement proper token refresh
- Handle embed errors gracefully
- Support configuration options from latest docs

**When I ask to deploy:**
- Use PowerShell commands (Windows environment)
- Use Azure CLI for all deployment steps
- Follow the tested deployment process above
- Include validation steps
- Provide clear progress updates

**When errors occur:**
- Check logs with `az webapp log download`
- Diagnose the root cause
- Provide specific fixes
- Test before confirming


# TECH STACK REQUIREMENTS

**IMPORTANT - Use This Exact Stack:**
- **Frontend**: Vanilla JavaScript (NO React/Vue/Angular)
  - Single HTML page with vanilla JS
  - Power BI JavaScript SDK (powerbi-client)
  - Simple CSS for styling
  - **NO CDN links** - download all JavaScript libraries locally to `/public` folder
  - Serve all dependencies from the application itself
- **Backend**: Node.js with Express
- **Database**: `sql.js` (pure JavaScript SQLite - NO better-sqlite3)
- **Auth**: JWT with bcryptjs for password hashing
- **Power BI Auth**: Azure AD Service Principal (MSAL)
- **Hosting**: Azure App Service (Linux, Free Tier)
- **Node Version**: 20 LTS


# DATABASE RULES - CRITICAL

**ALWAYS use sql.js, NEVER use better-sqlite3**

**Why sql.js?**
- Pure JavaScript - works on any platform
- No native compilation needed
- Deploys perfectly to Azure
- better-sqlite3 FAILS on Azure (native compilation issues)


# ENVIRONMENT VARIABLES

Create `.env` file with:
```
PORT=3000
JWT_SECRET=SpaceParts-SuperSecret-JWT-Key-Change-This-In-Production

# Azure AD for Power BI
AZURE_CLIENT_ID=your-client-id
AZURE_TENANT_ID=your-tenant-id
AZURE_CLIENT_SECRET=your-client-secret

# Power BI
POWERBI_WORKSPACE_ID=your-workspace-id
POWERBI_REPORT_ID=your-report-id
```

# FRONTEND ARCHITECTURE

**Single Page Application Pattern:**
- One HTML file with all pages as hidden sections
- JavaScript toggles visibility
- No page refreshes
- Power BI SDK loads reports dynamically

**Key Features to Include:**
1. Login page with username/password
2. Main portal with embedded Power BI report
3. Admin panel for managing reports
4. User profile display
5. Logout functionality

# COMMON DEVELOPMENT TIPS

1. **DO NOT include .deployment file** - causes build failures
2. **DO NOT use better-sqlite3** - native compilation fails on Azure
3. **DO NOT include node_modules in zip** - let Azure install them
4. **DO NOT forget to enable build automation** - dependencies won't install
5. **DO NOT use wrong runtime format** - use "NODE:20-lts" not "NODE|20-lts"
6. **DO NOT skip startup command** - Azure won't know which file to run

# WORKFLOW

## Step 1: Basic Structure
- Create Express server
- Set up static file serving
- Create simple HTML/CSS frontend
- Add basic routing

## Step 2: Database & Auth
- Initialize sql.js database
- Create users table
- Implement JWT authentication
- Add login/logout endpoints
- Seed with demo users

## Step 3: Power BI Integration
- Add Power BI service with MSAL
- Create embed token endpoint
- Implement frontend embed logic
- Add report loading/error handling

## Step 4: Enhanced Features
- Hide filter pane in Power BI
- Hide page tabs and create custom navigation
- Add fullscreen toggle
- Implement page switching

## Step 5: Admin Panel
- Create reports management table
- Add CRUD operations for reports
- Implement admin-only access
- Seed sample reports

## STEP 6: Deployment
- Follow Azure deployment steps
- Configure environment variables
- Test production deployment
- Verify all features work


# REMEMBER THESE TIPS
- Keep it simple - vanilla JS works great
- sql.js is reliable for small-scale apps
- Azure Free tier is perfect for demos
- Test locally before deploying
- Environment variables for all secrets