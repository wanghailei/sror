# Rails Structure

## Rails in one sentence

Rails is a development framework for creating <mark style="background-color:orange;">database-backed web applications</mark> according to the MVC pattern.

## MVC

<mark style="background-color:yellow;">% The Model handles business logic, the Controller handles application logic and the View handles presentation logic.</mark> %

<mark style="background-color:yellow;">% Controllers 負責生成並發回 HTTP Response，這個 HTTP Response  的內容主體（body）是一個HTML（或JSON等），而這個HTML是基於把某個template填充數據來完成的——被稱為 render。這些數據的填充是由Controller action決定的。Action中命令會操控某些Model進而訪問數據庫來準備好數據。20231219 %</mark>

### Model layer

The _**Model layer**_ represents the domain model (such as Account, Product, Person, Post, etc.) and encapsulates the business logic specific to your application.&#x20;

In Rails, <mark style="background-color:orange;">database-backed model classes</mark> are derived from `ActiveRecord::Base`. Active Record allows you to present the data from database rows as objects and embellish these data objects with business logic methods.&#x20;

Although most Rails models are backed by a database, models can also be ordinary Ruby classes, or Ruby classes that implement a set of interfaces as provided by the Active Model module.

### View layer

The _**View layer**_ is composed of "templates" that are responsible for providing appropriate representations of your application's resources. Templates can come in a variety of formats, but most view templates are HTML with embedded Ruby code (ERB files). Views are typically <mark style="background-color:orange;">rendered to generate a controller response</mark> . In Rails, View generation is handled by Action View.

### Controller layer

<mark style="background-color:orange;">The Controller works at a higher level, processing the HTTP requests and preparing the HTTP responses.</mark>

The _**Controller layer**_ is responsible for handling incoming HTTP requests and providing a suitable response. Usually, this means returning HTML. Controllers load and manipulate models, and render view templates in order to generate the appropriate HTTP response.&#x20;

In Rails, incoming requests are routed by Action Dispatch to an appropriate controller, and controller classes are derived from `ActionController::Base`.&#x20;

## Other Frameworks and libraries

Rails also comes with:

* Action Mailer, a library to generate and send emails
* Action Mailbox, a library to receive emails within a Rails application
* Active Job, a framework for declaring jobs and making them run on a variety of queuing backends
* Action Cable, a framework to integrate WebSockets with a Rails application
* Active Storage, a library to attach cloud and local files to Rails applications
* Action Text, a library to handle rich text content
* Active Support, a collection of utility classes and standard library extensions that are useful for Rails, and may also be used independently outside Rails

The model represents the '**state**' of the application.

The View presents the model data to the users and also enables them to modify the data. The View does not use the data from Model directly, but through the Controller, namely <mark style="background-color:orange;">the View has not direct connection with the Model.</mark>

The Controller is the bridge between the Model and the View and is responsible for application logic. It handles the user's input and interactions and updates the model and view accordingly.

In the Model-View-Controller (MVC) architecture, the View does not directly communicate with the Model. Instead, the Controller serves as the intermediary: Controller receives user input and makes calls to the Model.&#x20;

Model performs the business logic (like data manipulations or database interactions) and returns the results to the Controller. <mark style="background-color:orange;">Controller takes the data from the Model and decides how to present it</mark>, which is often by passing it to a View. View then uses this data to render the appropriate user interface.

<mark style="background-color:orange;">The View just renders the HTML, but does not "send" HTML back to the Browser.</mark>

The Controller then takes this rendered HTML from the View and sends it back as a response to the client (browser).



Here's a simplified version of how this flow generally works in a framework like Rails:

* The browser sends an HTTP request to the application.
* <mark style="background-color:orange;">The router within the application decides which controller should handle the request,</mark> based on the routing rules defined in the application.
* The controller receives the request and based on the request, might interact with a Model (which communicates with a database) to retrieve or manipulate data.
* The controller then passes this data to the View.
* The View uses this data the View might need to render the HTML.
* The HTML from the View is sent back to the Controller, which then includes it in an HTTP response. This HTTP response is sent back to the client by the web server.



***

**WHL: Who decides whether an interaction with the database is needed, the Controller or the Model?**

ChatGPT: <mark style="background-color:orange;">The Controller decides when an interaction with the database is necessary based on the business logic of the application.</mark>

When a request comes into the application, the Controller is the component that first handles the request. It then determines what needs to be done to satisfy that request.

If the Controller determines that data needs to be fetched, created, updated, or deleted from the database, it will interact with the appropriate Model to do so. The Model is responsible for handling the actual interaction with the database, but it's the Controller that initiates the process.

The Controller will then take the data returned by the Model (if any), and pass it to the View.&#x20;

In this way, the Controller acts as a kind of director, deciding when and how the other components of the application should do their work. The Model and the View, meanwhile, focus on their specific responsibilities: interacting with the database and generating HTML, respectively.

## Routes

Routes' primary purpose is to connect view to controller, and they also serve as a UI element--URL.

Rules:

