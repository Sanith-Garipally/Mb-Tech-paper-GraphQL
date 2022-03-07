# **GraphQl Architecture**

![](https://1vi3uw2r71ig39fow2sdrab1-wpengine.netdna-ssl.com/wp-content/uploads/2020/03/graphql-1120x600.png)

## **What is GraphQl ?**
GraphQL is a query language for [APIs](https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces) developed by Facebook in 2012. 

In simple words, it is used to load data from a server to a client (i.e. from an API to your application) much more efficiently than traditional services.

## **What is the problem with the current API's ?**
Let's understand with the help of a scenario,

Consider we are building an blogging app using REST API where we want to display the user's:

* First Name
* Titles of the user's posts

For this use case we will be requiring two API Endpoints:

1. /user/<id\> - (*To fetch the name of the user* )

```
    {
        "user": {
            "id": "qwerty1234",
            "name": "sanith",
            "address": "xyz",
            "birthday": "abc"
        }
    }

```
2. /user/<id\>/posts - (*To fetch the Titles of the blog posts* )

```
    {
        "posts": [{
            "id": "asdf0987",
            "title": "About GraphQl",
            "content": "GraphQL is ...",
            "comments": "[...]"
        }]
    }

```

The above two code snippets are the HTTP responses, we require only name and post's title but along with them we are fetching unnecessary data like address, content, comments.

There are two main problems with the current REST APIs:
* **Over fetching.**
When more data is delivered upon fetching than is required. In these cases, you are unable to utilize all of it.

* **Under fetching.**
When the data you get back is not enough. Often times, the data is so little that you have to run another query.

## **What makes GraphQl exicitingly different ?**

Considering the above scenario, In GraphQL on the other hand, you would simply send a single query to the GraphQL server that includes the concrete data requirements. The server then responds with a JSON object where these requirements are fulfilled.

```
    {
        "data": {
            "user": {
                "name": "sanith",
                "posts": [
                    {
                        "title": "About GraphQl"
                    }
                ]
            }
        }
    }
```

Using GraphQL, the client can specify exactly the data it needs in a query. Notice that the structure of the server response follows precisely the nested structure defined in the query which icludes the specific data requested by the client.

## **GraphQL Key Components**

The GraphQL API uses three main components:

* **Queries.**
A query is the request the client makes. 

* **Resolvers.**
A resolver tells GraphQL how (and where) to fetch the data corresponding to a specific query. 

* **Schema.**
A GraphQL schema describes the functionality clients can utilize once they connect to the GraphQL server. The core building block within schemas is called a type.

# **Architecture**
GraphQL was released as a specification. The specification describes the behavior of the GraphQL server. It provides some guidelines to handle requests from the clients and responses from the server, such as supported protocols, the format of the data that the server accepts, the format of the server's response, etc.

When a client requests a query to communicate with the server, the transport layer of GraphQL
can be connected with any available network protocol such as TCP, WebSocket, or any other transport layer protocol.

The GraphQL server doesn't care about the database you use. It is neutral to databases. You can use a relational or a NoSQL database.

## **Client-Server flow in GraphQL**

* The GraphQL query is not written in JSON. When a client makes a 'POST' request to send a GraphQL query to the server, this query is sent as a string.

* The server receives and extracts the query string. After that, the server processes and validates the GraphQL query according to the GraphQL syntax and the graph data model (GraphQL schema).

* Like the other API servers, the GraphQL API server also makes calls to a database or other services and retrieves the data requested by the client.
After that, the server takes the data and returns it to the client in a JSON object.

There are three common architectural models for a GraphQL server.

## **GraphQL server with a connected database**
This architecture setup is mostly used for new projects. 

In this architecture setup, the GraphQL server is integrated with the database. When the client sends a query, the server reads the requested query and fetches data from the database. This process is known as resolving the query. 

After resolving the query, the response is returned to the client in the official GraphQL specification format.

![](https://static.javatpoint.com/tutorial/graphql/images/graphql-architecture.png)

In the above architecture, you can see that the GraphQL server and the database are integrated on a single node. The client communicates with the GraphQL server by sending a query via computer/ mobile over HTTP
. After receiving the query, the GraphQL server processes the request, retrieves data from the database and returns it to the client.

## **GraphQL server integrated with the existing system**
This architecture model is used for companies having complicated projects which have legacy infrastructure and many different APIs. In this architecture model, GraphQL can be used to merge microservices, legacy infrastructure, and third-party APIs in the existing system and hide the complexity of data fetching logic. The server doesn't care about the database you use. It may be a relational or a NoSQL database.

![](https://static.javatpoint.com/tutorial/graphql/images/graphql-architecture2.png)

In the above architecture, you can see that the GraphQL server acts as an interface between the client and the existing systems.  

## **A hybrid approach with a connected database and integration of the existing system**
This architecture model is a combination of the above two approaches: the GraphQL server with a connected database and the GraphQL server integrated with the existing system. In this architecture model, when a query is received by the server, the server resolves the received query and retrieves data either from the connected database or from the integrated API's.

![](https://static.javatpoint.com/tutorial/graphql/images/graphql-architecture3.png)

# **Conclusion**
If your API is intended to be used on a mobile application or a large application like Facebook Newsfeed or applications where we usually need nested data to be fetched i.e. blog posts with their comments and people details, using GraphQL will be effective and efficient choice as it offers better bandwidth usage.

If you need caching and monitoring facilities in your API, Or, public APIs where we want to determine what to expose to the clients, using REST will be better choice.

You can also use a combination of GraphQL and REST for a project. It all depends on your data and performance requirements.

# **References**
[www.javatpoint.com](https://www.javatpoint.com/graphql-architecture)

[www.howtographql.com](https://www.howtographql.com/basics/0-introduction/)

[levelup.gitconnected.com](https://levelup.gitconnected.com/what-is-graphql-87fc7687b042)

[blog.back4app.com](https://blog.back4app.com/what-is-graphql/)

[www.medium.com](https://medium.com/@weblab_tech/graphql-everything-you-need-to-know-58756ff253d8)

[www.redhat.com](https://www.redhat.com/en/topics/api/what-is-graphql)