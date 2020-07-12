---
title: "Setting up an API server using Clojure"
published: false
---

# Setting up an API server using Clojure
---

Disclaimer: I am new to Clojure. Be gentle. Be kind.

Now that everyone has read the disclaimer, let's dive in. 

By trade I am a web developer. I primarily use Java, Spring Boot, Angular, and TypeScript. I was introduced to Clojure by a fellow teammate and I was instantly hooked. 

Being a web developer I thought the best way to learn Clojure was to create an API server. Needless to say, it took **a lot** of scouring the internet, using the fantastic [Clojure Slack community](http://clojurians.net/), and lots of reading of dispersed blog posts to be able to glue all the pieces together. 

I finally understood how to get an API server up and running but I also understood a lot of people's frustration when trying to get into Clojure. Specifically web development with Clojure. There is no "one stop show me how". 

So here we are. I am going to, hopefully, give all new Clojure peeps a resource in order to get an API server up and running with a database. We will be using Clojure (duh!), Leiningen, Compojure, Ring, Component, and HoneySQL. Don't worry if you do not know what all these things do. You will be the end of this blog post. 

Grab a glass of water (or your favorite beverage), a comfy chair, and let's get to work. 

## Table of Contents
1. Installing Clojure & Leiningen
2. Creating a Clojure application
3. Installing Dependencies
4. Spin up a server
5. Adding routes
6. Connect database
7. Migrate all the things!
8. Interacting with the database using HoneySQL
9. Fin

## Installing Clojure & Leiningen 
Before we do anything we need to install Clojure. The most reliable instructions can be found on [the official Clojure website](https://clojure.org/guides/getting_started). Follow the instructions for whichever platform you are developing on. 

After this, you will need to install Leiningen. Leiningen is an automation tool used for creating and managing Clojure projects. Instruction can be found on the [official Leiningen website](https://leiningen.org/). 

## Creating a Clojure application
We will need to create our Clojure application using Leiningen. First change into the directory where you want your project to live and then run the following command
```
lein new app your_app_name
```
Leiningen will begin to perform work and create a base Clojure project for you to work in. Your project structure should look similar to this
```
your_app
└─doc
└─resources    
└─src
│   └─your_app
|       └─core.clj 
└─test
└─.gitignore
└─.hgignore
└─CHANGELOG.md
└─LICENSE
└─project.clj
└─README.md
```

Now that we have our application, let's install three dependencies we will need in order to get our API server up and running.

## Installing Dependencies
There are several dependencies we will need in order to set up our API server for success. Below is a quick blurb for each and then instructions on where these dependencies go in our project.  

### [Ring - HTTP Server](https://github.com/ring-clojure/ring)
The standard in the Clojure community is to use Ring for your HTTP server. It is a library with all the standard features we will need in order to get an HTTP server up and running. 

### [Compojure - Routing Library](https://github.com/weavejester/compojure)
Since the Clojure community adheres pretty closely to the singular responsibility rule, the Ring library does not have any routing properties with it. Compojure will allow us to build out robust routes for our API sever with all the standard RESTful methods like `POST`, `GET`, `PUT`, `PATCH`, and `DELETE`. 

### [Component - Lifecycle Management](https://github.com/stuartsierra/component)
This library allows us to manage some lifecycles that you will want in your application. The one we will want to use is when the application boots up, we want to create an HTTP server and when the HTTP server is created, we want to create a connection to our database. 

### [PostgreSQL](https://www.postgresql.org/), [JDBC Connection](https://github.com/seancorfield/next-jdbc), & [Honey SQL - SQL](https://github.com/seancorfield/honeysql)
For this project you will be using PostgreSQL. Follow the link above to get it install on your machine. 

Honey SQL allows us to generate SQL queries without having to handroll all our queries into strings. It is a fantastic DSL. It will also make our code more readable.


In order to set our dependencies we will need to open the `project.clj` file and we need see a key called `:dependencies`. You will add the above dependencies in this list. In order to check what is the most up to date for each dependency, use the [Clojars website](https://clojars.org/). After adding the dependencies your list should look like
```
(defproject your_app "0.1.0-SNAPSHOT
   ...
   :dependencies [[org.clojure/clojure "1.10.1]
                  [ring "1.8.1"]
                  [compojure "1.6.1"]
                  [honeysql "1.0.444"]
                  [seancorfield/next.jdbc "1.0.13"]
                  [org.postgresql/postgresql "42.2.10.jre7"]
                  [com.stuartsierra/component "0.4.0"]])
```
Run `lein deps` to install these dependencies. 