* Always use canonical routes that conform to Rails’ defaults.
* Avoid custom actions in favor of creating new resources that use Rails’\
  default actions.
* User-friendly URLs should be added in addition to the canonical routes.

<mark style="background-color:orange;">Using resources to define routes:</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`resources :widgets`</mark><mark style="background-color:orange;">. It's the best way.</mark>

`bin/rails routes -g widgets`

If the app’s routes are made up entirely of calls to resources, it becomes easy to understand the app at a high level.



# Page

Reading the source code of a framework like Ruby on Rails is indeed a great way to deepen your understanding of both the framework and the Ruby language. Rails is a large codebase, so having a structured approach is beneficial. Here's a suggested order for reading through the Rails 7.1 repository:

1\. \*\*Start with the Documentation\*\*: Begin by reading the README and CONTRIBUTING files in the Rails repository. These documents often contain valuable information about the structure and philosophy of the project.

2\. \*\*Rails Guides\*\*: Before diving into the code, it's useful to read through the \[Rails Guides]\(https://guides.rubyonrails.org/). They provide a high-level overview of the components of Rails and how they work together.

3\. \*\*Configurations and Initializers\*\*: Look at the config and initializers directories. This will give you an understanding of the configuration options Rails provides and how it sets itself up.

4\. \*\*Rails Frameworks Overview\*\*:

\- \*\*Active Record\*\*: Start with Active Record, as it's one of the core components. Understand how Rails handles database interactions.

\- \*\*Action Controller\*\*: Then, move to Action Controller to see how Rails processes web requests and returns responses.

\- \*\*Action View\*\*: Next, explore Action View to understand how Rails handles views and rendering.

\- \*\*Active Support\*\*: Look into Active Support, which provides Ruby language extensions used throughout Rails.

\- \*\*Active Job\*\*: Investigate Active Job, which is for background jobs.

\- \*\*Action Mailer\*\*: Finally, read Action Mailer, which is for sending emails.

5\. \*\*Middleware\*\*: Rails makes heavy use of middleware. Understanding the middleware stack will give you insights into how Rails handles requests.

6\. \*\*Railties\*\*: This module ties the various frameworks together and is crucial for understanding how the Rails initialization process works.

7\. \*\*Tests\*\*: Read through the test suite. Rails has extensive tests, and reading them can provide insights into how features are supposed to work and how the code is structured.

8\. \*\*Sample Applications\*\*: Look at sample applications built with Rails. They can provide practical examples of how the Rails components are used in real-world scenarios.

9\. \*\*Contributions and Issues\*\*: Review the contributions and issues in the Rails GitHub repository. Observing the discussions and code changes can provide a deeper understanding of why certain decisions were made.

10\. \*\*Follow the Changelog\*\*: Keep an eye on the CHANGELOG file in the Rails repository to stay updated with the latest changes.

Remember, it's okay if you don't understand everything immediately. Rails is a complex framework, and understanding it deeply takes time and practice. Consider supplementing your reading with experimentation—modify the code, run it, and see what changes. This hands-on approach can significantly enhance your learning.



---

## Rails source code structure



Based on the provided screenshot, you have a view of the Rails `actionpack` gem directory structure, focusing on the `action_controller` module. Here is a detailed analysis of the directory structure and the purpose of the files within the `action_controller` module:

* **`abstract_controller`**: A directory that includes base functionality for both `ActionController` and `ActionMailer`, such as rendering and layout support.
	* `base.rb`: This is likely the base class that `ActionController::Base` inherits from, providing core functionality.
	* `caching.rb`: Adds caching support to controllers, such as page, action, and fragment caching.
* **`action_controller`**: The main directory for controller-related features.
	* `api.rb`: Defines `ActionController::API`, a lightweight version of `ActionController::Base` for API-only applications, stripping out browser-specific features.
	* `base.rb`: The core class `ActionController::Base` that most Rails controllers inherit from.
	* `helpers.rb`: Contains modules that provide helper methods to be used in views and controllers.
	* Other files like `mime_responds.rb`, `redirecting.rb`, and `strong_parameters.rb` provide specific functionalities for handling MIME type responses, HTTP redirects, and strong parameter filtering, respectively.
* **`action_dispatch`**: Related to the routing part of the request cycle, handling the dispatching of incoming requests to the appropriate controller and action.
* **`metal`**: Contains components for building "metal" controllers, which are minimalistic controllers that give more control over the performance trade-offs.
	* `metal.rb`: Likely provides the base functionality for creating metal controllers.
* **`railties`**: This directory integrates `ActionController` with the rest of the Rails framework.
* **`renderer.rb`, `rendering.rb`, and `template_assertions.rb`**: Concerned with rendering views and providing test assertions for view templates.

The `action_controller.rb` file in the root of the `action_controller` directory is typically the main entry point for requiring all the necessary files and dependencies for this module.

Each file or directory has a specific purpose, contributing to the overall functionality of `ActionController`. Together, they provide the necessary tools to process HTTP requests, render views, manage caching, and integrate with Rails' MVC framework.







