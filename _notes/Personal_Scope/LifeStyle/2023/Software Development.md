
## What is a Service on a Code Base (Domain Driven Approach)
### Definition, characteristics, types, and accessing Services

>## 🖊 **Definition**
*A Service is an operation that can't fit natural in a domain model without encapsulating state*
>

In simple words, a Service supports and extends the functions of a domain model without an internal state and with a well-defined responsibility

>## 🎨 Characteristics
*Services are not the only place that can host functionalitites*
>

Services must have clear characteristics to provide value and contribute to a more clean code base design:
- **Can't fit naturally on a domain model**, as described before Services are extending and supporting Domain Model Classes
- **Well-defined responsibility**, every service must have a clear and well-defined context that is responsible
- **Well-defined interface**, clients should use the service with ease and it should be resuable
- **Stateless**, any client can use any instance of a particular Service without the need to configure the inner state of the Service

> ## 🐶 Types
Services on a Layer Based Architecture App can fall into 3 types
[Design an Application with 3 Layer Architecture](https://petran.substack.com/p/design-an-application-with-3-layer?utm_source=substack&utm_campaign=post_embed&utm_medium=web)
>

*Application*
Services that support the application needs, lifecycle, and life.
Examples: **HttpRequestExtractService, AuthMIddlewareService, InvokeHttpControllerService, RouterService etc.**
*Domain*
Services that implement all the business requirements
*Infrastructure*
Services that aren't on the above 2 types
Examples: **Emailer, DatabaseCommunications, EventDispatcher, EventConsumers, HttpRequestClient, IOReaderWriter etc**

> ## 🍀 Accessing Services
Creating and fetching **Services** must be easy and straightforward for all client Classes.
>

**Thinking of Software Architecture Granularity**

For architectural design, the granularity of software is a perspective to think about. We have several options to select for our component sizess. It is not only limited to microservices vs monolith, right? We could use nano services, FaaS (serverless!?), or even further blockchains. But the first thing first, we should say 
>
IT DEPENDS ... OR your needs and sitituations
>

After this self-relief sentence, I must confess that you should think about your software from many perspectives. Most of the time, granularity is just a little thing to worry about and pre-selected (prejudged?) in our environments. And even as we liberated our minds, could we freely think about all 'pre-defined sizes' by our communitities? Okay, I know this is so much for now. Let's step back and jump into  thinking of granularity.

When I try do design something new, I just try to define all processes and their dependencies (nothing technical). While defining, some of them become typles and some of them become isolated from each other.










