# Construction Analytics Dashboard — Power BI

A 4-page interactive business intelligence dashboard analysing 
a synthetic dataset that contains 300-project Australian construction portfolio worth $14.3bn AUD. 
Built to demonstrate end-to-end Power BI development including 
data modelling, DAX measures, and business reporting for the 
construction industry.

---

## Dashboard Pages

### Page 1 — Portfolio Overview
![Portfolio Overview](Construction%20Analytics/Portfolio%20Overview.png)

Executive summary of the full construction portfolio:
- 300 projects across 5 Australian states (SA, NSW, VIC, QLD, WA)
- $14.3bn total budget with 7.05% average cost overrun
- 53 projects currently delayed (17.67% of portfolio)
- Interactive State slicer filters all visuals simultaneously
- Project status breakdown and budget distribution by project type

### Page 2 — Cost & Budget Analysis
![Cost & Budget](Construction%20Analytics/Cost%20%26%20Budget.png)

Deep dive into portfolio financials:
- Monthly budget vs actual spend trend across the full year
- $967M total cost variance across the portfolio
- Spend breakdown by category: Labour, Materials, Equipment, 
  Subcontractors, Preliminaries, Contingency
- Cost overrun ranking by project type — Commercial Office 
  highest at 12.08%
- Budget vs actual comparison across all 12 project types

### Page 3 — Timeline & Delays
![Timeline & Delays](Construction%20Analytics/Timeline%20%26%20Delays.png)

Analysis of project delays and milestone performance:
- 21.11 average delay days across the portfolio
- Permit Delays and Scope Change identified as #1 and #2 
  delay causes
- 55.68% of milestones Complete, 15.66% At Risk
- Infrastructure - Road projects have longest average delays
- 56.33% on-time delivery rate across all projects

### Page 4 — Contractor Scorecard
![Contractor Scorecard](Construction%20Analytics/Constractor%20Scoreboard.png)

Performance assessment of 20 major Australian contractors:
- Risk matrix bubble chart: Cost Overrun % vs Delay Days 
  vs Contract Value — reference lines mark portfolio averages
- Heatmap table with traffic light conditional formatting 
  (red/yellow/green) for instant performance assessment
- Buildcorp and Hansen Yuncken ranked highest overall
- Probuild leads on-time delivery at 66.7%
- Renascent highest avg delay at 50.6 days

---

## Tools & Techniques

| Tool | Usage |
|------|-------|
| Power BI Desktop | Report building, visualisations, publishing |
| DAX | Custom measures and business logic |
| Power Query | Data transformation and loading |
| Data Modelling | Relational model with cross-filtering |

### DAX Measures Written
```dax
Projects Delayed = 
    COUNTROWS(
        FILTER(SiteBook_Projects, 
        SiteBook_Projects[Status] = "Delayed")
    )

On Time Rate = 
    DIVIDE(
        COUNTROWS(
            FILTER(SiteBook_Projects, 
            SiteBook_Projects[Delay_Days] = 0)
        ), 
        COUNTROWS(SiteBook_Projects)
    ) * 100

Total Cost Variance = 
    SUM(SiteBook_Projects[Actual_Cost_AUD]) - 
    SUM(SiteBook_Projects[Budget_AUD])
```

---

## Data Model

4 linked tables with bidirectional cross-filtering:

| Table | Rows | Description |
|-------|------|-------------|
| SiteBook_Projects | 300 | Master project table |
| SiteBook_Milestones | 1,207 | Project milestone records |
| SiteBook_CostTracking | 21,477 | Monthly cost entries |
| SiteBook_ContractorPerformance | 20 | Contractor summaries |

**Relationships:**
- Projects → Milestones (one-to-many on Project_ID)
- Projects → CostTracking (one-to-many on Project_ID)
- Projects → ContractorPerformance (many-to-one on Contractor)

---

## Key Business Insights

- Portfolio is **$967M over budget** across 300 projects
- **Permit Delays** are the #1 controllable delay cause
- **Commercial Office** projects have the highest cost overrun (12%)
- **Infrastructure - Road** projects have the longest delays
- **Probuild** leads on-time delivery; **Renascent** has highest 
  avg delay at 50.6 days
- Only **3 of 20 contractors** achieve above 30% on-time rate

---

## How to Open

1. Download the `.pbix` file from this repository
2. Open with [Power BI Desktop](https://powerbi.microsoft.com/desktop) 
   (free download)
3. All data is embedded — no external connections required
4. Use the State slicer on Page 1 to filter by Australian state

---

## About

Built by Shafayet Ul Islam as a portfolio project demonstrating 
Power BI development, data modelling, and construction industry 
business analytics.
