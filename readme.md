# Lyft Toronto Rider Status Management

## Overview

Lyft Toronto Rider Status Management is a Node.js project that utilizes Apache Kafka for real-time tracking and management of rider statuses. The project revolves around the `rider-status` Kafka topic, which is divided into two partitions corresponding to the North Toronto and South Toronto regions.

## Use Case

The `rider-status` topic allows Lyft Toronto to monitor and respond to real-time changes in rider status, from ride requests to pickups and drop-offs. The partitioning of the topic into North and South Toronto enables efficient handling of region-specific events.

### Partitions

1. **North Toronto Partition**: Manages rider status updates specific to the North Toronto region.

2. **South Toronto Partition**: Manages rider status updates specific to the South Toronto region.

## Prerequisites

Before running the Lyft Toronto Rider Status Management project, ensure that you have the following prerequisites:

### Knowledge

- Intermediate level knowledge of Node.js
- Experience with designing distributed systems

### Tools

- [Node.js](https://nodejs.org/): Download and install Node.js
- [Docker](https://www.docker.com/): Download and install Docker
- [VSCode](https://code.visualstudio.com/): Download and install Visual Studio Code

## Getting Started

Follow these steps to set up the project:

1. **Start Zookeeper Container**: Run the following command to start a Zookeeper container and expose port 2181:

    ```bash
    docker run -p 2181:2181 zookeeper
    ```

2. **Start Kafka Container**: Execute the following command to start a Kafka container, expose port 9092, and configure the necessary environment variables:

    ```bash
    docker run -p 9092:9092 \
    -e KAFKA_ZOOKEEPER_CONNECT=<PRIVATE_IP>:2181 \
    -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://<PRIVATE_IP>:9092 \
    -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
    confluentinc/cp-kafka
    ```

    Replace `<PRIVATE_IP>` with the appropriate IP address.

3. **Run Node.js Application**: Start the Node.js application to interact with Kafka and manage rider status updates:

    ```bash
    npm install
    node admin.js
    node producer.js
    node consumer.js <user-name>
    ```

Adjust the application code as needed to suit your specific use case.

## License

This project is licensed under the [MIT License](LICENSE).
