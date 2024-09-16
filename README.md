
# Spotify ETL Data Pipeline

## Overview

The **Spotify ETL Data Pipeline** project scrapes data from Spotify's Global Top Songs playlist, processes the data, and stores it in Amazon S3. The extracted data is divided into distinct buckets for **artists**, **albums**, and **songs**. The project uses **Docker Compose Airflow** to orchestrate and automate the entire process.

This pipeline can be scheduled to run at specific intervals, leveraging the power of Airflow DAGs to handle extraction, transformation, and loading tasks seamlessly.

![Screenshot 2024-09-15 at 8 16 01 PM](https://github.com/user-attachments/assets/73a51161-f84e-4e24-ab2a-ac4d251c7762)

## Features

- **Data Extraction**: Scrapes data from Spotify's Global Top Songs playlist.
- **Data Transformation**: Processes the raw data and organizes it into three categories: artists, albums, and songs.
- **Data Loading**: The transformed data is uploaded to an Amazon S3 bucket for further usage or analysis.
- **Orchestration**: Apache Airflow DAG automates the ETL process, allowing for easy scheduling and monitoring.

## Technologies Used

- **Docker Compose Airflow**: Used to manage the ETL pipeline and its components.
- **Spotify API (Spotipy)**: Used to access and scrape Spotify's playlist data.
- **Amazon S3**: Cloud storage used to store the transformed data.
- **Apache Airflow Providers**: `apache-airflow-providers-amazon` package is required to interact with AWS services.
- **Python**: The core programming language used for writing the extraction, transformation, and loading scripts.

## Setup Instructions

### Prerequisites

- **Docker and Docker Compose**: Ensure you have Docker and Docker Compose installed to run Airflow.
- **AWS S3 Access**: You will need AWS credentials with appropriate permissions to create and upload data to an S3 bucket.
- **Spotify API Credentials**: Obtain your Spotify API credentials from the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/spotify-etl-data-pipeline.git
   cd spotify-etl-data-pipeline
   ```

2. Add the required dependencies for Airflow in your **Docker Compose YAML** file:

   - `spotipy` for interacting with the Spotify API.
   - `apache-airflow-providers-amazon` for connecting Airflow to Amazon S3.

   Example Docker Compose snippet:
   
   ```yaml
   services:
     airflow:
       image: apache/airflow:latest
       environment:
         - AIRFLOW__CORE__EXECUTOR=LocalExecutor
       volumes:
         - ./dags:/opt/airflow/dags
         - ./logs:/opt/airflow/logs
       ...
     pip_packages:
       - spotipy
       - apache-airflow-providers-amazon
   ```

3. Configure your environment variables for Spotify API:

   ```bash
   export SPOTIFY_CLIENT_ID='your_spotify_client_id'
   export SPOTIFY_CLIENT_SECRET='your_spotify_client_secret'
   ```

4. Configure Airflow:

   - Set up your Airflow variables for AWS and Spotify credentials.
   - Ensure you have set up your AWS S3 credentials in the `airflow.cfg` file or as environment variables.

5. Start Airflow with Docker Compose:

   ```bash
   docker-compose up
   ```

6. Open the Airflow UI:

   Once the services are running, you can access the Airflow UI by navigating to `http://localhost:8080` in your web browser. From there, you can enable and monitor the DAG execution.

## Data Flow

1. **Extract**: The pipeline scrapes the Spotify playlist and stores the raw JSON data in an S3 bucket.
2. **Transform**: The data is cleaned and categorized into artists, albums, and songs.
3. **Load**: The processed data is uploaded into separate S3 buckets for future analysis or usage.

## Future Enhancements

- **Database Integration**: Add the option to load transformed data into a SQL database for further querying.
- **Error Handling**: Add more robust error handling to capture any issues during the ETL process.
- **Data Quality Checks**: Implement data validation checks to ensure the quality of the data being processed.


