# Extra steps for PostgreSQL project setup

Follow the usual [Ruby with RSpec project setup - this page](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md) or [Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md), then add the following steps:

```ruby
# Additonal steps for databases
bundle add pg # postgres
touch lib/database_connection.rb
touch spec/seeds.sql
touch app.rb
```

## Copy the following to the database_connection.rb file

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
  def self.connect(database_name)
    @connection = PG.connect({ host: '127.0.0.1', dbname: database_name })
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

## ADD the following to the top of the spec/spec_helper.rb file

```ruby
# file: spec/spec_helper.rb

require 'database_connection'

# Make sure this connects to your test database
# (its name should end with '_test')
DatabaseConnection.connect('your_database_name_test')
```







[Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md)

[Ruby with RSpec project setup - this page](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md)

[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
