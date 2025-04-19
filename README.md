# pricing-engine
This repository contains a pricing engine that automatically adjusts product prices based on current inventory levels and recent sales performance. 

### Pricing Rules

1. **Rule 1 – Low Stock, High Demand (Highest Priority):**
    - **Condition:** If `stock < 20` **and** `quantity_sold > 30`.
    - **Action:** Increase the current price by 15%.
2. **Rule 2 – Dead Stock (Second Priority):**
    - **Condition:** If `stock > 200` **and** `quantity_sold == 0`.
    - **Action:** Decrease the current price by 30%.
3. **Rule 3 – Overstocked Inventory (Third Priority):**
    - **Condition:** If `stock > 100` **and** `quantity_sold < 20`.
    - **Action:** Decrease the current price by 10%.
4. **Rule 4 – Minimum Profit Constraint (Always Applied Last):**
    - **Condition:** Ensure that the computed new price is at least 20% above the `cost_price`.
        - If the computed price is below `cost_price * 1.2`, reset the new price to `cost_price * 1.2`.
    - **Action:** Finalize the price, rounding it to 2 decimal places.

## Approach
1. **Read input files**: `products.csv` and `sales.csv` using `pandas`.
2. **Merge datasets**: Combine product info and sales data using SKU as key.
3. **Apply pricing rules**: A function processes each product row by row based on defined conditions.
4. **Format final prices**: Rounded to 2 decimals and prefixed with `₹`.
5. **Export results**: Save updated data as `updated_prices.csv`.
