# Rails Utilities



# ActiveSupport

==% ActiveSupport 是個武器庫啊！是個寶庫，慢慢挖掘！20231227 %==

Active Support is a collection of utility classes and Ruby standard library extensions. Active Support is responsible for ==providing Ruby language extensions and utilities==. It offers a richer bottom-line at the language level.

These additions reside in this package so they can be loaded as needed in Ruby projects outside of Rails.

## Concerns

Concerns are a way to make large controllers or models easier to understand and manage. This also has the advantage of reusability when multiple models (or controllers) share the same concerns.

A concern is only responsible for a focused subset of the model's responsibility.

The ActiveSupport::Concern gives us a simpler way to include them.



****

# Rails Engine

==Modularising your monolith using Rails Engines.==

Rails Engines can be considered miniature applications that provide functionality to their host applications. ==A Rails application is actually just a "supercharged" engine, with the `Rails::Application` class inheriting a lot of its behaviour from `Rails::Engine`.==

A Rails engine is a self-contained piece of functionality that can be added to an existing Rails application, or used as the foundation for a new Rails application. Essentially, it's a miniature Rails application that can be packaged and reused across multiple projects.

Rails engines provide a modular way to organise and reuse code in a Rails application. ==They allow you to encapsulate related functionality (such as authentication, payments, or notifications) in a separate namespace, with its own models, views, controllers, routes, and assets.==

An engine can include all the same features as a regular Rails application, including generators, migrations, tests, and configuration options. It can also have its own dependencies, such as gems or other engines.

Therefore, engines and applications can be thought of as almost the same thing.

Engines are also closely related to plugins. The two share a common lib directory structure, and are both generated using the rails plugin new generator.

It's important to keep in mind at all times that the application should always take precedence over its engines. An application is the object that has final say in what goes on in its environment. The engine should only be enhancing it, rather than changing it drastically.

To call an engine method in a Rails application, you can simply require the engine and call its methods as you would with any other Ruby class.



# Zeitwerk

Rails uses a Gem called Zeitwerk for autoloading. When Rails encounters an undefined constant in the code, it uses Zeitwerk which uses file-naming conventions to find and require the needed Ruby script.

Zeitwerk has the concept of autoload paths, and the default autoload paths include the base directories of just about anywhere you would think of adding code to your Rails application.



# ActionCable - WebSocket

Rails offers an abstraction over WebSockets: ActionCable.







## bin/dev

The \``bin/dev`\` script is a new feature of Rails 7 to make it easier to start up your development environment. This script allows you to start the Rails server along with other services your application might depend on.

`bin/dev` will start both the Rails server and the JS build watcher (along with a CSS build watcher, if you're also using cssbundling-rails).

The \``bin/dev`\` script isn't automatically created when you generate a new Rails 7 application, so you'll have to create it yourself.

<mark style="color:blue;">在 rails new 時，如果我安裝了 tailwind-rails 後，就有了 bin/dev；但如果我</mark>

### **Here's an example of how to create a simple \`bin/dev\` script:**

1\. In your Rails root directory, create a new file \`bin/dev\` and open it in a text editor.

2\. Add the following content:

\#!/bin/bash

foreman start -f Procfile.dev

This will start all the services defined in your \`Procfile.dev\` using the Foreman tool.

If you're using another process manager like Overmind, replace \`foreman\` with \`overmind\`.

3\. Save and close the file.

4\. Make the script executable by running this command in your terminal:

$ chmod +x bin/dev

Now you can start your development environment by running \`./bin/dev\` from your Rails root directory. This will run all the commands specified in your \`Procfile.dev\`.

Depending on your needs, you might want to add more commands to it, like commands to check if necessary services like PostgreSQL or Redis are running, or commands to run setup scripts.

### Procfile.dev

A Procfile defines various services that your application is composed of, such as a web server and a CSS builder.

`web: bin/rails server -p 3000` is a command to start the Rails server on port 3000.

`css: bin/rails tailwindcss:watch` is a command that presumably watches for changes in your Tailwind CSS files and rebuilds them.

