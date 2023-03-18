# Most basic Ruby project setup

This is for a Ruby repo without RSpec

```
# create project directory
mkdir project-name
cd project-name

# select Ruby version
rvm get stable
rvm list # will show you current, default and installed versions
    rvm use 3.0.0 # only if you need to change from the current version
    rvm default # to switch to the default version
    rvm rvm use ruby --latest --install --default # not my personal choice!

# Install bundler
gem install bundler
bundle init

# initialise git
git init
git add .
git commmit -m  "Project setup"

# make a new parallel repo on GitHub with no README and copy the following from there
git remote add origin <YOUR_REMOTE_ADDRESS>.git
git branch -M main
git push -u origin main

```

<a href="http://example.com" target="_blank"></a>

[markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
