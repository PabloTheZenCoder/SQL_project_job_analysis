# Introduction
 Dive into the data job market! Focusing on entry level data/business analyst roles, this project explores what the most common industries that are hiring analysts are, the top skills wanted, the best months to apply, and the best job search engines to use.

SQL Queries? Check them out here: [SQL_project](/SQL_Project/)
# Background
Driven by a quest to navigate the job market more effectively, this project was born from a desire to pinpoint what industries and companies hire the most data analysts, which search engines are most effective and which areas of the world hire the most analysts.

Data hails from [Luke Barrousse's SQL Course](https://www.youtube.com/watch?v=7mz73uXD9DA&t=14297s). It's packed with data on data analyst job titles, salaries, locations, companies, job postings, and skills.

### The questions I wanted to answer through my SQL queries were:
1. What industries hire the most data analysts and whats the avg salary per industry
    Compare:
        a)entry level/junior vs senior, highest paying
        b)Remote
        c)Jobs located in the Southeast
        d)jobs located remote or in places I want to live(Colorado, PNW, Europe, Flagstaff, Fayetteville, Asheville)
2. What cities/countries have the most data analyst job postings?
3. Which job_via website has the most job postings?
4. How much more or less do companies pay for the remote option, with a degree, with health insurance included, with graduate degree?
5. WHich companies are hiring the most data analysts?
6. WHat months have the most data analyst job postings
7. What companies are hiring the most marketing analysts
8. compare avg number of jobs postings for data analysts, business analyst, data scientists, data engineers, cloud engineers and compare avg salaries for each of these roles

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

# What I Learned


# Conclusions
