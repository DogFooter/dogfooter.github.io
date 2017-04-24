---
layout: post
comments: true
title:'[domain] midterm 정리'
---
# 1장

## Software process

* Specification
* Design & Implementation
* Validation
* Evaluation

## Process description

* Product: Outcome of process
* Pre or Post condition
* Role

## Software Specifications

* Feasibility
* Requirement specification
* Requirement validationt
* Requirement elicitation., analysis

## Benefit of Iterative Development

* Less project failure
* Managed complexity
* Early rather than late migration of high risk
* Early feedback, user engagement, adaption
* Early visible progress



> Iteration : timeboxed, fied length



## OOAD

### Analysis

* investigation of the problem, requirement rather than solution

> do the right thing

### Design

* conceptional solution that fulfills requirement rather rhan implementation

> do the thing right

### OOA

* method of analysis examine requirement from perspective of classes object in vaca of domain
* finding, describing object or concept

### OOD

* refine, formalize analysis model to implement environment
* defining  software object, how they collaborate to fulfill requirement



## Method

* discipllined process for generating a set of models that describe various aspects of a software system

## Methodology

* collection of methods applide across the software.. life cycle

## Model 

* Simplification of reality
* abstraction of a system
* broken into several views each of which decribe an aspect of a target system

## Why Model

* better understand the system
* visualize system
* permit us to specify the behavior
* give us a template that guides us in constructing a system
* document the descisions

## Principles of Modeling

* what models to create has a profound influence on how a problem is attached and how a solution is shaped
* Every model may be epressed

## UP step

1. Inception
2. Elaboration
3. Coonstruction
4. Transition

### Inception

​	approximate vision, business usecase, scope

### Elaboration

​	refined vision iteration, implementation, core, high risk

### Construction 

​	Iteration, Implementation low risk, easier elements

### Transition

​	Beta test, deployment



# 2장

## Case study

* focus on core app logic layer
* other layer is technology, platform dependent

## Inception Phase

* envision product scope vision business case
* Gain stakeholders' basic agreement or the product vision

## Start in Inception

* Vision, Business case
* Use-Case model
  * name of user-goal
  * 10% of project
* Supplementary specification
* Glossary
* Risk list
* Prototypes
* Develop

## Requirement

- capabilities and condition

### UP Requirement

**FURPS+**

**FURP**

1. Functionality
2. Usability
3. Reliability
4. Performance
5. Supportability

**+ : 임인오팩리**

1. Implementation
2. Interface
3. Operation
4. Package
5. Legal

## Use case

Text stories of some actor using a system to meet goal

## Use case model

set of written use case

### Purpose

* Describe, decide functional requirement
* provide basis
* provide ability trace functioal

## Use case is functionality

* collection of related success and failure scenarioes
* set of use case instance
* analysis initiated by an actor
* design, implementation 신경 안 쓴다

## Use case format

* brief
* casual
* fully dressed

### Fully dressed format

* Use captures **all-and-only** behavior related to satisfying the stakeholders interests
* Precondition : state be true before scenario
* Postconditiion : state be true on success complementation use case
* Main scenario : state be changed by system

#### Extention

​	has two part **condition**, **handling**

#### Special Requirement

* non-functional requirement, quality attrbutes, and constraint(제약) related specification to a use case, recored it with the use case
* they are in supplementary specifiction

#### Technology, Data variation List 

​	variation in data scheme



## Writing Use case

### Essential Style

​	Avoid UI, Focus user intent

### Terse User case

​	terse means simple

### Black box

​	결과만 보여야한다

## How to find Use case

* choose system boundary
* Identify the primary actors
* Identify the goals of each primary actors
* Define Use case statisfy user goal
* Name Use case similar to user goal
* Define one Use case for one goal
* Exception to one Use case per goal is CRUD
* Start the name with verb

## Tests to find useful Use case

### Boss test

​	눈에 보이는 결과물을 내라

### EBP test

