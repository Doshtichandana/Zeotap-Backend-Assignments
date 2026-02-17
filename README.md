🚀 High-Throughput Fan-Out Engine
📌 Overview

This project implements a Java-based fan-out engine that reads records from a flat file and distributes them to multiple downstream systems (mock sinks).

Each sink receives data in a different transformed format and processes it with:

Rate limiting

Retry handling

Backpressure control

The system is designed to simulate real-world distributed data propagation.

✨ Features

✔ Streaming file ingestion (supports large files)
✔ Virtual thread–based concurrency (Java 21+)
✔ Sink-specific data transformations
✔ Configurable rate limits per sink
✔ Retry mechanism (max 3 attempts)
✔ Dead Letter Queue (DLQ) for failed records
✔ Periodic metrics logging

🛠 Technologies Used

Java 21+

Maven

SnakeYAML (for configuration)

Virtual Threads

BlockingQueue (for backpressure)

📁 Project Structure
HighThroughput-FanOut-Engine
│
├── pom.xml
├── application.yaml
├── sample-input.txt
└── src/main/java/com/example/fanout/

🔹 Main Components

FileProducer – Reads input file line by line

FanOutEngine – Orchestrates processing

Sink Classes – Mock REST, gRPC, MQ, and DB sinks

Transformer Classes – Handle format conversion

RetryHandler – Retry and DLQ logic

Metrics – Logs processing statistics

⚙️ Configuration

All configuration is defined in application.yaml.

You can configure:

Input file path

Queue size

DLQ path

Sink types

Rate limits

Example:
filePath: sample-input.txt
queueSize: 10000
dlqPath: dlq.txt

sinks:
  - type: REST
    rateLimit: 50
  - type: GRPC
    rateLimit: 100
  - type: MQ
    rateLimit: 200
  - type: DB
    rateLimit: 500

🔧 Build
mvn clean package

▶️ Run
java -Xmx512m -cp target/fanout-engine-1.0.0.jar com.example.fanout.Main

📊 Output

The application prints status every 5 seconds, including:

Total records processed

Throughput (records/sec)

Success count per sink

📎 Assumptions

Input file is line-based

Data transformation is simulated

Sinks are mock implementations

UTF-8 encoding is used
