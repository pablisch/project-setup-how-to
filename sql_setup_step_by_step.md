# Extra steps for PostgreSQL project setup

Follow on from [Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md) and then [extra_steps_for_postgresql](https://github.com/pablisch/project-setup/blob/main/extra_steps_for_postgresql.md)...

Complete [the design template](https://github.com/pablisch/databases/blob/main/resources/repository_class_recipe_template.md):

## 1. Design the Table, e.g.

Create the db, e.g. 
```bash
psql -h 127.0.0.1
CREATE DATABASE music_library
```

Table: artists

Columns:

id | name | genre

## 2. Create test SQL seeds 

Create a test library, e.g. 
```bash
psql -h 127.0.0.1
CREATE DATABASE music_library_test.
```
Insert the base table into it, e.g.
```bash
psql -h 127.0.0.1 your_database_name < {table_name}.sql
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

