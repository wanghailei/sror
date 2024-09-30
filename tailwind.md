

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

