# Contents

## What is Fastify?

[<img src="https://www.fastify.io/images/fastify-logo-menu.d13f8da7a965c800.png" width="200">](https://www.fastify.io)

Fastify is a web framework highly focused on providing the best developer experience with the least overhead and 
a powerful plugin architecture. It is inspired by Hapi and Express and as far as we know, it is one of the fastest 
web frameworks in town.

Fastify is also one of the fastest node.js framework. Check out the performance benchmarks <<
[Fastify Performance Benchmark](https://www.fastify.io/benchmarks/) >>

## Pre-requisuite
*  Node latest version
*  Visual Studio Code
*  Basics of Javascript


# Step 1: Setup Fastify environment
## Step 1.1: Initialize node.js project environment

- create project directory
```
$ mkdir SPLaSK
$ cd SPLaSK
```

- initialize node.js
```
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (splask) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/hanafiah/Documents/Development/SPLaSK/package.json:

{
  "name": "splask",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}


Is this OK? (yes) yes
```

## Step 1.2: Install Fastify
```
$ npm i fastify --save
```
Please verify from **package.json** file that Fastify is successfully installed
```
...
"dependencies": {
    "fastify": "^3.17.0"
  }
...
```

# Step 2: Configure Visual Studio Code

## Step 2.1: Open VS Code
At the project folder run the following command to open VS Code
```
$ code .
```

## Step 2.2: Install VS Code extensions
Install the following VS Code extensions:
*  Fastify Snippets
*  REST Client

# Step 3: Run Fastify Server

## Step 3.1: Create index.js file
From VS Code, click new file icon to create a file called **index.js**

<img src="/uploads/2132216f489a7412793f9393c455e175/image.png" width="300">

copy the following code snippets:
```
const fastify = require('fastify')({ logger: true })
fastify.get('/', async (request, reply) => {
  return { hello: 'world' }
})
fastify.post('/', async (request, reply) => {
  return request.body
})
fastify.listen(8080)
```
- tips: use Fastify Snippets - **ffhello**

Next, **Save index.js**
- tips: use CTRL-S to save file

## Step 3.2: Run the server
Open a terminal in VS Code, from menu -> Terminal -> New Terminal

<img src="/uploads/86e7759e81ffa5e8ed16d310b8807e00/image.png" width="300">

At the terminal, run the following command
```
$ node index.js
{"level":30,"time":1622352774811,"pid":43478,"hostname":"hanafiahs-MacBook-Pro.local","msg":"Server listening at http://127.0.0.1:8080"}
```

Open web browser, and browser to **localhost:8080** and you should get the following result:

<img src="/uploads/7599a5454d01fb7e047903bada0d0ce2/image.png" width="300">

# Step 4: Create API

## Step 4.1: Create POST API
Replace index.js with the following code snippets
```
const fastify = require('fastify')({ logger: true })
fastify.get('/', async (request, reply) => {
  return { hello: 'hanafiah' }
})
fastify.post('/', async (request, reply) => {
  return request.body
})
fastify.post('/profile', async (request, reply) => {
    let profiledata = request.body
    return profiledata
})
fastify.listen(8080)
```
Next, **Save index.js**

## Step 4.2: Test API
Create a new file called **test.http** and paste the following code snippets to test.http file
```
POST http://localhost:8080
content-type: application/json

{
"nama" : "hanafiah"
}
```
Next, save **test.http**

Click **Send Request** to test the API

<img src="/uploads/fedd12acd2fe1973e474309903a1d93a/image.png" width="300">

You should get the following result

<img src="/uploads/8faa3c6632198cba91b72091a4de7395/image.png" width="300">

Next, add the following code snippets **test.http**
```
###

POST http://localhost:8080/profile
content-type: application/json

{
"nama" : "hanafiah"
}
```

Next, save **test.http**

Click **Send Request** to test the API from *POST http://localhost:8080/profile*


## Step 4.3: API Routing
Replace index.js with the following code snippets
```
const fastify = require('fastify')({ logger: true })

fastify.register(require('./routing'))

fastify.listen(8080)
```
Next, **Save index.js**

Create new file called **routing.js**

Add the following snippets to routing.js

```
async function routing (fastify, options) {
    fastify.get('/', async (request, reply) => {
      return { hello: 'hanafiah' }
    })

    fastify.post('/', async (request, reply) => {
      return request.body
    })
    fastify.post('/profile', async (request, reply) => {
        let profiledata = request.body.nama
        return profiledata
    })
  }
  
module.exports = routing
```

Next, open **test.http** file and test the API again and you will get the same results. Please refer to [Step 4.2](#step-42-test-api)
