# Business Unit Configuration

The Business Unit Configuration HTML web resource provides a filtered, sortable user list and a controlled batch move operation.

## Features

- Filter users by business unit, enabled/disabled status, name, email, domain, manager, employee ID, job title, title, and location.
- Choose which columns appear in the table from the **Columns** picker. The selection is remembered per browser.
- Available columns: Name, Business unit, Manager, Job title, Title, Employee ID, Location, Street, Postal code, Email, Domain, and Status. Every column is sortable.
- Select multiple users and preview the destination business unit and record reassignment principal before making changes.
- Move users with Dataverse's supported `SetBusinessSystemUser` action.
- Require a reassignment option for records owned by each moved user, including keeping ownership with each selected user.
- Optionally clone direct roles and owner-team memberships from a selected source user after the move.
- Report per-user success or failure instead of hiding partial batch failures.
- Create a new business unit under a chosen parent without leaving the page. The new unit is selected as the destination automatically.
- Search across manager, employee ID, location, job title, title, domain, email, and business unit fields to identify user groups.

## Important behavior

Moving a user between business units can affect ownership and security. The tool requires explicit confirmation and does not silently remove existing permissions. Permission cloning adds matching assignments; it does not manage Microsoft Entra group membership.

Dataverse requires a reassignment option for records owned by a user being moved. The tool can keep ownership with each selected user, or reassign records to a selected user or owner team. Disabled users are shown for review but are not selected automatically. Service accounts whose names begin with `#` are excluded from the user list and user selectors.

Manager, employee ID, and address columns read `parentsystemuserid`, `employeeid`, and the `address1_*` fields on the user record. Dataverse does not synchronize these from Microsoft Entra ID, so they are blank unless your organization populates them.

Use the [Dataverse HTML Tools Suite](../dataverse-html-tools-suite/README.md) for the complete app. Use this individual solution only for a partial deployment.

## Build

Build `solution/DataverseHtmlToolsBusinessUnitConfiguration.cdsproj` in Release configuration to produce managed and unmanaged solution ZIPs.