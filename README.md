# System Design Cheatsheet

1. Functional Requirements
2. Non-Functional Requirements
3. High-Level Architecture
4. Deep-Dive into a single Service

## Functional Requirements

-	Be comprehensive - Create full list of features and discuss what to include in the focus
-	If there are multiple data types, describe them all
-	Always add:
    -	Monitoring / Resilience
    -	Usage Analytics
    -	Payment flow
    -	Authentication
-	Reduce: e.g. don't describe the CDN functionality if it is not the scope
- Are we talking CRUD - Create Remove Update Delete?

## Non-Functional Requirements

### Assumptions

-	CAP theorem: Prioritize Availability vs. Consistency
-	Read heavy (10,000/1) vs. write heavy (50/1)
    -	Get a specific number
        -	Number of users /Daily active users
        -	Number of Writes = Reads * x
    -	Purchase rate: 1/1000
    -	Requests/Queries per seconds "qpr"
    -	How big is one entry
       -	**Multiple data types with different sizes?**
- Availability:
    - Reduncancy
- Response time: If < 50ms, we need geo-location
    - Where are users located?
-	Storage: If unlimited, plan for 3 years of storage
    -	A day has 100,000 seconds
    -	3 years have 1000 days = 100,000,000 seconds
-	Throughput
    -	1 GBit per second = 100 Megabyte per second
-	Hotspots (Time vs. DB entry)
    - Assume 1000x than average for hotspot

### SLA - Service-Level Agreements

|      |99.9   (3 nines)	| 99.999    (5)  |	99.9999   (6) |
|------|-----------------:|---------------:|---------------:|
|Daily |	86s	            | 0.86s       	 | 0.086s         |
|Monthly |	43m 28s       |	26s         	 | 2.6s           |
|Yearly |	8h 41m 38s	    | 5m 13s	       |  31s           |

o	MTTD: Mean Time to Detection
o	MTBF: Mean Time Between Failures
o	MTTR: Mean Time To Respond / Recover

## High-Level Architecture

### API Definition

- Translate Functional Requirements into API Calls (only interface)
- Triggered by API call or BATCH processing?
- Public API vs. internal API

### Architectural Components in general

-	Load Balancer
-	Message Queue
-	Memcache
-	Timeseries DB
-	Relational DB
-	Key-Value Store

### Security

- Authentication
- IDOR
- SSRF (in case of CDN)
- CSFR
- XSS


## Deep Dive into individual service

Prepare:
- Quad Tree
- Reverse Index
