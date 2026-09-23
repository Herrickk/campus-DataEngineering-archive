# Goodreads Book Rating - Data Engineering & ML Pipeline

## Overview
This is a university project where we built an ETL pipeline to process a Goodreads dataset from Kaggle into a Star Schema. After the data is cleaned and structured, we used a Random Forest model to predict if a book will get a "High" or "Low" rating.

## Tools Used
* ETL: Pentaho Data Integration (Spoon)
* Database: MySQL
* Machine Learning: Python (Random Forest)

## Data Architecture
We modeled the data into a Star Schema to make it easier for analytical queries. It consists of 1 Fact table and 5 Dimension tables:
* Dim Author, Dim Book, Dim Publisher, Dim Language, Dim Time.

![Star Schema Diagram](docs/star_schema_diagram.png)

## ETL Process
The ETL process is built using Pentaho. We extracted the raw CSV, cleaned the data (like splitting multiple authors into separate rows), and generated surrogate keys. Everything is automated using a single Master Job (.kjb) that runs all transformations (.ktr) sequentially.

![Pentaho Job](docs/pentaho_job_orchestration.png)

## Machine Learning Results
We trained a Random Forest classifier to predict book ratings (Low <= 3.9, High >= 4.0).
* Accuracy: 94%
* Key Finding: A book's page count and publication year affect the rating more than the author or publisher's name.

You can read the full analysis in the `docs/Data_Engineering_Final_Report.pdf`.

## Note on Data Duplication
The attached ML report was trained on an earlier version of the pipeline that had a duplication bug (resulting in ~88k rows). The Pentaho files uploaded in this repository have been fixed and now correctly output the clean ~11,000 unique records.
