---
---

Apache OpenWhisk
1. [What is OpenWhisk](#what-is-openWhisk)
2. [Why do we need it](#why-do-we-need-it)
3. How is it different from serverless functions
4. [FAQ](#faq)


## Terminologies
* Actions
* Functions
* Events
* Triggers
* Feeds

## Notes
* Functions is expected to be stateless
* dynamically typed vs statically typed languages: statically typed languages need extra efforts for serialization of input / output (java).
 * python processes dictionary, JS works with Json.
### Actions
* Diagram of work
* Action chaining:
  * intermediate actions can have i/p o/p in other than JSON
  * can be linear pipline of actions
  * can be chanalled in more than one actions
    * This is possible with Triggers and Rules
  * trigger
* Actions can be packaged and shared.
* Actions doesnt have local storage: its a container deployed by invoker when event is received and is ephemeral.
* Actions are event driven
* Actions are time bound. max time is configurable.

### Resource cost:
* Charged for VMs where your OpenWhisk server is running
* Actions are charged for running containers

### OpenWhisk Architecture
#### Technologies used
It internally uses technologies like,
1. Nginx:
2. CouchDB:
3. Kafka:

#### Components
[Provide usecase diagram]

## FAQ
1. How to replay event i OpenWhisk?
2. Why Stateless is better than stateful?
  - Limits scalability: You need data store
  - Synchronization of states between the requests
  - Store may limit ability to scale your app
  - Operations for keeping state in sync while upscaling or downscaling

3. How event processing works in serverless?
4. Who sends input to action?
5. 


## References
https://learning.oreilly.com/library/view/learning-apache-openwhisk/9781492046158/ch01.html#idm45740216345080
