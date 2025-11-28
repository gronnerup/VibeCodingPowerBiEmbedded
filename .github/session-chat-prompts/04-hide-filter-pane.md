# Prompt 04: Hide Filter Pane

## User Request

When embedding the reports, hide the filter pane on the left-hand side of the report view.

## Expected Outcome

- Power BI embed configuration updated
- filterPaneEnabled set to false
- Clean report view without filters panel
- All other functionality remains intact

## Technical Detail

Modify the embed settings to include:
```javascript
settings: {
    panes: {
        filters: {
            visible: false
        }
    }
}
```
