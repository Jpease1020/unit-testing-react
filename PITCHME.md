## Unit Testing React Components

---

### Tools Used
  - React
  - Jest
  - Enzyme

---

This needs to be a discussion rather than a presentation. Ask questions, give feedback, challenge what I present.

---

### What's a unit?
  - Intuitively, one can view a unit as the smallest testable part of an application.
  - While Units can be many things, the units we are focusing on today are the functions within your react components.
  - Well written functions and clean code are generally much easier to test. (think SRP...)

---

### Methods Should Generally Do One Thing
  - This is not always possible but it is preferable.
  - Having a parent function with a descriptive name that runs all of your smaller SRP functions is generally preferable in both your src and test code.
  
+++

  - Even if a method needs to be refactored into smaller parts that each do one thing, hopefully the parent function has one main job to do that can be described by it's name.
  - It's easier to read, understand, change and unit test methods that have one job to do.

---

### React Class Functions
  - Can create or modify and return some data (data can be a string, array, html section, object, null etc)
  - Can return html with or without dynamic data depending on the data passed in or taken from another place such as the main or local state

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
  - If you find your units are difficult to test because too many things are happening, write better code aka. go refactor your function into smaller more single-responsibility units! SRP FTW!!!!!!!

---

#### Component functions can all be tested by
  1. Passing the data it needs to do it's job including a dom event which creates and sends over an object
  2. Calling the function
  3. Asserting it did it's job and produced the expected result.

---

  - You can test that the function returned the expected result
  - You can test that it kicked off another function or action (haven't figured out how to test that it kicked off an api call but it's probably doable)
  - You can test the state of the component before and after a function modifies it
  - You can test/assert on the html it returns by testing the render() function but it's probably faster to just use the find() method on shallow

---

### Shallow + .instance()
- My new favorite testing tool is the .instance() method called on a shallow rendered react component or calling the class prototype function
- Why?

+++

  - The component is just a class.
  - Both .instance() and Component.prototype.yourFunction() let you access the functions of that class directly and test them as individual units of code and assert on exactly what they are expected to do or return.

---

## Shallow
  - http://airbnb.io/enzyme/docs/api/shallow.html
  - http://airbnb.io/enzyme/docs/api/ShallowWrapper/shallow.html
  - https://facebook.github.io/react/docs/shallow-renderer.html
  - You can think of the shallowRenderer as a "place" to render the component you're testing, and from which you can extract the component's output.
  - shallowRenderer.render() is similar to ReactDOM.render() but it doesn't require DOM and only renders a single level deep. This means you can test parent components in isolation, rather than having to render their child components.

---

## .instance()
  - - http://airbnb.io/enzyme/docs/api/ShallowWrapper/instance.html
  - A function on the shallow render method from Enzyme
  - Using the .instance() works on an instance of that component/class and therefore will have access to the rest of the class including all functions(render, state, imported classes, functions)

---

### Class.prototype.myFunction()
- Using the prototype can be very helpful when mocking a function.  Sometimes you don't want the function you're testing to actually kick off an action or api call so you need to mock it.  

+++

- Then you can access the function via Class.prototype.myFunction and overwrite it with a jest.fn() mock. You need to save off the original function, then overwrite it, test it then change it back before using it again in the test suite depending on it's scope. Example - ComplianceBuddy-frontend Header.test:54

---

# Test Examples

Compliance Buddy ProductsPage_test
Test line: 125
  - test the component renders another component

Test line: 130
  - tests the child component receives the correct props

---

Test line: 139
  - tests the component will render something based on the state passed to it through props

Test line: 183
  - tests mocking an api call that a function dispatches

---

Test line: 276
  - tests a higher order function
	  (one thats returning another function)

Test line: 282
  - a function that returns a function that takes an event

---

Test line: 288
  - tests a function takes an event
  - calls another function
  - which happens to be an action
  - which the function gets from the props.

Test line: 300
  - tests a function thats returning a promise

---

ComplianceCategory Test
Test line: 143
  - tests a function that returns different data object depending on data passed in

---

Ripcord/ recordTest
Test line: 60
  - tests a function that changes the state of the object

Ripcord/ Header Test
  - mocks local storage
