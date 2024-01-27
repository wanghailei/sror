# Upgrade



==**Upgrade step by step, and use version control!** % Use Git to track changes after each step. %==

**Setup an up-to-date environment for developing webpps with Ruby on Rails.** First, the tools' value and relationship need to be understood.

- RubyGems belongs to Ruby. 
- RubyGems manages many Gems.
- Bundler is a Gem.
- Rails is a Gem.



## Upgrade the Ruby environment of macOS



### Update Ruby with `brew`

**Update Homebrew** to make sure it has the latest formulae for Ruby.&#x20;

```bash
$ brew update
```

Upgrade Ruby to the latest version available in Homebrew.

```bash
$ brew upgrade ruby
$ brew upgrade ruby@3.3.0 // or to a specific version.
```

## Install a new Ruby with brew

After brew install ruby, the .zshrc needs to be modified. 根據我的經驗教訓，.zshrc應該是這樣的：

```bash
export PATH="/opt/homebrew/bin:$PATH" 
export PATH="/opt/homebrew/sbin:$PATH" 
export PATH="/opt/homebrew/opt/ruby/bin:$PATH" 
export PATH="/opt/homebrew/lib/ruby/gems/3.3.0/bin:$PATH" 
export PATH=`gem environment gemdir`/bin:$PATH 
export LDFLAGS="-L/opt/homebrew/opt/ruby/lib" 
export CPPFLAGS="-I/opt/homebrew/opt/ruby/include" 
export PKG_CONFIG_PATH="/opt/homebrew/opt/ruby/lib/pkgconfig" 
export PATH="$PATH:/usr/local/bin" 
export PATH="$PATH:/Applications/RubyMine.app/Contents/MacOS" 
```

If you need to have ruby first in your PATH, run:

```bash
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
```

For compilers to find ruby you may need to set:

```bash
export LDFLAGS="-L/opt/homebrew/opt/ruby/lib"
export CPPFLAGS="-I/opt/homebrew/opt/ruby/include"  
```

For pkg-config to find ruby you may need to set:

```bash
export PKG_CONFIG_PATH="/opt/homebrew/opt/ruby/lib/pkgconfig"
```



% 我認為一般用 `brew` 升級Ruby就很好。但是我發現在 Ruby 3.3 發布一個星期之後，`brew` 都沒有更新到這個最新版。所以我不得不啟用`rbenv`。等到 brew 的最新版 Ruby 發布了，再重新安裝並切換回 brew 的版本。 %

### Update Ruby with `rbenv`

```bash
# list latest stable versions:
rbenv install -l

# list all local versions:
rbenv install -L

# install a Ruby version:
rbenv install 3.3.0

# make 3.3.0 the defaul version on macOS
rbenv global 3.3.0
```

==After `rbenv install` and `rbenv global`, the ~/.zshrc need to be modified for `ruby` to take effect:==

```bash
if command -v rbenv > /dev/null; then
	eval "$(rbenv init -)"
fi
```



## Bundler

Bundler is not a technology specific to Rails. ==Bundler is a dependency management tool for Ruby.== ==Bundler is a gem to bundle gems.== It is an exit from dependency hell.&#x20;

Bundler makes sure a Ruby app run the same code on every development, staging, and production machine. ==It records the exact versions that have been installed, so that others can install the exact same gems.== ==% 應該說，Bundler 是團隊開發協作用的。20230619 %==

==The Bundler update steps should be performed within the Rails app's directory, not in the home (`~`) directory.== This is important because Bundler needs to access the `Gemfile` and `Gemfile.lock` specific to your Rails application.

### How Bundler works

First, given the gems listed in the Gemfile of a Ruby app, Bundler checks the versions of every gem to make sure that they are compatible, and can all be loaded at the same time.

Then, Bundler downloads and installs those gems, as well as any other gems needed by the gems that are listed.  And ==it creates a file called Gemfile.lock with the list of the gems installed along with their respective versions.==

It will require them while booting.

After the gems have been installed, Bundler can help you update them when new versions become available. Bundler is also an easy way to create new gems.&#x20;



## RubyGems

RubyGems is a package management framework for Ruby. Commonly gems are used to distribute **reusable functionality** that is shared with other Rubyists for use in their applications and libraries.

The RubyGems software allows you to easily download, install, and use ruby software packages on your system. The software package is called ==a “gem” which contains a packaged Ruby application or library.==

#### Update RubyGems itself to the latest version on macOS

```bash
$ gem update --system
````

#### Upgrade all installed gems to the latest version on macOS

```bash
$ gem update
```

#### Upgrade a particular gem installed on macOS

```bash
$ gem update rails // updates a  gem
```

#### Error: can't find gem bundler (= 2.4.13) with executable bundle

```bash
$ gem i bundler -v 2.4.13
````

#### To install a gem (Ruby package), run:

```bash
$ gem install <gemname>
```

#### List installed gems

```bash
$ gem list
```

#### To check if any installed gems are outdated:

```bash
$ gem outdated
```

#### Remove old gem versions

RubyGems keeps old versions of gems, so feel free to do some cleaning after updating:

```bash
$ gem cleanup
```



## Upgrade a Rails app



### Verify the Rails version of an app

