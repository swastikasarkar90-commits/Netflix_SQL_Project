# Netflix Movies and TV shows Data Analysis using SQL

![Netflix Logo](https://github.com/swastikasarkar90-commits/Netflix_SQL_Project/blob/main/logo.png)


## Overview
This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

## Objectives
Analyze the distribution of content types (movies vs TV shows).
Identify the most common ratings for movies and TV shows.
List and analyze content based on release years, countries, and durations.
Explore and categorize content based on specific criteria and keywords.
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

SELECT COUNT(*) as total_content
FROM netflix_1;

SELECT 
DISTINCT typess
FROM netflix_1; 

-- 1.Count the Number of Movies vs TV Shows
SELECT 
    typess,
    COUNT(*)
FROM netflix_1
GROUP BY 1;

-- 2. List All Movies Released in a Specific Year (e.g., 2020)
SELECT *
FROM netflix_1
WHERE release_year = 2020;

-- 3.Find the Top 5 Countries with the Most Content on Netflix
SELECT country, COUNT(*) AS total_content
FROM netflix_1
WHERE country IS NOT NULL
GROUP BY country
ORDER BY total_content DESC
LIMIT 5;

-- 4.Find the Most Common Rating for Movies and TV Shows
SELECT typess, rating, COUNT(*) AS rating_count
FROM netflix_1
WHERE rating IS NOT NULL
GROUP BY typess, rating
ORDER BY rating_count DESC;

-- 5. Find Content Added in the Last 5 Years
SELECT title, typess, date_added
FROM netflix_1
WHERE YEAR(STR_TO_DATE(date_added, '%M %d, %Y')) >= YEAR(CURDATE()) - 5;

-- 6.Find All Movies/TV Shows by Director 'Kirsten Johnson' 
SELECT * FROM netflix_1
WHERE director = 'Kirsten Johnson';

-- 7.Count the Number of Content Items in Each Genre
SELECT listed_in AS genre, COUNT(*) AS total_content
FROM netflix_1
GROUP BY listed_in
ORDER BY total_content DESC;

-- 8.Find each year and the average numbers of content release in India on netflix. 
SELECT release_year, COUNT(*) AS total_content
FROM netflix_1
WHERE country = 'India'
GROUP BY release_year
ORDER BY release_year;

-- 9.List All Movies that are Documentaries
SELECT * 
FROM netflix_1
WHERE listed_in = 'Documentaries';

-- 10.Find All Content Without a Director 
SELECT * 
FROM netflix_1
WHERE director is NULL or director = '';

-- 11.Find How Many Movies Actor 'Salman Khan' Appeared in the Last 10 Years 
SELECT * 
FROM netflix_1
WHERE casts = 'Salman Khan'
AND release_year = year(curdate()) - 10;

SELECT COUNT(*) AS total_movies
FROM netflix_1
WHERE typess = 'Movie'
  AND casts = '%Salman Khan%'
  AND release_year >= YEAR(CURDATE()) - 10;