* Elemental Business Process
* 한 자리 한 사람 한 time에 처리 해야할 일

### Size test

​	Use case has many step



## Relating Use case

1. include
2. extend
3. generalize

### Include

* base (에서 점선 이어서 화살표가 이 쪽으로 <<include>> 표시) inclusion
* how the behavior of the inclusion use case can be inserted into the behavior of the base use case
* reusing
* inclusion set attributes for prohibit base use case acess that attributes

### Extend

​	to append existing use case without modifying

### Generalization

​	commonalities 를 찾는다



# 3장

## Elaboration goal

* Core risky software architecture (programmed, tested)
* major risk are mitigated or retired

## Best practices in Elaboration

* short time-boxed risk-driven iteration
* Start programming early
* Adaptively design, implentation core risky
* Test early, often, realistically
* Wrtie most use case, requirement in detail

## Artifacts in Elaboration

**3D3US**

### 3D

* Domain model
* Design model
* Data model

### 3U

* Use case story board
* UI prototype
* Update the things do in Inception

### S

* Softeware Architecture Document



## Static & Dynamic modeling

### Static modeling

* class diagram
* Define Structural relationship
  * Association, Aggregation...

### Dynamic modeling

* Interaction diagram
* Define Objects that participate in each use cae
* Define statecharts for state dependent use cases

## Objectives

* Identify conceptual classes
* create an initial domain model

## Domain model

​	Representation of conceptual classes, real-world object in domain of interests

### consist of

* conceptual classes
* association
* attributes



### Implementation을 취급 하지 않는다



## Conceptual classes

​	not a picture of a software class



## LRG

​	Low Representation Gap between Domain model and Design Model

## Domain Model Decomposition

### Structured Analysis

* decomposition by functions
* top-down analysis

### Object-Oriented Analysis

* decomposition by object
* bottom-up

## Three Stratagies to identify conceptual classes

1. Reuse or modify existing model
2. Indentify noun phrases
3. Use a conceptual class category list

## Add Specification or Description Conceptual Classes when:

* description about on item or service is needed, independent of the current existence

## UML does not

​	superimpose a method or modeling perspective on raw diagram

## Domain Model  & Design Model

### Domain Model

​	real word coverage visualization

### Design Model

​	Software component visualizatoin



## Association

* relationship between class meaningful connection
* semantic realationship
* need to remember association : needs to be presreved for some duration
* Common List가 있다.

### Goal of Association

* focus relationship needs to be preserved for some duration

### Identify conceptual classes, association

* Too many association: complex
* Avoid short redundant or derivable associations

## Attribute

​	logical data value, need to remember informatio



### Suitable Attribue types

* Simple attribute or primitive data type

* Relate conceptual calsses with an association not with an attribute

  ​

* Primitive Type

* Stirng, number 같은 건 괜찮다.

### 그러나

