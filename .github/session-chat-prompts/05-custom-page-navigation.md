# Prompt 05: Custom Page Navigation

## User Request

Now hide the pages (tabs at the bottom of the report when embedded). Instead, list the report pages in a left-hand side menu in a very neat and clean layout.

## Expected Outcome

- Page tabs at bottom of report hidden
- Custom sidebar on the left showing all report pages
- Sidebar styled with brown/green theme
- Clicking a page navigates to that page
- Active page highlighted
- Clean, professional appearance

## Technical Details

- Hide page navigation: `navContentPaneEnabled: false`
- Use `report.getPages()` to retrieve page list
- Use `page.setActive()` to switch pages
- Create custom sidebar with CSS styling
