# Generators



In Rails, generators are simply scripts that use templates to create boilerplate code and improve your workflow saving you a quite a bit of time.

rails generate model ModellName

rails generate controller ListController show edit

rails generate scaffold ModelName ControllerName

rails generate migration AddNewTable

rails generate plugin PluginName

rails generate integration\_test TestName

rails generate session\_migration

Usage: rails generate GENERATOR \[args] \[options]

General options:

\-h, \[--help] # Print generator's options and usage

\-p, \[--pretend] # Do a test run and show you what files will be generated without actually generating them.

\-f, \[--force] # Overwrite files that already exist

\-s, \[--skip] # Skip files that already exist

\-q, \[--quiet] # Suppress status output

### Types of Generators

controller

application\_record

benchmark

channel

generator

helper

integration\_test

jbuilder

job

mailbox

mailer

migration

model

resource

scaffold

scaffold\_controller

system\_test

task

active\_record:application\_record

active\_record:multi\_db

erb:controller

erb:mailer

erb:scaffold

stimulus

test\_unit:channel

test\_unit:generator

test\_unit:install

test\_unit:mailbox

test\_unit:plugin

#### Generate a Model

rails g model ModelName

### rails generate scaffold

A scaffold in Rails is a full set of model, database migration for that model, controller to manipulate it, views to view and manipulate the data, and a test suite for each of the above.

The following command will generate a scaffold for a single resource called Task:

rails generate scaffold Task title:string

### Creating and Customising Rails Generators & Templates

Since Rails 3.0, generators are built on top of Thor. Thor provides powerful options parsing and a great API for manipulating files.
