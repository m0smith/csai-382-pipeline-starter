# CSAI-382 · Week 2 · Lab 2.6 — Curated Data Set

This repository is a template for your Databricks lab submission. Replace the placeholder text with your own notes and screenshots as you work through the assignment.

## Student Information
- **Name:** _Your Name_
- **Section / Instructor:** _e.g., Section 1 — Prof. Smith_
- **Date Submitted:** _MM/DD/YYYY_

## Objective
Transform the sample **DeviceMessage** (sensor-level) and **RapidStepTest** (test-level) JSON datasets into a single machine learning training table. You will validate schemas, perform time-window joins, engineer features, design labels, export results, and run lightweight quality checks.

## Prerequisites
- Databricks Community or institutional workspace with a Python cluster
- Familiarity with PySpark DataFrames
- Access to the sample JSON listed in this README

## Getting Started
1. Open Databricks and create a new Python notebook.
2. Copy the **Sample Data Setup** cell below into the first notebook cell (or upload JSON files).
3. Work through each lab part (A–F), documenting your progress and observations directly in the notebook.

## Sample Data Setup
```python
# ---------- SAMPLE DATA (edit/extend as needed) ----------
device_json = [
  {
    "messageOrigin": "DEVICE",
    "sessionKey": None,
    "message": "Test Completed",
    "deviceId": "007",
    "date": 1659538351527,
    "sensorType": "ultraSonicSensor",
    "distance": "1cm",
    "timestamp": 1659538351527
  }
]

rapid_json = [
  {
    "token": "8bd85cf8-b4ae-4de0-9475-1ee19bdc517d",
    "startTime": 1741118938636,
    "stepPoints": [1764, 1016, 950, 797, 819, 653, 695, 677, 702, 703, 786, 711, 782, 654, 619, 604, 695, 638, 623, 643, 698, 649, 611, 686, 638, 685, 559, 767, 620, 612],
    "stopTime": 1741118960692,
    "testTime": 22056,
    "totalSteps": 30,
    "customer": "scmurdock@gmail.com",
    "deviceId": "007"
  }
]
# --------------------------------------------------------

from pyspark.sql import functions as F, types as T

device_schema = T.StructType([
    T.StructField("messageOrigin", T.StringType(), True),
    T.StructField("sessionKey", T.StringType(), True),
    T.StructField("message", T.StringType(), True),
    T.StructField("deviceId", T.StringType(), True),
    T.StructField("date", T.LongType(), True),
    T.StructField("sensorType", T.StringType(), True),
    T.StructField("distance", T.StringType(), True),
    T.StructField("timestamp", T.LongType(), True)
])

rapid_schema = T.StructType([
    T.StructField("token", T.StringType(), True),
    T.StructField("startTime", T.LongType(), True),
    T.StructField("stepPoints", T.ArrayType(T.IntegerType()), True),
    T.StructField("stopTime", T.LongType(), True),
    T.StructField("testTime", T.LongType(), True),
    T.StructField("totalSteps", T.IntegerType(), True),
    T.StructField("customer", T.StringType(), True),
    T.StructField("deviceId", T.StringType(), True)
])

device_df = spark.createDataFrame(device_json, schema=device_schema)
rapid_df  = spark.createDataFrame(rapid_json,  schema=rapid_schema)
```

## Lab Tasks
Document your work under the headings below. Include code snippets, results, and short reflections where appropriate.

### Part A — Validate & Clean
- Cast columns, parse units, and confirm required fields.
- Record any data-quality concerns.

### Part B — Join by Time Window
- Join **DeviceMessage** and **RapidStepTest** on `deviceId` and overlapping timestamp ranges.
- Note assumptions made for missing `deviceId` or timing edge cases.

### Part C — Aggregate Sensor Readings
- Aggregate distances per test and compute `n_readings`, `avg`, `min`, `max`, and `variance` of `distance_cm`.
- Describe any additional feature ideas.

### Part D — Step Features & Labels
- Create cadence features (`mean_step_ms`, `std_step_ms`, `cadence_steps_per_min`).
- Choose a label (e.g., regression on `totalSteps`, classification on cadence buckets) and justify the choice.

### Part E — Save Outputs
- Export features as Delta and CSV (`/tmp/rapid_features_delta`, `/tmp/rapid_features_csv`).
- Include screenshots or file listings showing the saved outputs.

### Part F — Quality Checks
- Confirm required columns exist, the dataset is non-empty, and `testTime` aligns with `stopTime - startTime` within ±50 ms.
- Document the assertions used and their results.

## Reflection Prompts (5–8 Sentences)
Address the following in your notebook and summarize here:
1. Which engineered features were most informative and why?
2. What challenges did you encounter while cleaning or joining the datasets?
3. How would you improve data quality in future iterations?
4. Ethics: Discuss privacy risks (sensor + identity), mitigation strategies, fairness considerations, and maintaining integrity in AI work.

## Submission Checklist
- [ ] Notebook includes Parts A–F with explanations and results.
- [ ] Features saved as both Delta and CSV formats.
- [ ] Quality checks executed and passing.
- [ ] Reflection completed.
- [ ] Repository README updated with personal notes (optional but encouraged).

## Honor Code Reminder
Use Databricks AI helpers responsibly. Read, understand, and verify generated code before submission. Act with integrity, verify truth, respect privacy, and focus on learning how results are produced—not just obtaining them.

