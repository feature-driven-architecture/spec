# Principles of Feature Driven Architecture for UI Engineering

1. A concept of a "feature" is the foundation of Feature Driven Architecture.
1. A feature is a self-contained user-facing reusable complex building block.
1. A feature scope is generally flexible. It depends on the product and organizational needs, but a specific feature should have a clearly defined scope.
1. A feature can not know about the existence of any other feature.
1. A feature must be cohesive and co-locate its implementation in the location associated with the feature name.
1. A feature can declaratively express its dependencies in a form designed to be understood and provided by its consumers.
1. A feature has to be disposable. You have to implement a feature in a way that lets you remove it without leaving any remains behind.
1. A feature has to be composable. You should be able to compose multiple features on the same or different screens without modifying a feature.
1. A feature should help engineers discover how the software works and help communicate with product owners.
