## Feature

Sometimes it is going to be hard to decide what a feature is and what it isn't.

### Problem is the core

At the core of any feature, there is a problem. A problem is a reason you have a feature in the first place. The first step in identifying your feature name and scope is defining what problem it is supposed to solve.

Once the problem definition is clearly stated, it is likely easy to say what feature you are building and what it should and shouldn't do.

### Login example

For example, let's say we want to implement a login functionality.

The first thing we need to understand is why we need a login in the first place and what it is. In simple terms, login is a way to identify a user. Login has a login and logout button, a login form, forgot login form, and potentially other functions.

Generalized, login is a form of authentication. The problem it solves is the need to provide certain data access only to authenticated users.

Therefore we could call the feature "authentication" and login button, and login form are its implementation details.

Having the feature definition as "authentication", we could add authentication using an OAuth service. It would still be part of the "authentication" feature because it is solving the same problem.