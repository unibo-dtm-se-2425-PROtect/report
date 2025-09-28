---
title: Design
has_children: false
nav_order: 4
---

# Design


## Architecture 

- We opted for a **LAYERED ARCHITECTURE**, where the *PRESENTATION LAYER* implies a Thkinter GUI with MCV separation and CLI for alternative interaction, *LOGIC LAYER* that handles cryptography, password operations, and orchestration between UI and DB, and *DATA LAYER* with a real MySQL backend, adding mock implementations for testing purposes. This is the classic layered structure where each component has its responsibility, the layers follow a "downward path" (from UI to Logic to DB), and the abstraction element is attributed by the simulated DB in testing (this has been done to avoid a real initial DB configuration every time we needed to test the GUI's functioning).
- Inside these layers, it is clearly distinguishable a further object/component structure, involving users, entries, cryptographic utilities, database connections, SQL queries, libraries, and MVC itself is an object-based decomposition. As a matter of fact, OOP is good at modeling real-world concepts, making tests, maintenance and extension easier.
- There is also an event-based structure concerning GUI interactions through thkinter by means of buttons, clicks and similar, but it is not about the whole system. The events remain strictly related to the GUI.
- There was no need to use other structures such as SHARED DATASPACE since we don't have independent subsystems communicating, yet the flow is quite linear with a user interacting with a GUI/CLI activaring the logic controller and automatically communicating with the database; or even a SERVICE-ORIENTED design which would not be applicable unless we split into microservices, which is not the case.

## More Details about the Architecture
The application is best described as following **3-Tier layered architecture**:
- PRESENTATION LAYER: the UI, specifically a **GUI** (with Thkinter and MCV pattern) and a **CLI**. It is responsible for capturing users' inputs, showing results (outputs) and handling events like button clicks and other general commands. The MVC pattern, as the name suggests, divides the **MODEL** (what the application does or can do, it focuses purely on functionalities independently from the other two parties, it is about the application's core logic and data), the **VIEW** (what is shown to the user) and the **CONTROLLER** (the glue between the view and the model, it dictates how changes in the view are reflected in the model. The controller is where we write what happens in reaction to input from the user, how the view should change and what functionality from the model should be triggered in response to inputs from the user). Such separation makes it **easier to test and debug** because parties do not interfere with one another (the UI does not deal with SQL and the DB does not have to do with GUI events), **testability** can be mocked so that the components are kept even more autonomous, it is **flexible** for changes (e.g., changing the technology from MySQL to SQLite someday) because we only need to modify the data layer and not the whole program, it is **maintainable** by adding new features extending the logic layer without touching the DB or UI code, and for **security** reasons keeping the cryptographic logic in the business logic reduces the risk of "mixing concerns" happening when different parts of a program are tangled together in the same place even if they focus on separate jobs;
- APPLICATION LAYER: controllers and services that coordinate the workflow. It handles password encryption and consequent decryption, hashing methods (SHA256, PBKDF2 as derivative function to generate cryptographic keys starting from a password);
- DATA LAYER: it is in charge of DB connection and queries handling, including a mock DB implementation for testing without accessing the real DB (otherwise we should remember to delete the created connection every time; the result of avoiding this step would be unsuccessful and incomplete testing and general conflicts during the implementation).

### Diagram for the architecture
<<img src="report/pictures/Blank board.jpeg" alt="diagram-view of the architecture">>

- Describe the responsibilities of each architectural component

> UML Components diagrams are welcome here

## Infrastructure (mostly applies to distributed systems)

- Are there **infrastructural components** that need to be introduced? Which and **how many** of each?
    - e.g. **clients**, **servers**, **load balancers**, **caches**, **databases**, **message brokers**, **queues**, **workers**, **proxies**, **firewalls**, **CDNs**, etc.
- How do components **distribute** over the network? **Where** are they located?
    - e.g. do servers / brokers / databases / etc. sit on the same machine? on the same network? on the same datacenter? on the same continent?
- How do components **find** each other?
    - How to **name** components?
    - e.g. **DNS**, **service discovery**, **load balancing**, etc.

> UML deployment diagrams are welcome here

## Modelling

### Domain driven design (DDD) modelling

- Which are the bounded contexts of your domain? 
- Which are domain concepts (entities, value objects, aggregates, etc.) for each context?
- Are there repositories, services, or factories for each/any domain concept?
- What are the relavant domain events in each context?

> Context map diagrams are welcome here

### Object-oriented modelling

- What are the main data types (e.g. classes) of the system?
- What are the main attributes and methods of each data type?
- How do data types relate to each other?

> UML class diagrams are welcome here

### In case of a distributed system

- How do the domain concepts map to the architectural or infrastuctural components?
    + i.e. which architectural/component is responsible for which domain concept?
    + are there data types which are required onto multiple components? (e.g. messages being exchanged between components)

- What are the domain concepts or data types which represent the state of the distributed system?
    + e.g. state of a video game on central server, while inputs/representations on clients
    + e.g. where to store messages in an instant-messaging app? for how long?

- Are there domain concepts or data types which represent messages being exchanged between components?
    + e.g. messages between clients and servers, messages between servers, messages between clients

## Interaction

- How do components *communicate*? *When*? *What*?

- Which **interaction patterns** do they enact?

> UML sequence diagrams are welcome here

## Behaviour

- How does **each** component *behave* individually (e.g., in *response* to *events* or messages)?
    + Some components may be *stateful*, others *stateless*

- Which components are in charge of updating the **state** of the system? *When*? *How*?

> UML state diagrams or activity diagrams are welcome here

## Data-related aspects (in case persistent storage is needed)

- Is there any data that needs to be stored?
    - *What* data? *Where*? *Why*?

- How should **persistent data** be **stored**? Why?
    - e.g., relations, documents, key-value, graph, etc.

- Which components perform queries on the database?
    - *When*? *Which* queries? *Why*?
    - Concurrent read? Concurrent write? Why?

- Is there any data that needs to be shared between components?
    - *Why*? *What* data?

