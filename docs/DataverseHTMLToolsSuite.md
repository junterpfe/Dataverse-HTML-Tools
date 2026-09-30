# Dataverse HTML Tools Suite

The Suite is the single installable option for the complete admin-tool set. It contains the `Admin Tools` model-driven app and all eight HTML web resources.

## Admin Tools app

The app provides the default Team and User list views. It intentionally does not replace them with custom views.

Opening a Team record uses only the `Admin Tools Team` form. That form keeps the standard Team tabs and adds the `Team Role and People Manager` tab.

Opening a User record uses only the `Admin Tools User` form. That form keeps the standard User tabs and adds `Effective Security Roles` and `User Record Access` tabs.

The app also contains standalone navigation pages for Flow Dependency Viewer, Role Table Permission Copier, and Solution Service Inspector.

The app also includes Connection Health Audit. It loads saved audit runs, can start a new collector run, reports connection health, and analyzes connection references across visible solutions. The reference analyzer groups references by connector, preserves bound connections and account identities where available, and flags same-connector references as consolidation candidates.

## Install

Choose the managed or unmanaged archive in [`packages/dataverse-html-tools-suite`](../packages/dataverse-html-tools-suite). Import it into a Dataverse environment, publish customizations if prompted, and give administrators access to the `Admin Tools` model-driven app.

The Suite does not grant privileges. Each web resource runs under the signed-in user's Dataverse security context.