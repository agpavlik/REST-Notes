# REST APIs

- [What is API?](#1)
  - [How API works?](#10)
  - [Types of APIs](#11)
  - [API protocols](#12)
- [What is REST?](#2)
  - [How REST APIs work?](#20)
  - [REST design principles](#21)
- [Ways to fetch data](#3)

  - [XMLHttpRequest](#30)
  - [fetch() method](#31)
  - [Async-Await in fetch()](#32)

    - [example 1 with fetch()](#311)
    - [example 2 with fetch()](#312)
    - [example 3 with fetch()](#313)
    - [example 4 with fetch()](#314)

  - [Axios library](#33)

    - [example 1 with Axios](#332)
    - [example 2 with Axios](#332)

  - [jQuery AJAX](#34)
  - [Custom Hook](#35)
  - [React Query library](#36)
    - [example 1 with React Query](#361)

- [What is JSON?](#4)
- [What is CRUD?](#5)

## 🔥 What is API? <a name="1"></a>

In simple terms, an `Application Programming Interface` is a set of protocols and tools for building software applications. APIs allow different software applications to communicate with each other and exchange data. It acts as an intermediary layer that processes data transfers between systems, letting companies open their application data and functionality to external third-party developers, business partners, and internal departments within their companies.

The definitions and protocols within an API help businesses connect the many different applications they use in day-to-day operations, which saves employees time and breaks down silos that hinder collaboration and innovation. For developers, API documentation provides the interface for communication between applications, simplifying application integration.

### 🔥 How API works? <a name="10"></a>

A simple way to understand how APIs work is to look at a common example—third-party payment processing. When a user purchases a product on an ecommerce site. This function relies on APIs to make the connection. When the buyer clicks the payment button, an API calls to retrieve information—also known as a `request`. This request is processed from an application to the web server via the `API’s Uniform Resource Identifier (URI)` and includes a request verb, headers, and sometimes, a request body. After receiving a valid request from the product webpage, the API makes a call to the external program or web server, in this case, the third-party payment system. The server sends a `response` to the API with the requested information. The API transfers the data to the initial requesting application, here the product website.

### 🔥 Types of APIs <a name="11"></a>

Today most APIs are web APIs that expose an application's data and functionality over the internet. Here are the four main types of web API:

- `Open-source APIs`, also known as public APIs, they have defined API endpoints and request and response formats.
- `Partner APIs` connect strategic business partners. Typically, developers access these APIs in self-service mode through a public API developer portal. Still, they need to complete an onboarding process and get login credentials to access partner APIs.
- `Internal APIs` remain hidden from external users. These private APIs aren't available for users outside of the company and are instead intended to improve productivity and communication across different internal development teams.
- `Composite APIs` combine multiple data or service APIs. They allow programmers to access several endpoints in a single call. Composite APIs are useful in microservices architecture where performing a single task may require information from several sources.

### 🔥 API protocols <a name="12"></a>

As the use of web APIs has increased, certain protocols have been developed to provide users with a set of defined rules, or API specifications, that create accepted data types, commands and syntax.

- `SOAP` (Simple Object Access Protocol): Built with XML, SOAP enables endpoints to send and receive data through SMTP and HTTP. SOAP APIs make it easier to share information between apps or software components that are running in different environments or written in different languages.
- `XML-RPC` (XML-Remote Procedure Call): The XML-RPC protocol relies on a specific XML format to transfer data. XML-RPC is older than SOAP, but much simpler, and relatively lightweight in that it uses minimum bandwidth.
- `JSON-RPC`: Like XML-RPC, JSON-RPC is a remote procedure call, but JSON (JavaScript Object Notation) is used instead of XML to transfer the data.
- `REST` (Representational State Transfer): REST is a set of web API architecture principles. REST APIs—also known as a RESTful API - are APIs that adhere to certain REST architectural constraints.

Traditionally, API referred to an interface connected to an application created with any of the low-level programming languages, such as Javascript. Modern APIs, however, adhere to REST principles and the JSON format. They are typically built for HTTP, resulting in developer-friendly interfaces that are easily accessible and widely understood by applications written in Java, Ruby, Python, and many other languages.

## 🔥 What is REST? <a name="2"></a>

REST is a set of conventions and practices in web development that deals with accessing and manipulating resources over HTTP.
`REST API` stands for `Representational State Transfer application programming interface`, sometimes referred to as the RESTful API, and it’s the primary interface that is used by React developers which allows API connections between different parts of an application or service over the internet.

### 🔥 How REST APIs work? <a name="20"></a>

REST APIs communicate via HTTP requests to perform standard database functions like creating, reading, updating, and deleting records (also known as CRUD) within a resource.

Each URL is called a `request` while the data sent back to you is called a `response`.

The anatomy of the `request`:

- `the endpoint`

  The endpoint (or route) is the url you request for. The `root-endpoint` is the starting point of the API you are requesting from. For example, the root-endpoint of Github’s API is https://api.github.com. The `path` determines the resource you’re requesting for. Any colons (:) on a path denotes a variable. You should replace these values with actual values of when you send your request. For example, you should replace `:username` in
  `/users/:username/repos` with the actual username of the user you’re searching for. The final part of an endpoint is `query parameters`. Technically, query parameters are not part of the REST architecture, but you’ll see lots of APIs use them. So, to help you completely understand how to read and use API’s we’re also going to talk about them. Query parameters give you the option to modify your request with key-value pairs. They always begin with a question mark (?). Each parameter pair is then separated with an ampersand (&), like this: `?query1=value1&query2=value2`

- `the method`

  The method is the type of request you send to the server. You can choose from these five types below: GET, POST, PUT, PATCH, DELETE. These methods provide meaning for the request you’re making. They are used to perform four possible actions: Create, Read, Update and Delete (`CRUD`).

  `GET` - This request is used to get a resource from a server. If you perform a GET request, the server looks for the data you requested and sends it back to you. In other words, a GET request performs a `READ` operation. This is the default request method.

  `POST`- This request is used to create a new resource on a server. If you perform a POST request, the server creates a new entry in the database and tells you whether the creation is successful. A POST request performs an `CREATE` operation.

  `PUT` and `PATCH` - These two requests are used to update a resource on a server. If you perform a PUT or PATCH request, the server updates an entry in the database and tells you whether the update is successful. A PUT or PATCH request performs an `UPDATE` operation.

  `DELETE` - This request is used to delete a resource from a server. If you perform a `DELETE` request, the server deletes an entry in the database and tells you whether the deletion is successful. A DELETE request performs a `DELETE` operation.

- `the headers`

  Headers are used to provide information to both the client and server. It can be used for many purposes, such as authentication and providing information about the body content.

- `the data (or body)`

  The data contains information you want to be sent to the server. This option is only used with POST, PUT, PATCH or DELETE requests.

## 🔥 REST design principles <a name="21"></a>

REST APIs can be developed using virtually any programming language and support a variety of data formats. The only requirement is that they align to the following six REST design principles - also known as architectural constraints:

- `Uniform interface`
  All API requests for the same resource should look the same, no matter where the request comes from. The REST API should ensure that the same piece of data, such as the name or email address of a user, belongs to only one uniform resource identifier (URI). Resources shouldn’t be too large but should contain every piece of information that the client might need.
- `Client-server decoupling`
  In REST API design, client and server applications must be completely independent of each other. The only information the client application should know is the URI of the requested resource; it can't interact with the server application in any other ways. Similarly, a server application shouldn't modify the client application other than passing it to the requested data via HTTP.
- `Statelessness`
  REST APIs are stateless, meaning that each request needs to include all the information necessary for processing it. In other words, REST APIs do not require any server-side sessions. Server applications aren’t allowed to store any data related to a client request.
- `Cacheability`
  When possible, resources should be cacheable on the client or server side. Server responses also need to contain information about whether caching is allowed for the delivered resource. The goal is to improve performance on the client side, while increasing scalability on the server side
- `Layered system architecture`
  In REST APIs, the calls and responses go through different layers. As a rule of thumb, don’t assume that the client and server applications connect directly to each other. There may be a number of different intermediaries in the communication loop. REST APIs need to be designed so that neither the client nor the server can tell whether it communicates with the end application or an intermediary.
- `Code on demand (optional)`
  REST APIs usually send static resources, but in certain cases, responses can also contain executable code (such as Java applets). In these cases, the code should only run on-demand.

## 🔥 Ways to fetch data <a name="3"></a>

### 🔥 XMLHttpRequest <a name="30"></a>

Before ES6 and modern libraries like Fetch and Axios, `XMLHttpRequest` was the only way to make API calls in JavaScript. It's still widely used because it's supported by all browsers.

```javascript
// This JavaScript code uses XMLHttpRequest to make a GET request to an API. After sending the request, it checks if the status is 200 (OK). If true, it parses the JSON response; otherwise, it handles errors.

const xhttpr = new XMLHttpRequest();
xhttpr.open("GET", "Api_address", true);
xhttpr.send();
xhttpr.onload = () => {
  if (xhttpr.status === 200) {
    const response = JSON.parse(xhttpr.response);
    // Process the response data here
  } else {
    // Handle error here
  }
};
```

### 🔥 fetch() method <a name="31"></a>

Fetch is a JavaScript's buit-in method to call an API. The request can be of any APIs that return the data of the format JSON or XML. The fetch() require only one parameter which is the URL. It returns a promise, which contains a single value, either response data or an error. You can handle success or failure using the `then()` and `catch()` methods. Respective type of data can be handle with various methods such as `json()`, `text()`, `blob()`, `formData()`, `arrayBuffer()`. In practice, you often can use the `async/await` with fetch() method.

`GET request`

```javascript
function App() {
  useEffect(() => { //useEffect allows to fetch data as soon as the application loads and avoid a side effect
    fetch("url", {method:"GET"}) // method: "GET" - default, so we can ignore it
      .then((response) => response.json()); // Parse the response data as JSON
      .then((data) => console.log(data)); // Process the response data here
      .catch((err) => console.log(err.message)); // This method handle promise rejection
  }, []);

  return data;
}
```

`POST request`
It works similarly to the GET request, the main difference being that you need to add the method and two additional parameters to the optional object (body and header)

```javascript
function App() { // It expects data from a form or whatever which will be send to server
    fetch("url", {
      method:"POST",
      headers: {
      "Content-type": "application/json; charset=UTF-8",
      }, //The header tells us the type of data, which is always the same when consuming REST API's.
      body: JSON.stringify({ message: 'Hello World!' })
    } ) //The body holds the data we want to pass into the API, which we must first stringify because we are sending data to a web server.
      .then((response) => response.json());
      .then((data) => console.log(data)); // Process the response data here
      .catch((err) => console.log(err.message));

  return data;
}


```

### 🔥 example 1 with fetch() <a name="311"></a>

GET request

```javascript
import React, { useState, useEffect } from "react";
// useState to store data retrieve from the API
// useEffect allows to fetch data as soon as the application loads

const App = () => {
  const [posts, setPosts] = useState([]); // create state to store the data retrieve from the API
  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts?_limit=10")
      .then((response) => response.json()) // It returns a response object, which isn't what we want. So we need to resolve the response object to JSON format
      .then((data) => {
        // This also returns a promise for us to get the actual data using the second .then().
        console.log(data);
        setPosts(data);
      })
      .catch((err) => {
        // This method handle promise rejection
        console.log(err.message);
      });
  }, []);

  return (
    <div className="posts-container">
      {posts.map((post) => {
        return (
          <div className="post-card" key={post.id}>
            <h2 className="post-title">{post.title}</h2>
            <p className="post-body">{post.body}</p>
            <div className="button">
              <div className="delete-btn">Delete</div>
            </div>
          </div>
        );
      })}
    </div>
  );
};
```

POST request

```javascript
import React, { useState, useEffect } from "react";
const App = () => {
  const [title, setTitle] = useState("");
  const [body, setBody] = useState("");
  // ...
};

const addPosts = async (title, body) => {
  // It expects these data from a form or whatever
  await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    body: JSON.stringify({
      //The body holds the data we want to pass into the API, which we must first stringify because we are sending data to a web server.
      title: title,
      body: body,
      userId: Math.random().toString(36).slice(2),
    }),
    headers: {
      //The header tells us the type of data, which is always the same when consuming REST API's.
      "Content-type": "application/json; charset=UTF-8",
    },
  })
    .then((response) => response.json())
    .then((data) => {
      // We also set the state to hold the new data and distribute the remaining data into the array.
      setPosts((posts) => [data, ...posts]);
      setTitle("");
      setBody("");
    })
    .catch((err) => {
      console.log(err.message);
    });

  const handleSubmit = (e) => {
    e.preventDefault();
    addPosts(title, body);
  };

  return (
    <div className="app">
      <div className="add-post-container">
        <form onSubmit={handleSubmit}>
          <input
            type="text"
            className="form-control"
            value={title}
            onChange={(e) => setTitle(e.target.value)}
          />
          <textarea
            name=""
            className="form-control"
            id=""
            cols="10"
            rows="8"
            value={body}
            onChange={(e) => setBody(e.target.value)}
          ></textarea>
          <button type="submit">Add Post</button>
        </form>
      </div>
    </div>
  );
};
```

DELETE request

```javascript
// This gets triggered when the button is clicked, and we get the id of the specific post in which the button was clicked. Then we remove that data from the entire retuned data.
const deletePost = async (id) => {
  await fetch(`https://jsonplaceholder.typicode.com/posts/${id}`, {
    method: "DELETE",
  }).then((response) => {
    if (response.status === 200) {
      setPosts(
        posts.filter((post) => {
          return post.id !== id;
        })
      );
    } else {
      return;
    }
  });
};

// This will be removed from the API but not immediately from the UI, which is why we have added a filter to remove the data as well. For each item in the loop, your delete button will look like this:
const App = () => {
  // ...
  return (
    <div className="posts-container">
      {posts.map((post) => {
        return (
          <div className="post-card" key={post.id}>
            <div className="button">
              <div className="delete-btn" onClick={() => deletePost(post.id)}>
                Delete
              </div>
            </div>
          </div>
        );
      })}
    </div>
  );
};
```

### 🔥 example 2 with fetch() <a name="312"></a>

Example - [Pizzolino](https://github.com/agpavlik/Pizzolino)

```javascript
const API_URL = "https://react-fast-pizza-api.onrender.com/api";

// GET
export async function getMenu() {
  const res = await fetch(`${API_URL}/menu`);

  // fetch won't throw error on 400 errors (e.g. when URL is wrong), so we need to do it manually. This will then go into the catch block, where the message is set
  if (!res.ok) throw Error("Failed getting menu");

  const { data } = await res.json();
  return data;
}

export async function getOrder(id) {
  const res = await fetch(`${API_URL}/order/${id}`);
  if (!res.ok) throw Error(`Couldn't find order #${id}`);

  const { data } = await res.json();
  return data;
}

// POST
export async function createOrder(newOrder) {
  try {
    const res = await fetch(`${API_URL}/order`, {
      method: "POST",
      body: JSON.stringify(newOrder),
      headers: {
        "Content-Type": "application/json",
      },
    });

    if (!res.ok) throw Error();
    const { data } = await res.json();
    return data;
  } catch {
    throw Error("Failed creating your order");
  }
}

// PATCH
export async function updateOrder(id, updateObj) {
  try {
    const res = await fetch(`${API_URL}/order/${id}`, {
      method: "PATCH",
      body: JSON.stringify(updateObj),
      headers: {
        "Content-Type": "application/json",
      },
    });

    if (!res.ok) throw Error();
    // We don't need the data, so we don't return anything
  } catch (err) {
    throw Error("Failed updating your order");
  }
}
```

### 🔥 example 3 with fetch() <a name="313"></a>

Example - [use-Popcorn](https://github.com/agpavlik/Udemy-use-popcorn)

```javascript
// search movie

import { useState, useEffect } from "react";

const KEY = "f84fc31d";

export function useMovies(query) {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [error, setError] = useState("");

  useEffect(
    function () {
      // callback?.();

      const controller = new AbortController(); // clean app fetch | clean app current request each time when new one comes in

      async function fetchMovies() {
        try {
          setIsLoading(true);
          setError("");
          const res = await fetch(
            `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
            { signal: controller.signal } // clean app current request each time when new one comes in
          );

          if (!res.ok)
            throw new Error("Something went wrong with fetching movies"); // error

          const data = await res.json();

          if (data.Response === "False") throw new Error("Movie not found");

          setMovies(data.Search);
          setError("");
        } catch (err) {
          if (err.name !== "AbortError") {
            console.log(err.message);
            setError(err.message);
          }
        } finally {
          setIsLoading(false); // change isLoading back to false
        }
      }

      if (query.length < 3) {
        setMovies([]);
        setError("");
        return;
      }

      // handleCloseMovie(); // close current movie if fetch another one

      fetchMovies();

      return function () {
        controller.abort(); // clean app current request each time when new one comes in
      };
    },
    [query]
  );

  return { movies, isLoading, error };
}
```

### 🔥 example 4 with fetch() <a name="314"></a>

Example - [Map-Marker](https://github.com/agpavlik/Map-Marker)

```javascript
function CitiesProvider({ children }) {
  const [{ cities, isLoading, currentCity, error }, dispatch] = useReducer(
    reducer,
    initialState
  );

  // Fetch the cities list data
  useEffect(function () {
    async function fetchCities() {
      dispatch({ type: "loading" });

      try {
        const res = await fetch(`${BASE_URL}/cities`);
        const data = await res.json();
        dispatch({ type: "cities/loaded", payload: data });
      } catch {
        dispatch({
          type: "rejected",
          payload: "There was an error loading cities...",
        });
      }
    }
    fetchCities();
  }, []);

  // Fetch data regarding the exact city
  // useCallback prevents infinite loops
  const getCity = useCallback(
    async function getCity(id) {
      if (Number(id) === currentCity.id) return;

      dispatch({ type: "loading" });

      try {
        const res = await fetch(`${BASE_URL}/cities/${id}`);
        const data = await res.json();
        dispatch({ type: "city/loaded", payload: data });
      } catch {
        dispatch({
          type: "rejected",
          payload: "There was an error loading the city...",
        });
      }
    },
    [currentCity.id]
  );

  // Add new city from the Form to the server
  async function createCity(newCity) {
    dispatch({ type: "loading" });

    try {
      const res = await fetch(`${BASE_URL}/cities`, {
        method: "POST",
        body: JSON.stringify(newCity),
        headers: {
          "Content-Type": "application/json",
        },
      });
      const data = await res.json();

      dispatch({ type: "city/created", payload: data });
    } catch {
      dispatch({
        type: "rejected",
        payload: "There was an error creating the city...",
      });
    }
  }

  // Delete the exact city
  async function deleteCity(id) {
    dispatch({ type: "loading" });

    try {
      await fetch(`${BASE_URL}/cities/${id}`, {
        method: "DELETE",
      });

      dispatch({ type: "city/deleted", payload: id });
    } catch {
      dispatch({
        type: "rejected",
        payload: "There was an error deleting the city...",
      });
    }
  }

  return (
    <CitiesContext.Provider
      value={{
        cities,
        isLoading,
        currentCity,
        error,
        getCity,
        createCity,
        deleteCity,
      }}
    >
      {children}
    </CitiesContext.Provider>
  );
}
```

### 🔥 Async-Await in fetch() <a name="32"></a>

It is the preferred way of fetching the data from an API as it enables to remove .then() callbacks and return asynchronously resolved data. In the async block, we can use Await function to wait for promise.

```javascript
// fetch() with async/await
async function fetchData() {
  const response = await fetch("url");
  const data = await response.json();

  return data;
}
```

> Example 1

```javascript
// To use async/await, first call async in the function. Then when making a request and expecting a response, add the await syntax in front of the function to wait until the promise settles with the result.

import React, { useState, useEffect } from 'react';

const App = () => {
   const [title, setTitle] = useState('');
   const [body, setBody] = useState('');
   const [posts, setPosts] = useState([]);

   // GET with fetch API
   useEffect(() => {
      const fetchPost = async () => {
         const response = await fetch(
            'https://jsonplaceholder.typicode.com/posts?_limit=10'
         );
         const data = await response.json();
         console.log(data);
         setPosts(data);
      };
      fetchPost();
   }, []);

   // DELETE with fetch API
   const deletePost = async (id) => {
      let response = await fetch(
         `https://jsonplaceholder.typicode.com/posts/${id}`,
         {
            method: 'DELETE',
         }
      );
      if (response.status === 200) {
         setPosts(
            posts.filter((post) => {
               return post.id !== id;
            })
         );
      } else {
         return;
      }
   };

   // POST with fetch API
   const addPosts = async (title, body) => {
      let response = await fetch('https://jsonplaceholder.typicode.com/posts', {
         method: 'POST',
         body: JSON.stringify({
            title: title,
            body: body,
            userId: Math.random().toString(36).slice(2),
         }),
         headers: {
            'Content-type': 'application/json; charset=UTF-8',
         },
      });
      let data = await response.json();
      setPosts((posts) => [data, ...posts]);
      setTitle('');
      setBody('');
   };

   const handleSubmit = (e) => {
      e.preventDefault();
      addPosts(title, body);
   };

   return (
      // ...
   );
};

export default App;
```

> Example 2

```javascript
//The `response` object provides the `status code` and `status text` via the `status` and `statusText` properties
async function fetchData() {
  const response = await fetch("url");

  console.log(response.status); //200
  console.log(response.statusText); //OK

  if (response.status === 200) {
    let data = await response.text();

    return data;
  }
}
```

### 🔥 Axios library <a name="33"></a>

Axios is an open-source library for making HTTP requests to servers. It is a promise-based approach. It supports all modern browsers and is used in real-time applications. It is easy to install using the npm package manager. With Axios, we can easily send asynchronous HTTP requests to REST APIs and perform create, read, update and delete operations.
Unlike the Fetch API method, no option is required to declare the method. We simply attach the method to the instance and query it.

```javascript
function App() {
  useEffect(() => {
    axios.get("url").then((response) => console.log(response.data));
  }, []);
  return data;
}
```

```javascript
import axios from "axios";

async function fetchData() {
  const response = await axios.get("url");
  const data = response.data;
  return data;
}
```

```javascript
import axios from "axios";

axios
  .get("APIURL")
  .then((response) => {
    const responseData = response.data; // Access the response data
    // Process the response data here
  })
  .catch((error) => {
    // Handle error here
  });
```

> Example 1

```javascript
// GET request
useEffect(() => {
  client.get("?_limit=10").then((response) => {
    setPosts(response.data);
  });
}, []);

// POST request
const addPosts = (title, body) => {
  client
    .post("", {
      title: title,
      body: body,
    })
    .then((response) => {
      setPosts((posts) => [response.data, ...posts]);
    });
};

// DELETE request
const deletePost = (id) => {
  client.delete(`${id}`);
  setPosts(
    posts.filter((post) => {
      return post.id !== id;
    })
  );
};
```

> Example 2

We can use async/await to write less code and avoid the .then() chaining. When we use async/await, all of our Axios requests will look like this:

```javascript
import React, { useState, useEffect } from 'react';

const App = () => {
   const [title, setTitle] = useState('');
   const [body, setBody] = useState('');
   const [posts, setPosts] = useState([]);

   // GET with Axios
   useEffect(() => {
      const fetchPost = async () => {
         let response = await client.get('?_limit=10');
         setPosts(response.data);
      };
      fetchPost();
   }, []);

   // Delete with Axios
   const deletePost = async (id) => {
      await client.delete(`${id}`);
      setPosts(
         posts.filter((post) => {
            return post.id !== id;
         })
      );
   };

   // Post with Axios
   const addPosts = async (title, body) => {
      let response = await client.post('', {
         title: title,
         body: body,
      });
      setPosts((posts) => [response.data, ...posts]);
   };

   const handleSubmit = (e) => {
      e.preventDefault();
      addPosts(title, body);
   };

   return (
      // ...
   );
};

export default App;
```

> Example 3

```javascript
//App.js

import React, { useState, useEffect } from "react";
import axios from "axios";
import "./App.css";

function App() {
  const [data, setData] = useState();

  useEffect(() => {
    axios
      .get("http://localhost:5000/api/products")
      .then((response) => {
        setData(response.data);
      })
      .catch((error) => {
        console.error(error);
      });
  }, []);

  return (
    <div className="App">
      {
        <div className="products">
          {data?.map((data) => {
            return (
              <div key={data.id}>
                <img className="img" src={data.image} alt="img" />
                <h1>{data.name}</h1>
                <p>{data.description}</p>
              </div>
            );
          })}
        </div>
      }
    </div>
  );
}
export default App;
```

### 🔥 example 1 with Axios <a name="331"></a>

### 🔥 example 2 with Axios <a name="332"></a>

Example - [Photolabs](https://github.com/agpavlik/Photolabs)

```javascript
const getPhotosByTopic = (topicId) => {
  console.log("topicId", topicId);
  axios
    .get(`/api/topics/photos/${topicId}`)
    .then((res) => {
      console.log("res", res);
      dispatch({
        type: ACTIONS.GET_PHOTOS_BY_TOPIC,
        payload: { photos: res.data },
      });
    })
    .catch((e) => {
      console.log("Error fetching photos by topic:", e);
    });
};

useEffect(() => {
  axios
    .get("/api/photos")
    .then((res) => {
      dispatch({ type: ACTIONS.ALL_PHOTOS, payload: { photos: res.data } });
    })
    .catch((e) => {
      console.log("Error fetching photos:", e);
    });

  axios
    .get("/api/topics")
    .then((res) => {
      dispatch({ type: ACTIONS.ALL_TOPICS, payload: { topics: res.data } });
    })
    .catch((e) => {
      console.log("Error fetching topics:", e);
    });
}, []);
```

### 🔥 jQuery AJAX <a name="34"></a>

jQuery is a library used to make JavaScript
programming simple and if you are using it
then with the help of the $.ajax() method you
can make asynchronous HTTP requests to get
data.

```javascript
$.ajax({
  url: "APIURL",
  method: "GET",
  success: function (response) {
    const parsedData = JSON.parse(response);
    // Process the response data here
  },
  error: function (xhr, status, error) {
    // Handle error here
  },
});
```

### 🔥 Custom Hook <a name="35"></a>

It is a React component

```javascript
// variant 1 with axios library
const useFetch = (url) => {
  const [isLoading, setIsLoading] = useState(false);
  const [apiData, setApiData] = useState(null);
  const [serverError, setServerError] = useState(null);

  useEffect(() => {
    setIsLoading(true);
    const fetchData = async () => {
      try {
        const resp = await axios.get(url);
        const data = await resp?.data;

        setApiData(data);
        setIsLoading(false);
      } catch (error) {
        setServerError(error);
        setIsLoading(false);
      }
    };
    fetchData();
  }, [url]);

  return { isLoading, apiData, serverError };
};
```

```javascript
// variant 2 with fetch method
const useFetch = (url) => {
  const [isLoading, setIsLoading] = useState(false);
  const [apiData, setApiData] = useState(null);
  const [serverError, setServerError] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      setIsLoading(true);
      try {
        const resp = await fetch(url);
        const data = await resp.json();

        setApiData(data);
      } catch (error) {
        setServerError(error);
      } finally {
        setIsLoading(false);
      }
    };
    fetchData();
  }, []);

  return { isLoading, apiData, serverError };
};
```

Import the useFetch hook and pass the URL of the API endpoint from where you want to fetch data. Now just like any React hook we can directly use our custom hook to fetch the data.

```javascript
import useFetch from "./useFetch";

const App = () => {
  const { isLoading, serverError, apiData } = useFetch("https://site.com");

  return (
    <div>
      <h2>API data</h2>
      {isLoading && <span>Loading ... </span>}
      {!isLoading && serverError ? (
        <span>Error in fetching data ... </span>
      ) : (
        <span>{JSON.stringify(apiData)}</span>
      )}
    </div>
  );
};
```

### 🔥 React Query library <a name="36"></a>

With this we can achieve a lot more than just fetching data. It provides support for caching and refetching, which impacts the overall user experience by preventing irregularities and ensuring our app feels faster.

```javascript
import axios from "axios";
import { useQuery } from "react-query";

function App() {
  const { isLoading, error, data } = useQuery("posts", () =>
    axios("https://site.com/")
  );
  console.log(data);

  return <div>Data</div>;
}
```

```javascript
import { useQuery } from "react-query";

function App() {
  const { isLoading, error, data } = useQuery("data", fetchData);
  if (isLoading) return <p> Loading ... </p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <ul>
      {data.map((item) => (
        <li key={item.id}>{iten.name}</li>
      ))}
    </ul>
  );
}
```

### 🔥 example 1 with React QueryReact <a name="361"></a>

Example - [Oasis-Backside](https://github.com/agpavlik/Oasis-Backside)

## 🔥 What is JSON? <a name="4"></a>

`JavaScript Object Notation` (JSON) is a standard text based data format used in web development to send and receive the data. It is supported by most programming languages and it's lightening fast. The popularity of JSON is continually growing, and now it’s most popular data exchange type. In JSON. the data are in key:value pairs with double quotes separated by a comma, just like JS object. JSON cannot contain functions.

JSON is used everywhere:

- Storing data in a database
- Sending data between API endpoints.
- Config files like package.json

JSON methods in JS

```javascript
JSON.parse(); // takes JSON string and convert into JS object

JSON.stringify(); // convert JS object into string
```

## 🔥 What is CRUD? <a name="5"></a>

REST and CRUD work together because CRUD can exist within a REST environment, and their functions often correspond to each other, but they are not the same. The best way to differentiate between them is to remember that REST is a standard (an API architecture), and CRUD is a function. Understanding this essential but straightforward difference is necessary for understanding both.
