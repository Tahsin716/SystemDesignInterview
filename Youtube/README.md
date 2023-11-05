# Design YouTube

### Problem
Design a video-sharing service like YouTube, where users can upload/view/search videos.

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Availability

4. How many videos are expected to be uploaded daily?
    - 1 million
      
5. Are there events that lead to a spike in activity?
    - Let's say none for simplicity.

6. What is the read-to-write ratio?
    - 200:1
    
7. What is the average size of each video?
    - 50MB

8. How many Daily Active Users are expected?
    - 800 million

