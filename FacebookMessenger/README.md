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

 - 20 billion * 30 = 600 billion messages

### 2. Storage Estimates

Total storage required daily:
 
 - 20 billion messages * 100 KB = 2TB
   
Total storage required for 1 month:

 - 600 billion messages * 100 KB *  = 60TB

Total storage required for 1 year:

 - 60TB * (1 year * 12 months) = 720TB

Total storage required for 10 years:

 - 720TB * 10 years = 7.2PB

### 3. Network Estimates

Since read and write are the same in ratio, both incoming and outgoing data will be the same

 - 230000 messages/s * 100 bytes = 23 MB/s

### 4. Memory Estimates

We will cache 20% of the requests (following the 80:20 principle where 20% of work provides 80% of the result)

Since we have 20 billion messages daily, which require 2TB storage:

To cache 20% of the messages, the amount of memory needed is:

 - 0.2 * 2TB = 400GB

### High-Level Estimates

| Parameter | Estimates  |
| ----------- | ----------- |
| New messages | 230000/s       |
| Incoming data  | 23 MB/s        |
| Outgoing data  | 23 MB/s        |
| Storage data in 1 year | 60TB        |
| Storage data in 10 years | 7.2PB        |
| Memory for cache daily | 400GB        |

## Data Model

What kind of database should we use?

 - Billions of messages
 - High rate of small updates.
 - Fetch range of records with minimal latency.

We will use a wide-column database like **Apache Cassandra** for storing the messages.

### Database Design

|  User    | 
| ----------- | 
| **Row key: user_id**   | 
| Columns: name, profile_picture, status, last_active_at, created_at, updated_at | 

|  Conversation    | 
| ----------- | 
| **Row key: conversation_id**   | 
| Columns: participants, last_message_id, created_at, updated_at |

|  Message    | 
| ----------- | 
| **Row key: conversation_id, timestamp** |
| Columns: message_text, message_type, attachments, read_status, created_at, updated_at   | 



