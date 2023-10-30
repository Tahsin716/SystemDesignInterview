# Design Dropbox

### Problem 
Design a cloud storage service like Dropbox where users can upload and share files with others.

Example:
- https://dropbox.com

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Consistency

4. How many new files are expected to be uploaded monthly?
    - 1 billion new files
      
5. Are there events that lead to a spike in activity?
    - No

6. What is the read-to-write ratio?
    - 10:1
  
7. What is the average file size?
    - 100 kb

8. What is the replication factor?
   - 3x

### Functional Requirements

|      | 
| ----------- | 
| 1. Users can upload/download/view files.      | 
| 2. Users should be able to share files or folders with other users.   | 
| 3. Automatic synchronization between devices.|
| 4. Offline editing and synchronization, when the user comes online. |

### Non-Functional Requirements

|      | 
| ----------- | 
| 1. High Reliability (no user upload should be lost)   | 
| 2. High Availability   | 
| 3. Scalable|
| 4. Strong Consistency |

## Capacity Estimation

### 1. Traffic Estimates

Since the read-to-write ratio is 10:1 and we are expected to have 1 billion files uploaded monthly, 
so the total number of reads monthly will be:

 - 10 * 1 billion = 10 billion reads

Read and write in seconds:

 - 1 billion / (30 days * 24 hours * 3600 seconds) = 385 files uploaded per second

 - 10 * 385 = 3850 file reads per second

### 2. Storage Estimates

Total storage required for 1 month:

 - 1 billion * 100 KB *  = 100TB

Total storage required for 1 year:

 - 100TB * (1 year * 12 months) = 1.2 PB

Total storage required for 10 years:

 - 1200TB * 10 years = 12 PB

With a replication factor of 3x, the storage required will be:
 - For 1 month: 100TB * 3 = 300TB
 - For 1 year: 1.2PB * 3 = 3.6PB
 - For 10 years: 12PB * 3 = 36PB

### 3. Network Estimates

For write requests per second:

 - 385 * 100KB = 38 MB/s

For read requests per second:

 - 3850 * 100KB = 380 MB/s

### High-Level Estimates

| Parameter | Estimates  |
| ----------- | ----------- |
| New file uploads | 385/s       |
| File reads   | 3850/s        |
| Incoming data  | 38 MB/s        |
| Outgoing data  | 380 MB/s        |
| Storage data in 1 year | 3.6 PB        |
| Storage data in 10 years | 36 PB        |

## Data Model

What kind of database should we use?

 - Billions of files
 - Read-heavy system
 - Large volume of unstructured data.

For storing files we will use an **Object Storage**, FileMetaData requires _ACID_ properties so we will use a **Relational Database**.
We will also have a relational database for Users.

### Database Design

|  FileMetaData    | 
| ----------- | 
| **FileId: int** |
| CreationDate: DateTime | 
| LastUpdateDate: DateTime | 
| CreatedBy: int   | 
| LastUpdatedBy: int   | 
| Title: varchar(512)  | 
| Chunks: [ ]  | 
| Snapshots: [ ]  | 

|  User    | 
| ----------- | 
| **UserId: int**   | 
| Name: varchar(20) | 
| Email: varchar(32) |
| CreationDate: DateTime |

## System Design

### System Design Diagram

![Dropbox Diagram](https://github.com/Tahsin716/SystemDesignInterview/blob/main/Dropbox/img/dropbox.png)
