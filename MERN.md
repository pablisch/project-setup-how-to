# Setting up a MERN stack app
```bash
# Create project directory and backend folder
mkdir mern-app
cd mern-app
```
```bash
# initialise git and add .gitignore
git init
touch .gitignore
```
```bash
# Create project directory and backend folder
mkdir backend
cd backend
```
```bash
# intialise a new Node.js project
npm init -y
# install express, mongodb driver, bcrypt, jsonwebtoken and nodemon
npm install express mongoose bcrypt jsonwebtoken
npm install nodemon --save-dev
# install jest
npm install --save-dev jest
# setup backend folders and files
mkdir controllers models routes middleware spec
touch app.js server.js .gitignore
```
```bash
# go back to the root directory
cd ..
```
```bash
# initialise the frontend as a new react app
npx create-react-app frontend
```
```bash
# cd into frontend and install react-router-dom, axios, axios mcok adapter and cypress
cd frontend
npm install react-router-dom axios axios-mock-adapter
npm install --save-dev cypress
```
```bash
# open cypress studio to configure testing
npx cypress open
```

## All of the above in one step...

Create you project directory and cd into it
```bash
git init
touch .gitignore
mkdir backend
cd backend
npm init -y
npm install express mongoose bcrypt jsonwebtoken
npm install nodemon --save-dev
npm install --save-dev jest
mkdir controllers models routes middleware spec
touch app.js server.js .gitignore
cd ..
npx create-react-app frontend
cd frontend
npm install react-router-dom axios axios-mock-adapter
npm install --save-dev cypress
npx cypress open
cd ..
code .
```

## To start your app servers

Open two terminals, one in the backend and one in the frontend
```bash
# in the backend
node server start
```
```bash
# in the frontend
npm start
```






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