* has seperate section ( phone #, person name..)
* has associated operation

## Quantity는 number이면 x 

​	단위가 필요하다.



# 4장

* System Sequence Diagram
* Operation Contracts

## System Sequence Diagrams

​	picture, for one particular scenario of a use case (event) that external actors generate, their order and intersystem events.

### Why draw SSD?

* Identify what events are **coming** to the system
* Investigate, define the system behavior as a **black box**
* Isolate system operations (external actor requests of a system)

### Guideline

​	Main success scenario of each use case, frequent or complex alternative scenario



#### : (colon) and _ (underline) means instance

* SSD shows system **events** for **one scenario** of **a use case**
* System event : solid arrow, actor가 주도

### Naming System Events and Operation

* To capture the intent(의미) of the operation
  * **enter**Item is better than **scan**Barcode
* To emphasize the command orientation: **use verb**
  * enter... , end.., make...

## Operation Contracts

### Objectives

* To define system opeartion(event)
* Contract describe **detailed system behavior** in terms of **state changes to objects in the Domain Model**, after a systemm operation has executed. (precondition, postcondition)

### Defined in terms of preconditions and postconditions

#### Operation

​	name of operation and parameters

#### Cross reference

​	user casese this operation can occur within

#### Preconditions

​	event 하기 전 상태

#### Postcondition

​	the state of obejects in the Domain Model after completion of the operation



### Use Cases, Domain model, SSD and Contracts

#### Use cases

​	are the **main repository of requirements** for the project, provide almost detailed requirements

#### Domain Model

​	is a **visual representation of conceptual classes** or real-world objects in a domain of interest.

#### System Sequence Diagrams

​	**shows**, for one particular scenario of **a use case, the events that external actors generate**, their order, inter-system events.

#### Contracts

​	**describe detailed system behavior** in terms of **state changes** to objects in the Domain Model, after a system operation has executed.

### Guidelines: Contracts

1. **Identify system operations** from SSDs.
2. **For system operations** that are complex and perhaps **subtle(세밀한)** in their result, or which are not clear in the use case, **construct a contract**
3. Contract are **expressed in a declarative** way **without describing how** they are to be achieved
   * **requirement analysis, not software design**
4. Writing contracts leads to Domain Model updates
5. Don't forget to include all the associations formed and broken - Whne new instances are created, it is very likely that associations to several objects need be established.

### Tips: Contracts - Post Conditions

* Post conditions describe **chages in the sate of objects in the Domain Model which include**:
  * insatnce creation and deletion
  * attribute modification 
  * association (links) formed and broken
* **Express post conditions in the past tense(과거 형으로 표현)**, to emphasize they ar declarations about a state change in the past
  * (better) A SalesLineItem **was created**
  * (worse) Create a SalesLineItem
* **Tip**
  * 무대-시스템
  * 연극 시작전 setting (Initial setup)
  * Close curtatin
    * 실제 뭐가 일어나는지는 몰라
    * 연극 끝나고 열어보니 좀 바뀌었어.
      * 사진 찍고 뭐가 달라졌는지 적기

### Contracts, Operations and the UML

* An **operation is an abstraction, not an implentations**. By contrast, a **method (in the UML) is an implementation an operation**.
* A UML operation has a signature, and also an operation specifiacation, which describes the effects produced by executing the operation; the postconditions
* **A UML operation specification** may not show an algorithm or solution, but **only the state changes or effects** of the operation

### Operation Contracts Withn the UP

* A pre- and postcondition contract is a well-known style to specify an operation. In UML, operations exist at  many levels,  from top level classes down to fine-grained classes.
* Operation specification contracts for the top level classes are part of the Use-Case Model.
* UP Phases
  * Inception
    * Contracts are not neede during inception
    * they are too detailed.
  * Elaboration
    * Most contracts willl be written during elaboration, when most use cases are written.
    * Only wrtie contracts for the most complex and subtle system operations.

# 5장

​	Logical Architecture using Layers

## Introduction

### Software Architecture

* the **primary carrier of system qualities** such as performance, modifiability and securit, etc
* an architecture is the set of significant decisions about the organiztion of a software system
* the selection of the **structural elements and their interfaces** by which the system is composed, together **with their behavior**
* the composition of these structural and behavioral elements into progressively larger subsystem
* the **architectural style that guides its organization**

### Logical Architecture

- logical architecture is the large-scale **organization of the software classes into packages, subsystems, and layers (a static view)**
- **It is called logical architecture because thers is no decision about how these elements are deployed across different phhysical platforms**

### Layer Architecture

- a layer is a very coarse-grained grouping of classes, packages, or subsystems that has cohesive responsibility for a major aspect of the system
- layers are organized such that high layers all upon serices of lower layers

### Typical Layers

* Presentation Layer
  * boundary objects which present information to external entities (e.g. human, another systems)
  * User Interface
* Application Logic Layer(or Domain Layer) : Domain specificc
  * software objects representing domain concepts (e.g. Sale) that fulfill application requirements 
* Technical Service Layer (not domain specific : 어디에도 있을 법 : login..)
  * **general purpose objects and subsystems** that provide supporting technical services, such as **interfacing with a database or error logging**
  * these services are usually **application-independent and reusable** across serveral systems

## Guideline: Design with Layers

### General Design Guides

* organize the large-scale logcal structure of a system into discrete layers of distinct, **cohesive responsibilities**, with a clean **separation of concerns (SOC)**
* the lower layers are low-level and general services, and the higher layers are more application specific
* **collaboration and coupling is from higher to lower layers; lower-to-higer layer coupling is avoided**

### Cohesive responsibility and separation of concerns

* the responsibilities of the **objects in a layer should be strongly related to each other**
* e.g. objects in the UI layer should focus on UI work, such as creating windows and widgets, capturing mouse and keyboard events, and should not do application logic

## Design with Layers

### Benefits using Layers

* **SOC reduces coupling and dependencies**, and increasing **cohesive**, clarity and resuse potential. (하나의 스콥에서 얼마나 realte한지 나타내는 척도)
* related complexity is encapsulated and decomposable
* some layers (UI, Application, Domainn) **can be replaced with new implementations**
* some layers (Domain, Technical serveices) can be distributed (service layer를 하나 더 두어서 distribution 가능 하다)
* development by teams is aided because of the logical segmentation



### Guideline: Model-View Separation Principle

* Model-View Separation Principle
  * do not connect or couple non-UI objects directly to UI objects (ui는 ui만)
  * do not put application logic in the UI objects
* MVC Model
  * model-view controller model
  * **a apttern originally designed for applications using GUI**
  * also applied on a large-scale architectural level
    * model - domain layer
    * view - UI layer
    * controller - application layer
* Motivatoin for Model-View Separation
  * To **support cohesive model definitions** that focues on the domain process
  * To **allow separae development of the model and user inteface layer** (병렬적으로 개발)
  * To minize the impact of requirements changes in the inteface layers
  * To allow new views to be easily connected to an exisintg domain layers
  * To allow multiple simultaneous views on the same model obejct
  * (interface, view : requirements 가 바뀔 때 영향을 많이 받는다)
* **Decouples data dan presentation**
* **Eases** the development

# 6장

* Introducing the UML
  * Overview
  * Concpetual Model
* Basic Structural Modeling
  * Class Diagrams
  * Object Diagrams
* Basic Behaviroal Modeling
  * Interactions
  * Sequence Diagrams
  * Communication Diagrams

## Overview of UML

### The UML is a language for 

* Visualizing
* Specifying
* Constructing
* Documenting

## A Concpetual Model of UML

### Building Blocks of UML

* Three kinds of building blocks
  1. Things
  2. Relatinoships
  3. Diagrams
* Things in UML
  1. Structural Things
  2. Behavioral Things
  3. Grouping Things
     * the organizational parts of UML, e.g. package
  4. Annotational things
     * Explanatory parts of UML models, e.g. note

## Structural Things

​	It is the mostly static parts of a mdel representing elements that are either conceptual or physical(also called classifiers)

### Class

​	is a description of a set of objects that share the same attributes, operatinos, relationships, and semantics

### Interface

​	a collection of operations that specify a service of a class or component

### Collaboration

​	defines an interaction and is a society of roles and other elemnts that work together to provide some cooperative behavior. It represents the implementation of patterns that make up  a system

### User case

​	a description of sequences of actinos that a system performs that yield observable resulates of value to a particular actor



### Active class

​	a class whose obejcts **own one or more processes or threads and therfore can initiate control activity**

### Components

​	a **modular parts of the system** design that hides its implementation behind a set of external interface

### Artifact

​	a physical and replaceable part of a system that contains physical information ("bits") such as source code files, executables, and scripts

### Node

​	a physical element that exists at runtime and represents a computational resource, generally having atleast some memory and processing capability

​	

## Behavior Things

​	It is dynamic parts of UML models, representing behavior over time and space

### Interaction

​	a behavior that comprises **a set of messages exchanged among a set of objects** or roles within a particular context to accomplish a specific purpose

### State machine

​	a behavior that specifies the **sequeences of states an object** or an interaction goes through during its lifetime in response to events

### Activity

​	a behavior that specifies the **sequence of steps a computational process perform**. A **step of an activity is callled an** **action**

## Relationships in UML

There are four kinds of relationships

* Dependency
* Association
* Generalization
* Realization

### Dependency

​	is a **semantic relationship** between two model elements in which **a change to one element may affect the semantics of the other element.** It is used to show one thing (Window) is using another(Event) (arror body : - - - - - - -)

### Association

​	is a **structural relationship** among classes that descibes aset of links (employer - employee)

### Generalization

​	is a **specialization/generalization relationship** in which the specialized element (child) builds on the specification of the generalized element(parent). It is called an "is-a-kind-of" relationship. It is used to show **inheritance relationship** (-----)

### Realization 

​	is a **semantic relationship** between classifiers wherein one classifier specifies a contract that another classifier guarantees to carry out ( - - - - - - - - -)

##  Diagrams in UML

### A diagram

* is the graphical presentation of a set of elements, rendered as a connectd graph of vertices (things) and paths (relationships)
* visualizaes a system from different perspectives
* UML inlcudes 13 kids of diagrams (not only class diagram)



## Extensibility Mechanisms

* UML is open-ended, making it possible for you to extend the language in controlled ways
* Three extensibility mechnisms
  * Stereotypes
  * Tagged values
  * Contraints

### Stereotypes

​	extends the **vocabulary of the UML**, allowing you to create new kinds of building blocks that are derived from exsiting ones

### Tagged value

​	extends the **properties of a UML stereotype**, allowing you to create new information in the stereotype's specification

### Constraints

​	extend the **semantics of a UML building block**, allowing you to create new reules or modify existing ones



## Basic Structural Modeling

* Class Diagrams shows a **set of clases, interfaces, and collaborations** and their relationshipos
* Object Diagrams shows a **set of objects** and their realtionship. It **illustrates data structures, the static snapshots of instances of the things found in class diagrams**
* Component Diagrams shows a **set of components** and their relationships. It illustrates the **static implementation view of a system**
* Composite Structure Diagram shows the internal structure of a class or a collaboration
* Deployment Diagram shows a set of nodes and their relationships. It illustrates the static deployment view of a system
* Artifacts Diagram shows a set of artifacts and their relatinoships to their artifacts and to the classes that they implement

## Class Diagrams

### Class

​	a description of a set of object6s that share the same attributes, operatins, relationships, and semantics

### Class Modeling Techniques

* Modeling Vocabulary of a System
  * Identify those things that users or implementers use to describe the problem or solution (e.g. use case-based analysis)
  * For each abstraction, identify a set of responsibilities
  * Provide the attributes and operations that are needed to carry out responsibilities
* Modeling Distribution of Responsibilities
  * Identify a set of classes that work together closely to carry out some behavior
  * Identify a set of responsibility for each of these classes
  * Look at this set of classese as a whole, split classes that have too much reponsibility into smaller abstractions, collapse tiny classes that have trivial responsibilities into larger ones
  * Reallocate responsibilities so that each abstaction reasonably statnds on its own
* A well-structed class
  * provides a crisp abstraction of something drawn from the vocabulary of the problem domain
  * embodies a small, well-defined set of responsibilities
  * provies a celat separation of the abstraction;s specification and its implementation
  * is understandable and simple, yet extensible and adaptable

## Relationships

* A relationship is a connection among things
* Three most-important relationship
  * Dependency
  * generalization
  * association

### Dependency

* Dependency relationship
  * a semantic connection between two elements, one dependent and one independent
  * independen element will affect the dependent element
* Predefined stereotypes applicable to dependency
  * import, access (package)
  * bind, derive, permit, instanceOf, instantiate, refine (classes, objects)
  * extend, include (use case)

## Generalization

* is the taxonomic relationship between a more general element (super class/parent) and a more specific element (subclass/child)
* is used for between classes, interfaces, packages, and other elements to show inheritance relationship

### Applied contraints

* complete: all children have benn specified in the model and no others are permitted.
* **incomplete** : not all children have been specified and additional children are permitted
* **disjoint** : An object instance will belong to only one subclass
* overlapping : An object instance may belong to more than one subclass

## Association

​	is a **structural relationship** that specifies that objects of one thing are connected to objects of another

* name
* role(end-name)
* multiplicity

## Aggregation

* is the "part-whole", "a-part-of" or "has-a" relationship
* a special form of association
* a part can be shared by several composites /wholes

### Composite aggregation

* is a strong form of aggregation
* requires that a part instance be included in **at most one** composite at a time
* requires that the composite object has sole responsibilitiy for the disposition of its part

## Advance Associations

* N-ary Association
* An n-ary association is the more general form of association, it is an association between three or more classifiers that all participate in the relationship. Multiplicity may be used on any of the roles, but no role can contain an aggregation or composition symbol, or a quilifier

### Association Class

* Modeling an association as a class
* The association itself might hace properties
* Company --- Job --- Person : 여기서 Job을 class로 만든다.

### Qualified Association(한정된)

​	has a qualifier that is used to select an object from a larger set of related obejcts, based on the qualifier key

## Realizations

* is a semantic relationship between calssifier in which one classifier specifies a contract that another classifier guarantees to carry out
* is used in two circumstances
  * in the context of interfaces
  * in the context of collaborations

## Relationship Modeling Techniques

### Modeling Dependency

* Dashed arrow line from dependent element (client) to indenpendent element (supplier)
* client having an attributye of the supplier
* client sending a message to a supplier; visibility to the supplier (attribute, parameter, local variable, or class visibility (invoking static or class methods))
* client receiving a parameter of the supplier type
* supplier is a super class or interface of the client

### Modeling Associations

* Use associations primarily where there are structural relationships among objects
* For each pari of classes, if objects of a class need to interact with objects of the other class, specify an association between the two
* If two classes has whole-part relationship, mark this as an aggregation

### Modeling Generalization

* Given a set of classes, look for responsiblities, and operations that are common to two or more clases (is-a relationship)
* Elevate these common responsibilities, attributes, operations to a more general class

## Object Diagrams

* shows a set of objects and their relationships at a point in time
* illustrate data structures, the static snapshots of instances of class diagrams
* illustrate how a complex class diagram can be instantiated into objects
* obejct diagram shows association between instances

## Basic Behavioral Modeling

### Use Case Diagram

​	shows a set of user cases and actors and their relationships. Itillustrate the static use case view of a system

### Sequence Diagram

​	is an interaction diagram that emphasizes the time ordering of the messages. It shows a set of roles and the messages sent and received by the instance playing the roles

### Communication Diagram

​	is an interactoin diagram that emphasizes the structural organizaion of the objects that send and receive message. It shows a set of roles, connectors among those roles, and message sent and received by the instance playing the roles

### State Diagram

​	shows a state machine, consisting of states, transitions, evnets, and activities. It emphasizes the event-orderd behaviors of an object in modeling reactive system.

### Activity Diagram

​	shows the flow from to step within a computation. It emphasizes the flows of control wihtin the execution of a behavior.

## Interactions

* is a behavior that comprises **a set of messages exchanged among objects** in a set of roels
* A message is a **specification of a communication between objects**

# 7장

* Responsibilities and Responsibility-Driven Design
* GRASP

## Object Design

### Use case **realization**

​	describes how a particular use case is realized within the esign model, in terms or collaborating obejcts in OOD

### OOD is sometimes taought as:

​	After identifying your requirements and creating a domain model, then add methods to the appripriate classes, and define the messaging between the objects to fulfill the requirements **(requirement를 어떻게 풀어 나가냐, 어떻게 solution 제공하냐)**



### But how

**It needs**

* a large set of **soft principle**
* a methodological approach
* pattern
* examples & practices



* The critical design tool for software developmetn is a mind well educated in design priciples. It is not eh UML or any other technology



### What are inputs to Object Design

#### Process Inputs

* two-day requirement workshop
* three of the twenty use cases
* programming experiments
* paln for next elaboration iteration
* large-scale logical architecture
* etc

#### Artifacts to object Design

* user case text
* system sequence diagram
* operations contracts



### What are activities of Object Design

* uer case realization which describes how a particular use case is realized within the design model
* cisual modeling for design
  * draw both  interactino(**behavior**) and class(**structural**) diagram
* apply OO design principles suck as GRASP, based on responsibility-driven design(RDD)
* apply GoF design patterns
* one day workshop out of three-week iteration

### What are the outputs

* UML interaction, class, package diagrams
* UI sketches and prototype
* database models

## Object Design Principles

### Software architecture

​	like MVC, 3-Tier, MVP tells us how overall projects are going to be structured

### Design pattern

​	**allow us to reuse the experience or rather, provides resusable solutions to commonly occuring problems**. (e.g. obj create problem.. instance management..)

### Principles

​	**represent a set of guidelines that helps us to avoid having a bad design**. In general, a hug OO principles are:

* **Encapsulate what varies**
* Code to an interface rather than to an implementation.
* Each calss in your application should have only one reason to change

#### The design principles are associated to Robert MArtin who gathered them in "Agile Software Development: Prin..." He suggested SOLID principle

### Single Responsibility Principle (SRP)

​	A class should have only one reason to chagn

​	example) sundae : topping은 아이스크림 클래스 그 자체에서만 바꿔야한다.

