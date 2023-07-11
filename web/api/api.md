# API

## Table of Content

- [What is an API](#what-is-an-api)
- [REST API](#rest-api)
- [API Security](#api-security)

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

## API Security

An API can be secured by several means such as **oAuth2** or **JWT**.

### oAuth2



### JWT

`JWT` means `JSON Web Tokens` and refers to an **open industry standard** that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

A `JWT` contains three parts:
1. **Header**: signing algorithm used + type of token (here JWT)
2. **Payload**: contains the JSON Object also called *the claims*
3. **Signature**: A string that is generated via a cryptographic algorithm that can be used to verify the integrity of the JSON payload

It appends the previous fields like `<header>.<body>.<signature>`:
```bash
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJhYmNkMTIzIiwiZXhwaXJ5IjoxNjQ2NjM1NjExMzAxfQ.3Thp81rDFrKXr3WrY1MyMnNK8kKoZBX9lg-JwFznR-M
<=============header===============>.<=========================body===========================>.<===============signature=================>
```

In resume, it has the following structure:

![jwt-structure](/web/api/resources/jwt-structure.png)


How can I generate such a token?

![jwt-mechanism](/web/api/resources/jwt-token-mechanism.png)

