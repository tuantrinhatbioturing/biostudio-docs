# Catalogs

Use the **Catalogs** panel to organize and discover workspace data files.
All actions are permission-gated.

## Before you start

- Open the target workspace.
- Click **Catalogs** in the left sidebar.
- Ensure your account has catalog access permission.

If permission is missing, actions are hidden, disabled, or blocked.

## General

The **Catalogs** area contains:
- a search input,
- a data source selector,
- catalog file rows with label chips,
- row action menu (**Overview**, **Edit**, **Copy path**, **Delete**),
- filter controls and panel display controls.

## Filter by data source

Use this flow to limit results by source (for example `Core`, `Cloud storage`).

1. Open **Catalogs**.
2. Click the source selector near the search box.
3. Choose the target source.

Expected behavior:
- Only catalog entries from the selected source are shown.
- Source switch updates the list immediately.
- Current source selection remains visible in the selector.

## Collapse/Expand catalog labels

Use this flow to control label visibility on each catalog row.

1. Open **Catalogs** with files that have multiple labels.
2. Click **View more labels** to expand hidden labels.
3. Click the collapse control to reduce label display.

Expected behavior:
- Expanded state reveals all labels for that row.
- Collapsed state shows summary labels only.
- Toggling labels does not change file data or label assignments.

## Advanced filter

Use this flow to build multi-condition filters for catalog discovery.

1. Open **Catalogs**.
2. Open **Advanced filter**.
3. Add one or more conditions.
4. Choose field, operator, and value for each condition.
5. Combine conditions with logical operators (**AND**/**OR**).
6. Add nested or additional filter rules if needed.

Expected behavior:
- Filtered results update based on configured logic.
- Multiple conditions are evaluated in configured order/grouping.
- Empty or invalid rules are ignored or blocked with clear feedback.

## Open catalog panel in full screen

Use this flow to focus on catalog browsing.

1. Open **Catalogs**.
2. Click the panel expand/full-screen control.

Expected behavior:
- Catalog panel expands to full-screen catalog view.
- File list shows larger working area for browsing and filtering.
- User can return to the normal split layout from the same control.

## Copy path

Use this flow to copy a catalog file path.

1. Open **Catalogs**.
2. On target row, open **More** menu.
3. Select **Copy path**.

Expected behavior:
- The selected file path is copied to clipboard.
- Success feedback is shown (toast or equivalent).

## Manage catalogs

### Overview

Use this flow to inspect catalog metadata in read-only form.

1. Open **Catalogs**.
2. On target row, open **More** menu.
3. Select **Overview**.

Expected behavior:
- A detail modal/panel shows catalog information (name/path, labels, metadata).
- Overview does not change catalog data.

### Edit

Use this flow to update catalog information.

1. Open **Catalogs**.
2. On target row, open **More** menu.
3. Select **Edit**.
4. Update editable fields.
5. Click **Save**.

Expected behavior:
- Updated catalog data appears immediately after save.
- Validation prevents invalid/empty required fields.
- If edit permission is missing, **Edit** is hidden or disabled.

### Delete

Deleting a catalog is a destructive action.

1. Open **Catalogs**.
2. On target row, open **More** menu.
3. Select **Delete**.
4. Review warning in the confirmation dialog.
5. Confirm deletion.

Expected behavior:
- Catalog item is removed from the list after confirmation.
- Destructive warning is shown before final action.
- If delete permission is missing, **Delete** is hidden or disabled.

## Label-based organization

Catalog files are managed through a label system.
When a data file is assigned catalog labels, the system treats that file as part of Catalogs.

Purpose:
- Help users find data faster.
- Group related files with consistent labels.
- Improve discoverability at workspace scale.

Expected behavior:
- Labeled files appear in Catalogs according to assigned labels.
- Updating labels updates grouping and discovery behavior.
- Unlabeled files are not treated as catalog files.

## Permission behavior reference

Apply this rule to all Catalog actions:

- permission granted: action is available,
- permission missing: action is hidden, disabled, or blocked with clear feedback.

This should be consistent across view, filter, copy path, edit, and delete flows.

#bioturing #biostudio #catalogs #workspace #permission
