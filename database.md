# Database

## Using the same database for all environments.

It's generally not recommended to use different databases for development and production in a Rails app. Something that works in SQLite may not work in PostgreSQL and vice versa. Using different databases can expose your app to potential database-specific bugs only in production.

## Setup and Reset the Database

The `rails db:setup` command will create the database, load the schema, and initialise it with the seed data.

The `rails db:reset` command will drop the database and set it up again. This is functionally equivalent to `rails db:drop db:setup`.

## `ActiveRecord::NoDatabaseError`

在T003實驗中，rails new 和 bundle install 之後，rails sever，會收到這個錯誤信息。因為，我沒有創建 PostgreSQL數據庫。

```ruby
We could not find your database: tiny2_development. 
Which can be found in the database configuration file located at config/database.yml.
```

點擊網頁上的一個按鈕就可以了 "Create database"。

並且，有一個提示：To create your database, run: `bin/rails db:create`

我做了T003實驗，在完成T002實驗的步驟後，我運行了 `bin/rails db:create`。此時再 `bin/rails server`，網頁運行正常。





# PostgreSQL vs MySQL

==% 停止探索、掙扎用哪個數據庫，就用 PostgreSQL。20231129 %==



***

### Normalization Principles

Normalisation is a database design technique that reduces data redundancy and eliminates undesirable characteristics like Insertion, Update and Deletion Anomalies. ==The goal is to divide your database schema into smaller tables and define relationships between them to increase the clarity, efficiency, and scalability of your database.==

***

**WHL: We are currently a small software company focusing on developing enterprise apps like ERP, CRM, WMS, TMS, PLM, for a client who running hundreds of bakery shops and two factories. they have about 1000-2000 persons access these system daily. We plan to use Rails 7, and we need to choose a database from PostgreSQL and MySQL. what's your suggestion?**

==**Bard: Based on the information you've provided, I would highly recommend PostgreSQL for your scenario.== Here's why:

**PostgreSQL's strengths for your case:**

* **Complex data models:** Enterprise applications like ERP, CRM, WMS, TMS, PLM often have intricate data models with complex relationships and queries. PostgreSQL's advanced data types, functions, and indexing capabilities are well-suited for handling these challenges effectively.
* **Scalability:** With hundreds of users accessing the system daily and potential for further growth, your database needs to handle increased activity efficiently. PostgreSQL scales very well, offering features like partitioning and replication to manage larger datasets and concurrent access.
* **Data integrity:** Enterprise applications require stringent data integrity to ensure accurate information and reliable operations. PostgreSQL's ACID transactions with multiversion concurrency control (MVCC) provide stronger data consistency and error protection compared to MySQL's strict ACID mode.
* **Advanced features:** PostgreSQL offers features like materialized views, full-text search, and JSONB data type, which can be very useful for improving query performance and handling various data formats in your enterprise applications.
* **Rails integration:** Rails 7 has further optimized its integration with PostgreSQL, making it easier to leverage its advanced features and benefit from its performance enhancements.

**While MySQL might be tempting due to its familiarity and ease of use, its limitations could become increasingly evident for your project:**

* **Complex queries:** MySQL can struggle with intricate queries and joins as your data model grows, potentially impacting performance and developer agility.
* **Scalability:** As your user base and data volume increase, MySQL could bottleneck under heavy load, requiring more frequent optimization or even sharding, which adds complexity.
* **Data integrity:** Although MySQL offers ACID transactions, its strict mode can impact performance. PostgreSQL's MVCC provides a more flexible and performant approach to data consistency.
* **Lack of advanced features:** Some features crucial for complex enterprise applications, like materialized views and advanced data types, are lacking in MySQL.

**Additional considerations:**

* **Team expertise:** If your team already has expertise in MySQL, switching to PostgreSQL might require additional training and investment. However, the long-term benefits of PostgreSQL for your specific needs may outweigh the initial learning curve.
* **Hosting environment:** Consider your hosting options. Some shared hosting providers might only offer MySQL. However, with increasing popularity of PostgreSQL, managed hosting options for PostgreSQL are readily available and often outperform shared hosting solutions.

**Conclusion:**

