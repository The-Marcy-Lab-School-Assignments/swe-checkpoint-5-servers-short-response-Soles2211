Short Response Questions
========================

Answer each of these questions completely but concisely. Use the proper technical terminology. You may refer to the [Marcy Lab School Docs](https://marcylabschool.gitbook.io/marcy-lab-school-docs) or Google but do NOT copy and paste definitions or explanations verbatim.

You can earn up to 6 points for each response (3 points for writing quality, 3 points for technical content).

Before submitting your responses, use a spell checker / AI to ensure that you have no grammar or spelling mistakes.

Question 1: Servers and HTTP
----------------------------

What is a server? Describe the HTTP request-response cycle including the key components of a request (method, endpoint, headers, body) and a response (status code, headers, body). Use an analogy to support your explanation.

**Your Answer:**

A server is a computer or computer system that provides data to other computers. When the client sends a request to the server, it specifies what it wants using the HTTP method, URL, headers and/or body. It's like mailing a letter, with the URL being the send address, the method being the purpose of the letter, the headers and the body being the information outside and inside the letter respectively. The server (recipient) receives the letter (request), prepares a response for the sender (the package) and sends it back to the client for use.

Question 2: Middleware
----------------------

What is middleware in Express? How does it differ from a regular controller? Explain the role of `next()` and provide an example of when middleware is useful.

**Your Answer:**

*   In Express, middleware is a controller between a request and a response that can be invoked for all incoming requests.
    
*   It is different from a regular controller because it uses `app.use` to register (invoke for all endpoints), and `next()` as opposed to `res.send()`.
    
*   `next()` sends the request to the next controller or middleware to be handled.
    
*   Middleware is useful when you want the server to do something like keep track of the requests it sends:
    
    ```js
    // Logging routes
    const logRoutes = (req, res, next) => {
      const time = new Date().toLocaleString();
      console.log(`${req.method}: ${req.originalUrl} - ${time}`);
      next();
    };
    app.use(logRoutes);
    ```

Question 3: API Key Security
----------------------------

Why is it dangerous to use API keys in client-side (frontend) code? Explain how a backend server solves this problem (the "proxy" pattern). Include what role environment variables (`.env`) play in this approach.

**Your Answer:**

*   It is dangerous to use API keys in client-side code because certain APIs charge you for each request using the key, and if someone steals your key, they can take advantage of request resources.
    
*   A backend server mitigates this issue by acting as a proxy. This allows the client to send the server a request without the API key, the server to send the request to the API with the key and pass the response along to the client.
    
*   You define your API key inside of the `.env` file in a key-value pair (no spaces) and use the variable in your code by installing the `dotenv` npm module and referencing the object it creates (`process.env`).
    

  

Question 4: Debugging a Server
------------------------------

A fellow student is building an Express server. They send a `PATCH` request to `/api/bookmarks/1` using Postman, but they receive a `404` status code. List at least three things you would check to debug this issue and explain why each one could be the cause of the problem.

**Your Answer:**

I would check:

*   If the routes are correctly defined
    
*   If the HTTP method is correct
    
*   If the order of the middleware and routes is correct