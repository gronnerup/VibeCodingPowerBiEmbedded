# 🤖 Copilot Instructions for Vibe Coding a Power BI Embedded Portal

These instructions guide you (Copilot) in helping me build a complete Power BI Customer Portal with authentication, administration, and Azure deployment.

---

## 🎯 Project Goal

Build a customer portal that:
- Embeds Power BI reports with authentication
- Has user login/logout functionality
- Includes admin features for managing users and reports
- Uses a simple database for user/report data
- Deploys successfully to Azure App Service

---

## 🧱 Tech Stack

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

---

## 📂 Project Structure

```
project/
├── server.js           # Main Express server
├── database.js         # sql.js database manager
├── auth-service.js     # JWT authentication
├── powerbi-service.js  # Power BI embedding logic
├── package.json
├── .env               # Environment variables
└── public/            # Static frontend files
    ├── index.html     # Single page app
    ├── app.js         # Frontend JavaScript
    ├── app-extended.js # Extended features
    └── styles.css     # Styling
```

---

## 🛢️ Database Rules - CRITICAL

**ALWAYS use sql.js, NEVER use better-sqlite3**

```javascript
const initSqlJs = require('sql.js');

// Initialize database
async initialize() {
    this.SQL = await initSqlJs();
    
    // Load or create database
    if (fs.existsSync(this.dbPath)) {
        const buffer = fs.readFileSync(this.dbPath);
        this.db = new this.SQL.Database(buffer);
    } else {
        this.db = new this.SQL.Database();
    }
}

// Always save after modifications
save() {
    const data = this.db.export();
    fs.writeFileSync(this.dbPath, data);
}

// Query pattern
const result = this.db.exec('SELECT * FROM users WHERE username = ?', [username]);
```

**Why sql.js?**
- Pure JavaScript - works on any platform
- No native compilation needed
- Deploys perfectly to Azure
- better-sqlite3 FAILS on Azure (native compilation issues)

---

## 🔐 Environment Variables

Create `.env` file with:
```
PORT=3000
JWT_SECRET=SpaceParts-SuperSecret-JWT-Key-Change-This-In-Production-2024

# Azure AD for Power BI
AZURE_CLIENT_ID=your-client-id
AZURE_TENANT_ID=your-tenant-id
AZURE_CLIENT_SECRET=your-client-secret

# Power BI
POWERBI_WORKSPACE_ID=your-workspace-id
POWERBI_REPORT_ID=your-report-id
```
---

# Get these values from Azure Portal and Power BI Service


## 🎨 Frontend Architecture

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

---

## 🚀 Azure Deployment - TESTED PROCESS

**CRITICAL STEPS TO AVOID ERRORS:**

### 1. Create Azure Resources

```powershell
# Variables
$resourceGroup = "YourProject-RG"
$location = "westeurope"
$appName = "yourapp-portal-$(Get-Random -Maximum 9999)"
$planName = "YourProject-Plan"

# Create resource group
az group create --name $resourceGroup --location $location

# Create app service plan (Free tier)
az appservice plan create --name $planName --resource-group $resourceGroup --sku F1 --is-linux

# Create web app with Node 20
az webapp create --resource-group $resourceGroup --plan $planName --name $appName --runtime "NODE:20-lts"
```

### 2. Configure Environment Variables

```powershell
az webapp config appsettings set `
  --resource-group $resourceGroup `
  --name $appName `
  --settings `
    JWT_SECRET="your-secret" `
    AZURE_CLIENT_ID="your-id" `
    AZURE_TENANT_ID="your-tenant" `
    AZURE_CLIENT_SECRET="your-secret" `
    POWERBI_WORKSPACE_ID="workspace-id" `
    POWERBI_REPORT_ID="report-id"
```

### 3. CRITICAL: Enable Build Automation

```powershell
az webapp config appsettings set `
  --resource-group $resourceGroup `
  --name $appName `
  --settings `
    SCM_DO_BUILD_DURING_DEPLOYMENT=true `
    ENABLE_ORYX_BUILD=true
```

### 4. Set Startup Command

```powershell
az webapp config set `
  --resource-group $resourceGroup `
  --name $appName `
  --startup-file "node server.js"
```

### 5. Create Deployment Package

```powershell
# Create zip with ONLY source files (no node_modules, no .deployment file)
$filesToDeploy = @("server.js", "database.js", "auth-service.js", "powerbi-service.js", "package.json", "public")
Compress-Archive -Path $filesToDeploy -DestinationPath deploy.zip -Force
```

### 6. Deploy

```powershell
az webapp deploy `
  --resource-group $resourceGroup `
  --name $appName `
  --src-path deploy.zip `
  --type zip `
  --async false
```

---

## ⚠️ Common Deployment Pitfalls to AVOID

1. **DO NOT include .deployment file** - causes build failures
2. **DO NOT use better-sqlite3** - native compilation fails on Azure
3. **DO NOT include node_modules in zip** - let Azure install them
4. **DO NOT forget to enable build automation** - dependencies won't install
5. **DO NOT use wrong runtime format** - use "NODE:20-lts" not "NODE|20-lts"
6. **DO NOT skip startup command** - Azure won't know which file to run

---

## 📋 Step-by-Step Feature Implementation

### Phase 1: Basic Structure
- Create Express server
- Set up static file serving
- Create simple HTML/CSS frontend
- Add basic routing

### Phase 2: Database & Auth
- Initialize sql.js database
- Create users table
- Implement JWT authentication
- Add login/logout endpoints
- Seed with demo users

### Phase 3: Power BI Integration
- Add Power BI service with MSAL
- Create embed token endpoint
- Implement frontend embed logic
- Add report loading/error handling

### Phase 4: Enhanced Features
- Hide filter pane in Power BI
- Hide page tabs and create custom navigation
- Add fullscreen toggle
- Implement page switching

### Phase 5: Admin Panel
- Create reports management table
- Add CRUD operations for reports
- Implement admin-only access
- Seed sample reports

### Phase 6: Deployment
- Follow Azure deployment steps
- Configure environment variables
- Test production deployment
- Verify all features work

---

## 🧠 Copilot Behavior Guidelines

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
- Follow the tested deployment process above
- Include validation steps
- Provide clear progress updates

**When errors occur:**
- Check logs with `az webapp log download`
- Diagnose the root cause
- Provide specific fixes
- Test before confirming

---

## ✅ Success Criteria

The portal is complete when:
- [x] Users can log in with username/password
- [x] Power BI reports embed and display correctly
- [x] Filter pane and page tabs are hidden
- [x] Custom page navigation sidebar works
- [x] Admin can manage reports
- [x] Multiple users have different roles
- [x] Application deploys to Azure successfully
- [x] All features work in production

---

## 🎓 Remember

- Keep it simple - vanilla JS works great
- sql.js is reliable for small-scale apps
- Azure Free tier is perfect for demos
- Test locally before deploying
- Environment variables for all secrets
