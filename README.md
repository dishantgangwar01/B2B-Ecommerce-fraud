# B2B-Ecommerce-fraud

---

#  B2B Ecommerce Fraud: Courier Charges Accuracy Analysis

## Problem Overview

ABC Company operates a B2B e-commerce platform handling thousands of orders daily. To ensure efficient deliveries, they partner with multiple courier companies.  
However, discrepancies were observed between **expected courier charges** and **actual billed amounts**.

The goal of this project is to **analyze** and **verify** the courier charges to detect:

- Orders correctly charged
- Orders overcharged
- Orders undercharged

This helps identify fraud, billing errors, and optimize operational costs.

---

## Datasets

The following datasets are used:

| Dataset Name               | Description |
|-----------------------------|-------------|
| Website Order Report        | Order IDs and SKUs for each order |
| SKU Master                  | Gross weight details for each SKU |
| Warehouse PIN Mapping       | Mapping of Warehouse PIN to Delivery PINs |
| Courier Company Invoice     | AWB Number, Order ID, Courier Weight, Delivery Zone, Charges |
| Courier Rate Card           | Base Fee and Additional Charges per weight slab and delivery area |

---

## Objective

✅ Calculate the **expected weight** and **expected charges** per order using ABC's internal data.  
✅ Compare them with the **courier company’s invoice**.  
✅ Identify **overcharged**, **undercharged**, and **correctly charged** orders.  
✅ Generate detailed and summary reports.

---

## Final Output Tables

### 1. Detailed Order Table

| Column Name | Description |
|:------------|:------------|
| Order ID | Order number |
| Total Weight | Total weight calculated from SKUs |
| Weight Slab | Weight rounded up to nearest 0.5 kg |
| Delivery Zone (ABC) | Zone determined from PIN codes |
| Expected Charge (Rs.) | Calculated courier charge |
| AWB Number | Courier’s tracking number |
| Weight as per Courier (KG) | Courier-reported weight |
| Delivery Zone (Courier) | Courier-reported delivery zone |
| Billing Amount (Rs.) | Courier-billed amount |
| Weight Slab (Courier) | Courier-reported weight slab |

---

### 2. Summary Table

| Description | Count | Amount (Rs.) |
|:------------|:------|:------------|
| Total Orders Correctly Charged | - | - |
| Total Orders Overcharged | - | - |
| Total Orders Undercharged | - | - |

---

## Project Steps

1. Load and clean all datasets.
2. Merge Website Order Report with SKU Master to calculate total weight per order.
3. Round total weight to the nearest 0.5 kg to form a weight slab.
4. Determine delivery zones using PIN code mappings.
5. Calculate the expected courier charge using the Rate Card (base + additional slab charges).
6. Compare expected weight/charges vs courier invoice data.
7. Identify overcharge, undercharge, and correct charge cases.
8. Generate final reports.

---

## Requirements

- Python 3.8+
- pandas
- numpy


You can install the requirements using:

```bash
pip install pandas numpy
```

---

## Example Python Code

Here’s a sample code snippet to **calculate the weight slab** for an order:

```python
import pandas as pd
import numpy as np

# Function to round weight to the nearest 0.5 kg
def round_up_weight(weight):
    return np.ceil(weight * 2) / 2

# Sample DataFrame
orders_df = pd.DataFrame({
    'Order ID': [2001827036, 2001821995],
    'Total Weight (KG)': [2.3, 3.7]
})

# Apply the rounding function
orders_df['Weight Slab (KG)'] = orders_df['Total Weight (KG)'].apply(round_up_weight)

print(orders_df)
```

**Output:**

```
     Order ID  Total Weight (KG)  Weight Slab (KG)
0  2001827036                2.3              2.5
1  2001821995                3.7              4.0
```

---

## Deliverables

- 📄 Detailed Order Accuracy Report (CSV/Excel)
- 📈 Summary Accuracy Report
- 📊 Visualizations (optional: bar plots for overcharged/undercharged orders)

---

## Notes

- Weight rounding is crucial for billing calculations.
- Delivery zones must match based on PIN code mapping.
- Rate cards vary based on delivery zone and weight slabs.
- Any discrepancy is important for business revenue protection.

---

## Author

Dishant Gangwar.

---

---
