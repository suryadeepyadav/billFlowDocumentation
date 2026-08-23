# Items and Inventory

## What Is the Inventory Area?

The Inventory area contains:

- Items & Services master
- Categories and Units
- Stock summary
- Stock movement history
- Manual stock adjustments
- Automatic stock effects from purchases, invoices, and site materials

## Important Terms

- **Stock item**: A physical item whose quantity is tracked.
- **Service**: A chargeable or purchasable service with no stock quantity.
- **Warehouse stock**: Quantity held centrally, where Site is blank on the stock ledger.
- **Site stock**: Quantity assigned directly to one or more sites.
- **Total stock**: Warehouse stock plus all site stock.
- **Minimum stock**: Warehouse threshold used for the Reorder/Low Stock indicator.
- **Stock movement**: Immutable IN or OUT ledger entry explaining a quantity change.
- **Opening stock**: Starting warehouse quantity recorded when a stock item is created.

## Items & Services

### Why Is It Used?

Selecting an item in a quotation, invoice, purchase, or material form fills the name, description, unit, rate, and tax defaults. Stock items also create stock movements when posted in stock-affecting documents.

### Item Fields

| Field | Required | What to enter | Effect |
| --- | --- | --- | --- |
| Item name | Yes | Clear product/service name | Copied into document line snapshots |
| Item code | No | Unique internal/SKU code | Normalized to uppercase; useful for search |
| Item type | Yes | STOCK or SERVICE | Determines whether transactions affect quantity |
| Category | No | Existing category | Organizational grouping; can be quick-created |
| Unit | No | Existing unit | Copied to transaction lines; can be quick-created |
| HSN / SAC | No | HSN for goods or SAC for services | Tax/document reference; normalized to uppercase |
| Tax rate (%) | No; defaults to 0 | Total GST percentage from 0 to 100 | Pre-fills transaction lines |
| Purchase rate | No; defaults to 0 | Normal unit cost | Pre-fills purchase and material/adjustment rate |
| Sale rate | No; defaults to 0 | Normal unit selling price | Pre-fills quotation and invoice rate |
| Opening stock | Conditional; STOCK only, defaults to 0 | Verified starting warehouse quantity | Creates an Opening Balance movement when positive |
| Minimum stock | Conditional; STOCK only, defaults to 0 | Warehouse reorder threshold | Drives Reorder/Low Stock status |
| Description | No | Item/service details | Copied to selected document lines |
| Active | No; defaults on | Whether available for new transactions | Historical snapshots remain when inactive |

Every numeric item field must be zero or positive.

### Stock Item Versus Service

Choose **STOCK** only for physical goods that should change quantity. Choose **SERVICE** for labour, installation, transport, consultation, or other non-stock charges.

Important behavior:

- A selected STOCK item in a purchase creates stock IN.
- A selected STOCK item in an invoice creates warehouse stock OUT.
- A selected SERVICE item changes document value but not quantity.
- A free-text document line without a valid item master is treated as a service and does not change stock.
- A quotation never changes stock, even when it contains stock items.

### Opening Stock Safety

Opening stock is intended only for the starting quantity when the item is first configured. Once any stock movement exists, BillFlow blocks changing Opening stock or Item type. Use a Stock Adjustment for corrections.

This prevents the opening value from silently changing underneath an existing movement history.

## Stock Summary

Open **Inventory > Stock Control > Stock summary**.

| Column | Meaning |
| --- | --- |
| Item | Item name plus code/HSN reference |
| Warehouse | Quantity centrally available |
| At sites | Combined quantity currently assigned to sites |
| Total | Warehouse plus site quantity |
| Minimum | Configured warehouse threshold |
| Availability | Available or Reorder based on Warehouse quantity versus Minimum |

Turn on **Low stock only** to show active stock items whose warehouse quantity is less than or equal to Minimum stock.

The low-stock calculation uses warehouse quantity, not total quantity. Material at a site is not assumed to be immediately available in the warehouse.

## Movement History

Open **Stock Control > Movement history** to trace every stock change.

