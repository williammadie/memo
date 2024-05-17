# Unit Tests

- [Backend Application](#backend-application)
- [End-to-End Testing](#end-to-end-testing)

## Backend Application

### Testing CRUD Operations

During my last school project, we were told to write `unit tests` for our CRUD operations. The template that our teacher gave us was as described by the following diagram:

#### The wrong way

![Testing CRUD Wrong Way](/software_testing/unit_tests/resources/testing-crud-wrong.png)

We simply request our REST endpoint and then based our assertions on what was being returned:
- HTTP Status Code
- Objects inside HTTP Body (if any were returned)

This process is simple and fast to set up. However, it has one major drawback. It does not include any way of asserting what has been written in our DB. It excludes this part from our test letting all kinds of bugs happen.

How can we fix it?

#### The right way

![Testing CRUD Right Way](/software_testing/unit_tests/resources/testing-crud-right.png)

Here is an updated process for testing our CRUD operations. This method allows us to test the whole process. In my opinion, it is way better as it covers the whole thing!

It has some drawbacks like the fact that it assumes that the `Read` operation should always be working before launching any other kind of tests.

It is also a bit more verbose as our tests need to do 2 requests and to assert several things. However, it allows us to completely test the whole process of the resource.

## End-To-End Testing

**End-To-End Testing** also called **e2e** verifies that all components of a system can run under real-world scenarios.

The purpose of such tests is to verify that the **behavior** of our application is correct