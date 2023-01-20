# What is Event Sourcing?

Event sourcing is an architectural pattern to store data as a sequence of events. An event is nothing but a context to the business operation. For instance a customer has requested a refund but you don’t know why? Event sourcing gives the context why refund was made.

Let’s understand some key terms associated with event sourcing:

# Events:

Events represent change in the state of data. These are immutable facts that provide context to the business. Let’s take an example of an e-commerce store. All the data changes will be stored as events like ProductAdded, ProductOrdered, ProductShipped, PaymentReceived etc.

Events are recorded in the past tense and provide the source of truth to the current business state. In addition to the context events also store metadata to provide more information.

# Event Source database:

Event source database also known as event source db records all the events in an append-only database. In event source db history of changes are maintained in chronological order.

Event source db can also be referred to as event logs and they can not be changed as events are immutable. There’s another counter argument that says that event source db can be changed by adding another event the state of the event source db or its outcome is changing.

The event source db for the e-commerce store will record each event along with associated metadata. Suppose there are two events in the Product’s event source db and a third product is added to the event source db. This added product is not new but is returned by the customer so the context of the event is returned product and the number of events is updated. The event source db holds all these events in chronological order.

The context and chronological order of events provide useful information for in-depth analysis.

# Streams:

Event streams provide a complete history of modifications related to a particular event. Events reside in the event source database and event streams represent the order in which events happen. Event streams can be short lived or long-lived based on the particular scenario. The events within the event stream are identified by a unique numeric value and are incremented as events are updated. You can retrieve the original state of events through these identifiers. In the ecommerce store example payment is a separate entity/domain object. The payment object has its own unique identifier and it’s event stream will be: **Payment confirmed -> Payment Received -> Refund is requested -> Refund amount deducted.**

# Query View:

In event sourcing query models represents logical transitioning of source write model to read model. They are also referred to as Projections or View Models. In the query view there are two types of concepts: read model and write model. Let’s recall the example of an e-commerce store where the write model events that are added to the query view are Order placed, payment received, order dispatched, product deducted and then we use the query view to generate a summary of all the orders made and the payments received in the read model.

# Why do we need event sourcing?

Event sourcing is an excellent choice in a variety of applications. Let’s discuss a few scenarios where event sourcing is an acceptable solution.

1.  Event sourcing is useful in auditing systems where logs can be stored in chronological order and has on-demand back up option.
2.  Traditional methods collect data in specific locations to be used only when needed. By quickly responding to newly available information, an event-driven approach can be more effective. By subscribing to the stream, an organization can receive updates about new occurrences and respond to them immediately. This makes it simpler to model and create intricate business procedures.
3.  It is possible to migrate legacy systems to contemporary distributed architectures slowly, eventually replacing particular functionalities with event-sourced services. While writes are directed to the services, the legacy system’s current read pathways can continue to be used.
4.  Dependent services can “catch up” when the originating service resumes operation if one goes down. When each service comes back up, synchronization may be accomplished because events are stored in the stream in a specific order.
5.  In an event-sourced system, data travels in one direction through separate models to read or update data. Due to the singular responsibility that each part of the data flow has, it makes it easier to reason about data and troubleshoot problems.


# How’s event source database (db) different from traditional databases?

Data is stored in databases using CRUD operation that is create, read, update and delete. Whenever a change happens the record is updated in the database and it preserves the current state of the system. In all relational and non-relational databases records can be deleted and the state of the system will be lost.

In event source db events are immutable; they can’t be deleted or altered. Event source db preserves the history of logs in chronological order. By tracking changes discrepancies between audit data and transactional data are avoided. Just like in CRUD system design, event sourcing stores the events in tables but in chronological order. Since the data is in order with the latest data at the top, filtering event sourcing is easier as compared to traditional databases.

# Does event sourcing outgrows databases?

In real world applications multiple concurrent users are updating records in the data store and often data is not updated in all places. This results in inconsistency across data stores. There is no mechanism to store the metadata of history of changes which can be used for in-depth analysis.

Event sourcing also provides context to the change happening in the database which helps in answering the business questions. Event sourcing works better with microservices and is reliable to share data between other services.

Here’re a few advantages that make event sourcing a better choice than traditional databases:

1.  Events can be saved using an append-only operation and are immutable. Tasks that deal with events can run in the background while the user interface, workflow, or process that started them can continue. This, along with the absence of conflict during transaction processing, can greatly enhance the performance and scalability of an application, particularly at the presentation level or user interface.
2.  Events are straightforward objects that explain an action that took place together with any additional information needed to fully describe the action that the event represents. A data store is not directly updated by events. They are merely recorded for handling when necessary. This can make administration and implementation simpler.
3.  For a domain expert, events often have meaning. However, object-relational impedance mismatch might make it challenging to comprehend complicated database tables. Tables are made up objects that depict the system’s current condition rather than actual events.
4.  Because event sourcing does not require updating data store objects directly, it can assist prevent conflicts caused by concurrent modifications. The domain model must still be built to withstand queries that can cause an inconsistent state, though.
5.  Tasks respond to events by performing actions as they are raised by the event source db.
6.  The jobs and events are separated, which offers flexibility and extensibility. Tasks are aware of the type of event that occurred and its data, but not the operation that caused it.
7.  Additionally, each event can be handled by numerous tasks. This makes it possible to integrate additional services and systems that are limited to monitoring new events raised by the event source db with ease. The event sourcing events, however, frequently have a very low level, thus it would be essential to create particular integration events in their place.
8. 

# Challenges with Event-Sourcing
Despite having a lot of advantages, event sourcing has a lot of challenges as well. Let's discuss a few challenges associated with Event-Sourcing
