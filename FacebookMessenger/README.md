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

4. How many Daily Active Users are expected monthly?
    - 100 million users
      
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
