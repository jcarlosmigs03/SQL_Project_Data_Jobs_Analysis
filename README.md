# 📊 Introduction
This project is a SQL-based exploration of the data analyst job market, created as part of my learning journey in mastering the basics of SQL for data analytics 🧠💻. It uses real-world job posting data to practice core SQL concepts while uncovering insights related to salaries, skill demand, and skill value in data analyst roles.

Through a collection of beginner-friendly SQL queries 🗄️, the project analyzes:

- 💰 Top-paying data analyst jobs

- 🧩 Skills required for high-paying roles

- 📈 Most in-demand skills

- 💎 Top-paying skills

- 🎯 Optimal skills that balance demand and compensation

The main focus is on building a strong SQL foundation, including filtering, aggregations, grouping, joins, and sorting 🔍, all applied to practical data analytics scenarios.

This repository serves as both a learning resource for SQL 📘 and a data-driven overview of current trends in the data analyst job market 🚀.

Check the SQL queries here: [project_sql folder](/project_sql/) 

# 📌 Background
SQL is one of the most essential skills for data analysts, widely used to query and analyze job market data. This project was created to build a strong foundation in SQL through hands-on practice using real-world job postings.

By exploring salary trends and skill demand, the project connects SQL fundamentals with practical data analytics, making it both a learning exercise and a market-focused analysis.

