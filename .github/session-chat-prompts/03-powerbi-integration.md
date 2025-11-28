# Prompt 03: Power BI Integration

## User Request

Integrate Power BI embedding using Azure AD Service Principal authentication. Create an endpoint to get embed tokens and display reports in the portal.

## Expected Outcome

- PowerBI service using MSAL for authentication
- Embed token endpoint that returns token and embed URL
- Frontend code to embed reports using powerbi-client SDK
- Error handling for failed embeds
- Loading indicators while report loads

## Environment Variables Needed

- AZURE_CLIENT_ID
- AZURE_TENANT_ID
- AZURE_CLIENT_SECRET
- POWERBI_WORKSPACE_ID
- POWERBI_REPORT_ID
