# 📊 Sales KPI Dashboard

This project is a **Sales KPI Dashboard** built in **Power BI**, designed to monitor performance against sales targets using dynamic visuals and calculated metrics. The dashboard presents both high-level and detailed views of key indicators such as actual sales, targets, variances, and YTD performance, along with employee-wise insights.

---

## 🚀 Features

- **Key Metrics Tracked**:
  - Total Sales Actual
  - Total Sales Target
  - Variance & Variance %
  - YTD Sales Actual
  - YTD Sales Target
  - YTD Variance & YTD Variance %

- **Visualizations**:
  - Clustered Column Chart for Actual vs Target
  - **Team Slicer**: Allows filtering the dashboard by one of four sales teams to view team-specific performance
  - Employee-wise performance table with:
    - Actual
    - Target
    - Variance %
    - Trendline (Sparkline)

---

## 🧮 DAX Measures Used

```DAX
Target Status = IF([Variance] > 0, 1, -1)

Total Sales Actual = SUM(Actual[Sales])

Total Sales Target = SUM(Targets[Sales])

Variance = [Total Sales Actual] - [Total Sales Target]

Variance % = DIVIDE([Variance], [Total Sales Target])

Variance Label = 
    VAR up = "✅"
    VAR down = "❌"
    VAR formatted_var_pct = FORMAT(ABS([Variance %]), "0.0%")
    RETURN formatted_var_pct & " " & IF([Variance %] > 0, up, down)

YTD Sales Actual = CALCULATE([Total Sales Actual], DATESYTD('Calendar'[Date]))

YTD Sales Target = CALCULATE([Total Sales Target], DATESYTD('Calendar'[Date]))

YTD Variance = [YTD Sales Target] - [YTD Sales Actual]

YTD Variance % = DIVIDE([YTD Variance], [YTD Sales Target])
