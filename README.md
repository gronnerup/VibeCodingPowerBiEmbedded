# 🚀 Power BI Embedded Portal - Vibe Coding Boilerplate

A complete boilerplate for building a Power BI Customer Portal with authentication, administration, and Azure deployment - designed for AI-assisted "vibe coding" with GitHub Copilot.

## 📖 About This Project

This repository is a **boilerplate/starter template** for rapidly building Power BI embedded portals using AI-assisted development (vibe coding). It includes comprehensive Copilot instructions that guide you through creating a fully functional customer portal from scratch.

Based on the presentation: **"Vibe Coding a Power BI Embedded Portal"** - demonstrating how to leverage GitHub Copilot and AI assistance to build production-ready applications efficiently.

## ✨ What You'll Build

A customer portal that includes:
- 🔐 User authentication (login/logout with JWT)
- 📊 Embedded Power BI reports with dynamic access
- 👥 User management and role-based access
- ⚙️ Admin panel for managing reports and users
- 🎨 Custom Power BI navigation (hidden filters, custom page tabs)
- ☁️ Ready for Azure App Service deployment

## 🛠️ Tech Stack

- **Frontend**: Vanilla JavaScript (no frameworks)
  - Power BI JavaScript SDK (powerbi-client)
  - Local dependencies (no CDN)
- **Backend**: Node.js with Express
- **Database**: sql.js (pure JavaScript SQLite)
- **Authentication**: JWT with bcryptjs
- **Power BI Auth**: Azure AD Service Principal (MSAL)
- **Hosting**: Azure App Service (Linux, Node 20 LTS)

## 📋 Prerequisites

Before you start, you'll need:

1. **GitHub Copilot** (required for vibe coding workflow)
2. **Node.js 20 LTS** installed locally
3. **Azure Subscription** (Free tier works fine)
4. **Power BI Pro or Premium** workspace
5. **Context7 MCP Server** (for Power BI documentation access)

### Required Azure Resources

You need to set up:
- Azure AD App Registration (Service Principal)
- Power BI Workspace with at least one report

## 🚀 Getting Started

### Step 1: Configure Copilot Instructions

The magic of this boilerplate is in the `.github/copilot-instructions.md` file. **Before you start coding**, update it with your Azure and Power BI details:

1. Open `.github/copilot-instructions.md`
2. Update the environment variables section with your information:

```env
# Azure AD for Power BI
AZURE_CLIENT_ID=your-client-id          # ⚠️ UPDATE THIS
AZURE_TENANT_ID=your-tenant-id          # ⚠️ UPDATE THIS
AZURE_CLIENT_SECRET=your-client-secret  # ⚠️ UPDATE THIS

# Power BI
POWERBI_WORKSPACE_ID=your-workspace-id  # ⚠️ UPDATE THIS
POWERBI_REPORT_ID=your-report-id        # ⚠️ UPDATE THIS
```

### Step 2: Set Up Context7 MCP Server

The instructions file references Context7 for fetching Power BI Embedded documentation. Install and configure it:

```powershell
# Install Context7 MCP server (if not already installed)
# Follow Context7 setup instructions for your environment
```

This enables Copilot to access the latest Power BI JavaScript SDK documentation and best practices.

### Step 3: Start Vibe Coding

Now you're ready! Simply start asking Copilot to build features:

```
"Create the basic Express server with authentication"
"Add Power BI embedding with token generation"
"Create the admin panel for managing reports"
"Deploy this to Azure App Service"
```

The Copilot instructions will guide the AI to:
- Use the correct tech stack
- Follow best practices
- Avoid common pitfalls
- Create production-ready code

## 📁 Project Structure (After Generation)

```
VibeCodingPowerBiEmbedded/
├── .github/
│   └── copilot-instructions.md   # AI coding guidelines
├── server.js                      # Express server
├── database.js                    # sql.js database manager
├── auth-service.js                # JWT authentication
├── powerbi-service.js             # Power BI embedding logic
├── package.json
├── .env                          # Environment variables (YOU CREATE)
└── public/                       # Static frontend
    ├── index.html                # Single page app
    ├── app.js                    # Frontend logic
    ├── app-extended.js           # Advanced features
    ├── styles.css                # Styling
    └── [libraries]               # Local JS dependencies
```

## 🔐 Azure AD App Registration Setup

### Create Service Principal for Power BI