### Open Close Principle (OCP)

​	software entities like classses, modules and functions shoudl be open for extension but closed for modifications

### 	Liskov's Substitution(대체) Principle (LSP)

​	Derived types must be completely substitutable for theri base type. Violating LSP make SW confusing - Delegate

### Interface Segregation(분리) Principle (ISP)

​	Client should not be forced to depend upon interfaces that they don't use

### Dependency Inversion Principele (DIP)

​	High-level modules should not depend on low-level modules. Both should depend on **abstractions** (interface)



## Responsibility-Driven Design

* Responsibility is "**a container or obligation of a classfier**"
* Two types of responsibilitie
  * **Doing** responsibilities
    * **doing** someting itself, such as **creating** an object or a calculation
    * **initiating** action in other object
    * **controlling** and **coordinating** activities in other objects
  * **Knowing** responsibilities
    * knowing about **private encapsulated data**
    * knowing about **realted obejct**
    * **knowing about things it can derive or calculate**
* Examples
  * a Sale is responsible **for creating SalesLineItems**
  * **a Sale is responsible for knowing its total**
* A responsibility is not the same thing as a method
  * responsibilities are implemented using metods that either act alone or collaborate with other methods or objects



## Responsibilities and Interaction Diagrams

* Determinig the assignment of responsibilities often occurs during the creation of interaction diagrams(part of Design Model)
* Intercation diagrams show choices in assigning responsibilities to objects

