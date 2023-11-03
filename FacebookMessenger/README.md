# Design Facebook Messenger

### Problem 
Design a messaging service like Facebook Messenger where users can chat in almost real-time.

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Consistency

4. How many messages are expected daily?
    - 20 billion messages
      
5. Are there events that lead to a spike in activity?
    - Let's say none for simplicity.

6. What is the read-to-write ratio?
    - 1:1
    
7. What is the average size of each text size?
    - 100 bytes

### Functional Requirements

|      | 
| ----------- | 
| 1. Messenger should support one-on-one conversations between users.      | 
| 2. Messenger should keep track of the online/offline statuses of its users.   | 
| 3. Messenger sends a notification once the user is online if there are new messages.   | 
| 4. Messenger should support persistent storage of chat history. |

### Non-Functional Requirements

|      | 
| ----------- | 
| 1. Low latency (users should have a real-time chat experience)   | 
| 2. Strong Consistency   | 
| 3. Moderate Availability is expected to have Strong Consistency | 
| 4. Scalable |

## Capacity Estimation

### 1. Traffic Estimates

Since the read-to-write ratio is 1:1 and we are expected to have 20 billion read and writes daily, 

Read and write in seconds:

 - 20 billion / (24 * 3600) ~= 230000 messages

Read and write monthly:

 - 20 billion * 30 = 600 billion

### 2. Storage Estimates

Total storage required for 1 month:

 - 600 billion * 100 KB *  = 60TB

Total storage required for 1 year:

 - 60TB * (1 year * 12 months) = 720TB

Total storage required for 10 years:

 - 720TB * 10 years = 7.2PB
