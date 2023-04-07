# Ruby for Web App with Sinatra & RSpec project setup

This is for a Ruby Web App with RSpec project setup

```ruby
# create project directory
mkdir project-name
cd project-name

# initialise bundler
bundle init

# add rspec
bundle add rspec
rspec --init
mkdir lib recipes

# Add the sinatra library, the webrick gem, and rack-test
bundle add sinatra sinatra-contrib webrick rack-test

# Create the app_spec.rb integration tests dir
mkdir spec/integration

# Create the main application file, the app_spec.rb integration tests file and the config.ru file
touch app.rb spec/integration/app_spec.rb config.ru

# initialise git
git init
git add .
git commmit -m  "Project setup"

# make a new parallel repo on GitHub with no README and copy the following from there
git remote add origin <YOUR_REMOTE_ADDRESS>.git
git branch -M main
git push -u origin main

# set up push path
git push -u origin main

# open repo in VSCode
code .
-f d  # abbreviation of --format documentation
```

## The app.rb file

When building Sinatra web applications, this file will contain the application class. Create an empty one for now, you will define routes later inside it (and learn about what a route is).

```ruby
require 'sinatra/base'
require 'sinatra/reloader'

class Application < Sinatra::Base
  # This allows the app code to refresh
  # without having to restart the server.
  configure :development do
    register Sinatra::Reloader
  end
end
```

## The `config.ru` file

We will later use the command `rackup` to "run" the web server. That command comes built-in with the `webrick` gem we installed earlier. By running it, our Sinatra application will run continuously in a terminal, waiting to receive HTTP requests, just like a "real" web server would.

To know how to run the Sinatra application class, it needs a few lines of configuration of the file `config.ru` — let's add this now.

```ruby
# file: config.ru
require './app'
run Application
```

You should now be able to run the app by using the `rackup` command, and get a similar output:

```
$ rackup

[2022-05-11 16:14:54] INFO  WEBrick 1.7.0
[2022-05-11 16:14:54] INFO  ruby 3.0.1 (2021-04-05) [x86_64-darwin20]
[2022-05-11 16:14:54] INFO  WEBrick::HTTPServer#start: pid=7377 port=9292
```

Now use your browser to visit `http://localhost:9292`. You should see the following page.

![sinatra home](./images/sinatra-home.png)

[Ruby basic project setup](https://github.com/pablisch/project-setup/blob/main/ruby_basic.md)

[Ruby with RSpec project setup](https://github.com/pablisch/project-setup/blob/main/ruby_with_rspec.md)

[SQL extra steps for PostgreSQL project setup](https://github.com/pablisch/project-setup/blob/main/sql_extra_steps_for_postgresql.md)

[SQL project step-by-step](https://github.com/pablisch/project-setup/blob/main/sql_project_step_by_step.md)

[Recipe design templates (GitHub)](https://github.com/pablisch/templates)

[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
