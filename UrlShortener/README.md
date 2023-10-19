# Url Shortener

### Problem 
Design a Url Shortener like tinyurl that generates short links, which redirect to original url.

Example:

Original Url: https://linkedin.com/in/tahsin-rashad

Short Link: https://tinyurl.com/h49w3mdd

## Requirements Engineering

### Questions:

1. Is the system read heavy or write heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important, Consistency or Availability?
    - Availability

4. How many daily active users does the system have?
    - 100 million active users

5. Are there events that lead to spike in activity?
    - No

6. What is the read to write ratio?
    - 100 : 1

### Functional Requirements

1. When given a url, the service should generate a unique shorter link.

2. When user clicks on the short link, it redirects the user to the original url.

3. The short links should have an expiry date.

### Non-Functional Requirements

1. High Availability

2. Low latency

3. Scalable


## Capacity Estimation




