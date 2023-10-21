# Postman

## Table of Contents

- [Introduction](#introduction)
- [Assertions](#assertions)
    - [Where to Put Assertions](#where-to-put-assertions)
- [Folders](#folders)
- [Organizational Patterns](#organizational-patterns)
    - [Happy Path and Sad Path Pattern](#happy-path-and-sad-path-pattern)
    - [Endpoint Pattern](#endpoint-pattern)
    - [User Stories Pattern](#user-stories-pattern)
    - [Validation Type Pattern](#validation-type-pattern)
- [Good Practices](#good-practices)
    - [Requests](#requests)
    - [Assertions](#assertions)
    - [Environments](#environments)
    - [Variables](#variables)
    - [Folders](#folders)
    - [Collections](#collections)
    - [Workspaces](#workspaces)

## Introduction

## Assertions

### Where to Put Assertions

There are 3 levels where you can put your assertions:
1. Collection Level -> Assertions that will be the same throughout the collection (ex: Header, Response Code, Response Time Assertions)
2. Folder Level -> Assertions that will be the same throughout the folder (ex: Response Code, Body Assertions)
3. Request Level -> Assertions that will be **unique** to that request (ex: Response Code, Body, JSON data Assertions)

## Folders

Folders are inside collections. They help to keep things organized.

## Organizational Patterns

### Happy Path and Sad Path Pattern

It is a good pattern for small APIs. It contains 2 folders:
1. Happy Path Folder
    - can be used as a quick regression check

2. Sad Path Folder
    - can be used for validation checking

### Endpoint Pattern

- It is a good pattern for APIs with lots of endpoints. It **has a folder for each type of endpoint**. (Manga, Library, Favorites, Users...)
- Everything can then be organized in **subfolders** for different operation types (GET, POST, UPDATE...)
- It is also possible to have **sub-subfolders** with Happy Path / Sad Path requests 

### User Stories Pattern

- It is a good pattern for APIs handling **customer workflows**.
- It can have a folder for each workflow (Create a new account, update account, search for a manga, add a manga to library)
- It can have subfolders for different scenarios

### Validation Type Pattern

- It is good for APIs that require a lot of validation. Folders are organized around validation types (security validations, JSON Body Validations, Header Validations, Student Scope (check that a student can modify grades of another student)...)
- also great for security testing

## Good Practices

### Requests

- Give descriptive names to your requests
- Don't include the HTTP action (GET, POST, PUT...) in the name of the request
- Don't make the names too long
- Use pipe for visual clarity (`Mangas|User|All`)

### Assertions

- Don't feel like you have to assert on every field of the response
- Give the assertions names that make sense

Bad assertion names (Too generic):
- Status Code
- Correct Record is Returned
- Error Message is Returned

Good assertion names (More specific):
- Status Code **is 200**
- Correct Employee ID is Returned
- Missing Last Name Error Message is Returned

### Environments

- Keep the naming conventions consistent
- Put the environment in the name with capital letters (mangatracker-PROD, mangatracker-FEATURE)

### Variables

- Remember that variables are case-sensitive
- Decide if you use snake_case, camelCase or PascalCaser and stick to it
- Don't use abbreviations
- Give your variables descriptive name (`User1` -> `UserWithCredentials`)

### Folders

- Keep every single request **in a folder**
- Follow a pattern when you choose what to put in a folder
- Give your folders easy-to-read names

### Collections

- Name your collection after your API (**1 collection = requests for 1 API**)
- Use the favorite function to move your most-used collections to the top of your workspace

### Workspaces

- Each team should have its own workspace
- Keep everything you need for an application in one workspace
- Share only necessary things in the team workspace
- Decide who should have admin rights in the workspace (Use Zero Trust)