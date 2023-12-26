# Upgrade

<mark style="background-color:red;">**Upgrade step by step, and use version control!**</mark> <mark style="background-color:red;"></mark><mark style="background-color:red;">Use Git to track changes after each step.</mark>

***

**Setup an up-to-date environment for developing webpps with Ruby on Rails.** First, the tools' value and relationship need to be understood.

\
RubyGems belongs to Ruby. \
RubyGems manages many Gems.\
Bundler is a Gem. \
Rails is a Gem.

## Bundler

<mark style="background-color:orange;">Bundler is not a technology specific to Rails.</mark> Bundler is a dependency management tool for Ruby. <mark style="background-color:orange;">Bundler is a gem to bundle gems.</mark> It is an exit from dependency hell.&#x20;

Bundler makes sure a Ruby app run the same code on every development, staging, and production machine. <mark style="background-color:orange;">It records the exact versions that have been installed, so that others can install the exact same gems.</mark> <mark style="background-color:red;">% 應該說，Bundler 是團隊開發協作用的。20230619 %</mark>

### How Bundler works

First, given the gems listed in the Gemfile of a Ruby app, Bundler checks the versions of every gem to make sure that they are compatible, and can all be loaded at the same time.

Then, Bundler downloads and installs those gems, as well as any other gems needed by the gems that are listed.  And <mark style="background-color:orange;">it creates a file called Gemfile.lock with the list of the gems installed along with their respective versions.</mark>

It will require them while booting.

After the gems have been installed, Bundler can help you update them when new versions become available. Bundler is also an easy way to create new gems.&#x20;

## Gemfile

A Gemfile describes the gem dependencies required to execute associated Ruby code. A Gemfile is evaluated as Ruby code. Place the Gemfile in the root of the directory containing the associated code.

<mark style="background-color:orange;">The Gemfile is indeed related to Bundler and not directly to RubyGemsRubyGems itse.</mark>

## RubyGems

RubyGems is a package management framework for Ruby. Commonly gems are used to distribute **reusable functionality** that is shared with other Rubyists for use in their applications and libraries.

The RubyGems software allows you to easily download, install, and use ruby software packages on your system. The software package is called <mark style="background-color:orange;">a “gem” which contains a packaged Ruby application or library.</mark>



***

## Upgrade Ruby to the latest version on macOS

**Update Homebrew** to make sure you have the latest formulae for Ruby.&#x20;

```bash
brew update
```

**U**pgrade Ruby to the latest version available in Homebrew:

```bash
brew upgrade ruby
brew upgrade ruby@3.3.0 // or to a specific version.
```



***

## Verify the Rails version of an app

<mark style="background-color:orange;">Note that the terminal commands will work only when you are inside the Rails application directory, otherwise, it will display the latest installed version of Rails on your system.</mark> If the application is using a different version specified in the Gemfile, it may not be accurate.

1\. Via the Gemfile.lock: The Gemfile.lock in a Rails application specifies the exact versions of each gem that the application is using. Look for the line specifying the rails gem version in this file.

2\. Via the command line:cIn the terminal, navigate to the directory of your Rails app and use the command `rails -v` . This will display the current version of Rails the application is using.

3\. Via the Rails console: Another option is to open the Rails console with the command rails console or `rails c`, then print the Rails version with `Rails.version`.



***

The Bundler update steps should be performed within the Rails app's directory, not in the home (`~`) directory. This is important because Bundler needs to access the `Gemfile` and `Gemfile.lock` specific to your Rails application.&#x20;

## Upgrade the Rails version of an app

Step 1: Update the gem and its dependencies. Modify the Rails gem version in your Gemfile, then run:

```
bundle update rails
```

Bundler will update the Rails gem to the latest version specified in the Gemfile, along with all its dependencies. But it does not make any changes to the configuration files, initializers, or other Rails-specific files in your application.

Make sure your application's configuration and boilerplate code are up-to-date with the new Rails version, by running:

```
bin/rails app:update
```



***

## Upgrade the Bundler version of an app

It's important to ensure that the newer Bundler version is compatible with your Rails 7 app and other gem dependencies.&#x20;

==% 其實我認為，一般就用最新版的 Bundler。20231221 %==

1. If the `Gemfile` explicitly specifies a Bundler version (like `gem 'bundler', '~> 2.4.13'`), update this line to allow the newer version. You might want to specify a version range that includes the new version but is still compatible with your app.
2.  Install the latest stable release of Bundler, or install a specific version:

    ```
    gem install bundler
    gem install bundler -v 2.4.13
    ```
3.  Go to your Rails application's root directory to update Gemfile.lock.

    ```bash
    bundle update --bundler
    ```

    This command updates the `BUNDLED WITH` section in your app's `Gemfile.lock` to the new Bundler version.
4.  After installing the required Bundler version, you can then run it specifically for your project. This command tells Bundler to use version 2.4.13 to manage your gems as specified in your `Gemfile`.

    ```bash
    bundle _2.4.13_ install
    ```

***

## **Update RubyGems itself**

`gem update --system`

## Upgrade the gems of an app&#x20;

1. Start by updating your `Gemfile`. For each gem, specify the latest version compatible with Rails 7. You might need to check each gem's documentation or repository for compatibility information.\
   <mark style="background-color:orange;">Update  gems incrementally. Avoid updating all gems at once</mark>, as this can introduce multiple breaking changes that are hard to debug. <mark style="background-color:orange;">Update one or a few gems at a time</mark>, then test your application to ensure it still works as expected.
2.  Once you've updated your `Gemfile`,  to update your `Gemfile.lock` with the new versions.

    ```sql
    bundle update
    ```


3.  To ensure all gems are installed correctly with the new Bundler version. This step will install the necessary gems based on your updated `Gemfile.lock`.

    ```bash
    bundle install
    ```

***

## Upgrade Rails and all gems on macOS to the newest version

```
gem update // updates all gems installed
gem update rails // updates a particular gem
```

#### RubyGems

\# To update to its latest version with:

$ gem update --system

\# Error: can't find gem bundler (= 2.4.13) with executable bundle

$ gem i bundler -v 2.4.13



