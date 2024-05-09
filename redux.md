# Redux

**Redux** is a state management library for JavaScript apps. It can be used with React, Angular, Vue and Vanilla JS because Redux is a state management

When an application UI needs to keep track of cosntantly changing data that flows through different components, this data could act in umpredictable ways or even enter infinite loops. Facebook encountered this problem and 
came up with an architectural pattern called *flux*. Redux is inspired by Flux but it has grown more popular due to its simplicity and elegance

**State Management Solutions**
- Flux
- Redux
- MobX

With Redux instead of scaterring application state in varios parts of the UI, we store all of the application State inside a central repository, that is a single JavaScript object called the **Store** that is the single source of Truth, you can think of it as a database for the front end, so with this architecture the different pieces of the UI will no longer maintain their own state, instead they get what they need for the store. If we need to update the data there is a single place we have to update, so this immediately solves the problem of synchronizing the data accross different parts of the UI, but Redux architecture also makes it easier to understand how the data changes in our applications if something goes wrong, we can see exactly how the data changed. How, why, when and where it came from

**Redux in a Nutshell** 
* Centralized application's state
* Makes data flow transparent and predictable

*Redux Dev Tools Chrome Extension*
We're going to work on a restaurant app. Imagine that you start adding items and suddenly you delete one, with *Time Travel Debbuging* you can return to how the previous UI lookled like.

We cal also sabe the entire application state in a file and reload the application from it later.

The tool *Log Rocket* gives you an always on Redux Dev Tools in production for everyone of your users, so if a user encounters a proble you can reload the application in the same state as the user and see what's going on. It's very powerful.

Another benefit of Redys