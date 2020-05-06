# How to Set Up Rails as an API

It's important to understand some hidden factors that go with setting a backend Rails API. The main file structure you want to have looks like this:

```javascript
// javascript-project/
//   backend/
//     app/
//     (...other rails files and folders)
//   frontend/
//     index.html
//     style.css
//     index.js
//   README.md
```

From here, you'll want to `cd` into your `backend/` and run `rails new YourAppName-api --api`.

*** IMPORTANT NOTE: Your backend Rails API automatically comes with a hidden `.git`. This means you get a default repo. You must `cd` into your backend directory. To check if a .git file exists, type `ls -la` into the console. To get rid of the `.git` file, type `rm -rf .git`. After following these steps, you will be able to push your backend to your github. This is because ONLY your main directory should have a `.git` repository. If your main directory & your backend API both have a `.git`, you're gonna have a bad time, m'kay? ***

Finally, set up (uncomment) your CORS gem in Gemfile, uncomment the middleware class in config & then `bundle install`. 

## Congration, U Dun It
Carry on, my wayward son. You can now write your backend.