Based on your project's requirements and future growth potential, PostgreSQL seems like a wiser choice compared to MySQL. It offers enhanced data modeling capabilities, superior scalability, robust data integrity, and advanced features ideal for complex enterprise applications. While you might need to invest in some initial learning or hosting adjustments, the long-term benefits and increased flexibility outweigh the drawbacks.

Ultimately, the final decision rests with you. I recommend thoroughly evaluating both options based on your specific needs, team expertise, and hosting environment. However, based on the information you've provided, PostgreSQL presents a stronger solution for your ambitious goals with enterprise applications.

I hope this helps! Let me know if you have any further questions or need help exploring specific considerations for your project.



***



## About using array in database

**WHL: You know in Ruby, you use array to store multiple objects, and a common place is to iterate the array to manipulate each element in it. **<mark style="background-color:red;">**You don't use Array for storage but for operation**</mark>**, right? Yet, in a database, the main purpose is to store data with integrity as the first consideration. Therefore, **<mark style="background-color:red;">**I don't think to have array as a datatype in a database is a good idea.**</mark>

**ChatGPT**: You bring up an excellent point. The data storage needs of an application are often quite different from the data manipulation needs within the application logic, and this is a key distinction to keep in mind when considering whether to use array data types in a database.

As you noted, arrays are used extensively in Ruby (and most other programming languages) for manipulating collections of objects in memory. <mark style="background-color:orange;">They're great for transient operations where you need to process a list of items and then discard it.</mark>&#x20;

However, databases are primarily designed for the persistent storage of data, and their design principles reflect this. Normalization, as we discussed, is a key principle of relational database design that helps ensure data integrity and consistency. <mark style="background-color:orange;">Storing arrays in a database can violate normalization principles, leading to potential data redundancy and anomalies.</mark>

For example, if you're storing a list of tags as an array in a blog post record, and you want to rename a tag, you would have to find and update every post that contains that tag in its array. This operation could be slow and error-prone, especially if you have a large number of posts. If you had a separate tags table with a many-to-many relationship to posts, you could simply update the tag in one place.

<mark style="background-color:orange;">So while PostgreSQL's support for array data types can provide some convenience and flexibility for developers, it's not always the best choice from a data integrity and database design perspective.</mark> As always, the best approach depends on the specific needs and constraints of your application.



**WHL: Plus, with the power of modern computing hardwares, more complex queries due to the need for more JOIN operations, is not a problem at all. Right?**

Indeed, modern hardware is increasingly capable of handling complex queries with multiple JOIN operations. Query optimizers in contemporary database management systems are also very sophisticated, and they can often process complex queries with remarkable efficiency.

That being said, the complexity and performance of database queries can still be a concern in certain situations, especially when dealing with large volumes of data or highly concurrent workloads. Even with powerful hardware, poorly designed or overly complex queries can lead to performance bottlenecks. This is why understanding the principles of database design and query optimization remains important.

While JOIN operations can be computationally intensive, a well-designed database schema and well-optimized queries can often handle these operations quite efficiently. Moreover, many relational database systems, including both MySQL and PostgreSQL, support various types of indexes that can dramatically improve the performance of JOIN operations.

So, while it's true that modern hardware is increasingly capable, and that more complex queries involving JOINs are often not a problem, it's still important to design your database schema and your queries with care, taking into account the specific needs and constraints of your application.



**WHL: With this under belt, data integrity is more important than query efficiency in an enterprise and money or business deals environment.**

ChatGPT: Absolutely, <mark style="background-color:orange;">in an enterprise and business context, data integrity is paramount</mark>. The cost of data corruption or loss can be immense, potentially leading to incorrect business decisions, regulatory violations, loss of customer trust, and other serious consequences. Therefore, maintaining data integrity should always be a top priority.

This is one of the reasons why relational databases, which have strong support for data integrity through features like ACID transactions, data constraints, and referential integrity, continue to be widely used in enterprise environments.

Query efficiency is also important, of course, because it affects the performance and responsiveness of your applications. However, it should not come at the expense of data integrity. A well-designed database and properly optimized queries can usually provide both good performance and strong data integrity.

