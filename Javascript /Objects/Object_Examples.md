# Helpful Examples of Javascript Objects

```javascript

const driver = {};

function updateDriverWithKeyAndValue(driver, key, value){
    return Object.assign({}, driver, {[key]: value});
    // Same as --> 
    // return {...driver, [key]: value}

        // -: Description :-
    // returns a driver with the original key value pairs and the new key value pair
    // it does not modify the original driver, but rather returns a clone with the new data
}

function destructivelyUpdateDriverWithKeyAndValue(driver, key, value){
    driver[key] = value;
    return driver;

        // -: Description :- 
    // updates `driver` with the given `key` and `value` (it is destructive) and 
    // returns the entire updated driver
}

function deleteFromDriverByKey(driver, key){
    let clone = Object.assign({}, driver);
    // Same as -->
    // let clone = {...driver};

    delete clone[key];
    return clone;

        // -: Description :-
    // deletes `key` from a clone of driver and returns the new driver (it is non-destructive)
    // does not modify the original driver (it is non-destructive)
}

function destructivelyDeleteFromDriverByKey(driver, key){
    delete driver[key];
    return driver;
}
```