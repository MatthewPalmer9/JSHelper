# Sending Data with Fetch

`fetch()` is able to send data as a `POST` request much like how `<form>` works to send a `POST` request using `method="POST"`. Only in this case, we are grabbing data from a JavaScript `Object`.

The general look of this function is as follows:
```javascript
fetch(destionationURL, configurationObject);
```

## The Method

The `configurationObject` contains three core components needed to send `POST` requests. To start off with, we need to set the `method`:

```javascript
configurationObject = {
    method: "POST"
};
```

## The Headers

Next, we need to add headers, which are sent ahead of the actual data/information (or "Payload") of the `POST` (Think: Any data that would normally be inserted into an `<input>` field, for example.) One very common header is `"Content-Type"` which is used to indicate what format the data being sent is in. With JavaScript's `fetch()`, JSON is the most common format used. And... We want out `POST` request to know this. So, we include this below our `method`:

```javascript
configurationObject = {
    method: "POST",
    headers: {
        "Content-Type": "application/json" //<-- The FORMAT
    }
}
```

Keep in mind, the individual headers are stored as key/value pairs. 
`"Content-Type"` will tell the destination server what type of data we are sending, then... you want to make sure the server knows what data format we are willing to `"Accept"` in return:

```javascript
configurationObject = {
    method: "POST",
    headers: {
        "Content-Type": "application/json",
        "Accept": "application/json"
    }
}
```

Addtionally, it is important to understand that some server may reject requests without the specific headers the server is configured to expect.

## Adding Data

When data is being sent in `fetch()`, it must be stored in the `body` of your `configurationObject`:

```javascript
configurationObject = {
    method: "POST",
    headers: {
        "Content-Type": "application/json",
        "Accept": "application/json"
    },
    body: // All data will go here.
}
```

## Using `JSON.stringify()` to Convert Objects to Strings

All data being sent in the `body` is only being sent as text. Therefore, our data must always be a string. So, in order to convert JSON data in a string, we use `JSON.stringify()`. When an `Object` is converted to JSON, it looks like this:

```javascript
"{"dogName":"Byron","dogBreed":"Poodle"}"
```

This allows us to "preserve" our key/value pairs of our object within a string. When it is sent to a server, the server will be able to convert this string back into key/value pairs in whatever language the server is written in. This process is made simple by using `JSON.stringify()` as shown below:

```javascript
configurationObject = {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
        "Accept": "application/json"
    },
    body: JSON.stringify({
        dogName: "Byron",
        dogBreed: "Poodle"
    })
};
```

## Sending the POST Request

Now that our configuration object is broken down, we can now incorporate it into `fetch()`:

```javascript
fetch("http://localhost:3000/dogs", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
        "Accept": "application/json"
    },
    body: JSON.stringify({
        dogName: "Byron",
        dogBreed: "Poodle"
    })
});
```

With a JSON server running, you can open up a `form` and use this code to successfully send a `POST` request and persist data to `db.json`. You can even set a method that you can then INSERT inside of `JSON.stringify()`. Let's Look at the large code snippet below to get a better idea:

```javascript
function submitData(name, email){
    let formData = {
        name: name,
        email: email
    }

    let configObj = {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Accept": "application/json"
        },
        body: JSON.stringify(formData)
    };

    return fetch("http://localhost:3000/users", configObj)
        .then(function(response) {
            return response.json();
        })
        .then(function(object) {
            console.log(object);
            document.body.innerHTML = object.id
        })
        // ^^ EVERYTHING ABOVE THIS LINE :
        // `response` is whatever the server sends back to us, and this is built 
        // into JSON. That `response` is then converted into JSON (remember how the
        // conversion preserves key/value pairs? This is where that 
        // conversion happens and gives us an OBJECT of that data.).
        // Also... `object.id` will vary depending on your database...

        .catch(function(error) {
            alert("Bad things! Ragnarok!");
            console.log(error.message);
            document.body.innerHTML = error.message
        });

        // As for .catch(), `error` will also be information provided to use by
        // JSON. JavaScript will not fail silently here. If a fetch() request
        // does not work, it will raise an error to use and log that error to 
        // both our console and innerHTML of our body.
}
```