| Column | Meaning |
| --- | --- |
| Date | Effective movement date |
| Item | Stock item and code |
| Location | Warehouse or a specific site |
| Movement | Source/reversal type |
| Direction | IN adds quantity; OUT removes quantity |
| Quantity | Quantity changed |
| Rate | Value rate used by the movement |
| Value | Quantity value associated with the movement |
| Reference | Source document number and narration |

### Movement Types

| Type | What caused it |
| --- | --- |
| OPENING_BALANCE | Positive Opening stock on item creation |
| PURCHASE_IN | Posted purchase of a stock item |
| PURCHASE_REVERSAL | Cancellation of that purchase |
| SALE_OUT | Posted invoice containing a stock item |
| SALE_REVERSAL | Cancellation of that invoice |
| ADJUSTMENT_IN | Manual increase |
| ADJUSTMENT_OUT | Manual decrease |
| SITE_ISSUE | Warehouse-to-site material issue pair |
| SITE_RETURN | Site-to-warehouse return pair |
| SITE_ISSUE_REVERSAL | Cancellation of an issue |
| SITE_RETURN_REVERSAL | Cancellation of a return |

Movements are ledger history and cannot be edited directly.

## Post a Stock Adjustment

Use an adjustment for physical count corrections, damage, found stock, migration corrections after setup, or other non-document movements.

### Adjustment Fields

| Field | Required | What to enter |
| --- | --- | --- |
| Stock item | Yes | Active STOCK item; a missing item can be quick-created |
| Direction | Yes | Add stock (IN) or Remove stock (OUT) |
| Quantity | Yes | Positive quantity, minimum 0.001 |
| Unit rate | Yes | Zero or positive valuation rate |
| Adjustment date | Yes | Effective date of correction |
| Reason / notes | No, but strongly recommended | Physical count, damage, migration, or other reason |

Select **Post adjustment** to create the movement.

An OUT adjustment is rejected if warehouse stock is insufficient. Adjustments affect warehouse stock only; use Site Materials for warehouse/site transfers.

## Automatic Stock Effects

### Purchase

- Site left empty: stock item quantity enters the warehouse.
- Site selected: stock item quantity is received directly at that site.
- Service lines do not affect stock.
- Cancelling the purchase posts an OUT reversal from the original location.
- Cancellation can fail if the original received stock is no longer available to reverse.

### Sales Invoice

- Selected stock item quantity leaves the warehouse.
- BillFlow requires sufficient warehouse stock before posting.
- A linked Site on an invoice is a financial/project link; invoice stock still comes from warehouse in the current implementation.
- Cancelling an unpaid invoice posts stock back into the warehouse.

### Site Materials

- Issue: OUT from warehouse and IN to the site.
- Return: OUT from site and IN to warehouse.
- Cancellation posts the opposite paired movements.
- BillFlow verifies stock at the source location.

See [Site Management](09-site-management.md) for material fields and cancellation.

## Stock and Document Values

Stock quantity and document money are related but separate:

- Purchase/invoice stock movement value uses the line taxable value.
- Site materials and adjustments use the entered unit rate.
- Inventory summary focuses on quantity; Site Costing uses relevant transaction values.
- GST is not itself stock value in these movements.

## Deactivation and Historical Stock

Deactivating an item removes it from new transaction selections. Existing stock movements and document snapshots remain. Before deactivating a stock item, review whether it still has warehouse or site quantity and decide how the business wants to handle that balance.

## Common Mistakes

- Creating labour as STOCK instead of SERVICE.
- Typing a stock item as free text, then expecting quantity to change.
- Using Opening stock for later corrections instead of an adjustment.
- Setting Minimum stock based on total site stock rather than warehouse reorder needs.
- Cancelling a purchase after its stock was consumed, which makes reversal impossible.
- Issuing material to a site when warehouse stock is insufficient.
- Returning more material than the site currently holds.

## Recommended Stock Control Routine

1. Review Low stock only each morning or before procurement.
2. Post purchases at the correct location.
3. Issue site material through Site Materials, not manual adjustments.
4. Use Movement history to investigate differences.
5. Post count corrections with a clear reason.
6. Export the Stock or Stock Movements report for period review.

Related reporting is explained in [Dashboard, Reports, Printing, and Exports](14-dashboard-reports-printing-and-exports.md).
