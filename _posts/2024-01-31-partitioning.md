---
title: "Partitioning"
tags: [design]
image: partition.png
featured: "true"
---

### | Design Topic - Partitioning | :heavy_division_sign:

Partioning helps to improve performance and scalability of large scale applications. Since data is distributed to multiple nodes, workload is balanced. 

1. Divide a large dataset into smaller/more manageable parts called partitions, based on criterias like data range, data size, or data type. 
2. Assign a separate processing node to each partition, which can perform operations on its assigned data subset independently of the others.
3. An effective 'Partition key'(data attribute to determine how data is distributed across partitions) should provide an even distribution of data and support efficient query patterns.

### Types of Partitioning

Horizontal             | Vertical |
-----------------------|----------|
Divide a DB table into multiple partitions/ shards, with each partition containing a subset of rows.| Divide a DB table into multiple partitions/shards, with each partition containing a subset of columns

> Hybrid Partitioning combines both. 

### Techniques for Sharding/Partitioning

1. Range based
2. Hash based
3. Directory based
4. Geography based
5. Hybrid