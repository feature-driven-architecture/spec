# Feature Driven Architecture

Feature Driven Architecture (FDA) is a structural framework that helps organize the codebase for visual interfaces in a way that helps you keep a constant velocity while the amount of Features is growing.

## Rationale

We have various component models that let us compose the UI. We have multiple data flow models that simplify working with the data. And yet, we struggle to build an application that allows many people to work in parallel. We suffer an exponential slow-down when the codebase grows.

The reason is the lack of agreement on splitting an application to prevent exponential growth in complexity as you add Features.

FDA is the missing piece that builds **on top** of existing components and data-flow models.

## Goals

**Discoverability and navigation** - see how the software is structured by looking at the file system. Help find any user-facing functionality in code.

**Work parallelization** - enable working in parallel with multiple people. Reduce the number of merge conflicts. Reduce the number of discussions about where to put some piece of code.

**Refactoring** - better understand the scope of a change. Gain much more confidence in changing a Feature by knowing it won't affect other Features. See what Features will be affected when changing a shared abstraction.

**AB Tests** - enable creating and removing experimental Features.

**Integration tests** - make it easier to write an integration test by clearly understanding what is being integrated.

## Non-goals

**Language and Franework** - it is language and framework agnostic. It leaves plenty of space to accommodate particular product needs and design decisions.

**Data flow model** - it is data flow agnostic. Unidirectional, reactive, or actor data model doesn't matter as long as the principles are not broken.

**Data fetching** - it is network layer agnostic.
Websockets or HTTP, REST, RPC or GraphQL - doesn't matter as long as the principles are not broken.

## How

Feature Driven Architecture defines three concepts: Feature, Cluster, and Screen. Each concept follows the core principles.

A concept of a "Feature" is the foundation of Feature Driven Architecture. Everything else exists to support it.

Breaking any principle described in this architecture will lead to specific problems in your codebase, and the goal here is to define the benefits and trade-offs.

## Core Principles

1. Decentralization
1. Co-location
1. Isolation
1. Disposability
1. Explicit sharing

## Feature

> A Feature is an isolated user-facing reusable complex building block(s) that solves a particular problem for a user.

Feature scope generally depends on the product and organizational needs, but a specific Feature should have a clearly defined scope by its maintainers.

A Feature implements Core Principles.

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

## Cluster

> Cluster is a reusable bundle of Features.

A Cluster is useful when you need to bundle several Features and reuse them together on different Screens.

A Cluster can be used to forward data from a Screen, from one Feature to another, and configure Features.

A Cluster is needed to avoid duplication of setup code for Features, and if the setup is trivial - you don't need it. _Cluster is an optional concept._

A Cluster implements Core Principles.

1. A Cluster can not know about the existence of any other Cluster.
1. A Cluster can not know about the Screen it's been used on.
1. A Cluster must be cohesive.
1. A Cluster can have dependencies.
1. A Cluster has to be disposable.

## Screen

> A Screen represents the content of the entire Screen.

A Screen can use Clusters and Features to position them on the Screen. A Screen is responsible for the global layout. A Screen knows all Clusters and Features it is using.

A Screen implements Core Principles.

1. A Screen can not know about the existence of any other Screen.
1. A Screen must be cohesive.
1. A Cluster has to be disposable.
