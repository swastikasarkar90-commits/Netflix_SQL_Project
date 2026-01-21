# Netflix Movies and TV shows Data Analysis using SQL

![Netflix Logo](https://github.com/swastikasarkar90-commits/Netflix_SQL_Project/blob/main/logo.png)


## Overview
This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.


## Objectives
i. Analyze the distribution of content types (movies vs TV shows).
ii. Identify the most common ratings for movies and TV shows.
iii. List and analyze content based on release years, countries, and durations.
iv. Explore and categorize content based on specific criteria and keywords.


## Schema

```sql
CREATE TABLE netflix_1 (
show_id	VARCHAR(20) PRIMARY KEY,
typess VARCHAR(50),
title VARCHAR(120),
director VARCHAR(220),
casts VARCHAR(1000),
country	VARCHAR(150),
date_added VARCHAR(50),
release_year INT,
rating VARCHAR(50),
duration VARCHAR(15),
listed_in VARCHAR(100),
descriptions VARCHAR(300)
);
```

## Business Problem and Solution

```sql
SELECT COUNT(*) as total_content
FROM netflix_1;
```

### Find out all types from the dataset

```sql
SELECT 
DISTINCT typess
FROM netflix_1; 
```

### 1.Count the Number of Movies vs TV Shows

```sql
SELECT 
    typess,
    COUNT(*)
FROM netflix_1
GROUP BY 1;
```
Objective: Determine the distribution of content types on Netflix.

### 2. List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT *
FROM netflix_1
WHERE release_year = 2020;
```

Objective: Retrieve all movies released in a specific year.

### 3.Find the Top 5 Countries with the Most Content on Netflix

```sql
SELECT country, COUNT(*) AS total_content
FROM netflix_1
WHERE country IS NOT NULL
GROUP BY country
ORDER BY total_content DESC
LIMIT 5;
```

### 4.Find the Most Common Rating for Movies and TV Shows

```sql
SELECT typess, rating, COUNT(*) AS rating_count
FROM netflix_1
WHERE rating IS NOT NULL
GROUP BY typess, rating
ORDER BY rating_count DESC;
```

Objective: Identify the most frequently occurring rating for each type of content.

### 5. Find Content Added in the Last 5 Years

```sql
SELECT title, typess, date_added
FROM netflix_1
WHERE YEAR(STR_TO_DATE(date_added, '%M %d, %Y')) >= YEAR(CURDATE()) - 5;
```

Objective: Retrieve content added to Netflix in the last 5 years.

### 6.Find All Movies/TV Shows by Director 'Kirsten Johnson' 

```sql
SELECT * FROM netflix_1
WHERE director = 'Kirsten Johnson';
```

Objective: List all content directed by 'Kirsten Johnson'.

### 7.Count the Number of Content Items in Each Genre

```sql
SELECT listed_in AS genre, COUNT(*) AS total_content
FROM netflix_1
GROUP BY listed_in
ORDER BY total_content DESC;
```

### 8.Find each year and the average numbers of content release in India on netflix. 

```sql
SELECT release_year, COUNT(*) AS total_content
FROM netflix_1
WHERE country = 'India'
GROUP BY release_year
ORDER BY release_year;
```

Objective: Calculate and rank years by the average number of content releases by India.

### 9.List All Movies that are Documentaries

```sql
SELECT * 
FROM netflix_1
WHERE listed_in = 'Documentaries';
```

Objective: Retrieve all movies classified as documentaries.

### 10.Find All Content Without a Director 

```sql
SELECT * 
FROM netflix_1
WHERE director is NULL or director = '';
```

Objective: List content that does not have a director.

### 11.Find How Many Movies Actor 'Salman Khan' Appeared in the Last 10 Years 

```sql
SELECT * 
FROM netflix_1
WHERE casts = 'Salman Khan'
AND release_year = year(curdate()) - 10;
```
or

```sql
SELECT COUNT(*) AS total_movies
FROM netflix_1
WHERE typess = 'Movie'
  AND casts = '%Salman Khan%'
  AND release_year >= YEAR(CURDATE()) - 10;
```

  Objective: Count the number of movies featuring 'Salman Khan' in the last 10 years.


## Findings and Conclusion

i. Content Distribution: The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
ii. Common Ratings: Insights into the most common ratings provide an understanding of the content's target audience.
iii. Geographical Insights: The top countries and the average content releases by India highlight regional content distribution.
iv. Content Categorization: Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.

This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.


## Author - Zero Analyst

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

## Stay Updated and Join the Community
For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

Email: [swastikasarkar90@gmail.com]
LinkedIn: [www.linkedin.com/in/swastika-sarkar-31a12b234]

Thank you for your support, and I look forward to connecting with you!
