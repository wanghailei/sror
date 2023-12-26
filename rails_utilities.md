# Rails Utilities



## Concerns

Concerns are a way to make large controllers or models easier to understand and manage.

This also has the advantage of reusability when multiple models (or controllers) share the same concerns.

A concern is only responsible for a focused subset of the model's responsibility.

The ActiveSupport::Concern gives us a simpler way to include them.

## Rails Engine

Modularising your monolith using Rails Engines.

Rails Engines can be considered miniature applications that provide functionality to their host applications. <mark style="background-color:orange;">A Rails application is actually just a "supercharged" engine, with the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`Rails::Application`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">class inheriting a lot of its behaviour from</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`Rails::Engine`</mark><mark style="background-color:orange;">.</mark>

A Rails engine is a self-contained piece of functionality that can be added to an existing Rails application, or used as the foundation for a new Rails application. Essentially, it's a miniature Rails application that can be packaged and reused across multiple projects.

Rails engines provide a modular way to organise and reuse code in a Rails application. <mark style="background-color:orange;">They allow you to encapsulate related functionality (such as authentication, payments, or notifications) in a separate namespace, with its own models, views, controllers, routes, and assets.</mark>

An engine can include all the same features as a regular Rails application, including generators, migrations, tests, and configuration options. It can also have its own dependencies, such as gems or other engines.

Therefore, engines and applications can be thought of as almost the same thing.

Engines are also closely related to plugins. The two share a common lib directory structure, and are both generated using the rails plugin new generator.

It's important to keep in mind at all times that the application should always take precedence over its engines. An application is the object that has final say in what goes on in its environment. The engine should only be enhancing it, rather than changing it drastically.

To call an engine method in a Rails application, you can simply require the engine and call its methods as you would with any other Ruby class.



## Zeitwerk

Rails uses a Gem called Zeitwerk for autoloading. When Rails encounters an undefined constant in the code, it uses a library called Zeitwerk which uses file-naming conventions to find and require the needed Ruby script.

Zeitwerk has the concept of autoload paths, and the default autoload paths include the base directories of just about anywhere you would think of adding code to your Rails application.

## ActionCable - WebSocket

Rails offers an abstraction over WebSockets: ActionCable.