## What are Patterns?

* Principle an solution codified in a structured format **describing a problem and a solution (not a coding solution)**
* A named **problem/solution** pair that can be applied in new contexts
* It is advice from previous designers to help designers in new situations

The idea behind design pattern is simple

​	**Write down and catalogue common interactions between obejct that programmers have frequentyl found useful**

Result

​	Facilitate **reuse of object-oriented code between proejcts and between programmers**



## Characteristics of Good patterns

* soloves a problem
* is a proven conept
* The solution isn't obvious
* It describes a relationship
* The pattern has a significant human component

## Types of pattern

### Architertural Pattern

​	Expresses a fundamental structural organization or schemea for software systems.

### Design Pattern

​	Provides a scheme for refining the subsystems or components of a software system, or the relationship between them.

### Idioms (language dependency)

​	An idiom describes how to implement particular aspects of components or the relationships between them using the features of the given language



## Describing patterns

* Name: meaningful
* Problem : statement of problem
* Context: tell us pattern's applicability
* Forces: A description of the relevant forces and constraints and how they interact/conflict with one another
* Solution: Static relationships and dynamic rules describing how to realize the desired outcome.
* Consequences : Implications(good and bad) of using the solution
* Example: One or more sample applications of the pattern



## GRASP Pattern

It is created to support the following principles

