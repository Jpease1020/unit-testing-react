## Unit Testing React Components

---

### What's a unit?
  - Intuitively, one can view a unit as the smallest testable part of an application.
  - While Units can be many things, most unit tests that will be challenging to write in react are going to be the functions within your react components or Plain Old Java classes and other exported functions
  - Hopefully your writing units/functions well

---

### Methods Should Generally Do One Thing
  - This is not always possible but it is preferable.
  - Even if a method needs to be destructed into smaller parts that each do one thing, hopefully the parent function has one main job to do that can be described by it's name.
  - It's easier to read, understand, change and unit test methods that have one job to do.

---

### React Class Functions
  - Can create or modify and return some data (data can be a string, array, html section, object, null etc)
  - Can return html with or without dynamic data depending on data passed in or taken from another place such as the main or local state

+++  

  - Can modify the component state
  - Can kick off a redux action
  - Send an http request out to an api
  - Can kick off another function
  ### All of these can be unit tested

---

## Why Unit Test?

+++

# So you can verify that your code works as expected!

+++

  - Unit Tests are fast!  Providing a very quick feedback loop allowing faster problem solving and development.
  - No need for the Dom. It only needs to interact with the code.  It works the same in your local machine as in Docker, Jenkins, Cloud Foundry etc.

---

#### These functions can all be tested by
  1. Passing what ever data it needs to do it's job
  2. Calling the function
  3. Asserting it did it's job and produced the expected result.

---

  - You can test that the function returned the expected data
  - You can test that it kicked of another function or action (haven't figured out how to test that it kicked off an api call but it's probably doable)
  - You can test the state of the class before and after a function modifies it
  - You can test/assert on the html it returns (kind of long and cluncky so maybe there's a faster way using other renders and find()). Example - ComplianceBuddy-frontend Header.test:54

---

### My new favorite testing tool is the .instance() method called on a shallow rendered react component or calling the class prototype function - Why?

  - The component is just a class.
  - Both .instance() and Class.prototype.myFunction() let you access the functions of that class directly and test them as individual units of code and assert on exactly what they are expected to do or return.

---

## .instance()
  - `const headerComponent = shallow(<Header />, document.createElement('div'))`
  - `let instance = headerComponent.instance()` (show example)
  - Using the .instance() works on an instance of that component/class and therefore will have access to the rest of the class including all functions including the render as well as state and any imported classes and functions (verify).

---

## Class.prototype.myFunction()
- Using the prototype can be very helpful when mocking a function.  Sometimes you don't want the function your testing to actually kick off an action of api call so you need to mock it.  

+++

- Then you can access the function via Class.prototype and overwrite it with a mock. You need to save off the original function, then overwrite it, test it then change it back before using it again in the test suite depending on it's scope. Example - ComplianceBuddy-frontend Header.test:54
---