The data came from an [SQL Course](https://youtu.be/7mz73uXD9DA) that I found on YouTube. It's about basic SQL for Data Analytics which enhanced my skill in SQL.





### The questions I wanted to answer through my SQL queries were:

1. What are the top-paying data analyst jobs?
2. What skills are required for these top-paying jobs?
3. What skills are most in demand for data analysts?
4. Which skills are associated with higher salaries?
5. What are the most optimal skills to learn?

# 🛠️ Tools Used
The following tools were used to support the analysis and development of this project, from writing queries to managing version control:

- **SQL:** Used to write queries that filter, join, group, and aggregate job posting data to analyze salaries, skill demand, and skill value for data analyst roles.

- **PostgreSQL:** Used as the relational database to store the job market dataset and execute SQL queries efficiently on structured data.

- **Visual Studio Code:** Used as the primary code editor to write, organize, and document SQL queries, making the workflow clean and reproducible.

- **Git & GitHub:** Used for version control to track changes, manage updates, and host the repository for collaboration and portfolio presentation.
# Analysis
This project explores the data analyst job market using SQL queries to extract meaningful insights from job posting data. The analysis focuses on understanding salary trends, skill demand, and the relationship between skills and compensation. Here’s a breakdown of the main analyses performed:

### 1. Top-Paying Data Analyst Job 💵 
 Retrieves the top 10 highest-paying Data Analyst positions that are remote/any location by selecting job details and average yearly salary, joining with company information, filtering out missing salaries, and ordering results from highest to lowest.

 ```sql
 SELECT 
    job_id,
    job_title,
    name AS company_name,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date
FROM job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'Anywhere' AND 
    salary_year_avg IS NOT NULL
ORDER BY
    salary_year_avg DESC
LIMIT 10;
```

Here's a breakdown of the top data analyst jobs:

- **Wide Salary Range:** Top 10 paying data analyst roles span from ₱184,000 to ₱650,000, highlighting strong earning potential in the field.

- **Diverse Employers:** Companies like SmartAsset, Meta, and AT&T offer high salaries, showing demand across multiple industries.

- **Job Title Variety:** Titles range from Data Analyst to Director of Analytics, reflecting varied roles and specializations within data analytics.

| Job ID  | Job Title                                       | Company Name                            | Job Location | Job Schedule Type | Salary Year Avg | Job Posted Date     |
| ------- | ----------------------------------------------- | --------------------------------------- | ------------ | ----------------- | --------------- | ------------------- |
| 226942  | Data Analyst                                    | Mantys                                  | Anywhere     | Full-time         | 650000.0        | 2023-02-20 15:13:33 |
| 547382  | Director of Analytics                           | Meta                                    | Anywhere     | Full-time         | 336500.0        | 2023-08-23 12:04:42 |
| 552322  | Associate Director- Data Insights               | AT&T                                    | Anywhere     | Full-time         | 255829.5        | 2023-06-18 16:03:12 |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements            | Anywhere     | Full-time         | 232423.0        | 2023-12-05 20:00:40 |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers                       | Anywhere     | Full-time         | 217000.0        | 2023-01-17 00:17:23 |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                              | Anywhere     | Full-time         | 205000.0        | 2023-08-09 11:00:01 |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                             | Anywhere     | Full-time         | 189309.0        | 2023-12-07 15:00:13 |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                                | Anywhere     | Full-time         | 189000.0        | 2023-01-05 00:00:25 |
| 1749593 | Principal Data Analyst                          | SmartAsset                              | Anywhere     | Full-time         | 186000.0        | 2023-07-11 16:00:05 |
| 387860  | ERM Data Analyst                                | Get It Recruit - Information Technology | Anywhere     | Full-time         | 184000.0        | 2023-06-09 08:01:04 |


### 2. Top-Paying Skills for Data Analyst Jobs
By analyzing recent data analysis job postings and their salaries to identify which skills are linked to higher pay. The results highlight the technical competencies from programming languages to cloud platforms and visualization tools that drive top compensation.

```sql
WITH top_paying_jobs AS (
    SELECT 
        job_id,
        job_title,
        name AS company_name,
        salary_year_avg
    FROM job_postings_fact
    LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
    WHERE
        job_title_short = 'Data Analyst' AND 
        job_location = 'Anywhere' AND 
        salary_year_avg IS NOT NULL
    ORDER BY
        salary_year_avg DESC
    LIMIT 10
)

SELECT
    top_paying_jobs.*,   
    skills_dim.skills
FROM
    top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
        salary_year_avg DESC;
```

Here is a breakdown for the top-paying skills for data analyst jobs:

- **Core Analytical Skills Drive High Salaries:** SQL, Python, and R consistently appear in top-paying data analysis roles, highlighting that strong expertise in data querying, programming, and statistical analysis is highly valued.

- **Cloud and Big Data Expertise Increases Earning Potential:** Skills in Azure, AWS, Databricks, Hadoop, and Snowflake are linked to higher salaries, showing that the ability to handle scalable data processing and cloud-based analytics is a premium skill.

- **Visualization and Reporting Skills Are Essential:** Proficiency in Tableau, Power BI, Excel, and Jupyter is frequently required for well-compensated positions, emphasizing the importance of effectively communicating insights through dashboards and reports.

| Job ID  | Job Title                                       | Company Name                 | Salary Year Avg | Skills     |
| ------- | ----------------------------------------------- | ---------------------------- | --------------- | ---------- |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | sql        |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | python     |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | r          |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | azure      |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | databricks |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | aws        |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | pandas     |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | pyspark    |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | jupyter    |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | excel      |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | tableau    |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | power bi   |
| 552322  | Associate Director- Data Insights               | AT&T                         | 255829.5        | powerpoint |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements | 232423.0        | sql        |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements | 232423.0        | python     |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements | 232423.0        | r          |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements | 232423.0        | hadoop     |
| 99305   | Data Analyst, Marketing                         | Pinterest Job Advertisements | 232423.0        | tableau    |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers            | 217000.0        | sql        |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers            | 217000.0        | crystal    |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers            | 217000.0        | oracle     |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers            | 217000.0        | tableau    |
| 1021647 | Data Analyst (Hybrid/Remote)                    | Uclahealthcareers            | 217000.0        | flow       |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | sql        |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | python     |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | go         |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | snowflake  |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | pandas     |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | numpy      |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | excel      |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | tableau    |
| 168310  | Principal Data Analyst (Remote)                 | SmartAsset                   | 205000.0        | gitlab     |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | sql        |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | python     |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | azure      |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | aws        |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | oracle     |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | snowflake  |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | tableau    |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | power bi   |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | sap        |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | jenkins    |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | bitbucket  |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | atlassian  |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | jira       |
| 731368  | Director, Data Analyst - HYBRID                 | Inclusively                  | 189309.0        | confluence |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                     | 189000.0        | sql        |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                     | 189000.0        | python     |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                     | 189000.0        | r          |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                     | 189000.0        | git        |
| 310660  | Principal Data Analyst, AV Performance Analysis | Motional                     |                 |            |


### 3. In-Demand Skills for Data Analyst Jobs
Using SQL counts and ranking functions, I identified the most frequently requested skills across all job postings, showing which abilities are currently valued by employers.

```sql
SELECT 
    skills_dim.skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' AND
    job_work_from_home = true
GROUP BY
    skills_dim.skills 
ORDER BY
 demand_count DESC
LIMIT 5;
```
Here is a breakdown for the in-demand skills for data analyst jobs:
- **SQL Dominates Job Requirements**: SQL appears in the majority of job postings, demonstrating that the ability to query and manage databases remains essential for data analysts.

- **Excel Remains a Key Tool:** Excel continues to be highly requested, reflecting its importance for quick data manipulation, reporting, and basic analysis across industries.

- **Programming and Visualization Skills Are Growing:** Python, Tableau, and Power BI are increasingly in demand, showing that modern data analysis relies heavily on programming, visualization, and business intelligence capabilities.

| Skills   | Demand Count |
| -------- | ------------ |
| sql      | 7291         |
| excel    | 4611         |
| python   | 4330         |
| tableau  | 3745         |
| power bi | 2609         |


### 4. Top-Paying Skills for Data Analyst Jobs
Identifying which skills are associated with the highest salaries, we analyzed recent job postings and their reported average salaries. The results highlight technical competencies and tools that command premium compensation in the data and tech industry.
```sql
SELECT 
    skills_dim.skills,
    ROUND(AVG(salary_year_avg), 2) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' AND
    salary_year_avg IS NOT NULL
GROUP BY
    skills
ORDER BY
    avg_salary DESC
LIMIT 25;
```
Here is a breakdown for the top-paying skills for data analyst jobs:
- **Version Control Expertise Commands Exceptional Salaries:** Skills like SVN, GitLab, and Bitbucket appear at the top of the salary list, with SVN averaging $400,000, showing that deep knowledge of version control and code management is highly rewarded.

- **Emerging Programming and AI/ML Skills Are Lucrative:** Languages and frameworks such as Solidity, Golang, MXNet, Keras, PyTorch, TensorFlow, and Dplyr are associated with high salaries, indicating that expertise in blockchain development, back-end programming, and AI/machine learning is increasingly valuable.

- **DevOps, Cloud, and Automation Tools Enhance Compensation:** Tools like VMware, Terraform, Puppet, Ansible, and Airflow appear among top-paying skills, highlighting that the ability to manage infrastructure, automate workflows, and orchestrate cloud environments significantly boosts earning potential.

| Skills       | Avg Salary |
| ------------ | ---------- |
| svn          | 400,000.00 |
| solidity     | 179,000.00 |
| couchbase    | 160,515.00 |
| datarobot    | 155,485.50 |
| golang       | 155,000.00 |
| mxnet        | 149,000.00 |
| dplyr        | 147,633.33 |
| vmware       | 147,500.00 |
| terraform    | 146,733.83 |
| twilio       | 138,500.00 |
| gitlab       | 134,126.00 |
| kafka        | 129,999.16 |
| puppet       | 129,820.00 |
| keras        | 127,013.33 |
| pytorch      | 125,226.20 |
| perl         | 124,685.75 |
| ansible      | 124,370.00 |
| hugging face | 123,950.00 |
| tensorflow   | 120,646.83 |
| cassandra    | 118,406.68 |
| notion       | 118,091.67 |
| atlassian    | 117,965.60 |
| bitbucket    | 116,711.75 |
| airflow      | 116,387.26 |
| scala        | 115,479.53 |


### 5. Optimal Skills for Data Analyst Jobs 
Combining demand and salary data, I analyzed which skills provide the best balance between high pay and high demand, helping guide which skills to prioritize for career growth.

```sql
WITH in_demand_skills AS (
    SELECT 
        skills_dim.skill_id,
        skills_dim.skills,
        COUNT(skills_job_dim.job_id) AS demand_count
    FROM job_postings_fact
    INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
    INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
    WHERE
        job_title_short = 'Data Analyst' AND
        job_work_from_home = true AND
        salary_year_avg IS NOT NULL
    GROUP BY
        skills_dim.skill_id
), top_paying_skills AS (
    SELECT 
    skills_job_dim.skill_id,
    ROUND(AVG(salary_year_avg), 2) AS avg_salary
    FROM job_postings_fact
    INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
    INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
    WHERE
        job_title_short = 'Data Analyst' AND
        salary_year_avg IS NOT NULL AND
        job_work_from_home = true
    GROUP BY
        skills_job_dim.skill_id
)

SELECT 
    in_demand_skills.skill_id,
    in_demand_skills.skills,
    demand_count,
    top_paying_skills.avg_salary
FROM
    in_demand_skills
INNER JOIN top_paying_skills ON in_demand_skills.skill_id = top_paying_skills.skill_id
WHERE
    demand_count > 10
ORDER BY
    avg_salary DESC,
    demand_count DESC
    
LIMIT 25;
```
Here is a breakdown for the optimal skills for data analyt jobs:

- **High Demand for Core Analytical Languages:** Python, R, and SQL Server appear frequently in job postings, with Python requested 236 times and R 148 times. This indicates that strong proficiency in programming and statistical analysis remains essential for data analysis roles.

- **Cloud, Big Data, and Database Skills Are Highly Valuable:** Skills such as Snowflake, Azure, AWS, Hadoop, Redshift, BigQuery, and NoSQL offer high average salaries, showing that expertise in cloud platforms, big data processing, and database management is critical for well-compensated positions.

- **Business Intelligence and Project Management Tools Enhance Effectiveness:** Tools like Tableau, Looker, Confluence, and Jira are both in demand and associated with competitive salaries, highlighting the importance of visualization, reporting, and collaboration skills in driving impactful data-driven decisions.

| Skill ID | Skills     | Demand Count | Avg Salary |
| -------- | ---------- | ------------ | ---------- |
| 8        | go         | 27           | 115,319.89 |
| 234      | confluence | 11           | 114,209.91 |
| 97       | hadoop     | 22           | 113,192.57 |
| 80       | snowflake  | 37           | 112,947.97 |
| 74       | azure      | 34           | 111,225.10 |
| 77       | bigquery   | 13           | 109,653.85 |
| 76       | aws        | 32           | 108,317.30 |
| 4        | java       | 17           | 106,906.44 |
| 194      | ssis       | 12           | 106,683.33 |
| 233      | jira       | 20           | 104,917.90 |
| 79       | oracle     | 37           | 104,533.70 |
| 185      | looker     | 49           | 103,795.30 |
| 2        | nosql      | 13           | 101,413.73 |
| 1        | python     | 236          | 101,397.22 |
| 5        | r          | 148          | 100,498.77 |
| 78       | redshift   | 16           | 99,936.44  |
| 187      | qlik       | 13           | 99,630.81  |
| 182      | tableau    | 230          | 99,287.65  |
| 197      | ssrs       | 14           | 99,171.43  |
| 92       | spark      | 13           | 99,076.92  |
| 13       | c++        | 11           | 98,958.23  |
| 186      | sas        | 63           | 98,902.37  |
| 7        | sas        | 63           | 98,902.37  |
| 61       | sql server | 35           | 97,785.73  |
| 9        | javascript | 20           | 97,587.00  |

# What I Learned

Throughout my journey into SQL, I’ve leveled up my database skills with some serious wizardry:

- **🧩 Query Foundations:** Mastered SELECT statements, filtering with WHERE, and sorting with ORDER BY to pull exactly the data I need.

- **🔗 Joining Forces:** Learned to combine tables using INNER JOIN, LEFT JOIN, and other joins to unlock insights hidden across multiple datasets.

- **🧮 Aggregation Magic:** Got cozy with GROUP BY, COUNT, SUM, and AVG to turn raw data into meaningful summaries.

- **🛠️ Data Transformation:** Learned how to use functions, aliases, and simple subqueries to reshape data for analysis.

- **💡 Problem-Solving Mindset:** Turned real-world questions into SQL queries that answer them, building confidence in data exploration and manipulation.
# Conclusions
### Insights

1. **Top-Paying Data Analyst Roles:** Remote data analyst positions with the highest salaries can offer compensation up to $650,000, highlighting the financial potential in this field.

2. **Essential Skills for High-Paying Roles:** Advanced proficiency in SQL is often required for top-paying data analyst jobs, making it a critical skill for maximizing earnings.

3. **Most In-Demand Skills:** SQL remains the most sought-after skill in the data analyst job market, emphasizing its importance for career growth and employability.

4. **Specialized Skills and Higher Salaries:** Expertise in niche areas such as SVN and Solidity correlates with higher average salaries, reflecting a premium on specialized knowledge.

5. **Optimal Skills for Market Value:** SQL’s high demand and strong salary potential position it as a key skill for data analysts aiming to enhance their market value and career prospects.

### Closing Thoughts

This project helped me in getting introduced to SQL queries and enhancing my skills in SQL and provided insights into the data analyst job market. The findings from the analysis game me an idea on what skills to prioritize when job searching. The data clearly shows that success in this field isn't just about what you know, but how effectively you can adapt to high-growth technologies. I am walking away from this project with a more refined SQL toolkit and a strategic perspective on how to thrive in a competitive, data-centric world.
