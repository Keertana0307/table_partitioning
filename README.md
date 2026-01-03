# Table Partitioning Methods Implementation

This repository contains the implementation and comparison of different **table partitioning methods** commonly used in database systems to improve query performance, data management, and scalability.

## Implemented Partitioning Methods

The following partitioning techniques are implemented in this project:

### 1. Range Partitioning
Partitions data based on a specified range of values. This method is effective for queries that frequently involve range-based conditions.

### 2. Hash Partitioning
Distributes data across partitions using a hash function applied to a partition key. This approach provides uniform data distribution and helps reduce data skew.

### 3. List Partitioning
Partitions data according to predefined lists of values. This method is suitable when data can be categorised into distinct, known groups.

### 4. Composite Partitioning
Composite partitioning combines multiple partitioning strategies to achieve better performance and flexibility.

The following composite approaches are implemented:
- **List**
- **Range + Hash**
- **Range + Key**
- **List + Key**

## Project Structure
Each partitioning method is implemented as a separate module with supporting sub-components to ensure clarity, modularity, and ease of execution.

```bash
python main.py
