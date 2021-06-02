# What is Dapr?
<img src="https://raw.githubusercontent.com/dapr/dapr/master/img/dapr_logo.svg" width="200">

**Distributed Application Runtime**

Dapr is a portable, serverless, event-driven runtime that makes it easy for developers to build resilient, 
stateless and stateful microservices that run on the cloud and edge and embraces the diversity of languages 
and developer frameworks.

It is a free and open source runtime system designed to support cloud native and serverless computing.

## Why Dapr?

Why Dapr?
Writing high performance, scalable and reliable distributed application is hard. Dapr brings proven patterns 
and practices to you. It unifies event-driven and actors semantics into a simple, consistent programming model. 
It supports all programming languages without framework lock-in.

# Step 1: Dapr installation & configuration

Pre-requisuite
- Docker latest version
- Basics of Javascript
- Node.js API project based on the following guide - [Using Fastify as API server](Using%20Fastify%20as%20API%20server.md)

## Step 1.1: Dapr installation
[Click here to install Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/)

## Step 1.2: Verify Dapr installation
You can verify the CLI is installed by restarting your terminal/command prompt and running the following command

```
$ dapr
	 __                
    ____/ /___ _____  _____
   / __  / __ '/ __ \/ ___/
  / /_/ / /_/ / /_/ / /    
  \__,_/\__,_/ .___/_/     
	      /_/            
	      
======================================================
A serverless runtime for hyperscale, distributed systems
...
```

## Step 1.3: Initialize Dapr
Dapr runs as a sidecar alongside your application, and in self-hosted mode this means it is a process on your local machine. 
Therefore, initializing Dapr includes fetching the Dapr sidecar binaries and installing them locally.

In addition, the default initialization process also creates a development environment that helps streamline application 
development with Dapr. This includes the following steps:
1. Running a **Redis** container instance to be used as a local state store and message broker
1. Running a **Zipkin** container instance for observability
1. Creating a default components folder with component definitions for the above
1. Running a Dapr placement service container instance for local actor support



- Run the following command to initialize Dapr
```
$ dapr init
⌛  Making the jump to hyperspace...
↖  Downloading binaries and setting up components... Installing Dapr to /usr/local/bin
✅  Downloading binaries and setting up components...
✅  Success! Dapr is up and running. To get started, go here: https://aka.ms/dapr-getting-started
```

- Check Dapr version
```
$ dapr --version
CLI version: 0.5.0 
Runtime version: 1.2.0
```

- Verify containers are running
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                      NAMES
3748290c25e3        daprio/dapr         "./placement"            About a minute ago   Up About a minute   0.0.0.0:50005->50005/tcp   dapr_placement
48764937a7f6        redis               "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:6379->6379/tcp     dapr_redis
```
# Step 2: Running node.js API using Dapr

## Step 2.1: Run the API
At the project folder, run the following command:
```
dapr run --app-id splask-api --app-port 8080 node index.js
...
✅  You're up and running! Both Dapr and your app logs will appear here.
...
```

## Step 2.2: Test the API
Run the test based on **test.http** code snippets, for example
```
POST http://localhost:8080
content-type: application/json

{
"nama" : "hanafiah"
}
```
Refer to this guide to test the API - [Using Fastify as API server](Using%20Fastify%20as%20API%20server.md)
