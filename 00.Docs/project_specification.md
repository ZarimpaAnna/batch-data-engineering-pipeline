# Project Specification

This project simulates a batch data engineering workflow involving structured CSV ingestion and relational data integration.

This project was originally developed as part of a technical evaluation exercise and later refactored into a standalone data engineering pipeline.

## Objective

To design and implement a Spark-based ETL pipeline that:

- Cleans and validates subscriber data
- Persists cleaned data to a relational database
- Processes transactional data
- Joins transactional records with subscriber metadata
- Produces parquet outputs for downstream analytics
- Handles unmatched records with retry logic

## Core Concepts Demonstrated

- Spark DataFrame transformations
- Schema enforcement and type casting
- Relational persistence (PostgreSQL)
- Deterministic key generation
- Incremental reprocessing logic
- Containerized execution environment
