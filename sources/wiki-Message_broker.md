---
source: https://en.wikipedia.org/wiki/Message_broker
fetched: 2026-06-19
---

Computer program module [![](//upload.wikimedia.org/wikipedia/commons/thumb/9/91/Message_Broker.png/500px-Message_Broker.png)](./File:Message_Broker.png)Sequence diagram for depicting the Message Broker pattern 

A **message broker** (also known as an **integration broker** or **interface engine**[[1]](./Message_broker#cite_note-GartnerIB-1)) is an intermediary computer [program module](./Modular_programming) that translates a message from the formal messaging protocol of the sender to the formal messaging protocol of the receiver. Message brokers are elements in telecommunication or computer networks where software applications communicate by exchanging formally defined messages.[[1]](./Message_broker#cite_note-GartnerIB-1) Message brokers are a building block of [message-oriented middleware](./Message-oriented_middleware) (MOM) but are typically not a replacement for traditional middleware like MOM and [remote procedure call](./Remote_procedure_call) (RPC).[[2]](./Message_broker#cite_note-KaleGuide14-2)[[3]](./Message_broker#cite_note-ClarkWeb13-3)

 

## Overview

 

A message broker is an [architectural pattern](./Architectural_pattern) for message validation, transformation, and routing. It mediates communication among applications[*[vague](./Wikipedia:Vagueness)*], minimizing the mutual awareness that applications should have of each other in order to be able to exchange messages, effectively implementing [decoupling](./Coupling_(computer_programming)).[[4]](./Message_broker#cite_note-EjsmontWeb15-4)

 

### Purpose

 

The primary purpose of a broker is to take incoming messages from applications and perform some action on them. Message brokers can decouple end-points, meet specific [non-functional requirements](./Non-functional_requirement), and facilitate reuse of intermediary functions. For example, a message broker may be used to manage a workload queue or [message queue](./Message_queue) for multiple receivers, providing reliable storage, guaranteed message delivery and perhaps transaction management.

 

### Life cycle

 

The following represent other examples of actions that might be handled by the broker:[[2]](./Message_broker#cite_note-KaleGuide14-2)[[3]](./Message_broker#cite_note-ClarkWeb13-3)

 
- Route messages to one or more destinations
- Transform messages to an alternative representation
- Perform message aggregation, decomposing messages into multiple messages and sending them to their destination, then recomposing the responses into one message to return to the user
- Interact with an external repository to augment a message or store it
- Invoke [web services](./Web_service) to retrieve data
- Respond to events or errors
- Provide content and topic-based message routing using the [publish–subscribe pattern](./Publish–subscribe_pattern)

 

Message brokers are generally based on one of two fundamental architectures: [hub-and-spoke](./Spoke–hub_distribution_paradigm) and message bus. In the first, a central server acts as the mechanism that provides integration services, whereas with the latter, the message broker is a communication backbone or distributed service that acts on the [bus](./Bus_(computing)).[[3]](./Message_broker#cite_note-ClarkWeb13-3) Additionally, a more scalable multi-hub approach can be used to integrate multiple brokers.[[3]](./Message_broker#cite_note-ClarkWeb13-3)

 

## Real-time semantics

 

Message brokers that are purpose built to achieve time-bounded communications with end-to-end predictability allow for the development of real-time systems that require [execution predictability](./Real-time_computing). Frequently systems with real-time requirements involve interaction with the real world ([robotics](./Robotics), [vehicle automation](./Vehicle_automation), [software-defined radio](./Software-defined_radio), et al.)

 

The [Object Management Group](./Object_Management_Group) Real-time CORBA specification provides a theoretical foundation for predictable communications technologies by levying the following requirements:[[5]](./Message_broker#cite_note-5)

 

For the purposes of this specification, "end-to-end predictability" of timeliness in a fixed priority CORBA system is defined to mean:

 
- respecting thread priorities between client and server for resolving resource contention during the processing of CORBA invocations;
- bounding the duration of thread priority inversions during end-to-end processing;
- bounding the latencies of operation invocations.

 

## List of message broker software

 
- Amazon Web Services (AWS) [Amazon MQ](https://aws.amazon.com/amazon-mq/)
- Amazon Web Services (AWS) [Kinesis](https://aws.amazon.com/kinesis/)
- **Apache** 
- [Apache ActiveMQ](./Apache_ActiveMQ)
- [Apache Artemis](https://activemq.apache.org/components/artemis/)
- [Apache Camel](./Apache_Camel)
- [Apache Kafka](./Apache_Kafka)
- [Apache Qpid](./Apache_Qpid)
- [Apache Thrift](./Apache_Thrift)
- [Apache Pulsar](./Apache_Pulsar?action=edit&redlink=1)

- Cloverleaf (Enovation Lifeline - NL)
- Comverse Message Broker ([Comverse Technology](./Comverse_Technology))
- Coreflux [Coreflux MQTT Broker](https://www.coreflux.org/)
- Eclipse [Mosquitto MQTT Broker](https://mosquitto.org/) ([Eclipse Foundation](./Eclipse_Foundation))
- EMQX [EMQX MQTT Broker](https://www.emqx.com/en/products/emqx)
- Enduro/X Transactional Message Queue (TMQ)
- Financial Fusion Message Broker ([Sybase](./Sybase))
- [Fuse Message Broker](./Fuse_Message_Broker) (enterprise ActiveMQ)
- [Gearman](./Gearman)
- Google Cloud [Pub/Sub](https://cloud.google.com/pubsub) ([Google](./Google))
- HiveMQ [HiveMQ MQTT Broker](https://www.hivemq.com/hivemq/)
- [HornetQ](./HornetQ) ([Red Hat](./Red_Hat)) (Now part of Apache Artemis)
- [IBM App Connect](./IBM_Integration_Bus)
- [IBM MQ](./IBM_MQ)
- [JBoss Messaging](./JBoss_Messaging) ([JBoss](./JBoss))
- [JORAM](./JORAM?action=edit&redlink=1)
- [LavinMQ](https://lavinmq.com) written in [Crystal](./Crystal_(programming_language))
- [Microsoft Azure Service Bus](./Microsoft_Azure) ([Microsoft](./Microsoft))
- [Microsoft BizTalk Server](./Microsoft_BizTalk_Server) ([Microsoft](./Microsoft))
- [MigratoryData](https://migratorydata.com) (a publish/subscribe [WebSockets](./WebSockets) message broker written to address the C10M problem [[6]](./Message_broker#cite_note-migratoryacm-6))
- [NATS](./NATS_Messaging) ([MIT License](./MIT_License), written in [Go](./Go_(programming_language)))
- NanoMQ [MQTT Broker for IoT Edge](https://nanomq.io/)
- [Open Message Queue](./Open_Message_Queue)
- Oracle Message Broker ([Oracle Corporation](./Oracle_Corporation))
- [ORBexpress](./ORBexpress) ([OIS](./Objective_Interface_Systems))

- [ORBexpress](./ORBexpress) written in [Ada](./Ada_(programming_language))
- [ORBexpress](./ORBexpress) written in [C#](./C_Sharp_(programming_language))
- [ORBexpress](./ORBexpress) written in [C++](./C++)
- [ORBexpress](./ORBexpress) written in [Java](./Java_(programming_language))

- [RabbitMQ](./RabbitMQ) ([Mozilla Public License](./Mozilla_Public_License), written in [Erlang](./Erlang_(programming_language)))
- Redpanda (implement Apache Kafka API, written in [C++](./C++))
- [Redis](./Redis) An open source, in-memory data structure store, used as a database, cache and message broker
- [SAP PI](./SAP_PI) ([SAP AG](./SAP_AG))
- SMC [SMC Platform](http://www.smcsystem.ru/)
- [Solace](./Solace_Corporation) PubSub+
- [Spread Toolkit](./Spread_Toolkit)
- [Tarantool](./Tarantool), a NoSQL database, with a set of [stored procedures](./Stored_procedure) for message queues
- [TIBCO](./TIBCO_Software) Enterprise Message Service
- [WSO2 Message Broker](./WSO2)
- [ZeroMQ](./ZeroMQ)

 

## See also

 
- [Broker injection](./Broker_injection)
- [Publish–subscribe pattern](./Publish–subscribe_pattern)
- [MQTT](./MQTT)
- [Comparison of business integration software](./Comparison_of_business_integration_software)
- [Message-oriented middleware](./Message-oriented_middleware)

 

## References

 
1. [1](./Message_broker#cite_ref-GartnerIB_1-0) [2](./Message_broker#cite_ref-GartnerIB_1-1) ["IB (integration broker)"](https://www.gartner.com/it-glossary/ib-integration-broker). *IT Glossary*. Gartner, Inc. Retrieved 17 May 2018.
2. [1](./Message_broker#cite_ref-KaleGuide14_2-0) [2](./Message_broker#cite_ref-KaleGuide14_2-1) Kale, V. (2014). ["Integration Technologies"](https://books.google.com/books?id=1IuZBQAAQBAJ&pg=PA117). *Guide to Cloud Computing for Business and Technology Managers: From Distributed Computing to Cloudware Applications*. CRC Press. pp. 107–134. [ISBN](./ISBN_(identifier)) [9781482219227](./Special:BookSources/9781482219227). Retrieved 17 May 2018.
3. [1](./Message_broker#cite_ref-ClarkWeb13_3-0) [2](./Message_broker#cite_ref-ClarkWeb13_3-1) [3](./Message_broker#cite_ref-ClarkWeb13_3-2) [4](./Message_broker#cite_ref-ClarkWeb13_3-3) Samtani, G.; Sadhwani, D. (2013). ["Integration Brokers and Web Services"](https://books.google.com/books?id=2EonCgAAQBAJ&pg=PA71). In Clark, M.; Fletcher, P.; Hanson, J.J.; et al. (eds.). *Web Services Business Strategies and Architectures*. Apress. pp. 71–84. [ISBN](./ISBN_(identifier)) [9781430253563](./Special:BookSources/9781430253563). Retrieved 17 May 2018.
4. [↑](./Message_broker#cite_ref-EjsmontWeb15_4-0) Ejsmont, A. (2015). "Asynchronous Processing". *Web Scalability for Startup Engineers*. McGraw Hill Professional. pp. 275–276. [ISBN](./ISBN_(identifier)) [9780071843669](./Special:BookSources/9780071843669).
5. [↑](./Message_broker#cite_ref-5) ["Real-time CORBA Specification"](https://www.omg.org/spec/RT/1.2/PDF). [Object Management Group](./Object_Management_Group). 2005-01-04. section 1.3.4 on page 1-4.
6. [↑](./Message_broker#cite_ref-migratoryacm_6-0) Rotaru, Mihai; et al. (December 2017). "Reliable messaging to millions of users with migratorydata". *Proceedings of the 18th ACM/IFIP/USENIX Middleware Conference: Industrial Track*. pp. 1–7. [arXiv](./ArXiv_(identifier)):[1712.09876](https://arxiv.org/abs/1712.09876). [doi](./Doi_(identifier)):[10.1145/3154448.3154449](https://doi.org/10.1145%2F3154448.3154449). [ISBN](./ISBN_(identifier)) [9781450352000](./Special:BookSources/9781450352000). [S2CID](./S2CID_(identifier)) [35552786](https://api.semanticscholar.org/CorpusID:35552786).