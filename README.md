# Retail vs Online Shopping in Canada, 2017–2025 (Power BI)

**E-commerce nearly tripled, but stores still win 93% of sales.**

![Online Shopping Trend](images/page 1.png)

## The question
How much of Canada's shopping happens online, how fast is it growing, and how does it compare with shopping in stores?

## The data
- **Source:** Statistics Canada, Table 20-10-0056 (Monthly retail trade sales by province and territory)
- **Period:** January 2017 to August 2026 (about 81,000 rows)
- **Note:** 2025 is used as the latest full year, because 2026 only runs to August.

## How I built it
1. **Cleaned the data in Power Query:** kept unadjusted figures; filtered to the regions and store types needed (Canada, the 13 provinces and territories, total retail, and the 9 store types); removed nulls; set date types; converted values from thousands to dollars; removed category codes such as [441]; renamed columns.
2. **Built a data model:** a Calendar date table joined one-to-many to the sales table.
3. **Wrote DAX measures**, including:
   ```
   Total Retail Sales = CALCULATE(SUM(Retail_Sales[Sales]), Retail_Sales[SalesType] = "Total retail sales")
   E-commerce Sales   = CALCULATE(SUM(Retail_Sales[Sales]), Retail_Sales[SalesType] = "Retail e-commerce sales")
   Online Share %     = DIVIDE([E-commerce Sales], [Total Retail Sales])
   E-commerce LY      = CALCULATE([E-commerce Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))
   E-commerce YoY %   = DIVIDE([E-commerce Sales] - [E-commerce LY], [E-commerce LY])
   In-store Sales     = [Total Retail Sales] - [E-commerce Sales]
   ```
4. **Added share measures** for the KPI cards, such as each province's and store type's share of total sales.
5. **Designed 3 pages** with a shared header, page navigation buttons, KPI cards, and a year slicer.

## Key findings
- **Online share nearly tripled,** from **2.6% in 2017** to **7.0% in 2025**.
- **Stores still dominate:** from 2017 to 2025, Canadians spent **$6.5 trillion** in retail, and **$347 billion** of it was online.
- **Online shopping spikes every November and December.** November and December average about 6.5% online, compared with about 4.7% in July and August.
- **E-commerce grew 75% in 2020,** dipped 9% in 2022, then rebounded 28% in 2024.
- **Car dealers are the biggest store type:** $229B in 2025, or 27% of all retail sales.
- **Ontario made up 38%** of Canada's 2025 retail sales, and the top 4 provinces (ON, QC, BC, AB) made up 86%.

## Dashboard pages
| Page | What it shows |
|---|---|
| Online Shopping Trend | KPI cards, online share by month, in-store vs online sales by year, e-commerce growth by year |
| Store Types | KPI cards and sales by type of store, with a year slicer |
| Provinces | KPI cards and sales by province, with a year slicer |

![Store Types](images/page 2.png)
![Provinces](images/page 3.png)

## Limitations
- E-commerce figures are only published for Canada as a whole, so online share can't be split by province or store type.
- I used figures that are not seasonally adjusted, so the real holiday spikes show up. This also means month-to-month changes include normal seasonal ups and downs.
- 2026 data only runs to August, so yearly comparisons stop at 2025.

## Files
- `Canada Online Shopping Boom.pbix` – the Power BI file (download and open in Power BI Desktop)
- `images/` – dashboard screenshots

