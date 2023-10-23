# Pastebin

### Problem 
Design a service like Pastebin where users can paste text, and share via short link generated.

Example:
- https://pastebin.com

## Requirements Engineering

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Availability

4. How many new pastes are expected to be generated monthly?
    - 30 million new pastes
5. Are there events that lead to a spike in activity?
    - No

6. What is the read-to-write ratio?
    - 5:1
  
7. How long is the expiration of pastes?
    - 1 year
    
8. What is the max paste size?
    - 10 MB
  
9. Any file type restriction of pastes?
    - Only text is allowed

      
### Functional Requirements

|      | 
| ----------- | 
| 1. When a paste is uploaded a unique URL is generated via which the paste can be accessed.      | 
| 2. Only text can be uploaded   | 
| 3. The paste has an expiry date.|

### Non-Functional Requirements

|      | 
| ----------- | 
| 1. High Reliability (no pastes should be lost)   | 
| 2. High Availability   | 
| 3. Low latency | 
| 4. Scalable|

## Capacity Estimation

### 1. Traffic Estimates

Since the read-to-write ratio is 5:1 and we are expected to have 30 million new short links generated monthly, 
so the total number of paste reads monthly will be:

 - 5 * 30 million = 150 million paste reads

Read and write in seconds:

 - 30 million / (30 days * 24 hours * 3600 seconds) = 11 (pastes per second)

 - 5 * 11 = 55 (paste reads per second)

### 2. Storage Estimates

Pastes generated in 1 year (since the expiry of the paste is 1 year):

 - 30 million * (1 year * 12 months) = 360 million

Assuming each paste is 10KB in memory. So, the total storage used in 1 year:

 - 360 million * 10KB = 3 TB

### 3. Network Estimates

For write requests per second:

 - 11 * 10KB = 110 KB/s

For read requests per second:

 - 55 * 10KB = 550 KB/s

### 4. Memory Estimates

We will cache 20% of the requests (following the 80:20 principle where 20% of work provides 80% of the result)

Since we have 55 requests per second, so we have:

 - 55 * (24 hours * 3600 seconds) =~ 4.7 million requests daily

To cache 20% of the request, the amount of memory needed is:

 - 0.2 * 4.7 million * 10KB = 9.5 GB

### High-Level Estimates

| Parameter | Estimates  |
| ----------- | ----------- |
| New pastes | 11/s       |
| Paste reads   | 55/s        |
| Incoming data  | 110 KB/s        |
| Outgoing data  | 550 KB/s        |
| Storage data in 1 year | 3TB        |
| Memory for cache daily | 9.5 GB        |

## Data Model

What kind of database should we use?

 - Billions of records
 - No relationship between objects
 - Paste objects can be a few MB.

For storing paste records we will use **NoSQL** and for storing paste objects we will use an object storage db like **AWS S3**

### Database Design

|  Paste    | 
| ----------- | 
| **Hash: varchar(8)** |
| ContentKey: varchar(512)   | 
| CreationDate: DateTime | 
| ExpirationDate: DateTime |
| UserId: int   | 

|  User    | 
| ----------- | 
| **UserId: int**   | 
| Name: varchar(20) | 
| Email: varchar(32) |
| CreationDate: DateTime |

