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
