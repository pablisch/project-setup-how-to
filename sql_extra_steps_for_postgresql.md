# SQL extra steps for PostgreSQL project setup

Follow the usual [Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md) or [Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md), then add the following steps:

```ruby
# Additonal steps for databases
bundle add pg # postgres
touch lib/database_connection.rb
touch spec/seeds.sql
touch app.rb
```
```ruby
touch lib/database_connection.rb spec/seeds.sql app.rb
```

### Copy the following to the database_connection.rb file

```ruby
# file: lib/database_connection.rb

require 'pg'

# This class is a thin "wrapper" around the
# PG library. We'll use it in our project to interact
# with the database using SQL.

class DatabaseConnection
  # This method connects to PostgreSQL using the 
  # PG gem. We connect to 127.0.0.1, and select
  # the database name given in argument.
  def self.connect(database_name) # <🎃🎃🎃> DATABASE NAME
    @connection = PG.connect({ host: '127.0.0.1', dbname: database_name }) # <🎃🎃🎃> DATABASE NAME
  end

  # This method executes an SQL query 
  # on the database, providing some optional parameters
  # (you will learn a bit later about when to provide these parameters).
  def self.exec_params(query, params)
    if @connection.nil?
      raise 'DatabaseConnection.exec_params: Cannot run a SQL query as the connection to'\
      'the database was never opened. Did you make sure to call first the method '\
      '`DatabaseConnection.connect` in your app.rb file (or in your tests spec_helper.rb)?'
    end
    @connection.exec_params(query, params)
  end
end
```

### ADD the following to the top of the spec/spec_helper.rb file

```ruby
# file: spec/spec_helper.rb

require 'database_connection'

# Make sure this connects to your test database
# (its name should end with '_test')
DatabaseConnection.connect('your_database_name_test') # <🎃🎃🎃> DATABASE NAME
```

### Add SQL seeds

Add seeds where needed depending on your project.

### The Main File

app.js is the program main file and the "entrypoint" of the program — it is the file you will execute with the ruby command.

Its job is to connect to the database using DatabaseConnection.connect, and then execute whatever logic the program needs to do.

In the example below, we simply execute a SELECT SQL query on the database and print the returned result set.

### file: app.rb
```ruby
require_relative 'lib/database_connection'
```
### We need to give the database name to the method `connect`.
```ruby
DatabaseConnection.connect('music_library')
```
### Perform a SQL query on the database and get the result set.
```sql
sql = 'SELECT id, title FROM albums;'
result = DatabaseConnection.exec_params(sql, [])
```
### Print out each record from the result set .
```ruby
result.each do |record|
  p record
end
```
Running the main file should output a list of records to the terminal.




[Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md)

[Ruby with RSpec project setup - this page](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md)

[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
