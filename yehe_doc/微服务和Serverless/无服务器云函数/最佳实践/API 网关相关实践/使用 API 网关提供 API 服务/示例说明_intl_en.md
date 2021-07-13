In this tutorial, suppose that:
- You want to use SCF to implement a web backend service, such as querying the articles in a blog and providing the article contents.
- You want to use APIs to provide services for webpages and applications.

## Implementation Overview

The implementation process of the service is as follows:

- Create a function, configure API rules in API Gateway, and point the backend service to the function.
- A user sends a request that contains an article ID to the API.
- SCF queries the content corresponding to the ID according to the request parameters and responds to the request in JSON format.
- The user performs subsequent processing after receiving the response in JSON format.


Note: after going through this tutorial, your account will have the following resources:

- An SCF function triggered by API Gateway.
- An API service in API Gateway and related API rules.

This tutorial is divided into three parts:

- Complete the coding, creation, and testing of a function.
- Complete the design, creation, and configuration of an API service and API rules.
- Test and verify the correctness of the API through a browser or HTTP request tool.

## API Design

The design of APIs for modern applications usually follows the RESTful specification. Therefore, in this example, we design the API for getting blog articles as follows:

* /article GET
Return the article list

* /article/{articleId} GET
Return the article content based on the article ID


