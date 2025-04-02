# Real-Time Ride-Sharing Analytics with Apache Spark

This project demonstrates a real-time analytics pipeline for a ride-sharing platform using Apache Spark Structured Streaming. It processes simulated live ride-sharing data, performs real-time aggregations, and analyzes trends using time-based windows.

---

## 📁 Project Structure

```
ride-sharing-analytics/
├── data_generator.py              # Python script to simulate streaming data
├── task1_streaming_ingestion.py  # Task 1: Ingest and parse streaming data
├── task2_driver_aggregations.py  # Task 2: Real-time driver-level aggregations
├── task3_windowed_analytics.py   # Task 3: Time-windowed fare trend analysis
├── output/                       # Output directory for CSV files
├── checkpoints/                  # Checkpoint directory for stateful operations
└── README.md                     # This file
```

---

## 🧪 Data Format
Each line of simulated data is a JSON string:
```json
{
  "trip_id": "t123",
  "driver_id": "d456",
  "distance_km": 12.5,
  "fare_amount": 25.0,
  "timestamp": "2025-04-01T17:45:00"
}
```

---

## ▶️ How to Run

### Step 1: Install Dependencies
```bash
pip install pyspark
pip install faker
```

### Step 2: Start Data Generator
In one terminal:
```bash
python data_generator.py
```

This will stream data to `localhost:9999`.

### Step 3: Run Spark Tasks

> Make sure you have Apache Spark installed and `spark-submit` available in your terminal.

#### ✅ Task 1: Streaming Ingestion and Parsing
```bash
spark-submit task1_streaming_ingestion.py
```
This will print parsed records to the console.

#### ✅ Task 2: Real-Time Driver Aggregations
```bash
spark-submit task2_driver_aggregations.py
```
This performs real-time aggregations (total fare, average distance) per driver and writes results to:
```
output/driver_aggregations/
```

#### ✅ Task 3: Windowed Time-Based Fare Analysis
```bash
spark-submit task3_windowed_analytics.py
```
This computes total fare over 5-minute windows sliding every 1 minute, and writes to:
```
output/windowed_analytics/
```

---

## 📝 Tasks Overview

### Task 1: Ingestion and Parsing
- Reads streaming data from a socket.
- Parses JSON into structured columns.
- Outputs to console.

### Task 2: Real-Time Aggregations
- Groups by `driver_id`.
- Calculates:
  - Total fare per driver
  - Average distance per driver
- Outputs to CSV.

### Task 3: Time Windowed Analysis
- Converts timestamps to `TimestampType`.
- Aggregates `fare_amount` over 5-minute windows, sliding every 1 minute.
- Outputs to CSV.

---

## 📦 Output Example (CSV)
Sample row from task3 output:
```
"[2025-04-01 17:40:00,2025-04-01 17:45:00]", 210.0
```
Where the first column is the time window, and the second is the total fare.

---

## ✅ Requirements
- Python 3.8+
- Apache Spark 3.x
- PySpark (`pip install pyspark`)
- Faker (`pip install faker`)

---

## 📌 Notes
- Use separate terminals for the data generator and each Spark job.
- Make sure output and checkpoint directories are writable.
- Socket source is for development/demo only — not suitable for production.

---


## 📚 References
- [Apache Spark Structured Streaming Documentation](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)

