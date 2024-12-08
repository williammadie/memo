# Authentication

## Table of Contents

- [Authentication and Authorization](#authentication-and-authorization)
- [Authentication Methods](#authentication-methods)
    - [HTTP Basic Auth](#http-basic-auth)

## Authentication and Authorization

**Authentication**: process of verifying **who** is attempting to access a restricted system.

**Authorization**: process of verifying **what a given user can do** on the system.

Authentication always come before Authorization. 

## Authentication Methods

### HTTP Basic Auth

This method is directly built into the HTTP protocol. It is the most basic method of authentication. Here, the login credentials are sent in the request headers with each request. It is done as below:

```bash
"Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=" your-website.com
```

Here `dXNlcm5hbWU6cGFzc3dvcmQ=` corresponds to `username:password` encoded in base64 (=binary representation).

![http-basic-auth-flow](/web/auth/resources/http-basic-auth-flow.png)

To sum up, the following sequence takes place:

1. The client makes an unauthenticated request to a protected endpoint.

2. The server responds with status code `401 Unauthorized` and the header `WWW-Authenticate: Basic` to indicate which authentication method should be used.

3. The client's web browser prompts the user for a username and a password. These credentials are then sent with each request by automatically adding the header `Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ=` where `dXNlcm5hbWU6cGFzc3dvcmQ=` is the base64 encoded `username:password`

4. The server verifies each request by decoding the base64 `Authorization: Basic <encoded-credentials>` and checking that the user exists in its database.

Web browsers automatically prompt for the username and password and the following pop-up will appear:

![http-basic-auth-prompt](/web/auth/resources/http-basic-auth-prompt.png)


|                              Pros                             |                                                             Cons                                                            |
|:-------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------------------------------:|
|   Authentication is fast as there aren't a lot of operations  | User credentials are encoded in base64 but not encrypted. It is mandatory to use HTTPS/SSL with this authentication method  |
|                     Very easy to implement                    |                                         Credentials must be sent with every request                                         |
| Supported by all browsers as it is built in the HTTP protocol |                       The only way to log out a user is to write the credentials with an invalid input                      |

[Sources used to write article](https://testdriven.io/blog/web-authentication-methods/#session-based-auth)