# Power Automate Collector Flow

Use this collector when the Maker/Admin app list shows apps that the same-environment Dataverse inventory does not return. This is common in Default environments with many personal productivity canvas apps.

The packaged Solution Service Inspector solution includes a cloud flow named **Solution Service Inspector - Admin Inventory Export**. The flow produces a JSON file that Solution Service Inspector can import with **Inspect = Power Automate collector JSON**.

Use this file if you need to understand or recreate the flow manually.

## Connector actions

Use these admin connector actions:

| Connector | Action | Purpose |
|---|---|---|
| Power Apps for Admins | Get Apps as Admin | Lists Power Apps visible to the admin connector |
| Power Apps for Admins | Get App Role Assignments as Admin | Optional, gets app sharing/role assignments |
| Power Automate Management | List Flows as Admin (V2) | Lists flows visible to the admin connector |
| Power Automate Management | Get Flow as Admin | Optional, gets richer flow definition/connection metadata |

## Flow outline

1. Import the Solution Service Inspector solution package.
2. During import, create/select connections for **Power Apps for Admins**, **Power Automate Management**, and **SharePoint**.
3. After import, open the flow named **Solution Service Inspector - Admin Inventory Export**.
4. Turn the flow on.
5. Run the flow manually.
6. Provide:
   - `EnvironmentName`: the target environment name/ID.
   - `OutputSiteUrl`: the SharePoint site where the JSON file should be created.
   - `OutputFolderPath`: the folder path, for example `/Shared Documents`.
   - `IncludeFlowDefinitions`: optional; use only when you need richer flow dependency details because it calls **Get Flow as Admin** once per flow.
7. Download the generated `power-platform-admin-inventory-*.json` file.
8. Load it in Solution Service Inspector with **Inspect = Power Automate collector JSON**.

## Manual build outline

If you need to recreate the packaged flow manually:

1. Create an instant cloud flow.
2. Add manual trigger inputs named `EnvironmentName`, `OutputSiteUrl`, `OutputFolderPath`, and `IncludeFlowDefinitions`.
3. Initialize a string variable named `EnvironmentName` from the trigger input.
4. Initialize an array variable named `FlowDetails` to `[]`.
5. Add **Get Apps as Admin**.
6. Add **List Flows as Admin (V2)**.
7. Turn on pagination in both list actions and set a threshold above the expected app/flow count.
8. Optional: for each listed flow, call **Get Flow as Admin** with **Include Flow Definition = Yes**, then append the body to `FlowDetails`.
9. Compose a JSON object with `EnvironmentName`, `PowerApps`, and `Flows`.
10. Create a `.json` file in OneDrive or SharePoint.
11. Load that file in Solution Service Inspector.

## Expected JSON shape

```json
{
  "EnvironmentName": "Default-00000000-0000-0000-0000-000000000000",
  "PowerApps": [],
  "Flows": []
}
```

`PowerApps` should contain the items from **Get Apps as Admin**. `Flows` should contain either **List Flows as Admin (V2)** rows or the richer **Get Flow as Admin** rows.

## Notes

- This route does not require PowerShell.
- The flow must run with a connection that has enough Power Platform admin privileges to list the target environment's apps and flows.
- The imported JSON gives broader Admin Center coverage, but it still does not prove solution package membership unless that data is included in the export.
