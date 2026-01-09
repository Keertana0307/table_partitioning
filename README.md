# Comparing Different Strategies for Efficient Storage and Querying in Large Database
**Objective**: 
- Evaluate how MySQL partitioning methods manage and query large datasets efficiently.
- Demonstrate how the same large dataset is stored in MongoDB.
- Compare these two strategies in terms of data storage and query handling.

This repository contains the implementation different table partitioning methods using MySQL and implementation of storing and querying using MongoDB.


## Implemented Partitioning Methods using MySQL

### 1. Range Partitioning
Partitions data based on a specified range of values. This method is effective for queries that frequently involve range-based conditions.

### 2. Hash Partitioning
Distributes data across partitions using a hash function applied to a partition key. This approach provides uniform data distribution and helps reduce data skew.

### 3. List Partitioning
Partitions data according to predefined lists of values. This method is suitable when data can be categorised into distinct, known groups.

### 4. Composite Partitioning
Composite partitioning combines multiple partitioning strategies.

The following composite approaches are implemented:
- **Range + Hash**
- **Range + Key**
- **List + Key**

## Implemented Data Storing and Querying using MongoDB

