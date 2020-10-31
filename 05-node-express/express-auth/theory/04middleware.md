# Middleware

We want to be able to check if our user is logged in from within any of our routes. One strategy for doing this is to expand our request object \(req\) using an express middleware. Middleware is code that exists in the "middle" between receiving the request/response objects from the client and handling them on the server.

We've already used 3rd party Express middleware (remember all those `app.use` statements we've written??) and we can create our own.

**Creating our own middleware**

app.use simply accepts a function as it's parameter and gives us that function 3 arguments:

* `req` - the request object
* `res` - the response object
* `next` - a callback function \(moves to the next middleware\)

We can modify each of these arguments and the modification will be reflected in the next middleware and finally in our route code.

**Example**

```javascript
app.use((req, res, next) => {
  req.getParamNames = () => {
    return Object.keys(req.params);
  }
  next();
});

// ...later on in your code...

app.get('/sum/:x/:y', function(req, res) {
  res.send(req.getParamNames());
});
//outputs: ['x','y']
```

Using this concept we can create a middleware to get our currently logged in user from the `req.session`.

