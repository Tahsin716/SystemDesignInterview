# Url Shortener

### Problem 
Design a URL shortener like TinyURL that generates short links that redirect to the original URL.

Example:
- Original Url: https://linkedin.com/in/tahsin-rashad
- Short Link: https://tinyurl.com/h49w3mdd

## Requirements Engineering

### Questions:

1. Is the system read-heavy or write-heavy?
    - Read heavy

2. Is it a distributed system or a single server?
    - Distributed System

3. Which is more important: Consistency or Availability?
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

Short links generated in 5 years (since the expiry of the short link is, 5 years):

 - 500 million * (5 years * 12 months) = 30 billion

Assuming each link is 1KB in memory. So, total storage used in 5 years:

 - 30 billion * 1KB = 30 TB

### 3. Network Estimates

For write requests per second:

 - 200 * 1KB = 200 KB/s

For read requests per second:

 - 20000 * 1KB = 20 MB/s

### 4. Memory Estimates

We will cache 20% of the requests (following the 80:20 principle where 20% of work provides 80% of the result)

Since we have 20000 requests per second, so we have:

 - 20000 * (24 hours * 3600 seconds) =~ 1.7 billion requests daily

To cache 20% of the request, the amount of memory needed is:

 - 0.2 * 1.7 billion * 1KB = 340 GB

### High-Level Estimates

| Parameter | Estimates  |
| ----------- | ----------- |
| New URLS | 200/s       |
| Url redirections   | 20000/s        |
| Incoming data  | 200 KB/s        |
| Outgoing data  | 20 MB/s        |
| Storage data in 5 years | 30TB        |
| Memory for cache daily | 340 GB        |

## Data Model

What kind of database should we use?

 - Billions of rows
 - No relationship between objects

So the answer is **NoSQL**

### Database Design

|  ShortLink    | 
| ----------- | 
| **Hash: varchar(8)** |
| OrignialUrl: varchar(512)   | 
| CreationDate: DateTime | 
| ExpirationDate: DateTime |
| UserId: int   | 

|  User    | 
| ----------- | 
| **UserId: int**   | 
| Name: varchar(20) | 
| Email: varchar(32) |
| CreationDate: DateTime |

## API design

|  Endpoint    | Verb | Response|
| ----------- | ------- | ------ |
| /createshortlink | Post | { "shortlink": "h49w3mdd"} |
| /getoriginalurl?shortlink=h49w3mdd | Get | { "original_url": `https://linkedin.com/in/tahsin-rashad` } |


## System Design

### 1. Encoding Algorithm

For generating short links we will use the MD5 Hash algorithm. We will hash the DateTime stamp + the user's IP Address.

``` console
    shortlink = md5_hash(datetime + ip_address);
```

We will use the first 8 characters of the hash generated as the short link.

### 2. Database Sharding/Partition

Since we have billions of data to store, we need to partition the database to store them efficiently.

Let's assume we have 512 shards/machines where we can store our data.

We will partition based on hashing. Each database will be identified with a hash number, and we will decide which database to store the short link
by using a hash function.

``` console
    hash_function(shortlink) = 0-511 machines/shards
```
### 3. System Design Diagram

![Url Shortener Diagram](https://github.com/Tahsin716/SystemDesignInterview/blob/main/UrlShortener/img/url_shortener.png)