In the context of your original question about choosing between MySQL and PostgreSQL for Rails 7 applications, both databases have strong support for data integrity and can be a good choice depending on your specific needs. <mark style="background-color:orange;">PostgreSQL's advanced features and closer alignment with Rails philosophies may offer some advantages in terms of developer experience and flexibility</mark>, but <mark style="background-color:orange;">both databases are capable and mature choices for enterprise applications</mark>.



<mark style="color:green;">**WHL: Why MySQL didn't implement array datatype, I do believe they are capable of developing this feature. But they didn't. Does it mean the MySQL guys follow a more loyal philosophy to normalisation principles?**</mark>

**ChatGPT**: MySQL, indeed, has chosen not to implement an array data type, unlike PostgreSQL. While I can't speak for the MySQL development team, <mark style="background-color:orange;">it's reasonable to infer that this decision aligns with a more traditional interpretation of relational database principles, which emphasise atomicity of data.</mark>

In relational database theory, each value in a table is supposed to represent a single, indivisible piece of information. This is known as the principle of atomicity, and it's one of the key ideas behind the first normal form (1NF). By not implementing array types, which inherently contain multiple pieces of information, MySQL stays more closely aligned with this principle.

It's important to note that this doesn't necessarily make MySQL inherently better or worse than PostgreSQL—it's just a different design philosophy. Some developers and applications may benefit from PostgreSQL's more flexible approach, which includes support for arrays and other non-traditional data types. Others may prefer MySQL's more strict adherence to traditional relational database principles.

In the end, the best database system for a given application depends on the specific needs and constraints of that application. It's up to the developer to understand these needs and constraints, and to choose the database system that best meets them.

Yet, MySQL implemented JSON datatype, do you think it's a violation to the atomicity and normalisation principles?

ChatGPT

ChatGPT

1 / 1

The JSON data type in MySQL does represent a somewhat different approach compared to traditional relational database principles. JSON data can be complex and nested, so it doesn't necessarily comply with the concept of atomicity, which is a key component of the first normal form (1NF).

However, the introduction of the JSON data type in MySQL (and other relational databases) is largely a recognition of the evolving needs of modern applications. JSON has become a standard data interchange format, and many applications need to store and query JSON data. By supporting the JSON data type, MySQL allows these applications to store JSON data natively and perform complex queries on it, which can be more efficient and convenient than storing JSON data as a string and processing it in the application.

It's important to note that just because MySQL supports JSON data doesn't mean it's always the best choice. For many applications, a traditional relational schema will be more appropriate. Normalization and atomicity are still important principles that can help ensure data integrity and consistency.

Using JSON fields in MySQL, or any other SQL database, should be a deliberate design decision based on the specific needs of your application. It can be useful for storing semi-structured data or data with a flexible schema, but it should not be used as a replacement for proper database design and normalization where those principles apply.

1 / 1

Do you think using JSON accordingly but strictly forbidding array in database usage is a good practice?

ChatGPT

ChatGPT

1 / 1

Whether using JSON and forbidding arrays in database usage is a "good practice" really depends on the specific needs and constraints of your application. Here are a few points to consider:

JSON for semi-structured data: JSON can be a good choice for storing semi-structured data, or data with a flexible schema that doesn't fit neatly into a relational model. For example, you might use a JSON field to store custom attributes for a user profile or product listing, where different records might have different sets of attributes.

Avoid arrays for atomicity and normalization: As we discussed earlier, storing arrays in a database can violate the principles of atomicity and normalization. It can lead to data redundancy and anomalies, and it can make certain types of queries and updates more difficult and less efficient. Therefore, in many cases, it's better to represent many-to-many relationships with a separate join table, rather than storing arrays of values in a single field.

Performance considerations: JSON fields and array fields can have performance implications. For example, querying and indexing JSON data or array data can be less efficient than querying and indexing traditional scalar data types. This might not be a concern for small datasets, but it can become a bottleneck for larger datasets or more complex queries.

Portability considerations: Not all databases support JSON or array data types in the same way. If you're using these data types extensively, it could make it more difficult to switch to a different database system in the future.

In conclusion, using JSON and avoiding arrays in your database can be a good practice, depending on your specific needs. However, it's important to understand the implications and trade-offs of these decisions, and to design your database schema and your queries with care.

1 / 1

For data analysis, which is more suitable?

ChatGPT

ChatGPT

1 / 1

