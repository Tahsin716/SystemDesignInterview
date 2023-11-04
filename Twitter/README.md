# Design Twitter

### Problem 
Design a social networking service like Twitter where users can post tweets, and follow other people and favorite tweets.

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Availability

4. How many tweets are expected daily?
    - 100 million tweets
      
5. Are there events that lead to a spike in activity?
    - Yes, breaking news and emergencies, live events and sporting matches, etc, can lead to a spike in events.

6. What is the read-to-write ratio?
    - 100:1
    
7. What is the average size of each text size?
    - 200 bytes

8. How many Daily Active Users does the system have?
    - 200 million users
  
9. How many favorites does the system have per day?
    - 1 billion favorites

10. How many total views does the system generate per day?
     - 28 billion views