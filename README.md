# Shark_Tank
A comprehensive data analysis of the Shark Tank TV show using SQL.

### Project Overview

The Shark Tank SQL Project involved a comprehensive data analysis of the Shark Tank TV show using SQL. The project aimed to derive key insights and metrics to provide a detailed understanding of the show's dynamics. The analysis included evaluating the number of episodes, unique pitches, funding conversion rates, gender ratios, investment amounts, and other critical metrics. The project demonstrated advanced SQL skills, including data cleaning, exploratory data analysis, and complex query execution.

### Data Source

- The dataset was manually gathered by watching each episode of Shark Tank and supplemented with information from the Shark Tank Wikipedia page. 
- The dataset includes details about the episodes, contestants, deals, investments, and more.

### Tools

- Microsoft SQL Server
- Microsoft Excel (for initial data verification)

### Data Cleaning/Preparation

- Data Collection: Data was gathered from watching episodes and from Wikipedia.
- Data Import: The collected data was imported into Microsoft SQL Server using the "Import Data" wizard.
- Database Creation: A new database named "Project" was created.
- Table Creation: The dataset was imported into a table within the created database.

### Exploratory Data Analysis (EDA)

- Total Episodes: Counted the total number of episodes telecasted.
- Total Pitches: Counted the unique number of startups that pitched.
- Funding Analysis: Analyzed the number of startups that received funding versus those that did not.
- Participant Analysis: Analyzed the gender ratio of participants.
- Investment Analysis: Calculated the total amount invested, average equity taken, and highest deal amounts.
- Location and Sector Analysis: Identified the most common locations and sectors from which startups pitched.

### Data Analysis

```sql
/* Count the total number of unique episodes */
SELECT COUNT(DISTINCT episode_number) AS total_episodes 
FROM project_data;

/* Count the total number of unique pitches (brands) */
SELECT COUNT(DISTINCT brand_name) AS total_pitches 
FROM project_data;

/* Count the number of pitches that received funding */
SELECT SUM(CASE WHEN amount_invested > 0 THEN 1 ELSE 0 END) AS pitches_converted 
FROM project_data;

/* Calculate the gender ratio of female to male contestants */
SELECT SUM(female) * 1.0 / SUM(male) AS gender_ratio 
FROM project_data;

/* Calculate the total amount invested in pitches */
SELECT SUM(amount_invested) AS total_invested 
FROM project_data;

/* Calculate the average equity taken in deals where investment was made */
SELECT AVG(equity_taken) AS average_equity 
FROM project_data 
WHERE amount_invested > 0;

/* Find the highest deal amount invested */
SELECT MAX(amount_invested) AS highest_deal 
FROM project_data;

/* Find the highest equity percentage taken in deals */
SELECT MAX(equity_taken) AS highest_equity 
FROM project_data;

/* Count the number of startups with at least one female contestant */
SELECT COUNT(*) AS female_startups 
FROM project_data 
WHERE female > 0;

/* Calculate the average number of team members per startup */
SELECT AVG(total_team_members) AS average_team_members 
FROM project_data;

/* Calculate the average investment amount per deal where investment was made */
SELECT AVG(amount_invested) AS average_investment_per_deal 
FROM project_data 
WHERE amount_invested > 0;

/* Count the distribution of startups by average age group */
SELECT average_age_group, COUNT(*) AS count 
FROM project_data 
GROUP BY average_age_group 
ORDER BY count DESC;

/* Count the number of startups from each location */
SELECT location, COUNT(*) AS count 
FROM project_data 
GROUP BY location 
ORDER BY count DESC;

/* Count the number of startups in each sector */
SELECT sector, COUNT(*) AS count 
FROM project_data 
GROUP BY sector 
ORDER BY count DESC;

/* Count the number of deals involving collaborations among sharks */
SELECT partners, COUNT(*) AS deal_count 
FROM project_data 
WHERE partners IS NOT NULL 
GROUP BY partners 
ORDER BY deal_count DESC;

/* Example detailed metrics for one shark, Vineeta */
SELECT 'Vineeta' AS shark,
       COUNT(*) AS total_deals_present,
       SUM(CASE WHEN amount_invested > 0 THEN 1 ELSE 0 END) AS deals_converted,
       SUM(amount_invested) AS total_amount_invested,
       AVG(equity_taken) AS average_equity_taken
FROM project_data
WHERE ashni_invested IS NOT NULL;
```

### Results/Findings

- Total Episodes: 30 episodes were analyzed.
- Total Pitches: 98 unique startups pitched their ideas.
- Pitches Converted: 57 out of 98 startups received funding (58% conversion rate).
- Gender Ratio: The gender ratio of female to male contestants was approximately 0.42.
- Total Investment: The total amount invested was significant, with the highest deal being 150 lakhs.
- Average Equity Taken: The average equity taken by sharks was around 16.55%.
- Most Frequent Location: Most startups came from Delhi.
- Dominant Sector: The food sector had the most startups pitching.

### Recommendations
- Increase Diversity: Encourage more female entrepreneurs to participate.
- Sector Focus: Given the high number of food sector startups, more specialized investment strategies could be developed.
- Geographic Expansion: Initiatives to attract startups from a wider range of locations could enhance the diversity of pitches.
