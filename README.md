# Batch Data Engineering Pipeline

This repository contains a batch data engineering pipeline built with PySpark and PostgreSQL. The project demonstrates data cleaning, relational integration, and parquet export in a containerized environment.

## Architecture Overview

1. Raw CSV ingestion  
2. Data cleansing & transformation using PySpark  
3. Persistence to PostgreSQL  
4. Join operations and validation  
5. Parquet file generation  
6. Handling of unmatched records with retry logic  

---

## Technical aspects

- **Language:** Python  
- **Framework:** PySpark  
- **Database:** PostgreSQL (Dockerized)  
- **Containerization:** Docker & Docker Compose  
- **Environment:** Jupyter PySpark Notebook  
- **Version Control:** Git 

---

## Project Structure

```
Batch_Data_Engineering_Pipeline/
├── OO.Docs/                                              
│   ├── project_specification.md
│ 
├── O1.Data/                                       # Initial csv files
│   ├── data_transactions.csv  
│   ├── subscribers.csv   
│ 
├── OO.Spark_app/
│   ├── Subscribers.ipynb                           # Cleans and writes subscribers data to PostgreSQL
│   ├── Transactions_join.ipynb                     # Cleans transactions, performs join, handles unmatched entries and produces parquet file
│ 
├── O3.Parquet_files/                               # Parquet files are saved here. Generated parquet files are not version-controlled and will be created locally during execution.
│ 
├── README.md                                       # Project information and instructions
├── docker-compose.yaml                             # To initiate docker services (Postgres & Jupyter)
├── .gitignore                                      # Ignore .env file, checkpoints etc.
├── .env                                            # Created but not used (For demonstration purposes, database credentials are defined locally.)

```

---

## Steps Implemented

### 1. Subscribers Notebook

- Cleaned duplicate `subscriber_id` entries, keeping only the most recent based on `activation_date`
- Casted data types appropriately
- Wrote the cleaned database to PostgreSQL (`subscribers` table)

### 2. Transactions Notebook

- Cleaned nulls and casted `timestamp`, `subscriber_id`, and `amount` columns
- Joined transactions with the `subscribers` table on `subscriber_id`
- Extracted unmatched records and saved them in a separate PostgreSQL table(`unmatched_transactions`). On every run, previous unmatched entries are rechecked and merged with the new data to verify if matching subscribers have been added.
- Final dataset is written to Parquet format file


## How to Run

1. **Clone the repository**

```bash
git clone https://github.com/your-username/Batch_Data_Engineering_Pipeline.git
cd Batch_Data_Engineering_Pipeline
```

2. **Start the Docker containers (PostgreSQL & Jupyter Notebook)**

```bash
docker-compose up -d
```

3. **Access Jupyter Notebook**

- Visit `http://localhost:8888` and open the notebooks located in the designated folder
- To find the Jupyter access token run the following command according to your shell type and paste it in the browser when prompted:

```bash
docker logs pyspark_notebook_batch 2>&1 | grep token (Git Bash/Linux/macOS)
docker logs pyspark_notebook_batch 2>&1 | findstr token (PowerShell)
```
---

## Notes

- For demonstration purposes, database credentials are defined locally into the yaml file and inside the notebooks. 
- In production scenarios, environment variables or secret management tools should be used.

---

## Author

Anna Zarimpa

---

## Contact information

- Email: annazarimpa@gmail.com
- LinkedIn: linkedin.com/in/annazarimpa
- Github: github.com/ZarimpaAnna
---

