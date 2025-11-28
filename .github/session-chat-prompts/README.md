# Vibe Coding Demo - Prompt Sequence

This folder contains the sequential prompts for recreating the Power BI Customer Portal in a live demo session.

## How to Use

1. Start with a blank workspace
2. Use each prompt in order (01 through 10)
3. Let Copilot implement each feature completely before moving to the next
4. Prompts 09 is optional (for demonstrating troubleshooting)
5. End with verification in prompt 10

## Prompt Overview

| # | Prompt | Focus |
|---|--------|-------|
| 01 | Initial Portal Setup | Basic Express server, HTML, routing |
| 02 | Database and Auth | sql.js setup, JWT, user login |
| 03 | Power BI Integration | MSAL auth, embed tokens, report display |
| 04 | Hide Filter Pane | Clean up Power BI UI |
| 05 | Custom Page Navigation | Replace tabs with sidebar |
| 06 | Admin Page | Reports management interface |
| 07 | Seed Sample Reports | Add demo data |
| 08 | Azure Deployment | Deploy to production |
| 09 | Troubleshooting (Optional) | Fix build issues |
| 10 | Verify Production | Test all features |

## Key Learnings to Highlight

- **sql.js over better-sqlite3**: Pure JavaScript works everywhere
- **Build automation**: Must enable for Azure deployments
- **.deployment files**: Remove them to allow Oryx builds
- **Vanilla JS**: Simple and effective for SPAs
- **Environment variables**: Never hardcode secrets

## Demo Tips

- Have your Azure credentials ready
- Prepare Power BI workspace/report IDs in advance
- Show the Kudu logs to demonstrate build process
- Emphasize the deployment pitfalls and how to avoid them
- Demonstrate both admin and regular user experiences

## Time Estimate

- Full demo: 45-60 minutes
- Without deployment: 30-40 minutes
- Just core features (01-05): 20-25 minutes