* avoid or minizie additional dependencies
* maximise cohesion and minise coupling
* increase reuse and decrease maintenance
* maximise understandability

### GRASP

#### Creator

#### Information Expert

#### High Cohesion

#### Low Coupling

#### Controller

## Creator

* Problem
  * Who should be responsible for creating a new instances of some class
* Solution
  * Assign calss B the responsibility to create an instance of calss A if on or more of the following is true:
    * B aggregates or contains A objects
    * B records instances of A objects
    * B closely uses A objects
    * B has the initializing data for A objects
* Example
  * Who should be responsible for creating a SalesLineItem instance?

## Information Expert( 중요 )

* Problem
  * What is a general principle by which to assign reponsibilities to objects
* Solution
  * Assign a responsibility to the information expert class that has the information necessary to fulfill the responsibilty (Do-It-Myself strategy)
* Example
  * Who shoul be responsible for knowing the grand totla of a sale?
* Contradiction
  * who should be responsible for **saving a Sale in a database?**
  * by information expert, the answer would be **Sale**
  * But, **this leads to problems in cohesion, coupling, duplication and violate a basic archtectural principle, separation of concerns**
  * Keep application logic in one place, **keep database logic in another palce (DB handling 하는 abstrcat class를 두자)**
* Benefits
  * Information encapsulation : low coupling
  * Behavior is distributed across the classes that have the required information : high cohesion

