# Active Record Migration

## Migration

In Rails, you typically ==define the attributes of a model in a database migration, rather than in the model file itself.== When you create a new `LineItem` object, Rails will check the `line_items` table definition and automatically give the new `LineItem` object attributes that match the columns of the table. So even though you don't see a definition of `price` in the `LineItem` model file, Rails provides that attribute for you based on the database schema. You can access and modify these attributes just like any other property of the object.

For example, `price` and `quantity` would be columns in the `line_items` table in the database. ==Rails then automatically creates getter and setter methods for those columns, namely, Rails will infer their existence from the database schema.==

==% Migrations 是用來改變數據庫表結構的：創建表，刪除表，重命名表；增加欄位，減少欄位，改變欄位。%==

Before this migration is run, there will be no table. After, the table will exist.

Migrations are subclasses of the Rails class `ActiveRecord::Migration`.

### Migration Naming

==Migrations 也是延用了 Convention over Configuration 的原則。==

If the migration name is of the form "AddColumnToTable" or "RemoveColumnFromTable" and is followed by a list of column names and types then a migration containing the appropriate add\_column and remove\_column statements will be created.

The name of the migration class (CamelCased version) should match the latter part of the file name. For example, `20080906120000_create_products.rb` should define class `CreateProducts` and `20080906120001_add_details_to_products.rb` should define class `AddDetailsToProducts`.

% 我認為 migration的命名，應該用名詞而非動詞，因為這會產生一個 Class name。 例如：ProductsCreation，ProductsDetailsAddition。也就是TableNameContentAction三部分。20240119 %

### Supported Column Types

The column types supported by migrations are:

`:string, :text,`

`:integer, :decimal, :float,`

`:boolean,`

`:date, :datetime, :time, and :timestamp,`

`:binary`

### Migration Generator

The `model`, `resource`, and `scaffold` generators will create migrations appropriate for adding a new model.

```ruby
rails generate migration AddPartNumberToProducts part_number:string price:decimal
```

This will generate the following class:

```ruby
class AddPartNumberToProducts < ActiveRecord::Migration[7.0]
	def change
		add_column :products, :part_number, :string
		add_column :products, :price, :decimal
	end
end
```

References are a shorthand for creating columns, indexes, foreign keys, or even polymorphic association columns.

==% 一般地，我就統一使用 `change`，不使用 `up` 和 `down`。%==

### creating and dropping tables

```ruby
def change
	create_table :histories do |t|
		t.integer :order_id, null: false
		t.text :notes
     end
end
```

Generally the call to `drop_table` isn’t needed, as `create_table` is reversible.

### Renaming Tables

If refactoring leads us to rename variables and columns, then it’s probably not a sur

```ruby
def change
	rename_table :order_histories, :order_notes
```

### Changing Columns

Like the `remove_column` and `add_column`, Rails provides the `change_column` migration method.

Note that `change_column` command is irreversible.

### Running Migrations

The very first migration-related rails command you will use will probably be `rails db:migrate`. In its most basic form it just runs the `change` or `up` method for all the migrations that have not yet been run. If there are no such migrations, it exits. It will run these migrations in order based on the date of the migration.

If you specify a target version, Active Record will run the required migrations (`change`, `up`, `down`) until it has reached the specified version.

### Rolling Back

Active Record knows how to reverse this migration as well: if we roll this migration back, it will remove the table. A common task is to rollback the last migration.

==The `rails db:rollback` will rollback the latest migration==, either by reverting the `change` method or by running the `down` method. If you need to undo several migrations you can provide a `STEP` parameter.

The `rails db:migrate:redo` command is a shortcut for doing a rollback and then migrating back up again.

## Schema

Migrations, mighty as they may be, are not the authoritative source for your database schema. Your database remains the authoritative source. By default, Rails generates `db/schema.rb` which attempts to capture the current state of your database schema.

It tends to be faster and less error prone to create a new instance of the app's database by loading the schema file via `rails db:schema:load` than it is to replay the entire migration history.

Schema files are also useful if you want a quick look at what attributes an Active Record object has.

Because schema files are commonly used to create new databases, it is strongly recommended that you check your schema file into source control.

## Seed

To add initial data after a database is created: fill up `db/seeds.rb` with some Ruby code, and run `rails db:seed`.

### Using gem seed\_dump

https://github.com/rroblak/seed_dump

#### Add it to your Gemfile with:

gem 'seed\_dump'

#### Dump all data directly to db/seeds.rb:

rake db:seed:dump

\# Append to db/seeds.rb instead of overwriting it:

rake db:seed:dump APPEND=true

\# Dump only data from the users table and dump a maximum of 1 record:

$ rake db:seed:dump MODELS=User LIMIT=1

\# Use another output file instead of db/seeds.rb:

rake db:seed:dump FILE=db/seeds/users.rb

