#  Weather ETL Pipeline with Airflow & Astro

This project implements an **ETL (Extract, Transform, Load)** pipeline that fetches **current weather data** for London from the **Open-Meteo API**, processes the data using Python, and loads it into a **PostgreSQL** database. The workflow is orchestrated using **Apache Airflow** and **Astro (Astronomer)**.

---

##  Features

- **Extract**: Current weather data from Open-Meteo API.
- **Transform**: Clean and structure weather data.
- **Load**: Insert into a PostgreSQL table.
- **Orchestration**: Managed with Airflow tasks and dependencies.
- **Automation**: Scheduled to run daily.

---

##  Project Structure

open-meteo-etl/
?
??? dags/
?   ??? etlweather.py         # Main ETL DAG for weather data
?
??? airflow_settings.yaml     # Airflow configuration settings
??? docker-compose.yml        # Docker Compose file to run Airflow
??? Dockerfile                # Dockerfile to build your Airflow environment
??? LICENSE                   # License file
??? README.md                 # Project documentation (this file)




---

##  Requirements

- **Airflow** (via Astro CLI or standard installation)
- **PostgreSQL** database
- Airflow connections configured:
  - `open_meteo_api` – HTTP connection to Open-Meteo
  - `postgres_default` – PostgreSQL connection

---

##  Airflow Connection Setup

### 1. `open_meteo_api`
- **Type**: HTTP
- **Host**: `https://api.open-meteo.com`

### 2. `postgres_default`
- **Type**: PostgreSQL
- **Host**: Your PostgreSQL hostname
- **Login/Password**: Your credentials
- **Schema**: target database name

You can add these connections using the Airflow UI or Astro CLI.

---

##  How It Works

### DAG: `weather_etl_pipeline`

| Step                    | Description                                        |
|-------------------------|----------------------------------------------------|
| `extract_weather_data()`  | Calls Open-Meteo API to retrieve current weather |
| `transform_weather_data()`| Extracts and cleans required fields              |
| `load_weather_data()`     | Inserts the data into a PostgreSQL table         |

Weather data includes:
- Latitude
- Longitude
- Temperature
- Wind speed
- Wind direction
- Weather code
- Timestamp (auto-generated)

---

##  How to Run

1. **Clone the repository** and navigate into it:
   ```bash
   git clone <your-repo-url>
   cd your-repo


2. Start Astro project:
astro dev start

3. Ensure connections are set up in Airflow UI under Admin > Connections.
4. Trigger the DAG manually via the Airflow UI or wait for the daily schedule.

??? Sample Output Table

Table: weather_data

latitude
longitude
temperature
windspeed
winddirection
weathercode
timestamp
51.5074
-0.1278
20.1
5.3
180
1
2025-08-06 10:00:00
## Testing & Monitoring
* View DAG runs in the Airflow UI
* Logs are available per task for debugging
* PostgreSQL DB can be inspected to verify successful data loads
## Schedule
* Frequency: Daily (@daily)
* Catchup: Disabled (catchup=False)


