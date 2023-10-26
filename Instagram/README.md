# Design Instagram

### Problem 
Design a photo-sharing service like Instagram where users can upload and share images with others.

Example:
- https://instagram.com

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Availability

4. How many new images are expected to be generated monthly?
    - 1 billion new images
      
5. Are there events that lead to a spike in activity?
    - Any events like concerts, or holidays like Christmas might lead to a spike in activity.

6. What is the read-to-write ratio?
    - 10:1
    
7. What is the maximum file size allowed to upload?
    - 10 MB
  
