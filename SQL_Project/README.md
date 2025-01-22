# Introduction
 Dive into the data job market! Focusing on entry level data/business analyst roles, this project explores what the most common industries that are hiring analysts are, the top skills wanted, the best months to apply, and the best job search engines to use.

SQL Queries? Check them out here: [SQL_project](/SQL_Project/)
# Background
Driven by a quest to navigate the job market more effectively, this project was born from a desire to pinpoint what industries and companies hire the most data analysts, which search engines are most effective and which areas of the world hire the most analysts.

Data hails from [Luke Barrousse's SQL Course](https://www.youtube.com/watch?v=7mz73uXD9DA&t=14297s). It's packed with data on data analyst job titles, salaries, locations, companies, job postings, and skills.

### The questions I wanted to answer through my SQL queries were:
1. What industries hire the most entry-level data analysts and whats the avg salary per industry?
2. What industries hire the highest paid data analysts and whats the avg salary per industry?
2. What are the top skills desired for entry-level data analysts
3. WHat are the top skills for any data professional, from analysts to engineers? (* 12/12/24 edit:Change to highest paid data professionals???)
4. What cities/countries have the most data analyst job postings?
5. How much more or less do companies pay for the remote option, with a degree, with health insurance included, with graduate degree?



# Tools I used
- **SQL**: The backbone of my analysis, allowing me to query the database and unearth critical insights
- **PostgresSQL**:The Chosen database management system
- **Visual Studio Code**: My go-to for database management and executing SQL queries
- **Git & GitHub**: Essential for version control and sharing my SQL scripts and analysis, ensuring collaboration and project tracking.
- **Excel**: For exported SQL query CSV files, I used simple data analysis and visualization techniques in Excel to help complete my graphs and visualizations
- **Tableau**: For the building of visualizations and two final dashbaords showcasing my main insights
- **ChatGPT**: For miscellaneous assistance in building graphs and visualizations

This project marks my second full-length SQL project. The first being the Covid-19 SQL exploration located here:  [SQL_COVID_Project_#1](https://github.com/PabloTheZenCoder/Patricks_Portfolio/blob/main/SQLCovidproject%231.sql). It was the first time I've used postgreSQL and Visual Studio Code which allowed me to gain valuable skills in database management, SQL querying, and project management. I've used git/github before but this course really helped me understand how to more effectively use Github for showcasing and publishing projects, as well as, version contol and setting myself up for potential collaboration. Additionally, by using Excel, Tableau and chatGPT for help in creating data visualizations, I was able to see the potential of a data analytics tech stack. Overall this project allowed me to better understand the process and evolution of a data analytics capstone project
# The Analysis
Each query for this project is aimed at analyzing specific aspects of the data analytics job market. Here's how I approached each question:

### 1. Common Industries hiring Data/Business Analysts

To see what industries are hiring the most entry-level data analysts, I filtered my data to focus on job postings that included the key word "entry-level" or "junior". I also filtered specifically for "data/business analysts". Additionally, I wanted to keep the job postings located in the U.S., where I reside, focusing on "full-time' positions that included the average yearly salary.

```sql
Select
  job_title,
  job_title_short,
  job_location,
  job_schedule_type,
  job_country,
  salary_year_avg,
  name as company_name
FROM 
  job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE 
    (job_title_short = 'Data Analyst'  OR
     job_title_short = 'Business Analyst') 
  and (job_title LIKE '%Entry_Level%' 
    OR job_title LIKE '%junior%')
   AND Salary_year_avg IS NOT NULL 
   AND job_schedule_type = 'Full-time'
    AND job_country = 'United States'
ORDER BY 
  Salary_year_avg DESC
;
```

![Top Industries Hiring Entry-level Data/Business Analysts](image.png) *Bar graph visualizing the top industries that are hiring Data/Business Analysts filtered by average salary and number of job postings*

Insights from the "Top Industries Hiring Entry-Level Data Analyst"

**-Diverse Industries:** The main industries hiring entry level data analyst's are:
1. Transportation/logistics
2. Real-estate tech
3. Software
4. AI education
5. IT Services
6. fintech
7. Insurance
8. Non-profit

**-IT Services hire the most entry-level analysts with 26 job postings:** AI training and education has the second highest amount of job postings at 8 postings

**-Wide Salary Range:** The salary range for entry level analyst's spans $45,000 to $81,000 with the average entry level analyst role paying around $64,000

**-Transportation/Logistics pays entry-level analysts the most with an $81,000 average annual salary**

**-Overall:** Entry-level analyst's should focus on applying to IT companies if they are simply looking to get an analyst job quickly. Transportation/Logistics would be a good industry to aim for since it pays the highest out of all of these industries 


### 2. The "Highest Paying" Industries Hiring Data Analyst's in 2023 Filtered by Salary and Number of Job Postings
For the second query I wanted to see what industries are hiring the highest paid data analyst's and how that differs from industries hiring entry-level data analysts. So I filtered for "data/business analysts",located in the U.S., where I reside, focusing on "full-time' positions that included the average yearly salary. Then I looked at the top 50, highest paying analyst job postings. 

From there, I exported this sub-dataset to Excel where I used ChatGPT to research and assign an industry based on each company in this dataset. 

Finally, I uploaded this newly updated dataset to Tableau where I created my bar graph visualization. I focused on industries that had more than one job posting.

```sql
Select
  job_title,
  job_title_short,
  job_location,
  job_schedule_type,
  job_country,
  salary_year_avg,
  name as company_name
FROM 
  job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE 
     (job_title_short = 'Data Analyst' 
    OR job_title_short = 'Business Analyst')
   AND Salary_year_avg IS NOT NULL 
   AND job_schedule_type = 'Full-time'
   AND job_country = 'United States'
ORDER BY 
  Salary_year_avg DESC
  LIMIT 50
;
```
![Top Paying Industries](image-1.png)
*Bar graph visualizing the top paying industries with multiple job postings that are hiring Data/Business Analysts. 

Insights from the "Top Paying Industries with Multiple Job Postings"

**-Diverse Industries:** The main industries hiring entry level data analyst's are:
1. Financial Services
2. Artificial Intelligence Research
3. Defense and Intelligence
4. Staffing and recruitment
5. Manufacturing and Packaging
6. Financial Recruitment
7. Healthcare
8. Fintech

**-Social Media and Entertainment hire the most entry-level analysts with 9 job postings:** This is includes companies like Meta, or Tiktok, Instagram, which makes sense that they would hire lots of data analyst since they are large companies with complex data ecosystems. Financial Services(i.e. Fintech) has the second highest amount of job postings if you combine Fintech, financial services, and financial recruitment with 7 job postings

**-High Salary Range:** The salary range for top paying analyst roles is high! It spans $200,000 to $300,000 with the average top paying analyst role paying around $241,086


**-Overall:** Social media and Entertainment companies like Facebook, Netflix, pinterist are going to be hiring many data analyst's for the forseable future. They have a lot of consumer data and thus, marketing skills will likely be a big part of these job roles. Therefore an entry level analyst would be smart to build marketing analyst skills knowing that there will be many high-paying social media company jobs in the future. 

***-Financial Services, Artificial Intelligence Research, and Defense and Intelligence Services pay top paid analysts the most with an $294,244 average annual salary*** These three industries and the skills associated with them, like AI, are good industries to focus on for a entry level analyst looking to maximize their yearly salary. 

***Other industries in this visualization like healthcare, biotechnology and Big Pharma, Manufacturing/packaging are also good industries to take note of and to build skills in.*** All of the industries in this visualization are top paying industries with a high demand for analyst's.

### 3. Top 20 Entry-Level, Data Analyst Skills Listed in Job Postings
For the third query, I wanted to see what were the most desired skills from entry-level/junior analyst's. By using my previous query that looked at Entry level jobs and industries, I was able to join the skills table which then allowed me to see every skill that is associated with each job posting. Later on, in Tableau I was able to group by skill and and then visualize these skills by how often they were listed in job postings.

```sql
WITH entry_us_jobs AS (
Select
  job_id,
  job_title,
  job_title_short,
  job_location,
  job_schedule_type,
  job_country,
  salary_year_avg,
  name as company_name
FROM 
  job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE 
   (Job_country = 'United States' AND
   job_title LIKE '%Analyst%') AND
  (job_title LIKE '%Entry_Level%' OR
  job_title LIKE '%Junior%')
ORDER BY 
  Salary_year_avg DESC
)

SELECT 
  entry_us_jobs.*,
  skills
FROM entry_us_jobs
INNER JOIN skills_job_dim ON entry_us_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY salary_year_avg DESC;
```

![Top 20 Entry-Level, Data Analyst Skills Listed in Job Postings](image-2.png)
*Bar graph visualizing the most frequently listed skills in entry-level data/business analyst job postings. 

Insights from the "Top 20 Entry-Level, Data Analyst Skills Listed in Job Postings"

-Excel is the most sought after skill for entry-level analyst's and was listed in 792 entry-level job postings

-Tableau and SQL are basically tied for the second most sought after skill having been listed in over 650 entry-level job postings

-The best entry-level data analyst skill stack is to be adept at Excel, Tableau, SQL, Python, SAS; in that order.

### 4. Top 5 Skills to for any Data Professional Job
To contrast this last visualization, I wanted to see what the top five skills desired are for any data professional, from analysts to engineers. I filtered for remote jobs since remote work seems to be more desired amoung data professionals and personally I would prefer to work remotely.

```sql
SELECT 
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
GROUP BY skills
ORDER BY demand_count DESC
limit 5;
```
![Top 5 Skills for Remote Data Professionals](image-3.png)

Insights from the "Top 5 Skills for Remote Data Professionals"

-SQL and Python are highly sought after skills for all data professionals, whether entry-level or seasoned professionals

-Having some knowledge and experience with cloud computing software like AWS or Azure would be beneficial to any data professional

-R is a very sought after skill for data professionals

### 4. Top Cities and States in the U.S. for Data Analyst Jobs
Even if remote jobs largely dominate the data job market, as an entry-level analyst, I felt like it's still very beneficial to network in person. Therefore knowing what states and cities in the U.S. have the most data jobs was important information to find out. 

To accomplish these graphs and maps, I simply counted the number of job postings per city. Then I exported that dataset over to Excel where I separated the city and state. Finally in Tableau, I used that new Excel dataset to aggregate the amount of jobs by city and state, visualizing the states and cities with the most job postings.

```sql
SELECT 
    job_location,
    COUNT(*) AS Jobs_per_place
FROM job_postings_fact
WHERE job_country = 'United States'
    AND job_location <> 'United States' 
    AND job_location <> 'Anywhere'
GROUP BY job_location
Order BY
    jobs_per_place DESC;
```
![Top states for Data jobs](image-4.png)
![Sum(job_per_place)](image-5.png)

![Top 8 States For Data Jobs ](image-6.png)

![Top Cities for Data Analysis](image-8.png)
![Top 11 Cities for Data Analysis](image-7.png)

Insights from the "Top Cities and States in the U.S. for Data Jobs"

-The top three states with the highest number of data analyst jobs are California, Texas and Florida. 

-My homestate of Tennessee is not one of the top states. However there are quite a few states close by in the Southeast region that do have substantial amounts of data jobs listed:
-Virginia
-Georgia
-North Carolina
-Florida

-The top states 3 states for data jobs are New York, Atlanta, and Chicago. Most of the big cities in the U.S. make this list from L.A. to Seattle to Boston to Denver.

-However the interactive map published in Tableau Public shows that many smaller, medium sized cities have large concentrations of data jobs. For instance: Alphareta, GA, Bentonville, AR, Charleston, SC, Colorado Springs, CO. (Personally, I love medium sized cities so I would be more inclined to seek out cool, outdoorsy, medium sized cities for a data job)


# What I Learned


# Conclusions
