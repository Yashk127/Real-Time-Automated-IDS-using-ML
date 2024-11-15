# Automated Real-Time Network Intrusion Detection System (IDS) with Machine Learning

This project implements a fully automated **Real-Time Network Intrusion Detection System (IDS)** using **Machine Learning** to classify network traffic into various attack categories, such as **Denial of Service (DoS)**, **Probe**, **Remote to Local (R2L)**, and **User to Root (U2R)**. The system captures packets, processes them, extracts key features, and classifies them using a neural network model.

## Features

- **Real-Time Detection**: The system processes packets in real-time using Scapy to capture and analyze network traffic.
- **Automated Pipeline**: The entire pipeline is automated, from packet capture to classification, using a batch processing approach and queue data structure for efficient data management.
- **Multi-Class Classification**: The system classifies network traffic into multiple attack types using a neural network model.
- **Threading for Concurrency**: The system uses multithreading for concurrent packet sniffing and data processing, ensuring the real-time operation of the IDS.

## Features Used for Classification

The system uses several network traffic features to classify the network packets, which are extracted and processed before being passed to the machine learning model for classification:

1. **dur**: Duration of the connection (time between first and last packet).
2. **proto**: The protocol used in the packet (TCP, UDP, ICMP, etc.).
3. **service**: The type of service the packet is associated with (HTTP, DNS, etc.).
4. **state**: The state of the connection (e.g., ESTABLISHED, CLOSED).
5. **sbytes**: The number of bytes sent by the source IP.
6. **dbytes**: The number of bytes sent by the destination IP.
7. **sttl**: Time-To-Live (TTL) value of the source IP.
8. **dttl**: TTL value of the destination IP.
9. **sload**: Source load (average size of packets sent).
10. **dload**: Destination load (average size of packets received).
11. **spkts**: Number of packets sent by the source IP.
12. **dpkts**: Number of packets received by the destination IP.
13. **smean**: The mean packet size for the source IP.
14. **dmean**: The mean packet size for the destination IP.
15. **ct_srv_src**: The number of connections to the same service from the source.
16. **ct_srv_dst**: The number of connections to the same service from the destination.
17. **ct_dst_ltm**: The number of connections made to the destination within the last time interval.

Each of these features is carefully selected based on their relevance to network traffic patterns and potential attack indicators. These features help the model distinguish between normal network behavior and potential malicious activity.

## Project Overview

### Packet Capture
The system uses **Scapy** to sniff and capture packets from the network in real-time. The packets are then parsed to extract relevant features, such as IP address, protocol, TTL, bytes transferred, and packet counts.

### Feature Extraction
For each packet, the features listed above are extracted and stored for processing. The system ensures that the data is prepared and formatted correctly before being passed to the model for prediction.

### Data Preprocessing
Before feeding the data into the neural network, feature scaling is applied using **StandardScaler** to normalize the values, ensuring that the model performs optimally. The system uses **queue data structures** to manage data processing in batches, ensuring that the system remains efficient while processing a large number of packets.

### Model Training
The machine learning model used for classification is a **Neural Network** built using **Keras**. The network is trained on labeled datasets that contain known attack types. The model learns to classify network traffic into categories like DoS, Probe, R2L, and U2R based on the extracted features.

### Automated Pipeline
The entire process of packet capture, feature extraction, preprocessing, model prediction, and classification is fully automated. This end-to-end pipeline allows the IDS to operate without manual intervention. The automated pipeline handles incoming packets in real-time, processes them, and classifies them into the appropriate attack category.

### Real-Time Classification
After training, the system is ready to classify live network traffic. As new packets are captured, they are processed through the pipeline, and predictions are made using the trained neural network model. The system can detect and identify attacks in real-time and can be configured to raise alerts or take other actions based on the classification results.

## Key Techniques Used

- **Multithreading**: Utilized for concurrent packet sniffing and data processing to ensure that the IDS operates in real-time without delays.
- **Machine Learning**: A neural network model is used to classify the network traffic into different attack categories, providing an effective way to detect a variety of attacks based on historical data and learned patterns.
- **Scapy**: A powerful Python library used for packet capturing, which allows deep customization and flexible handling of network traffic.
- **Keras**: Used for building and training the neural network model, providing a simple yet effective way to implement and train deep learning models.
- **Queue Data Structure**: Employed to handle the processing of packet data in batches, which is crucial for real-time performance.
