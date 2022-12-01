---
---

Apache OpenWhisk
1. [What is OpenWhisk](#what-is-openWhisk)
2. [Why do we need it](#why-do-we-need-it)
3. [How is it different from serverless functions]
4. [FAQ](#faq)


## Terminologies
* Actions
* Functions
* Events
* 

## Notes
* Functions is expected to be stateless
* interpreted languages vs pre-compiled languages: Runs on JVM
### Actions
* Diagram of work
* Action chaining:
  * intermediate actions can have i/p o/p in other than JSON
  * can be linear pipline of actions
  * can be chanalled in more than one actions
    * This is possible with Triggers and Rules
    * 
* Actions can be packaged and shared.

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
