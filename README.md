# OM 620 — Assignments (Brenda Raquel Laime Jalil)

**Class:** OM 620 — Tools & Technologies for Analytics  
**Student:** Brenda Raquel Laime Jalil  
**Repo:** `om620-assignments`

This repository is my working showcase for **Assignment 1** (data cleaning & exploration) and **Assignment 2** (safety stock analysis) using our group’s transactional dataset.

---

## What’s here
- `data/transaction_data.csv` — group dataset used in A1 & A2  
- `notebooks/om620_a1_a2.ipynb` — **single combined notebook** (A1 + A2, with my commentary)  

---

## Dataset (short overview)
Transactional records of finished goods (mixed inventory types). For Milestone work I focus on **Make-to-Stock (MTS)** finished goods to prepare the **safety stock** analysis.

- Key fields used: `sku_number`, `order_quantity`, `lead_time`, `inventory_type`, `division`, `site_id`, (others as needed)

---

## Assignment 1 — Data cleaning & exploration (highlights)

**Goals**
- Standardize column names and fix inconsistencies.  
- Inspect numeric fields with `describe()`; note and correct oddities.  
- Handle **NaN** values by column (with rationale).  
- Filter to **finished goods** AND **MTS** inventory for downstream analysis.  
- Answer “useful info” questions on the filtered data.

**My actions**
- Renamed columns to a single convention (lowercase + underscores).  
- Investigated outliers & weird values via `describe()` and targeted checks.  
- Addressed missingness with column-specific strategies:
  - e.g., imputed `lead_time` using group medians by SKU/site when justified.  
- Filtered `finished goods` + `MTS` to create my analysis frame: `fg_mts`.

**Quick answers (from my notebook)**
- Top/bottom 10 by order quantity: shown in notebook  
- Top/bottom 10 by **total sales** (computed), shown in notebook

---

## Assignment 2 — Safety stock & distribution (highlights)

**Background**  
Safety stock for MTS accounts for demand variability and lead time. I computed:
- **Parametric formula** (Normal assumption):  
  \[
  SS = z_\alpha \cdot \sigma_{\text{demand}} \cdot \sqrt{\text{lead\_time}}
  \]
- **Empirical (non-parametric) quantile** (side quest) using the observed demand distribution.

**What I built**
- Aggregated stats per SKU: **min, max, mean, median, variance, std of demand** + **avg lead time**.  
- Safety stock at **75%**, **90%**, **95%** service levels (z-scores).  
- Empirical/quantile-based safety stock (e.g., 95th percentile × √avg_lead_time).

**Takeaways**
- The parametric formula is efficient but **sensitive to non-normal demand**.  
- The empirical method is robust for skew/heavy-tail SKUs.  
- Operationally, select service level by **stockout tolerance** and **cash constraints**.

---

## How to run
1. Place your dataset in `data/transaction_data.csv`.  
2. Open `notebooks/om620_a1_a2.ipynb`.  
3. Run cells top-to-bottom (the notebook reads `data/transaction_data.csv`).  

**Dependencies**: `pandas`, `numpy`, `scipy`, `matplotlib` (optional), `jupyter`.

---

## References
- Course PDFs & lectures (OM 620).  
- SciPy `stats` (ppf / z-scores).  
- Standard inventory control references on safety stock.

---

© 2025 Brenda Raquel Laime Jalil
