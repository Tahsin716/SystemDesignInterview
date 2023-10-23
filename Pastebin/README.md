# Pastebin

### Problem 
Design a service like Pastebin where users can paste text, and share via short link generated.

Example:
- https://pastebin.com

## Requirements Engineering

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
    - Availability

4. How many new pastes are expected to be generated monthly?
    - 30 million new pastes
5. Are there events that lead to a spike in activity?
    - No

6. What is the read-to-write ratio?
    - 5:1
  
7. How long is the expiration of pastes?
    - 1 year

### Functional Requirements

|      | 
| ----------- | 
| 1. When a paste is uploaded a unique URL is generated via which the paste can be accessed.      | 
| 2. Only text can be uploaded   | 
| 3. The paste has an expiry date.|
