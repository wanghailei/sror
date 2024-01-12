# `rails new`

The `rails new` command creates a new Rails application with a default directory structure and configuration at the path you specify.

You can specify extra command-line arguments to be used every time 'rails new' runs in the .railsrc configuration file in your home directory, or in $XDG\_CONFIG\_HOME/rails/railsrc if XDG\_CONFIG\_HOME is set.

==But tailoring rails new command should be as little as possible, since it can be hard to add back parts of Rails you initially skip==, and for the most part, the parts of Rails you don’t use can sit there, inert, not bothering anyone.

```bash
rails new appname -a=propshaft
```



## ```rails new``` Options:

```bash
-d, --database=DATABASE # Preconfigure for selected database (sqlite3/mysql/postgresql)
-a, --asset-pipeline=ASSET_PIPELINE # Choose asset pipeline (sprockets, propshaft)
-j, --javascript=JAVASCRIPT # Choose JavaScript approach [importmap, webpack, esbuild, rollup]
-c, --css=CSS # Choose CSS processor [options: tailwind, bootstrap, bulma, postcss, sass]

--api # Preconfigure smaller stack for API only apps
--minimal # Preconfigure a minimal rails app

-s, --skip-keeps # Skip source control .keep files
-f, --force # Overwrite files that already exist
-p, --pretend # Run but do not make any changes
```



## .railsrc

```bash
--asset-pipeline=propshaft
```



****

## Rails

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