## Low Coupling

* Problem

  * How to support low dependency, low change impact, and increased resuse?

* Solution

  * Assign a responsibility so that coupling reamins low
    * Coupling is a measure of how strongly one element is connected to or relies on the other elements
    * It's an evaluative principle

* kinds of Coupling

  * class X has an attribute referring to class y instance

  * calss x object call on the services of a class y object

  * class x has method referencing instances of class y

    ....

* Benefits of low coupling

  * changes are localized
  * easier to understand
  * easier to reuse



## High Cohesion

* Problem
  * How to keep complexity manageable?
* Solution
  * Assign a responsibility so that cohesion remains high
  * Cohesion is a **measure of haow strongly related and focused the responsibilties of an element are**
  * As with low coupling, use this to evaluate alternatives for placing responsibilites in objects
* Benefit
  * clarity and understanding of design is increased
  * simplified maintenance and enhancement
  * low coupling is achieved
  * easier to reuse
* Contradiction
  * SQL statements in one class
  * Coarse-grained Remote Interface



## Controller

* Problem
  * Who should be responsible for handling an **input system evnet**?
  * What first obejct beyond the **UI layer(I/O data system 인식 위해 도움)** receives and coordinates ("controls") a system operations?
* Solution
  * Assign the responsibilitiy for receiving or handling a system event message to a class representing one of the following choices
    * class is "**root object" for overall system** (or major subsystem) - **facad controller**
    * **a new class based on use case name (use case 마다  다른 message) - use case/session controller**
* Benefit
  * **increased potential for reuse and pluggable interface**
  * **easier to capture the state of the use case**
* A controller is **non-user interface obeject** responible for receiving or handling a system event
* A controller defines the method for the system operation



# 8장

* Design Model : Use-case Realization
* Design Model : Creating Design Calss Diagrams
* Mapping Design to Code

## Design Model: Use-Case Realizations

### Objectives

* design use-case realizations
* apply the GRASP to assign responsibilities to classses
* use the UML to illustrate and think trough the design of objects

### Use-case realization

* describes how a particurlar use case is realized within the design model, in terms of collaborating objects
* UML class 
