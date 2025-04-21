
# COVID-19 Vaccination Data Analysis

This project focuses on **data cleaning, transformation, and analysis** of global COVID-19 vaccination data using **SQL Server**. It demonstrates how to track vaccination progress over time, calculate vaccination percentages, and build a solid base for future dashboard visualizations.

## Table of Contents

- [Overview](#overview)
- [Objectives](#objectives)
- [SQL Techniques Used](#sql-techniques-used)
- [Data Sources](#data-sources)
- [Key Outputs](#key-outputs)
- [View Creation](#view-creation)
- [Future Scope](#future-scope)
- [Author](#author)

---

## Overview

This project involves analyzing COVID-19 death and vaccination datasets. It includes:

- Population-level vaccination percentage tracking
- Cumulative vaccination trends
- Preparation of views for Power BI visualizations

---

## Objectives

- Clean and structure raw `.xlsx` data in SQL Server.
- Track rolling number of people vaccinated by country.
- Calculate the percentage of vaccinated population over time.
- Create a view for easy dashboard integration.

---

## SQL Techniques Used

- CTEs and temporary tables
- Window functions (`SUM() OVER(PARTITION BY ...)`)
- Data type conversions
- Joins between death and vaccination datasets
- Creating views for visualizations

---

## Data Sources

The data was derived from the following tables:

- **CovidDeaths** – Contains daily death reports per country.
- **CovidVaccinations** – Contains records of vaccination progress.

Cleaned `.xlsx` versions of these datasets were prepared before importing into SQL Server.

---

## Key Outputs

- A temporary table: `#PercentPopulationVaccinated` was created to hold country-level cumulative vaccination stats.
- Final query shows:
  - Country
  - Date
  - Total population
  - New vaccinations
  - Cumulative vaccinated count
  - **% of population vaccinated**

---

## View Creation

A SQL **view** named `PercentPopulationVaccinated` was created for later use in Power BI:

```sql
Create View PercentPopulationVaccinated as
Select dea.continent, dea.location, dea.date, dea.population, vac.new_vaccinations,
SUM(CONVERT(int,vac.new_vaccinations)) OVER (Partition by dea.Location Order by dea.location, dea.Date) as RollingPeopleVaccinated
From CovidDeaths dea
Join CovidVaccinations vac
  On dea.location = vac.location
  and dea.date = vac.date
Where dea.continent is not null
```

---

## Future Scope

- Build a Power BI dashboard using this view
- Add death/vaccination ratio analysis
- Explore continent-wise vaccination differences
- Introduce real-time dashboard updates

---

## Author

**Anshupriya Singh**  
Data Analyst | SQL Enthusiast  
[LinkedIn](https://www.linkedin.com/in/anshupriya-singh01) | [Portfolio](https://github.com/anshupriya01)

---
