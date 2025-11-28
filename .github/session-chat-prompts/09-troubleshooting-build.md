# Prompt 09: Troubleshooting Build Issues (Optional)

## User Request

The deployment succeeded but I'm getting MODULE_NOT_FOUND errors. It seems like npm install isn't running.

## Expected Outcome

- Identify that build automation wasn't enabled
- Enable SCM_DO_BUILD_DURING_DEPLOYMENT and ENABLE_ORYX_BUILD
- Verify .deployment file doesn't exist (or remove it)
- Redeploy application
- Confirm npm install runs in Kudu logs
- Application starts successfully

## Common Issues

1. .deployment file blocking Oryx build
2. Build automation disabled
3. Wrong startup command
4. Native modules (better-sqlite3) failing to compile

## Solutions

- Remove any .deployment file
- Enable build settings
- Use sql.js instead of better-sqlite3
- Check Kudu deployment logs for "npm install" execution
