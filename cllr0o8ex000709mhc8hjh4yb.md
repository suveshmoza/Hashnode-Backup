---
title: "REST APIs in depth"
seoTitle: "Mastering REST API Fundamentals: A Comprehensive Guide"
seoDescription: "Unlock the potential of modern web development with our comprehensive guide to learning and implementing REST APIs."
datePublished: Fri Aug 25 2023 19:59:52 GMT+0000 (Coordinated Universal Time)
cuid: cllr0o8ex000709mhc8hjh4yb
slug: rest-apis-in-depth
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693854529019/70322722-92b1-455b-b06e-7e17b767cef6.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693854557714/ef7c5aae-cfdc-4eac-b2fb-7d9c4b5ecb34.png
tags: apis, rest-api

---

### Introduction

An API, or application programming interface, is a set of rules that define how applications or devices can connect to and communicate with each other.

REST stands for Representational State Transfer. It is a style of designing web services with a set of guidelines/principles that allows different software applications to communicate and interact with each other over the Internet.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693854449299/ec308f85-610c-4e55-8ff8-e7ca9b2b9f4e.gif align="center")

So, when a client requests data from a REST API, the server will return a representation of the state of the data required.

### Guidelines to follow while building REST APIs

**<mark>6 guidelines</mark>** are to be followed while building REST API's. Let's discuss each guideline in detail:

1. **Client-Server Architecture**
    
    Client-Server architecture is a fundament concept in REST APIs. In this client and server are separate entities and the interaction between them is only in the form of requests. It is the client that makes a request for a resource to the server and the server responds it back by sending the requested data as a response.
    
2. **Cacheable**
    
    In the context of REST APIs, cacheable refers to the ability to store the server response in browsers. Caching significantly improves the efficiency and performance of the server by reducing the need for repeated requests for the same resource. This can reduce network traffic and latency, leading to faster response times.
    
3. **Layered Architecture**
    
    By layered architecture, we mean the organization of components in a hierarchical manner and each component serves a specific purpose. Each layer can communicate with its adjacent component only. For example when a client requests data from the server, then the server looks for the data in the database and returns it to the client. But the client doesn't know about the database, it only knows about the server.
    
4. **Stateless**
    
    This is the most important guideline of the REST API. By stateless, we mean that the server doesn't store information about a client. The server can get multiple requests from different clients as well as multiple requests from the same client. Clients must send all the required information in each request. This information can include authentication credentials, request parameters, and any data needed to perform the requested action.
    
5. **Uniform Interface**
    
    1. Each resource in a RESTful API should be identified by a unique URL (Uniform Resource Locator). The URL serves as a universal address to access and manipulate the resource.
        
    2. Clients interact with resources by exchanging representations. A representation is a format that conveys the state of a resource. Common representations include JSON, XML etc. Clients can request, modify, or delete resources by sending appropriate representations in their requests.
        
    3. The uniform interface specifies the use of standard **HTTP** methods to perform actions on resources. These methods include:
        
        * **GET**: Used to retrieve a representation of a resource.
            
        * **POST**: Used to create a new resource.
            
        * **PUT**: Used to update or replace an existing resource.
            
        * **DELETE**: Used to remove a resource.
            
6. **Code On Demand \[Optional\]**
    
    It is an optional feature that allows the server to send executable code to the client, which the client can then execute to perform certain tasks.
    

### REST API Example

Let's assume we're building a simple CRUD (Create, Read, Update, Delete) API for managing a collection of books.

Suppose our base URL is [https://api.books.com](https://api.example.com)

1. **GET: Retrieve a List of Books**
    
    * Description: Retrieve a list of all books in the collection.
        
    * Endpoint: `/books`
        
    * Method: GET
        
    * Response: List of book objects in JSON format.
        
2. **POST: Create a New Book**
    
    * Description: Add a new book to the collection.
        
    * Endpoint: `/books`
        
    * Method: POST
        
    * Request Body: New book object in JSON format.
        
    * Response: The newly created book object in JSON format along with a status code (201 Created).
        
3. **PUT: Update a Book**
    
    * Description: Update an existing book's information.
        
    * Endpoint: `/books/{bookId}`
        
    * Method: PUT
        
    * Request Body: Updated book object in JSON format.
        
    * Response: The updated book object in JSON format with a status code (200 OK).
        
4. **PATCH: Partial Update of a Book**
    
    * Description: Update specific attributes of an existing book.
        
    * Endpoint: `/books/{bookId}`
        
    * Method: PATCH
        
    * Request Body: JSON object containing attributes to be updated.
        
    * Response: The updated book object in JSON format with a status code (200 OK).
        
5. **DELETE: Delete a Book**
    
    * Description: Remove a book from the collection.
        
    * Endpoint: `/books/{bookId}`
        
    * Method: DELETE
        
    * Response: A success message with a status code (204 No Content).
        
    
    I have implemented the above API using Node.js
    
    ```javascript
    const express = require('express');
    const bodyParser = require('body-parser');
    
    const app = express();
    const port = 3000;
    
    // Sample book data
    let books = [
      {
        id: 1,
        title: "Sample Book 1",
        author: "John Doe",
        genre: "Fiction",
      },
      {
        id: 2,
        title: "Sample Book 2",
        author: "Jane Smith",
        genre: "Fantasy",
      },
    ];
    
    
    app.use(bodyParser.json());
    
    // GET: Retrieve all books
    app.get('/books', (req, res) => {
        res.json(books);
    });
    
    // POST: Create a new book
    app.post('/books', (req, res) => {
        const newBook = req.body;
        newBook.id = books.length + 1;
        books.push(newBook);
        res.status(201).json(newBook);
    });
    
    // PUT: Update a book by ID
    app.put('/books/:id', (req, res) => {
        const id = parseInt(req.params.id);
        const updatedBook = req.body;
        const index = books.findIndex(book => book.id === id);
    
        if (index !== -1) {
            books[index] = { ...books[index], ...updatedBook };
            res.json(books[index]);
        } else {
            res.status(404).json({ message: 'Book not found' });
        }
    });
    
    // DELETE: Delete a book by ID
    app.delete('/books/:id', (req, res) => {
        const id = parseInt(req.params.id);
        const index = books.findIndex(book => book.id === id);
    
        if (index !== -1) {
            books.splice(index, 1);
            res.status(204).send();
        } else {
            res.status(404).json({ message: 'Book not found' });
        }
    });
    
    // Start the server
    app.listen(port, () => {
        console.log(`Server is running on port ${port}`);
    });
    ```
    

### Conclusion

That wraps up this blog on REST APIs in depth. Hope you like it!

We started by looking at an introduction to API and REST API. Then we learned about the guidelines that are followed while building REST APIs and ended it with an example of book collection API.