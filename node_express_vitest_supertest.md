# Setting up a Node Express project with Jest & Supertest

```bash
nvm use node

git init
npm init -y

npm i express nodemon
npm install --save-dev jest supertest

mkdir __tests__ routes controllers
touch .gitignore app.js index.js __tests__/app.test.js routes/userRoutes.js controllers/userController.js
code .
```
**Add `node_modules` to `.gitignore` or use the `ignorejs` snippet.**

Add type and scripts to `package.json`.
```bash
"type": "module",
"scripts": {
  "test": "vitest --run --globals --reporter verbose",
  "watch": "vitest --globals --reporter verbose",
  "coverage": "vitest run --coverage",
  "start": "nodemon index.js"
},
```
**NOTE:** `"type": "module",` only needed if using ESM module syntax for imports and exports.
