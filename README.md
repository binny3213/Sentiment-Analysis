# 🧠 Real-Time Sentiment Analysis with Spring WebFlux, Kafka & NewsAPI

This project is a **reactive real-time sentiment analysis system** that fetches news articles in real-time, analyzes their sentiment, and streams the results using **Kafka** and **Spring WebFlux**.

Originally based on Twitter stream, the project was adapted to use **NewsAPI** due to access restrictions on Twitter.

---

## 🎯 Project Goal

Build a real-time, scalable system to:
- Ingest news data in real-time
- Perform sentiment analysis on article contents
- Stream results live to Kafka consumers
- Reactively expose the data via a REST API

---

## ⚙️ Tech Stack

![Java](https://img.shields.io/badge/Java-17-blue)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.0-brightgreen)
![Maven](https://img.shields.io/badge/Maven-3.9.9-red)
![Kafka](https://img.shields.io/badge/Kafka-Message_Queue-orange)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ed)
![Docker Compose](https://img.shields.io/badge/Docker--Compose-Orchestration-blue)
![Swagger](https://img.shields.io/badge/Swagger-Enabled-yellowgreen)

---

## 🚀 Why Kafka?

Apache Kafka was chosen for:
- **Scalability** – supports multiple producers/consumers
- **Asynchronous communication** – decouples data producers and consumers
- **High throughput** – efficient for large volumes of real-time data
- **Fault tolerance** – built-in replication and durability

Kafka helps distribute sentiment analysis tasks and consumer dashboards independently, enhancing **parallelism and responsiveness**.

---

## ⚡️ Why Reactive Programming?

Spring WebFlux and **Project Reactor** provide a **non-blocking** and **asynchronous** model that enables:
- Handling thousands of concurrent requests efficiently
- Streaming results using `Flux` instead of waiting for full computation
- Fine-grained backpressure control using `Publisher-Subscriber` pattern

Using `Mono` and `Flux`, the API exposes real-time streams of sentiment data in a highly performant manner.

---

## 🧪 Main Endpoints

| Endpoint                     | Description |
|-----------------------------|-------------|
| `/sendKafka?text=...`       | Sends a message to Kafka topic |
| `/getKafka`                 | Streams messages from Kafka |
| `/startTwitter?text=...`    | Starts NewsAPI stream for a keyword |
| `/stopTwitter`              | Gracefully stops the stream |
| `/grouped?text=...`         | Groups messages into time windows |
| `/sentiment?text=...`       | Streams messages with average sentiment per window |

> Note: Twitter was replaced by **NewsAPI**, providing rich article data from global news sources.

---

## 🧠 Sentiment Analysis

The system uses **Stanford CoreNLP** to compute a sentiment score for each article sentence.

Scores range from **-1 (very negative)** to **+1 (very positive)**, and average scores are calculated per time window.

---

## 🧰 Project Structure

```text
src/
 └── main/
     ├── java/com/handson/sentiment/
     │   ├── controller/        # REST endpoints
     │   ├── kafka/             # Kafka producer and receiver logic
     │   ├── nlp/               # Sentiment analysis using CoreNLP
     │   └── twitter/           # NewsAPI stream (replacing Twitter)
     └── resources/
         └── application.properties
