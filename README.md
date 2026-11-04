
# Sales Analysis Dashboard: Time Intelligence in Power BI

### Tracking Year-to-Date, Month-over-Month and Quarter-over-Quarter performance with DAX

A Power BI dashboard that turns raw sales transactions into time-based performance metrics, built on Microsoft's AdventureWorksDW sample data warehouse. It answers the questions a sales manager asks every week: how are we doing so far this year, how does this month compare with last month, and which markets are most profitable?


## Why time intelligence matters

Cumulative sales totals hide how performance changes over time. Time-intelligence metrics show growth, seasonality and short-term swings that a single total cannot:

- **Year-to-Date (YTD):** cumulative sales from the start of the year to a given date
- **Month-over-Month (MoM):** percentage change in sales between consecutive months
- **Quarter-over-Quarter (QoQ):** percentage change in sales between consecutive quarters

## What is in the dashboard

One report page, **Sales Forecast Dashboard**, with a country slicer that filters every visual:

| Visual | What it shows |
|---|---|
| Title banner | "Sales Trend 2011 - 2014" |
| Country slicer | Filter the whole page by country |
| 7 KPI cards | Total Sales, Total Cost, Profit, Profit Margin %, YTD Sales, MoM Change %, QoQ Change % |
| Line chart | Total Sales by year, with drill-down to quarter, month and day |
| Stacked area chart | YTD Sales by year, with drill-down to quarter and month |
| Clustered column chart | Total Sales, Total Cost and Profit side by side over time |
| Combo chart | Profit (columns) with Profit Margin % (line) by year |
| Donut chart | Split of Total Cost and Profit |

## Data and model

**Source:** [AdventureWorksDW2022](https://github.com/microsoft/sql-server-samples), a sample data warehouse published by Microsoft. It is fictional data for a bicycle manufacturer and is free to use under the repository's licence.

**Tables used:**

| Table | Role |
|---|---|
| `FactInternetSales` | Transactions: order date, sales amount, tax, product cost |
| `DimDate` | Calendar table, essential for DAX time-intelligence functions |
| `DimProduct` | Product-level slicing and filtering |
| `DimCustomer` | Customer segmentation (for example by age group) |
| `DimGeography` | Country and regional analysis |

A separate measures table holds the calculations below.

## Measures (DAX)

```dax
Total Sales = SUM(FactInternetSales[SalesAmount])

YTD Sales = TOTALYTD([Total Sales], DimDate[FullDateAlternateKey])

MoM Change % = DIVIDE([Total Sales] - [Previous Month Sales], [Previous Month Sales])
```

The report also defines `Total Cost`, `Profit`, `Profit Margin %`, `Previous Month Sales` and `QoQ Change %`, which can be read in the `.pbix` file.

`DIVIDE` returns blank instead of an error when the previous period is zero, and `TOTALYTD` resets automatically each year.

## Results



## Opening it

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows).
2. Open `Sales_Trend.pbix`.

To rebuild it from the source, restore `AdventureWorksDW2022.bak` in SQL Server, then connect Power BI to the five tables listed above and recreate the measures.


## Author

**Yaw Asante** - Data Scientist, Statistician and Financial Economist

Email: vkpoasante@gmail.com

## Licence

**MIT**
