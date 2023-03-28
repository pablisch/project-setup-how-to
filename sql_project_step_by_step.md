# Extra steps for PostgreSQL project setup

Follow on from [Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md) and then [extra_steps_for_postgresql](https://github.com/pablisch/project-setup/blob/main/extra_steps_for_postgresql.md)...

Complete [the design template](https://github.com/pablisch/databases/blob/main/resources/repository_class_recipe_template.md):

## CHECK...

> that you have entered THIS PROJECT"S database name in the spec_helper.rb file!
> that you use the DATABASE-NAME and the TABLE-NAME in the correct places and don't mix them up!
> Create a database AND database_test AND load them both!

## 1. Design the Table, e.g.

Table: artists

Columns:

id | name | genre

Create the db, e.g. 
```bash
psql -h 127.0.0.1

pablo=# CREATE DATABASE music_library
pablo=# CREATE DATABASE music_library_test

psql -h 127.0.0.1 your_database_name < {table_name}.sql
psql -h 127.0.0.1 your_database_name_test < {table_name}.sql
```

## 2. Create test SQL seeds 

Create a test library, e.g. 
```bash
psql -h 127.0.0.1
CREATE DATABASE music_library_test; # if you have not done so already!
```
Insert the base table into it, e.g.
```bash
psql -h 127.0.0.1 your_database_name < {table_name}.sql # if you have not done so already!
```
Create seeds to go in a seed file in the spec folder e.g. spec/seeds_<table-name>.sql with content like the example below: 
```sql
TRUNCATE TABLE artists RESTART IDENTITY;

INSERT INTO artists (name, genre) VALUES ('CAN', 'Krautrock');
INSERT INTO artists (name, genre) VALUES ('Fred Williams', 'Afro Funk');
```
## 3. Define class names
```ruby
# model class FILE lib/artist.rb
class Artist
end

# repository class FILE lib/artist_repository.rb
class ArtistRepository
end
```
## 4. Implement the model class

This will be very basic and will not need testing.

Create the model class file, e.g. lib/artists.rb
```ruby
# model class FILE lib/artist.rb
class Artist
  attr_accessor :id, :name, :genre
end
```
## 5. Define the Repository class interface
```ruby
# repository class FILE lib/artist_repository.rb
class ArtistRepository
  def all
    # executes the SQL query:
    # SELECT id, name, genre FROM artists;
    # returns an array of artist objects as hashes
  end
end
```
## 6. Write Test examples
```ruby
repo = ArtistRepository.new

artists = repo.all # an array of Artist objects
artists.length # => 2
artists.first.id # => '1'
artists.first.name # => 'CAN'
```
## 7. Reload SQL seeds before each run

Create the spec file for the repository class, e.g. artist_repository_spec.rb set up RSpec and add code to reload seeds before each test, e.g.
```ruby
require 'artist_repository'

RSpec.describe ArtistRepository do

  def reset_artists_table # reload method
    seed_sql = File.read('spec/seeds_artists.sql')
    connection = PG.connect({ host: '127.0.0.1', dbname: 'music_library_test' })
    connection.exec(seed_sql)
  end

  before(:each) do 
    reset_artists_table # reloads for each test
  end

  it "" do # first test
  end
end
```

## 8. Test drive

Implement tests in the usual TDD way, e.g.
```ruby
  it "returns values for Artist objects" do
    repo = ArtistRepository.new
    artists = repo.all # an array of Artist objects
    expect(artists.length).to eq(2) # => 2
    expect(artists.first.id).to eq('1') # => '1'
    expect(artists.first.name).to eq('CAN') # => 'CAN'
  end
```
This will need the repository class to be coded. The code for this is still fairly obscure at the moment but for this example would be:
```ruby
require_relative './artist'

class ArtistRepository
  def all
    sql = 'SELECT id, name, genre FROM artists;'
    result = DatabaseConnection.exec_params(sql, []) # sends the sql request

    artists = [] # creates new array

    result.each do |record| # iterates over the query results
      artist = Artist.new # instantiates a new Artist object
      artist.id = record['id'] # adds values from the hash result
      artist.name = record['name']
      artist.genre = record['genre']

      artists << artist # pushes each Artist into the artists array
    end

    return artists # returns the array of Artist objects
  end
end
```

## 9. Write app.rb

Once testing is done, we are ready to write the app.rb file.

In this example, we only have one method to call on:
```ruby
require_relative 'lib/database_connection'
require_relative 'lib/artist_repository'

# We need to give the database name to the method `connect`.
DatabaseConnection.connect('music_library')

artist_repository = ArtistRepository.new

artist_repository.all.each { |artist| p artist }
```

[Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md)

[Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md)

[SQL extra steps for PostgreSQL project setup](https://github.com/pablisch/project-setup/blob/main/sql_extra_steps_for_postgresql.md)

[SQL project step-by-step](https://github.com/pablisch/project-setup/blob/main/sql_project_step_by_step.md)

[Recipe design templates (GitHub)](https://github.com/pablisch/templates)

[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)