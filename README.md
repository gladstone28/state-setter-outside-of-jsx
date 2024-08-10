[Link to codecademy lesson](https://www.codecademy.com/courses/react-101/lessons/the-state-hook/exercises/use-state-setter-outside-of-jsx)

### The State Hook

**Use State Setter Outside of JSX**

Let’s see an example of managing the changing value of a string as a user types into a text input field:
```
import React, { useState } from 'react';

export default function EmailTextInput() {
  const [email, setEmail] = useState('');
  const handleChange = (event) => {
    const updatedEmail = event.target.value;
    setEmail(updatedEmail);
  }

  return (
    <input value={email} onChange={handleChange} />
  );
}
```
Here’s a breakdown of how the above code works:

- We use array destructuring to create our local state variable email and our local setter function setEmail().
- The local variable email is assigned the current state value at index 0 from the array returned by useState().
- The local variable setEmail() is assigned a reference to the state setter function at index 1 from the array returned by useState().
- It’s a convention to name the setter variable using the current state variable (in this example, email) with “set” prepended.

The JSX input tag has an event listener called onChange. This event listener calls an event handler each time the user types something in this element. In the example above, our event handler is defined inside of the definition for our function component, but outside of our JSX. Earlier in this lesson, we wrote our event handlers right in our JSX. Those inline event handlers work perfectly fine, but when we want to do something more interesting than just calling the state setter with a static value, it’s a good practice to separate that logic from our JSX. This separation of concerns makes our code easier to read, test, and modify.

It’s common in React code to simplify this:
```
const handleChange = (event) => {
  const newEmail = event.target.value;
  setEmail(newEmail);
}
```
to this:
```
const handleChange = (event) => setEmail(event.target.value);
```
or, using object destructuring, this:
```
const handleChange = ({target}) => setEmail(target.value);
```

All three code snippets above behave the same way, so there really isn’t a right and wrong between these different code snippets. We’ll use the last, most concise version moving forward.

