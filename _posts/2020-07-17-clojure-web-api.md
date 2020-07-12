---
title: "Setting up an API server using Clojure"
published: false
---

# Setting up an API server using Clojure
---

Disclaimer: I am new to Clojure. Be gentle. Be kind.

Now that everyone has read the disclaimer, let's dive in. 

By trade I am a web developer. I primarily use Java, Spring Boot, Angular, and TypeScript. I was introduced to Clojure by a fellow teammate and I was instantly hooked. 

Being a web developer I thought the best way to learn Clojure was to create an API server. Needless to say, it took **a lot** of scouring the internet, using the fantastic Clojure Slack community, and lots of reading of dispersed blog posts to be able to glue all the pieces together. 

I finally understood how to get an API server up and running but I also understood a lot of people's frustration when trying to get into Clojure. Specifically web development with Clojure. There is no "one stop show me how". 

So here we are. I am going to, hopefully, give all new Clojure peeps a resource in order to get an API server up and running with a database. We will be using Clojure (duh!), Leiningen, Compojure, Ring, Component, and HoneySQL. Don't worry if you do not know what all these things do. You will be the end of this blog post. 

Grab a glass of water (or your favorite beverage), a comfy chair, and let's get to work. 

## Table of Contents
1. Installing Clojure & Leiningen
2. Creating a Clojure application, installing dependencies
3. Ring - HTTP Server
4. What is & Why use Component?
5. Let's Compojure the right routes
6. Connect database
7. Migrate all the things!
8. Interacting with the database using HoneySQL
9. Fin

## Installing Clojure & Leiningen 
