SELECT * FROM coviddeath 
SELECT country, date, population, total_cases, new_cases, total_deaths, population 
FROM coviddeath 
ORDER BY country

--Calculate the percentage of covid total deaths compared to total cases in the United States 
--Death_percetage indicating likelihood of dying after getting covid
SELECT country, date, total_cases, total_deaths, 
(total_deaths/total_cases)*100 AS death_percentage 
FROM coviddeath 
WHERE country = 'United states'

--Calculate the percentage of covid total cases compared to the population in the United States
SELECT continent,country, date, total_cases, population, 
(total_cases/population)*100 AS infection_rate 
FROM coviddeath 
WHERE country = 'United states'

--Let's examine average infection rate and death percentage based on countries.
SELECT country, AVG((total_cases/population))*100 AS averege_infection_rate, 
AVG((total_cases/population))*100 AS average_death_rate 
FROM coviddeath 
WHERE continent is not null 
GROUP BY country

--How many hospitalized patients are likely be end up in icu on each country in average?
SELECT country, AVG(cast(icu_patients as int)) AS aver_icu_pat, 
AVG(cast(hosp_patients as int)) AS aver_hosp_pat, 
AVG(cast(icu_patients as int))/ AVG(cast(hosp_patients as int))*100 AS percentage_of_icu_patients 
FROM coviddeath 
WHERE continent is not null 
GROUP BY country

--Examine which countries has the highest infection count 
--United States has the highest infection count compared to other countries in the world
SELECT country, population, MAX(total_cases) AS highest_count, 
MAX((total_cases/population))*100 AS highest_infection_rate 
FROM coviddeath 
WHERE continent is not null 
GROUP BY country, population 
ORDER BY highest_count desc

--Examine which countries has the highest covid death count 
--United States has the highest death count compared to other countries in the world
SELECT country, population, MAX(cast(total_deaths as int)) AS highest_death_count, 
MAX((total_deaths/population))*100 AS highest_death_rate FROM coviddeath 
WHERE continent is not null GROUP BY country, population 
ORDER BY highest_death_count desc

--Let's break the highest covid infection count and covid death count by continent 
--North America has the highest infection counts and death counts compared to other continents in the world
SELECT continent,MAX(total_cases) AS highest_infection_count, 
MAX(cast(total_deaths as int)) AS highest_death_count 
FROM coviddeath WHERE continent is not null 
GROUP BY continent 
ORDER BY highest_infection_count desc

--Total new cases, new deaths,and covid death percentage around the globe per day
SELECT date,SUM(new_cases) AS total_new_cases, SUM(cast(new_deaths as int)) AS total_new_death, 
SUM(cast(new_deaths as int))/SUM(new_cases)*100 AS death_percentage 
FROM coviddeath WHERE continent is not null 
GROUP BY date ORDER BY 1,2

--Numbers of people vaccinated, fully vaccinated and total boosters, and total_vaccinations by date 
--when vaccinations occured 
SELECT coviddeath.country, coviddeath.date, 
people_vaccinated, people_fully_vaccinated, total_boosters, total_vaccinations, population
FROM covidVaccinations JOIN coviddeath 
ON coviddeath.country = covidVaccinations.country AND coviddeath.date = covidVaccinations.date


--Vaccinated, fully vaccinated, booster, total percentages of vaccination in a total population
SELECT date,SUM(new_cases) AS total_new_cases, 
SUM(cast(new_deaths as int)) AS total_new_death, 
SUM(cast(new_deaths as int))/SUM(new_cases)*100 AS death_percentage 
FROM coviddeath WHERE continent is not null 
GROUP BY date 
ORDER BY 1,2


SELECT coviddeath.country,coviddeath.date, (people_vaccinated/population)*100 AS percentage_of_vacc, 
(people_fully_vaccinated/population)*100 AS percentage_of_fully_vacc, 
(total_boosters/population)*100 AS total_percentage_of_booster, 
(total_vaccinations/population)*100 AS total_percentages_of_vaccination, population 
FROM covidVaccinations JOIN coviddeath 
ON coviddeath.country = covidVaccinations.country AND coviddeath.date = covidVaccinations.date 
WHERE coviddeath.continent is not null 

--Create Views for visualization


--highest infection and death rate sorted by country
Create View Max_infection_death_rate_by_country AS
SELECT coviddeath.country, MAX((total_cases/population))*100 AS highest_infection_rate, 
MAX((total_deaths/population))*100 AS highest_death_rate,population
FROM covidVaccinations 
JOIN coviddeath
ON coviddeath.country = covidVaccinations.country 
GROUP BY coviddeath.country, population



--highest infection and death rate sorted by continent
CREATE View Max_infection_death_rate_by_continent AS
SELECT continent,MAX(total_cases) AS highest_infection_count, 
MAX(cast(total_deaths as int)) AS highest_death_count 
FROM coviddeath WHERE continent is not null 
GROUP BY continent 
