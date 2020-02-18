# Unit 6 Lesson 1 Practice: Promises

## Directions
Fork and clone this lab. Respond to questions in clear, concise sentences directly within this markdown file.

**1. What will the following code snippet log? Why?**
  ```javascript
  console.log('Line 1')
  setTimeout(() => console.log('Line 2'), 1000)
  console.log('Line 3')
  ```
Logs line 1 line 3 and then line 2, the set timeout runs in the background for one second before it returns.


**2. What does the following code snippet log? Why?**
  ```javascript
  function createPromise(seconds) {
    return new Promise((resolve) => {
      setTimeout(function() {
        resolve(`After ${seconds} second(s), this promise is resolved.`)
      }, seconds * 1000)
    })
  }

  console.log(createPromise(1000))
  ```
This will log pending since the promise is not tied to anything that can be accessed. If this was captured in a variable, accessing that variable would update the status after the timeout was finished.

**3. How do we use our `createPromise` function to log `"After 1 second(s), this promise is resolved."`**

To get the function to log we would have to log the string when the promise is resolved.

**4. What does the following code snippet return? What does it log?**
  ```javascript
  const ourPromise = new Promise((resolve) => {
    resolve(12);
  })

  ourPromise.then(value => value * 2);
  ```
The resolved value is taken with a then statement and the value is then adjusted as the callback function is calling for.


**5. What does the following code snippet return? What does it log?** <br> _**Note:** Instead of using the `Promise` constructor to create a Promise that immediately resolves to 12, we can just use the [`Promise.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) method._
  ```javascript
  const ourPromise = Promise.resolve(12);
  ourPromise.then(value => value * 2).then(value => value + 10);
  ```

The final promise resolve will be 34 since the value is first doubled and then 10 is added to that number.

**6. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => console.log(value + 10))
  ```
This logs 34 and then a pending promise it is different because the number is resolved with a number and then logged with the final value, so promise syntax does not return it as a value to resolve the promise.

**7. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    });
  ```
The return value actually returns a value to the promise so both the console.log and the promise object return the proper value.

**8. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.reject(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    }).catch(reason => {
      const message = `${reason} is a bad number.`;
      console.error(message);
      return reason;
    });
  ```
  since the promise is rejected immedietely the number is never transformed with the then statements finally the error message is logged following the catch statement.