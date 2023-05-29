# Setting up a JavaScript project with Jest
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

# Install esbuild
npm install -g esbuild
npm install
npm run build
```
```bash
# create base project files
touch index.html index.js styles.css .gitignore
mkdir images
```
```bash
# create base project files and MVC + test files
touch index.html index.js styles.css .gitignore view.js view.test.js model.js model.test.js client.js client.test.js
mkdir images
```

most of the time, this bit of package.json is not automatically added
it is needed to run `npm run build`.
```bash
"build": "esbuild index.js --bundle --outfile=bundle.js --watch"
```