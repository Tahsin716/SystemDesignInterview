# Url Shortener

### Problem 
Design a URL shortener like TinyURL that generates short links, that redirect to the original URL.

Example:
- Original Url: https://linkedin.com/in/tahsin-rashad
- Short Link: https://tinyurl.com/h49w3mdd

## Requirements Engineering

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important, Consistency or Availability?
    - Availability

4. How many new short links are expected to be generated monthly?
    - 500 million new short links

5. Are there events that lead to a spike in activity?
    - No

6. What is the read-to-write ratio?
    - 100:1
  
7. How long is the expiration of short links?
    - 5 years

### Functional Requirements

|      | 
| ----------- | 
| 1. When given a URL, The service should generate a unique shorter link.      | 
| 2. When a user clicks on the short link, it redirects the user to the original URL.   | 
| 3. The short links should have an expiry date.|

### Non-Functional Requirements

|      | 
| ----------- | 
| 1. High Availability   | 
| 2. Low latency | 
| 3. Scalable|

## Capacity Estimation

### 1. Traffic Estimates

Since the read-to-write ratio is 100:1 and we are expected to have 500 million new short links generated monthly, 
so the total number of redirections monthly will be:

 - 100 * 500 million = 50 billion (URL redirections per month)

Read and write in seconds:

 - 500 million / (30 days * 24 hours * 3600 seconds) = 200 (URL's generated per second)

 - 100 * 200 = 20000 (URL redirections per second)

### 2. Storage Estimates



