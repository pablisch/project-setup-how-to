# Setting up a MERN stack app
```bash
# Create project directory and backend folder
mkdir mern-app
cd mern-app
```
```bash
# Create project directory and backend folder
mkdir backend
cd backend
```
```bash


# Setup our environment to use node latest version
nvm use node

# Initialise the NPM project (this will create a file package.json)
npm init -y

# Add the jest package to our project
# (this will update package.json and package-lock.json)
npm add jest

# Also install jest "globally"
# (this is so we can run the `jest` command)
npm install -g jest

# Run our tests
jest

# make gitignore file
touch .gitignore
```
