# Extra steps for PostgreSQL project setup

Follow on from [Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md) and then [extra_steps_for_postgresql](https://github.com/pablisch/project-setup/blob/main/extra_steps_for_postgresql.md)...

Complete [the design template](https://github.com/pablisch/databases/blob/main/resources/repository_class_recipe_template.md):

1. Design the Table, e.g.

Table: artists
Columns:
id | name | genre

2. Create test SQL seeds to go in e.g. spec/seeds_<table-name>.sql with content like the example below: 

```sql
TRUNCATE TABLE albums RESTART IDENTITY;

INSERT INTO albums (title, release_year, artist_id) VALUES ('Future Days', '1973', 1);
INSERT INTO albums (title, release_year, artist_id) VALUES ('Tell Her', '1969', 2);
```

To insert into test db:
```bash
psql -h 127.0.0.1 your_database_name < seeds_{table_name}.sql
```

1. Define class names

```ruby
# model class FILE lib/artist.rb
class Artist
end

# repository class FILE lib/artist_repository.rb
class ArtistRepository
end
```
4. Implement the model class




5. Define the Repository class interface






6. Write Test examples






7. Reload SQL seeds before each run








8. Test drive



