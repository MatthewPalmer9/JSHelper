# How to Use `fetch()`

Most API's will only allow you to fetch on their website.
This means you couldn't run this code in the console on 
google.com because:
		1. Google demands the fetch request be from https
		2. open-notify's API blocks the request outside of their website

```javascript
fetch('http://api.open-notify.org/astros.json')
.then(function(response) {
  return response.json();
})
.then(function(json) {
  console.log(json)
});
```

Here is another example. A method (function) that grabs Game of Thrones books from an API ...

```javascript
function fetchBooks() {
  return fetch('https://anapioficeandfire.com/api/books')
    // returns the fetch() request
  .then(resp => resp.json())
    //  converts the request response to JSON
  .then(json => renderBooks(json));
    // passes the returned JSON data as an argument renderBooks(json)
}

// For concepts below, please check the DOM Manipulation File in this Repo (To-Be Added)
function renderBooks(json) {
  const main = document.querySelector('main')
  json.forEach(book => {
    const h2 = document.createElement('h2')
    h2.innerHTML = `<h2>${book.name}</h2>`
    main.appendChild(h2)
  })
}

document.addEventListener('DOMContentLoaded', function() {
  fetchBooks()
  // This makes such fetchBooks() is only run after the DOM has fully loaded
})
```