1. Go to [Azure Portal](https://portal.azure.com) → Azure Active Directory → App Registrations
2. Click **New registration**
   - Name: `PowerBI-Embedded-Portal`
   - Supported account types: Single tenant
3. After creation, note down:
   - **Application (client) ID** → `AZURE_CLIENT_ID`
   - **Directory (tenant) ID** → `AZURE_TENANT_ID`
4. Go to **Certificates & secrets** → New client secret
   - Note down the **secret value** → `AZURE_CLIENT_SECRET`
5. Go to **API permissions** → Add permission
   - Select **Power BI Service**
   - Add these delegated permissions:
     - `Report.Read.All`
     - `Dataset.Read.All`
6. Grant admin consent

### Configure Power BI Workspace

1. Go to [Power BI Service](https://app.powerbi.com)
2. Navigate to your workspace → Settings → Access
3. Add your service principal with **Member** or **Admin** role
4. Note down:
   - Workspace ID (from URL or workspace settings)
   - Report ID (from report URL)

## 🎯 Vibe Coding Workflow

This boilerplate is designed for iterative AI-assisted development:

1. **Phase 1**: Basic structure (server, routing, static files)
2. **Phase 2**: Database & authentication
3. **Phase 3**: Power BI integration
4. **Phase 4**: Enhanced features (custom navigation, fullscreen)
5. **Phase 5**: Admin panel
6. **Phase 6**: Azure deployment

Each phase is documented in the Copilot instructions. Just ask Copilot to implement the next phase!

## ☁️ Deployment to Azure

The boilerplate includes **tested, battle-proven** Azure deployment steps in the Copilot instructions:

```powershell
# Ask Copilot: "Deploy this to Azure App Service"
# It will guide you through:
# - Creating Azure resources
# - Configuring environment variables
# - Building and deploying the app
# - Avoiding common pitfalls
```

**Critical Success Factors** (handled by instructions):
- ✅ Uses sql.js (NOT better-sqlite3 - which fails on Azure)
- ✅ Enables build automation
- ✅ Excludes node_modules from deployment
- ✅ Sets correct startup command
- ✅ Configures Node 20 runtime

## 📚 Resources

### Documentation
- [Power BI Embedded Documentation](https://learn.microsoft.com/en-us/power-bi/developer/embedded/)
- [Power BI JavaScript SDK](https://github.com/microsoft/PowerBI-JavaScript)
- [Azure App Service - Node.js](https://learn.microsoft.com/en-us/azure/app-service/quickstart-nodejs)

### Presentation
- **"Vibe Coding a Power BI Embedded Portal"** - Session materials included

### Context7 & AI Tools
- Context7 MCP Server - For accessing Power BI documentation
- GitHub Copilot - AI pair programming

## ⚠️ Important Notes

### Database Choice: sql.js
This boilerplate uses **sql.js** instead of better-sqlite3 because:
- ✅ Pure JavaScript - no native compilation
- ✅ Works perfectly on Azure App Service
- ✅ No deployment issues
- ❌ better-sqlite3 fails on Azure (native dependency issues)

### Local Dependencies
All JavaScript libraries are downloaded locally to `/public` folder:
- ✅ No CDN dependencies
- ✅ Works offline
- ✅ Full control over versions
- ✅ Faster loading in production

### Security Considerations
- Change `JWT_SECRET` to a strong random value
- Never commit `.env` file to source control
- Rotate client secrets regularly
- Use Azure Key Vault for production secrets

## 🤝 Contributing

This is a boilerplate/template project. Feel free to:
- Fork it for your own projects
- Submit improvements to the Copilot instructions
- Share your vibe coding experiences

## 📄 License

MIT License - Feel free to use this boilerplate for any purpose.

## 🙋 Support

This boilerplate is designed to be self-explanatory with comprehensive Copilot instructions. If you encounter issues:

1. Check the Copilot instructions file for guidance
2. Ask Copilot to help troubleshoot
3. Review the presentation materials
4. Check Azure logs: `az webapp log download`

## 🎓 Learning Path

**New to Vibe Coding?**
1. Read through `.github/copilot-instructions.md`
2. Watch the presentation "Vibe Coding a Power BI Embedded Portal"
3. Start with Phase 1 - let Copilot guide you
4. Iterate and learn as you build

**Key Principle**: Trust the AI, but verify. The instructions are battle-tested to avoid common pitfalls.

---

**Happy Vibe Coding! 🎉**

Built with ❤️ and AI assistance
