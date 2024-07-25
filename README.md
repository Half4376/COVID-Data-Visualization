# COVID Data Visualization Project

This portfolio project showcases my skills as a data analyst using Grafana a data visualization tool. The project involves analyzing 
COVID-19 data that was cleaned from my [previous project](https://github.com/Half4376/COVID-Data-Exploration-Project),
creating insightful visualizations, and demonstrating the ability to handle and transform data from different sources.

[![COVID Dashboard](Images/COVID%20Dashboard.png)](http://localhost:3000/dashboard/snapshot/Jr9dhu9wnVK0pX4aLl0uc8Tov5rpssin?orgId=0)

## Table of Contents
- [Project Overview](#project-overview)
- [Tools and Technologies](#tools-and-technologies)
- [PostgreSQL Queries](#PostgreSQL-queries)
- [Data Transformation](#data-transformation)
- [Visualizations](#visualizations)
- [Conclusion](#conclusion)

## Project Overview

This project involves:
1. Running PostgreSQL queries to analyze COVID-19 data.
2. Transforming data using Excel.
3. Creating visualizations using Grafana.
4. Analyzing and interpreting the results.

## Tools and Technologies

- **PostgreSQL**: For querying the COVID-19 data.
- **Excel**: For data transformation and cleaning.
- **Grafana**: For creating visualizations and dashboards.

## PostgreSQL Queries

### Query 1: Death Percentage
This query calculates the total cases, total deaths, and death percentage.

```sql
Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, 
	SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From covidDeaths
where continent is not null 
order by 1,2;
```
### Query 2: Total Continent Death Count
```sql
Select location, SUM(cast(new_deaths as int)) as TotalDeathCount
From covidDeaths
Where continent is null 
and location not in ('World', 'European Union', 'International', 'Upper middle income',
	'High income', 'Lower middle income', 'Low income')
Group by location
order by TotalDeathCount desc;
```

### Query 3: Highest Infection Count and Population Infection Percentage
Query finds the country with the highest infection count and calculates the percentage of the population infected
```sql
Select Location, Population, MAX(total_cases) as HighestInfectionCount,  
	Max((total_cases/population))*100 as PercentPopulationInfected
From covidDeaths
Group by Location, Population
order by PercentPopulationInfected desc;
```

### Query 4: Infection Count and Population Infection Percentage Within Countries
```sql
Select Location, Population,date, MAX(total_cases) as HighestInfectionCount,  
	Max((total_cases/population))*100 as PercentPopulationInfected
From covidDeaths
Group by Location, Population, date
order by PercentPopulationInfected desc;
```

## Data Transformation
- **Handling Null Values**: Replaced all nulls/blanks with 0 in Excel using CTRL+H.
- **Data Linking**: Ensured that data is tied together by dates, continent, or location.

## Visualizations

Using Grafana, the following visualizations were created:

1. **Global Numbers Table**: Displaying total cases, total deaths, and death percentages.
2. **Death Count per Continent Bar Graph**: Visual representation of death counts across continents.
3. **Total Infection by Country Geomap**: Geomap visualization showing the total infections by country.
4. **Average Percent Population Infected Line Graph**: Line graph depicting the average percentage of the population
   infected over time for 5 countries. Data transformed using Grafana tools into a multi-frame time series.

## Conclusion
This project demonstrates my ability to analyze and visualize data using PostgreSQL, Excel, and Grafana. The skills showcased include data querying, 
cleaning, transformation, and creating insightful visualizations to drive data-driven decisions.

Feel free to explore the [visualizations](http://localhost:3000/dashboard/snapshot/Jr9dhu9wnVK0pX4aLl0uc8Tov5rpssin?orgId=0) and PostgresSQL queries provided. Your feedback is welcome!
