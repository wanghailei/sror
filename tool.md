---
description: Ruby tools and Rails tools.
---

# Tools

## Bundler

<mark style="background-color:orange;">Bundler: a gem to bundle gems.</mark>

Bundler is not a technology specific to Rails, but it is the way to manage your application’s Rubygem dependencies. One of the most important things that Bundler does is dependency resolution on the full list of gems specified in your configuration, all at once.

Bundler is a dependency management tool for Ruby. Bundler makes sure Ruby applications run the same code on every machine. Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production.

It does this by managing the gems that the application depends on. Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. It records the exact versions that have been installed, so that others can install the exact same gems.

Starting work on a project is as simple as bundle install.

<mark style="background-color:red;">% 應該說，Bundler 是團隊開發協作用的。20230619 %</mark>

Given a list of gems, it can automatically download and install those gems, as well as any other gems needed by the gems that are listed. Before installing gems, it checks the versions of every gem to make sure that they are compatible, and can all be loaded at the same time.

Bundler reads the Gemfile for the list of gems and ensures that the gems you need are present in development, staging, and production. It also fetches the metadata from the source provided, resolves the dependencies of each gem, installs them and then requires them while booting.

Bundler then makes use of RubyGems to install the gems listed on the Gemfile along with their dependencies and it creates a file called Gemfile.lock with the list of the gems installed along with their respective versions.

After the gems have been installed, Bundler can help you update some or all of them when new versions become available.

Bundler is also an easy way to create new gems. Just like you might create a standard Rails project using rails new, you can create a standard gem project with bundle gem. Create a new gem with a README, .gemspec, Rakefile, directory structure, and all the basic boilerplate you need to describe, test, and publish a gem.

## Gemfile

A Gemfile describes the gem dependencies required to execute associated Ruby code.

Place the Gemfile in the root of the directory containing the associated code.

A Gemfile is evaluated as Ruby code.

## RubyGems

RubyGems is a package management framework for Ruby.

The RubyGems software allows you to easily download, install, and use ruby software packages on your system. The software package is called <mark style="background-color:orange;">a “gem” which contains a packaged Ruby application or library.</mark>

Gems can be used to extend or modify functionality in Ruby applications. Commonly they’re used to distribute **reusable functionality** that is shared with other Rubyists for use in their applications and libraries.

**Updates all the gems installed.**

`gem update`

**Update RubyGems itself.**

`gem update --system`

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



### Copilot in Vim

`:Copilot setup`



###

