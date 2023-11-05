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

### Functional Requirements

|      | 
| ----------- | 
| 1. Users should be able to upload videos.      | 
| 2. Users should be able to share and view videos.   | 
| 3. Users should be able to perform searches based on video titles.   | 
| 4. Users should be able to add and view comments on videos. |
| 5. The system should record statistics of likes, dislikes, views, etc. |

### Non-Functional Requirements

|      | 
| ----------- | 
| 1. High Reliability (no user upload should be lost)   | 
| 2. High Availability   | 
| 3. Low latency | 
| 4. Scalable |

## Capacity Estimation

### 1. Traffic Estimates

Since the read-to-write ratio is 200:1 and we are expected to have 1 million video uploads daily, so
daily video views will be 200 million.

Read and write in seconds:

 - 1 million / (24 * 3600) = 12 video uploads/s
 - 200 * 12 = 2400 views/s

Read and write monthly:

 - 1 million * 30 = 30 million video uploads per month
 - 200 * 30 = 6 billion views per month
