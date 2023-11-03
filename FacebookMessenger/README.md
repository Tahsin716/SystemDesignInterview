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
