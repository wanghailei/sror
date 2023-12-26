# Upgrade a Rails app

## 2. rails new

The `rails new` command creates a new Rails application with a default directory structure and configuration at the path you specify.

You can specify extra command-line arguments to be used every time 'rails new' runs in the .railsrc configuration file in your home directory, or in $XDG\_CONFIG\_HOME/rails/railsrc if XDG\_CONFIG\_HOME is set.

<mark style="background-color:orange;">But tailoring rails new command should be as little as possible, since it can be hard to add back parts of Rails you initially skip</mark>, and for the most part, the parts of Rails you don’t use can sit there, inert, not bothering anyone.

`rails new appname -d=postgresql -a=propshaft`

`rails new appname -d=postgresql -a=propshaft -c=tailwind`

`rails new appname -d=postgresql -a=propshaft -c=tailwind --skip-action-mailer --skip-action-mailbox --skip-active-job`

`rails new appname -css=tailwind -asset-pipeline=propshaft --skip-action-mailer --skip-action-mailbox --skip-active-job --skip-active-storage --no-skip-action-text`

Options:

\-d, \[--database=DATABASE] # Preconfigure for selected database (sqlite3/mysql/postgresql)\


\-G, \[--skip-git] # Skip .gitignore file

\[--skip-keeps] # Skip source control .keep files

\-M, \[--skip-action-mailer] # Skip Action Mailer files

\[--skip-action-mailbox] # Skip Action Mailbox gem

\[--skip-action-text], \[--no-skip-action-text] # Skip Action Text gem

\-O, \[--skip-active-record] # Skip Active Record files

\[--skip-active-job] # Skip Active Job

\[--skip-active-storage] # Skip Active Storage files

\-C, \[--skip-action-cable] # Skip Action Cable files

\-A, \[--skip-asset-pipeline] # Indicates when to generate skip asset pipeline\


\-a, \[--asset-pipeline=ASSET\_PIPELINE] # Choose asset pipeline (sprockets, propshaft)

\-J, \[--skip-javascript], \[--no-skip-javascript] # Skip JavaScript files

\[--skip-hotwire] # Skip Hotwire integration

\[--skip-jbuilder] # Skip jbuilder gem

\-j, \[--javascript=JAVASCRIPT] # Choose JavaScript approach \[importmap, webpack, esbuild, rollup]

\-c, \[--css=CSS] # Choose CSS processor \[options: tailwind, bootstrap, bulma, postcss, sass]\


\-B, \[--skip-bundle], \[--no-skip-bundle] # Don't run bundle install

\-T, \[--skip-test] # Skip test files

\[--skip-system-test] # Skip system test files

\[--skip-bootsnap] # Skip bootsnap gem

\[--no-rc], \[--no-no-rc] # Skip loading of extra configuration options from .railsrc file

\[--api], \[--no-api] # Preconfigure smaller stack for API only apps

\[--minimal], \[--no-minimal] # Preconfigure a minimal rails app

\-f, \[--force] # Overwrite files that already exist

\-s, \[--skip], \[--no-skip] # Skip files that already exist\


\-p, \[--pretend], \[--no-pretend] # Run but do not make any changes

\-h, \[--help] # Show this help message and quit

\-v, \[--version], \[--no-version] # Show Rails version number and quit

#### .railsrc

\--database=postgresql

\--asset-pipeline=propshaft

\--javascript=importmap

## 3. Configuring Database

#### 3.1 database.yml for configuring database connection.

You'll need to specify your PostgreSQL username, password, host, and database name for the development, test, and production environments.

Make sure not to include sensitive data like your database password directly in the database.yml file. Instead, use environment variables to store sensitive data.

default: \&default

adapter: postgresql

encoding: unicode

username: myuser

password: mypassword

pool: <%= ENV.fetch("RAILS\_MAX\_THREADS") { 5 } %>

development:

<<: \*default

database: myapp\_development

test:

<<: \*default

database: myapp\_test

\# In Rails, drop and recreate the PostgreSQL database:

rake db:drop

rake db:create

#### 3.2 Setup PostgreSQL for Rails on macOS

Install PostgreSQL:

brew install postgresql@16

You will need to manage the server on its own, setting up the user(s) and database(s) before connecting them to Rails.

Homebrew starts the server and creates a default database named postgres automatically upon installation.

You can check your server status by:

brew services list

To start, stop or restart a Postgre server:

brew services start postgresql@16

brew services stop postgresql@16

brew services restart postgresql@16

\# If you don't want/need a background service you can just run:

/opt/homebrew/opt/postgresql@14/bin/postgres -D /opt/homebrew/var/postgresql@14

#### 3.3 Create databases for Rails environments

\# Create databases for Rails development and test, with the "psql" tool.

psql postgres

CREATE DATABASE appname\_development;

CREATE DATABASE appname\_test;

\# Create a database superuser and set password.

CREATE USER dillone WITH SUPERUSER ENCRYPTED PASSWORD 'Mac2Milan\_\_';

ALTER DATABASE appname\_development OWNER TO dillone;

ALTER DATABASE appname\_test OWNER TO dillone;

\# Copy data from SQLite3 to PostgreSQL with "sequel" tool.

\# Make sure the PostgreSQL database is empty before running the sequel command.

bundle exec sequel -C sqlite://db/development.sqlite3 postgres://dillone:Mac2Milan\_\_@localhost/depot\_development

## 4. Modify gemfiles???

1\. rails new appname

2\. bin/dev

Rails Environment and Versions

### Set up a new environment of Rails



\# To install a gem (Ruby package), run:

$ gem install \<gemname>

\# List installed gems

$ gem list

\# To check if any installed gems are outdated:

$ gem outdated

\# Remove old gem versions

\# RubyGems keeps old versions of gems, so feel free to do some cleaning after updating:

$ gem cleanup

#### Rails

$ sudo gem install rails

$ rails new my-app --css tailwind -a propshaft

\# Propshaft is an asset pipeline library for Rails.

\# It's built for an era where bundling assets to save on HTTP connections is no longer urgent.

\# How to run a Rails deposit on a new Mac.

$ rails db:migrate

$ rails db:seed

$ rake assets:precompile

\# When you're developing your application, you want to run Tailwind in watch mode, so changes are

\# automatically reflected in the generated CSS output. You can do this either by running:

$ rails tailwindcss:watch as a separate process,

or by running:

$ ./bin/dev

which uses foreman to starts both the Tailwind watch process and the rails server in development mode.

#### Tailwind CSS for Rails

$ rails tailwindcss:build

\# This input file will be used to generate the output in app/assets/builds/tailwind.css.

\# Error：The asset "tailwind.css" is not present in the asset pipeline.

$ rake assets:precompile
