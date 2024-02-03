# REST

- [What is API?](#1)
- [What is REST?](#2)
- [Ways to fetch data](#3)
  - [fetch() method](#31)
  - [Async-Await ](#32)
  - [Axios library](#33)
  - [jQuery AJAX](#34)
  - [Custom Hook](#35)
  - [React Query library](#36)

## 🔥 What is API? <a name="1"></a>

In simple terms, an `Application Programming Interface` is a set of protocols and tools for building software applications. APIs allow different software applications to communicate with each other and exchange data.

## 🔥 What is REST? <a name="2"></a>

`REpresentational State Transfer`

❗

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

Fetch is a method to call an API in JavaScript. The request can be of any APIs that return the data of the format JSON or XML. It returns a promise, which contains a single value, either response data or an error.

```javascript
function App() {
  useEffect9(() => {
    fetch("https://site.com/")
      .then((response) => response.json())
      .then((json) => console.log(json));
  }, []);

  return <div>Data</div>;
}
```

```javascript

fetch('Api_address')
.then(response => {
  if (response.ok){
    return response.json(); // Parse the response data as JSON
  } else {
    trhrow new Error("API request failed")
  }
  . then(data => {
    // Process the response data here
    console.log(data)
  })
  .catch(error => {
   // Handle error here
   console.error(error)
  })
})
```

### 🔥 Async-Await <a name="32"></a>

It is the preferred way of fetching the data from an API as it enables to remove .then() callbacks and return asynchronously resolved data. In the async block, we ccan use Await function to wait for promise.

```javascript
function App() {
  useEffect(() => {
    (async () => {
      try {
        const result = await axios.get("https://site.com/");
        console.log(result.data);
      } catch (error) {
        console.error(error);
      }
    })();
  });
  return <div>Data</div>;
}
```

### 🔥 Axios library <a name="33"></a>

Axios is an open-source library for making HTTP requests to servers. It is a promise-based approach. It supports all modern browsers and is used in real-time applications. It is easy to install using the npm package manager. With Axios, we can easily send asynchronous HTTP requests to REST APIs and perform create, read, update and delete operations.

```javascript
function App() {
  useEffect(() => {
    axios
      .get("https://site.com/")
      .then((response) => console.log(response.data));
  }, []);
  return <div>Data</div>;
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
