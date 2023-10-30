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
