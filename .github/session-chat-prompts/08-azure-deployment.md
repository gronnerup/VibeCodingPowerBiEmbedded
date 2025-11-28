# Prompt 08: Deploy to Azure

## User Request

Now help me deploy this application to Azure App Service.

## Expected Outcome

- Azure resources created (resource group, app service plan, web app)
- Application packaged for deployment
- Environment variables configured in Azure
- Build automation enabled
- Application successfully deployed and running
- Accessible via Azure URL

## Deployment Steps

1. Create resource group in West Europe
2. Create Free tier App Service plan (Linux)
3. Create Web App with Node 20 LTS runtime
4. Configure all environment variables
5. Enable build automation (CRITICAL)
6. Set startup command to "node server.js"
7. Create deployment zip (source files only, no node_modules)
8. Deploy using az webapp deploy
9. Verify deployment successful

## Critical Settings

- Runtime: "NODE:20-lts"
- SCM_DO_BUILD_DURING_DEPLOYMENT=true
- ENABLE_ORYX_BUILD=true
- Startup file: "node server.js"
- NO .deployment file
- Use sql.js (not better-sqlite3)
