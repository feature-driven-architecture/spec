# Feature Driven Architecture

Feature Driven Architecture (FDA) is a structural framework that helps organize the codebase for visual interfaces in a way that lets you keep a constant development velocity while the amount of Features is growing.

These are three types of boundaries this specification defines:

- __Files System__ - how to name files and folders
- __Dependencies__ - which boundary can depend on each other
- __Knowledge Scope__ - which boundary has what type of knowledge

## Rationale

We have various component models that let us compose the UI. We have multiple data flow models that simplify working with the data. And yet, we struggle to build an application that allows many people to work in parallel. We suffer an exponential slow-down when the codebase grows.

The reason is the lack of agreement on splitting an application in a way that allows more people to work in parallel and keep the complexity under control.

FDA is the missing piece that builds **on top** of existing component and data-flow models.

Instead of organizing code by data and abstraction types, we want to organize the code based on the user-facing features that solve a user problem. This way, we believe it is easier to scale, communicate and navigate the codebase.

## Goals

**Discoverability and navigation** - see how the software is structured by looking at the file system. Help find any user-facing functionality in code.

**Work parallelization** - enable working in parallel with multiple people. Reduce the number of merge conflicts. Reduce the number of discussions about where to put some piece of code.

**Refactoring** - better understand the scope of a change. Gain much more confidence in changing a Feature by knowing it won't affect other Features. See what Features will be affected when changing a shared abstraction.

**Experiments** - enable creating and removing experimental Features.

## Non-goals

**Language and Framework** - it is language and framework agnostic. It leaves plenty of space to accommodate particular product needs and design decisions.

**Data flow model** - it is data flow agnostic. Unidirectional, reactive, or actor data model doesn't matter as long as the principles are not broken.

**Data fetching** - it is network layer agnostic.
Websockets or HTTP, REST, RPC or GraphQL - doesn't matter as long as the principles are not broken.

## How

Feature Driven Architecture defines foundational boundaries: Feature, Cluster, Screen, Shared and Library. Each concept follows the core principles.

A concept of a "Feature" is the foundation of Feature Driven Architecture. Everything else exists to support it.

Breaking any principle described in this architecture will lead to specific problems in your codebase, and the goal here is to define the benefits and trade-offs.

## Core principles

1. Decentralization

    Avoid a central point of failure as much as possible.

1. Co-location

    Locate dependencies as close as possible to their consumers.

1. Isolation

    Subsystems should know as little as possible. Every piece of knowledge comes at a price of coupling.

1. Disposability

    Optimize for ease of removal. Removing a feature folder in an ideal implementation would remove most of the Feature. The rest should be easy to track down and remove cleanly.
    
1. Explicit sharing

    Make sharing code between boundaries super explicit.

## Feature

> A Feature is an isolated user-facing reusable complex building block(s) that solves a particular problem for a user.

Feature scope generally depends on the product and organizational needs, but a specific Feature should have a clearly defined scope by its maintainers.

[Read more about how to identify a feature.](./feature.md)

A Feature follows these principles:

1. A Feature can not know about the existence of any other Feature.

   This principle is **the most important** one, and without it - your entire architecture is considered broken.

1. A Feature can not know about the Screen it's been used on.

   Without it, you won't be able to reuse a Feature across multiple screens.

1. A Feature must be cohesive.

   A Feature must co-locate its implementation in the location associated with the Feature name.

1. A Feature can have dependencies.

   A Feature must express dependencies in a form designed to be understood and provided by its consumers.

1. A Feature has to be disposable.

   You should be able to remove a Feature without leaving any remains behind.

1. A Feature has to be composable.

   You should be able to compose multiple Features on the same or different screens without modifying a Feature.

## Screen

> A Screen represents the content of the entire Screen.

A Screen can use Clusters and Features to position them on the Screen. A Screen is responsible for the global layout. A Screen knows all Clusters and Features it is using.

A Screen follows these principles:

1. A Screen can not know about the existence of any other Screen.
1. A Screen must be cohesive.
1. A Screen has to be disposable.

## Cluster

> Cluster is a reusable bundle of Features.

A Cluster is useful when you need to bundle several Features and reuse them together on different Screens.

A Cluster can be used to forward data from one Feature to another, and to configure Features.

A Cluster is needed to avoid duplication of setup code for Features. If the setup is trivial - you don't need it. _Cluster is optional._

A Cluster follows these principles:

1. A Cluster can not know about the existence of any other Cluster.
1. A Cluster can not know about the Screen it's been used on.
1. A Cluster must be cohesive.
1. A Cluster can have dependencies.
1. A Cluster has to be disposable.

## Shared

>Shared code is reusable across Screens, Clusters, and Features and has application-specific knowledge.

Shared code follows these principles:

1. Shared code has no knowledge of a particular Feature, Cluster, or Screen.
1. Shared code can use Libraries.
1. Shared code can use shared code.

## Library

> Library code is the lowest level abstraction, reusable across Screens, Clusters, Features, and Shared and has __no__ application-specific knowledge.

The Library is often called lib, node_modules, etc.

1. Library code has no knowledge of a particular Feature, Cluster, Screen, or Shared code. In fact, it knows nothing about the application.
1. Library can use Libraries.