When it comes to data analysis, both PostgreSQL and MySQL can serve as effective database management systems, and they both integrate well with popular data analysis tools and languages like Python, R, and Tableau. The choice between the two often comes down to specific needs and requirements of the project.

Here are a few points to consider:

Advanced Features: PostgreSQL's advanced features, such as support for complex queries and rich set of functions, can be beneficial for complex data analysis tasks. For example, PostgreSQL supports window functions, which are powerful tools for analyzing data in a relational database.

Performance: MySQL can be faster for read-heavy workloads, which is often the case in data analysis where you are pulling large amounts of data but not necessarily writing back to the database. MySQL's read performance can be a significant advantage for data analysis tasks.

JSON Support: If your data analysis involves a lot of semi-structured data stored as JSON, PostgreSQL's advanced JSON functions might be beneficial. PostgreSQL allows for complex querying of JSON data, which could be handy for certain data analysis tasks.

Scalability: If your data analysis tasks involve large datasets, MySQL might have an edge because it's generally considered to be more scalable than PostgreSQL, especially in read-heavy workloads. But, PostgreSQL has also made significant strides in scalability and performance in recent years.

In the end, both PostgreSQL and MySQL have their strengths, and the best choice depends on your specific needs. It may also be worth considering other types of databases designed specifically for analytics workloads, such as columnar databases (e.g., Amazon Redshift, Google BigQuery) or distributed SQL databases (e.g., CockroachDB), depending on the scale and nature of your data analysis tasks.

I actually have no much experience in neither of the database, since I'm a developer. But I want to choose and technically invest in one of the database for the coming years. Developer experience and happiness or painlessness, as well as less complicated is more important to me. Which do you suggest?

ChatGPT

ChatGPT

1 / 1

When it comes to developer experience and simplicity, PostgreSQL tends to be the preferred choice, especially in the Ruby on Rails community. The Rails framework and ActiveRecord ORM have excellent support for PostgreSQL, and developers often find that PostgreSQL's advanced features make it easier to work with. Here's why:

Advanced Features: PostgreSQL supports a number of advanced features, like window functions, recursive queries, and geospatial data types, which can make certain types of queries simpler and more efficient.

Array and JSON Support: PostgreSQL's support for array and JSON data types can also simplify the development process, especially when dealing with semi-structured data.

Strong Rails Integration: PostgreSQL has traditionally had better support for advanced features in ActiveRecord, which is the default ORM used in Rails. This means that you can often use more advanced SQL features while still leveraging the simplicity and convenience of ActiveRecord.

Community Support: PostgreSQL seems to be more popular among Rails developers. This can lead to better community support, more up-to-date tutorials and resources, and potentially faster resolution of any issues you encounter.

Conformance to Standards: PostgreSQL has a high conformance to SQL standards, which can make it easier for developers to use because they can rely on their knowledge of SQL without having to learn many quirks or vendor-specific syntax.

On the other hand, MySQL is also a solid choice and is used by many large, high-profile internet companies. It has a reputation for being very reliable and efficient, especially for read-heavy workloads.

Ultimately, the best choice between MySQL and PostgreSQL will depend on your specific needs and circumstances. However, given your priorities of developer experience, simplicity, and integration with Rails, I would suggest looking more closely at PostgreSQL.

## SQLite

SQLite is an in-process library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine.

Unlike most other SQL databases, SQLite does not have a separate server process. SQLite reads and writes directly to ordinary disk files.

A database in SQLite is a single disk file. The database file format is cross-platform and make SQLite a popular choice as an Application File Format. SQLite database files are a recommended storage format by the US Library of Congress.

SQLite is a compact library. With all features enabled, the library size can be less than 600KiB.

SQLite reads and writes small blobs (for example, thumbnail images) 35% faster¹ than the same blobs can be read from or written to individual files on disk. Furthermore, a single SQLite database holding 10-kilobyte blobs uses about 20% less disk space than storing the blobs in individual files.

SQLite is very carefully tested prior to every release and has a reputation for being very reliable.

SQLite responds gracefully to memory allocation failures and disk I/O errors. Transactions are ACID even if interrupted by system crashes or power failures.

SQLite does not need to be "installed" before it is used. There is no "setup" procedure. Nothing needs to be done to tell the system that SQLite is running. No actions are required to recover after a system crash or power failure.

