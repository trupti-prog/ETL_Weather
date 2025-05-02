ETL_Weather
================
To build ETL Weather Pipeline using AirFlow and Astro.

**1) Problem**
   
Astro platform manages the entire Airflow to schedule the workflow of pipeline which needs to be run daily, weekly, monthly, as to get the data continuously from all the particular sources(DB, IOT & Paid APIs).

**2) Data**

The data we're using is from Open-Meteo API.

**3) Libraries**

1. airflow
2. airflow.providers.http.hooks.http
3. airflow.providers.postgres.hooks.postgres
4. airflow.decorators
5. airflow.utils.dates
6. json

**4) About**

In this project, we will create ETL data pipelines. We will combine all the sources of data and perform some kind of transformation. The entire data is converted into JSON/ Dataframe and we load this data into some other source(PostgreSQL). Sources of data keeps on getting updated with respect to time. (For example- Today we have some other data. Tomorrow the IOT devices may create more data). Hence, it is important to run this ETL pipeline regularly. 'ASTRO' is a platform called as ASTRONOMER.IO. It manages the entire airflow, because if we want to run Airflow in the form of Dockers and all, astronomer plays a very good role. Let say, will be having an API, we will read the data from API, will do some kind of transformation, will be loading some kind of database, deploy this with Astro and AWS and using some cloud 'ASTRO CLOUD PLATFORM'. We will pull the data from API performing Transformation, then take the data and try to push this into PostgreSQL. We have longitude & latitude, based on that will use the weather app API to get some climatic information about particular place. We are using DBeaver to connect with PostgreSQL DB. We get 4 docker containers after running 'astro dev start' command. 

- <ins>Postgres</ins>: Airflow's Metadata Database
- <ins>Webserver</ins>: The Airflow component responsible for rendering the Airflow UI
- <ins>Scheduler</ins>: The Airflow component responsible for monitoring and triggering tasks
- <ins>Triggerer</ins>: The Airflow component responsible for triggering deferred tasks

Astro project contains the following files and folders:

- `dags`: This folder contains the Python files for Airflow DAGs(DIRECTED ACYCLIC GRAPH). By default, this directory includes one example DAG:
    - `exampledag`: This DAG shows a simple ETL pipeline example that queries the list of astronauts currently in space from the Open Notify API and prints a statement for each astronaut. The DAG uses the TaskFlow API to define tasks in Python, and dynamic task mapping to dynamically print a statement for each astronaut.
    - `etlweather`: Create a folder named 'ETLWeather', as API we are going to use is from Open-Meteo for 'weather'. We will install the Astro CLI and initialize the astro project pulling flow development files from Astro runtime 12.1.1 and initialize an empty Astro project in this particular folder loc. Here, we are reading some APIs, getting the data and displaying it.
- `Dockerfile`: This file contains a versioned Astro Runtime Docker image that provides a differentiated Airflow experience.
- `include`: This folder contains any additional files. It is empty by default.
- `packages.txt`: Install OS-level packages needed for project by adding them to this file. It is empty by default.
- `requirements.txt`: Install Python packages needed for project by adding them to this file. It is empty by default.
- `plugins`: Add custom or community plugins for project to this file. It is empty by default.
- `airflow_settings.yaml`: Use this local-only file to specify Airflow Connections, Variables, and Pools instead of entering them in the Airflow UI as we develop DAGs in this project.
- `docker_compose.yml`: If we want to run PostgreSQL in local, we need to run it as a container.


Entire DAG Pipeline will display like this, provides entire UI. For Graph, what all things we really need to run in the form of task. 

![Screenshot (228)](https://github.com/user-attachments/assets/fef2e80f-98f9-4b92-a4e9-34353dd30b5a)

![Screenshot (229)](https://github.com/user-attachments/assets/cc1ccf66-a4cb-4028-afb2-cb892e857bcd)

We need to setup connection for any error occured. Connections- postgres_default and open_meteo_api. Now execute the weather_etl_pipeline in DAG and it will get succeed. 

![Screenshot (232)](https://github.com/user-attachments/assets/cc74c634-9217-4b6f-8978-985e792d1484)

![Screenshot (233)](https://github.com/user-attachments/assets/f5903bde-4444-42e5-9f1e-3a13b62adc46)

![Screenshot (236)](https://github.com/user-attachments/assets/b044bfa0-3059-4ba6-afef-f07cb783b4df)

To take this into Deployment- Create PostgreSQL in AWS and update endpoint in the connection. It will automatically get saved in DB present in the AWS. 
