---
---
# Service Discovery With Eureka

# Plan
- [x] What is Service Discovery
- [x] Types of Service Discovery
- [ ] Role of Eureka
- [ ] Practical
___

# Index
- [What is Service Discovery](what-is-service-discovery)
- [Types of Service Discovery](types-of-service-discovery)

# What is Service Discovery
When application is distributed across the microservices, communication between the services becomes difficult because of,</p>
1. Caller Service needs to know URL of Cally Service.
2. URL might change over time
3. Exposing internal service information might not be safe
In such case Service Discovery comes to rescue.</p>

Service Discovery(SD) holds the information of cally services inside service registery & caller service asks SD to know this information.

# Types of Service Discovery
1. Client Side SD
2. Server Side SD

## Client Side Service Discovery
Service discovery is managed by SD Server which holds service registry</p>
Client calls the SD & gets the information about the cally service.</p>
Then Client calls the Cally server.</p>
This is similar to Looking into `Yellow Pages` or Searching for info on Google & calling the right info.</p>
Drawback: Caller service needs to make 2 calls to get information.

## Server Side Service Discovery
SD Server is hosted at server side</p>
Client Request goes to SD Server</p>
SD Server looks up in Service registery & routes the request to right cally service.</p>
Here Client doesnt know internals about that server and is also unaware where cally service is</p>
This analogy is similar to calling a receptionist of office for perticular person and who redirects the call to receptive employee</p>

