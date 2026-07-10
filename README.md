# Google Cloud Pub/Sub Order Processing System

## Overview

This project demonstrates a complete **event-driven messaging pipeline** using **Google Cloud Pub/Sub** and **Python**. It consists of two applications:

- **Producer (Publisher)** – Generates realistic mock e-commerce order data and publishes it to a Pub/Sub topic.
- **Consumer (Subscriber)** – Continuously listens to the Pub/Sub subscription, processes incoming JSON messages, and acknowledges them after successful processing.

This project showcases the fundamentals of asynchronous messaging, real-time data ingestion, and cloud-native application development on Google Cloud Platform (GCP).

---

## Architecture

```
                    +----------------------+
                    |   Python Producer    |
                    | (Publishes Orders)   |
                    +----------+-----------+
                               |
                               |
                               ▼
                    +----------------------+
                    | Google Cloud Pub/Sub |
                    |      Topic           |
                    +----------+-----------+
                               |
                               |
                               ▼
                    +----------------------+
                    | Pub/Sub Subscription |
                    +----------+-----------+
                               |
                               |
                               ▼
                    +----------------------+
                    |   Python Consumer    |
                    | Processes Messages   |
                    +----------------------+
```

---

## Features

### Producer

- Generates realistic mock order data
- Publishes JSON messages to a Pub/Sub topic
- Asynchronous publishing with callback support
- Simulates streaming data every two seconds
- Displays published message IDs

### Consumer

- Pulls messages from a Pub/Sub subscription
- Deserializes JSON payloads
- Processes messages in batches
- Acknowledges successfully processed messages
- Prevents duplicate message delivery
- Runs continuously until stopped

---

## Technologies Used

- Python 3.x
- Google Cloud Platform (GCP)
- Google Cloud Pub/Sub
- Google Cloud SDK
- JSON
- Event-Driven Architecture

---

## Project Structure

```
gcp-pubsub-order-processing/
│
├── producer.py
├── consumer.py
├── requirements.txt
└── README.md
```

---

## Prerequisites

Before running the project, ensure you have:

- Google Cloud Platform account
- Google Cloud Project
- Pub/Sub API enabled
- Pub/Sub Topic
- Pub/Sub Subscription
- Python 3.9+
- Google Cloud SDK installed
- Service Account credentials

---

## Installation

### Clone the repository

```bash
git clone https://github.com/yourusername/gcp-pubsub-order-processing.git

cd gcp-pubsub-order-processing
```

### Install dependencies

```bash
pip install -r requirements.txt
```

or

```bash
pip install google-cloud-pubsub
```

---

## Authentication

Create a Google Cloud Service Account with Pub/Sub permissions and download the JSON key.

### Windows

```powershell
set GOOGLE_APPLICATION_CREDENTIALS=C:\path\service-account.json
```

### Linux / macOS

```bash
export GOOGLE_APPLICATION_CREDENTIALS="/path/service-account.json"
```

---

## Configuration

Update the following values in both scripts.

### Producer

```python
project_id = "your-project-id"
topic_name = "your-topic-name"
```

### Consumer

```python
project_id = "your-project-id"
subscription_name = "your-subscription-name"
```

---

# Running the Project

## Step 1 — Start the Consumer

```bash
python consumer.py
```

The consumer begins listening for incoming messages.

Example output:

```text
{
    "order_id": 1,
    "customer_id": 412,
    "item": "Laptop",
    "quantity": 3,
    "price": 1099.95,
    "shipping_address": "123 Main St, City A, Country",
    "order_status": "Pending",
    "creation_date": "2024-11-30"
}
==================
```

---

## Step 2 — Start the Producer

Open another terminal.

```bash
python producer.py
```

Example output:

```text
Published message with ID:
1028347562849375

Published message with ID:
1028347562849376
```

Every two seconds a new order is published to Pub/Sub.

---

## Sample Order Message

```json
{
    "order_id": 1,
    "customer_id": 412,
    "item": "Laptop",
    "quantity": 2,
    "price": 1099.99,
    "shipping_address": "123 Main St, City A, Country",
    "order_status": "Pending",
    "creation_date": "2024-11-30"
}
```

---

## How the Producer Works

1. Creates a Pub/Sub Publisher client.
2. Generates random e-commerce order data.
3. Converts the data into JSON.
4. Publishes the message to a Pub/Sub topic.
5. Waits for confirmation from Google Cloud.
6. Prints the generated Message ID.
7. Repeats every two seconds.

---

## How the Consumer Works

1. Connects to the Pub/Sub subscription.
2. Pulls up to ten messages at a time.
3. Decodes the message payload.
4. Converts JSON into a Python dictionary.
5. Processes and prints the message.
6. Acknowledges processed messages.
7. Waits for additional messages.

---

## Event Flow

```
Generate Order
      │
      ▼
Serialize to JSON
      │
      ▼
Publish to Pub/Sub Topic
      │
      ▼
Subscription Receives Message
      │
      ▼
Consumer Pulls Message
      │
      ▼
Deserialize JSON
      │
      ▼
Process Order
      │
      ▼
Acknowledge Message
```

---

## Requirements

Create a `requirements.txt` file.

```text
google-cloud-pubsub>=2.20.0
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Skills Demonstrated

This project demonstrates practical experience with:

- Google Cloud Pub/Sub
- Event-Driven Architecture
- Publisher–Subscriber Pattern
- Cloud Messaging
- JSON Serialization
- Python Programming
- Asynchronous Publishing
- Cloud Authentication
- Real-Time Data Streaming
- Message Acknowledgement
- Distributed Systems Fundamentals

---

## Future Enhancements

- Store orders in BigQuery
- Stream data into Cloud Storage
- Deploy using Cloud Run
- Containerize with Docker
- Add structured logging
- Implement retry policies
- Configure Dead Letter Topics
- Add unit and integration tests
- Build a real-time monitoring dashboard
- Integrate with Apache Beam or Dataflow for stream processing

---

## Author

**Bartequa Blackmon**

**Data Engineer | Cloud Engineer | Python Developer**

### Technical Skills

- Google Cloud Platform (GCP)
- Pub/Sub
- Python
- Apache Spark
- Databricks
- Snowflake
- SQL
- ETL Pipelines
- Data Warehousing
- Cloud Computing

---

## License

This project is licensed under the MIT License.