==Note that the terminal commands will work only when you are inside the Rails application directory, otherwise, it will display the latest installed version of Rails on your system.== If the application is using a different version specified in the Gemfile, it may not be accurate.

1\. Via the Gemfile.lock: The Gemfile.lock in a Rails application specifies the exact versions of each gem that the application is using. Look for the line specifying the rails gem version in this file.

2\. Via the command line: In the terminal, navigate to the directory of your Rails app and use the command `rails -v` . This will display the current version of Rails the application is using.

3\. Via the Rails console: Open the Rails console with the command `rails console` or `rails c`, then print the Rails version with `Rails.version`.

### Upgrade the Rails version of an app

**Frist step**: to update the Rails gem and its dependencies, by modify the Rails gem version in your Gemfile, then run:

```bash
$ bundle update rails
```

Bundler will update the Rails gem to the latest version specified in the Gemfile, along with all its dependencies. ==But it does not make any changes to the configuration files, initializers, or other Rails-specific files in the app.==

**Second step**: to make sure the app's configuration and boilerplate code are up-to-date with the new Rails version, by running:

```bash
$ bin/rails app:update
```

The command `$ bin/rails app:update` is used to update the Rails application with any new changes or updates that have been made in the Rails framework since the application was first created or last updated. This command is typically run when you upgrade your Rails version. It helps to ensure that your application is using the latest conventions and features provided by the updated Rails framework.

==When you run this command, Rails will create a new set of configuration files, initializers, and other necessary files for the updated version of Rails. It will also create a new `config/routes.rb` file and a new `config/application.rb` file.== It won't just overwrite your existing files. Instead, it will create new files with a `.new` extension (for example, `config/routes.rb.new`). This allows you to see what the new default files look like so you can decide whether to keep your old files, use the new ones, or merge the changes from the new files into your old ones.

It's recommended to always backup your application before running `$ bin/rails app:update`, thoroughly review and test the changes, and have a rollback plan in case something goes wrong.

### Gemfile

A Gemfile describes the gem dependencies required to execute associated Ruby code. A Gemfile is evaluated as Ruby code. Place the Gemfile in the root of the directory containing the associated code.

==The Gemfile is indeed related to Bundler and not directly to RubyGems itself.==

```ruby
gem "rails", "~> 7.1.3"
```

The `gem` method is used to declare a gem dependency for your application. 

This line says that the application depends on the "rails" gem, and requires a version that's compatible with version 7.1.3.

Remember to run `bundle install` after you update your Gemfile to install the required versions of each gem.

#### Gem Version Specifier

==The "`~> 7.1.2`" is a version specifier, also known as a pessimistic version constraint. This means that Bundler will update the Rails gem to the latest minor or patch version==, but not to a new major version (which could potentially include breaking changes). For example, with this constraint, Bundler could update Rails to version 7.1.3 or 7.2.0, but not to 8.0.0.

```ruby
gem "pg"
```

==The `gem` command without a version specifier tells Bundler to install the most up-to-date version of the gem that's compatible with your project.== Bundler will try to get the latest version of the gem that is compatible with all other gems in the Gemfile, taking into account all the requirements specified in your application's codebase.

`gem 'pg', '>= 1.1.0'` : install any version greater than or equal to 1.1.0
`gem 'pg', '1.1.0'`    : install exactly version 1.1.0
`gem 'pg', '~> 1.1.0'` : install the latest version of the 1.x series 
			(greater than or equal to version 1.1 but less than version 2.0) .

### Upgrade the gems versions of an app&#x20;

1. Start by updating your `Gemfile`. For each gem, specify the latest version compatible with Rails 7. You might need to check each gem's documentation or repository for compatibility information.
   ==Update gems incrementally. Avoid updating all gems at once==, as this can introduce multiple breaking changes that are hard to debug. ==Update one or a few gems at a time==, then test your application to ensure it still works as expected.
2.  Once you've updated your `Gemfile`, ==to update your `Gemfile.lock` with the new versions.==

    ```bash
    $ bundle update
    ```


3.  To ensure all gems are installed correctly with the new Bundler version. This step will install the necessary gems based on your updated `Gemfile.lock`.

    ```bash
    $ bundle install
    ```

### Upgrade the Bundler version of an app

It's important to ensure that the newer Bundler version is compatible with your Rails 7 app and other gem dependencies.&#x20;

==% 其實我認為，一般就用最新版的 Bundler。20231221 %==

1. If the `Gemfile` explicitly specifies a Bundler version (like `gem 'bundler', '~> 2.4.13'`), update this line to allow the newer version. You might want to specify a version range that includes the new version but is still compatible with your app.

2.  Install the latest stable release of Bundler, or install a specific version: ==% 用 brew install ruby 後，一定要 gem install bundler 安裝 bundler。否則就會報錯LoadError。20240119 %==

	```bash
	$ gem install bundler
	$ gem install bundler -v 2.5.5
	```

3.  Go to your Rails application's root directory to update Gemfile.lock.

	```bash
	$ bundle update --bundler
	```

	This command updates the `BUNDLED WITH` section in your app's `Gemfile.lock` to the new Bundler version.

4.  After installing the required Bundler version, you can then run it specifically for your project. This command tells Bundler to use version 2.4.13 to manage your gems as specified in your `Gemfile`.

	```bash
	$ bundle _2.5.5_ install
	```

