## Building the todo-list app

```
 docker build -t todo-list-app .
```

## Listing the images


```
 docker images
REPOSITORY                            TAG               IMAGE ID       CREATED          SIZE
ajeetraina/tod                        latest            895dd0758057   7 seconds ago    1.77GB
```


## Running the container

```
 docker run -d -p 3000:3000 todo-list-app
```

## Accessing the app

Open https://localhost:3000 to access the todo-list app.

<img width="668" alt="image" src="https://github.com/ajeetraina/todo-list/assets/313480/9c63f847-3ca6-491a-aca2-1bcb593e63cb">


## Explanation of src/index.js

The index.js is a well-structured Express.js application that implements CRUD (Create, Read, Update, Delete) operations on items using a persistence layer (db). Here's a breakdown of the code:

### 1. Dependencies and Initializations:

- `express`: Imports the Express framework for building the web server.
- `app`: Creates an instance of the Express application.
- `db`: Requires a separate module (./persistence) likely containing functions to interact with a database or other storage solution.
- `getItems, addItem, updateItem, deleteItem`: These functions are imported likely from separate route files (./routes/) handling specific API endpoints.

### 2. Middleware:

- `app.use(express.json())`: This middleware parses incoming JSON data in request bodies and makes it accessible on the req.body object.
- `app.use(express.static(__dirname + '/static'))`: This middleware serves static content (like HTML, CSS, JavaScript) from the static directory in the project root.

### 3. Route Definitions:

These routes define how the server responds to different HTTP methods and URLs:

- app.get('/items'): Handles GET requests to the /items endpoint, likely using the getItems function to retrieve a list of items.
- app.post('/items'): Handles POST requests to the /items endpoint, likely using the addItem function to create a new item.
- app.put('/items/:id'): Handles PUT requests to the /items/:id endpoint, likely using the updateItem function to update an existing item based on its ID.
- app.delete('/items/:id'): Handles DELETE requests to the /items/:id endpoint, likely using the deleteItem function to delete an item based on its ID.

### 4. Server Start and Error Handling:

- `db.init().then(...)`: This code attempts to initialize the database connection (defined in db.js) using a promise.

On successful initialization:
- The server starts listening on port 3000 and logs a message to the console.
- On error during initialization:
- The error is logged to the console.
- The process exits with an error code (1).

### 5. Graceful Shutdown:

- gracefulShutdown(): This function defines how the server should shut down gracefully when receiving specific signals.

It attempts to call db.teardown() (likely defined in db.js) to disconnect from the database (if applicable).
After teardown (or if teardown fails), the process exits.
Process signal handlers:

- `process.on('SIGINT', gracefulShutdown)`: Listens for the SIGINT signal (often sent by pressing Ctrl+C) and triggers graceful shutdown.
- `process.on('SIGTERM', gracefulShutdown)`: Listens for the SIGTERM signal (often sent by termination signals) and triggers graceful shutdown.
- p`rocess.on('SIGUSR2', gracefulShutdown)`: Listens for the SIGUSR2 signal (often sent by tools like nodemon) and triggers graceful shutdown.

Overall, this code demonstrates a well-structured and robust Express application ready to handle CRUD operations on items using a database or persistence layer.
