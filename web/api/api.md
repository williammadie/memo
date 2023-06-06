# API

## Table of Content

## What is an API

**API** (**Application Programming Interface**): set of definitions and protocols for building and integrating application software.

The benefits of using an API is that **we do not need** to know of a system works for making use of its features.

## REST API

**REST** (**REpresentational State Transfer**): architecture based on resources/objects. 

REST APIs are based on path after the url of the web server. For instance, if I want to retrieve all Pokemons from the API, I will use the following request:

```bash
curl -X GET http://localhost/pokemons
```

- `http://localhost`: Web Server Address
- `/pokemons`: Route of the resource

An API can be secured by **oAuth2** or **JWT**.

## oAuth2

## JWT