## Postgre

PostgreSQL is often considered to be more feature-rich than MySQL. It supports a larger set of SQL standards, including complex queries, foreign keys, views, transactional integrity, and multi-version concurrency control. It also supports a wide variety of data types, such as geometric shapes and arrays, which MySQL does not.

Given that you are developing multiple business applications including an ERP, CRM, MES, PLM, and franchise store sales management, it sounds like your system might be complex and could benefit from PostgreSQL's advanced features and robustness. However, if your applications are read-intensive and you want to ensure speed, MySQL might be the better option.

Rails has good support for both MySQL and PostgreSQL. ActiveRecord supports both out of the box. Active Record is designed to be database-agnostic and provides a high level of abstraction for database operations. MySQL's support in Active Record is mature and robust, covering all the basic and most commonly-used features. However, PostgreSQL has traditionally had better support for advanced features in ActiveRecord.

Active Record supports PostgreSQL's array and hstore data types, which allow you to store arrays and hashes directly in the database. This can simplify your data model and make certain types of queries more efficient.

Full-Text Search: PostgreSQL's full-text search is supported by Active Record, providing powerful and efficient text search capabilities without needing to use a separate search server.

PostGIS Extension: If you're working with geospatial data, Active Record can take advantage of the PostGIS extension in PostgreSQL.

#### Schema.rb

??? We should also delete db/schema.rb, since that will no longer be used. Rails will store the SQL schema in db/structure.sql.\


#### Using Arrays in PostgreSQL?

**WHL: Let's consent it together with Rails in mind. Since Ruby has array and Rails use array a lot. Is it more compatible to support array in database?**

ChatGPT: From a programming perspective, the ability to use arrays natively in PostgreSQL can be attractive to Rails developers due to the ease and familiarity of working with arrays in Ruby. Here are some factors to consider:

Convenience: Ruby is very array-oriented, and Rails developers often use arrays to handle collections of objects. Being able to store and retrieve arrays directly from the database can be convenient and intuitive.

Easy Mapping: Arrays in PostgreSQL map directly to arrays in Ruby, which can make certain types of operations easier and more efficient. For example, you can store a multi-select form input (which comes in as an array) directly to a PostgreSQL array field.

Array Operations: PostgreSQL supports many powerful operations on array fields, such as intersection, union, and difference, which can make certain types of queries easier and more efficient.

Simplicity: Storing arrays directly in a column can simplify your data model, especially for one-to-many relationships that don't require a separate table.

Performance: Retrieving an array from a single field can be faster than joining and fetching from another table.

Advanced Querying: PostgreSQL allows for sophisticated querying on array fields, such as checking if an array contains a certain value or querying on array length.

**However, there are also potential downsides:**

Database Agnosticism: One of the key principles of Rails is to be database-agnostic, and using arrays in PostgreSQL could tie your application more closely to a specific database system. % 我不認為這是一個實際問題，既然我們選擇了一種成熟的數據庫，我們在未來的多少年裡就可以一直使用它，行程自己的 best practice。 20230724 %

Normalization Principles: Using arrays can break normalisation principles, potentially leading to data redundancy and anomalies.

Complexity with Associations: If you need to associate other data with the elements in an array (e.g., if you need to track when each item was added or who added it), you'll likely need a separate table anyway.

Search and Indexing: Searching for a specific element in an array or indexing an array column can be more complex and less performant than using a normalised schema, especially for large arrays.

Limited Indexing and Performance: While you can index array fields in PostgreSQL, the performance benefits might not be as good as with normalised data, especially for large arrays. Querying and updating large array fields can also be slow.

Complex Queries: For complex queries or operations involving the elements of the array, a normalised schema with join tables might be more suitable and perform better.

As a rule of thumb, arrays can be a good fit for simple, one-to-many relationships where the "many" side doesn't need to be queried or operated on individually, and the size of the array is relatively small.

% 使用場景：一個員工的緊急聯繫信息，可以放在一個 Arrary裡，裏面包含：聯繫人姓名、聯繫人手機號碼、聯繫人地址、聯繫人關係等。因為緊急聯繫信息不是企業環境裡的主要數據，所以，完全可以做一個開放式的 Arrary存儲。%
