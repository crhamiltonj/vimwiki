# Node Express

## Basic package.json

```json
{
  "name": "nodejs_complete",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon app.js",
    "start-server": "node app.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "nodemon": "^1.19.4"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}

```

## Node Express Minimal Server

The express server is installed with `npm install --save express`.

```javascript
// Import the server
const express = require('express')

// Create the server object
const app = express();

// express.use() is middleware that has access to requests and response and can forward
// it to another middleware or return a response.
app.use((req, res, next) => {
  console.log('In the middleware')
  next() // Allows the request to continue to the next middleware in line
});

// Since this is defined after the previous use it will always be called second.  This applies
// to all middleware that may be defined after this.  They are always processed in order.
app.use((req, res, next) => {
  console.log('In another middleware')
  res.send('<h1>Hello from Express</h1>')
});

app.listen(3000)

```

[Bare HTTP Server Example](node_express__bare_http.md)
