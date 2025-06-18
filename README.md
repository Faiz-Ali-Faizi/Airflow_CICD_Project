# ✈️ Flight Booking Data Pipeline (GCP + GitHub CI/CD)

This project automates a modern data pipeline using **Apache Airflow**, **PySpark**, and **Google Cloud Platform (GCP)** — powered by **GitHub Actions** for CI/CD. It transforms raw flight booking data stored in **Google Cloud Storage (GCS)**, processes it using **Dataproc Serverless**, and loads analytical insights into **BigQuery**.

---

## 📌 Key Features

- ✅ Fully automated CI/CD via GitHub Workflows
- 🌀 Environment-based deployments (`dev` & `main`)
- 🗂 Data orchestration using Apache Airflow (GCP Composer)
- ⚡ Serverless PySpark transformations on Dataproc
- 📊 Scalable insights delivered to BigQuery

---

## 🧠 Architecture


## 🛠 Tech Stack
Component	          Technology
Orchestration	      Apache Airflow (Composer)
Transformations	    PySpark on Dataproc Serverless
Cloud Platform	    Google Cloud Platform (GCP)
Storage	            Google Cloud Storage (GCS)
Warehouse	          Google BigQuery
CI/CD	              GitHub Actions


🔁 End-to-End Flow

1-CSV file is uploaded to GCS at:
gs://airflow-projetcs-gds/airflow-project-1/source-{env}/flight_booking.csv

2-Airflow DAG detects the file and triggers a Dataproc Serverless job.

3-PySpark Job performs:

 *Data cleaning and enrichment

 *Feature engineering (e.g. is_weekend, lead_time_category, booking_success_rate)

 *Aggregations by route and origin

4-BigQuery Tables:

 *transformed_flight_data_*

 *route_insights_*

 *origin_insights_*

5-GitHub Actions handles automated deployment of DAGs and environment configs to GCP Composer.



## 🔧 Airflow DAG

Tasks:

1-GCSObjectExistenceSensor: Waits for file in GCS.
2-DataprocCreateBatchOperator: Triggers PySpark job.

## 🔥 PySpark Logic
File: spark_transformation_job.py

Core Logic:
1-Reads CSV from:
gs://airflow-projetcs-gds/airflow-project-1/source-{env}/flight_booking.csv

2-Adds derived features:

is_weekend

lead_time_category

booking_success_rate

3-Computes insights:

Bookings, average flight duration by route

Booking success rate and lead time by origin

4-Writes all data to BigQuery tables:

transformed_flight_data_*

route_insights_*

origin_insights_*

## ⚙️ CI/CD via GitHub Actions
Trigger:

Push to dev or main branch
Actions:
1-Authenticate with GCP

2-Deploy DAG to Composer

3-Push environment-specific variables to Airflow


## 🧪 Running the Pipeline
Upload CSV to GCS:

`gsutil cp flight_booking.csv gs://airflow-projetcs-gds/airflow-project-1/source-dev/`

## 🔐 IAM Permissions Required
Make sure your Dataproc Serverless service account has:

1-roles/dataproc.editor

2-roles/bigquery.dataEditor

3-roles/storage.objectViewer

4-roles/composer.user



