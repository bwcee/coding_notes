# React

## Storing Values in React - Variables vs useState vs useRef

### **Summary**

- 3 reasons why using variables is not advisable
  1. display will not be synced w changes in variable value
  2. variables will be reset whenever re-render occurs
  3. placing variables outside of function component also not desirable. if multiple components
     used, all instances of the component will share variable value whereas prob want each instance to haf their own unique values
- useState
  - use it when need to store a value and need tt value to be synced w display
  - however cos e way value is synced w display is by re-running the function component and any child components, it is a waste to use this to store value tt does not need to be synced w display
  - plus behavior of re-running entire function component places constraints on structure/org of code
- useRef
  - simply provides a way to store value just like a variable, just tt e value does not get reset when set state re-runs function component to re-render display
  - this seems best option if just need to store and persist a value

#### References:

- [When it’s not good to use state for storing data in React](https://blog.devgenius.io/when-its-not-good-to-use-state-for-storing-data-in-react-adcf261e8467)
- [Storing values with the useRef hook](https://www.emgoto.com/storing-values-with-useref/)

### **Variables**

1. variable value change does not trigger view re-render => what is shown is not updated variable value
   - in HTML script files prev, DOM elements called and manipulated directly when variable changes
   - when `someVariable` changes, `#someId` display changes
     - `document.getElementById("someId").innerHTML=someVariable`
   - in react, display only changes through a render function e.g. `render(<App />, rootElement)`
   - when `someVariable` changes, `<p>` display does not change
   - function containing react element and render function haf to re-run in order for `<p>` to show latest value of `someVariable`
     - `const myEl = (<p>This para contains a variable called someVariable:{someVariable}</p>)`
2. variables not able to hold on to changed values between renders
   - to re-render, entire function component is run again => variable values will be reset
3. storing variable outside of function component => will be able to hang on to value even if function component re-run. however, if there are multiple instances of the component used, all instances of the component will share the same variable, which is prob not desirable.

#### References:

- [difference between using useref for a variable vs declaring outside the component (hooks) to maintain value after rerender](https://www.reddit.com/r/react/comments/ox0quh/difference_between_using_useref_for_a_variable_vs/)
- [React Hooks - using useState vs just variables](https://stackoverflow.com/questions/58252454/react-hooks-using-usestate-vs-just-variables)

### **useState**

#### What is it

- stores a value in a state _and_ re-renders display when set state function used to update state
- think the way set state re-renders display is to re-run the function component, all its child components and finally the render function

#### How to use it

- always try to update state via set state function. not doing so cld cause state & display to be out of sync
- notwithstanding the above, shld u manipulate value of a state b4 setting it using set state, need to use a spread operator
  ```
  state = state.push("some new element")
  setState(state) // think will not work cos setSet will simply update state w old state value
  setState([...state]) // will work cos spread operator returns a new array, which in this case is state.push("some new element")
  ```

#### Potential Pitfalls

1. infinite loop
   - becos set state function will re-run function component, simply placing a set state function within a function component will cause an infinite loop
     - set state function within function component triggers -> re-run entire function component so view re-rendered -> set state function within function component triggers -> re-run entire function component so view re-rendered -> set state function within function component triggers -> re-run entire function component so view re-rendered...
   - to prevent infinite loops, set state must be included in such a way tt it is only triggered under certain circumstances e.g. within an onclick function
2. set state function **replaces** old value in state with watever new value is passed to it
   - this explains why if state contains an array, cannot use `setState(state.push("new element")` cos `push()` returns length of modified array rather than the array itself
   - instead use `setState(state.concat("new element"))` cos it returns a new modified array
   - can also make use of spread operator to clone old array and add new element `setState([...state, "new element"])`
   - also means haf to be careful in updating objects held in state. if only updating part of the object, still need to use spread operator to make a copy of the old object and update the relevant key:value pairs

#### References:

- [What Every React Developer Should Know About State](https://www.freecodecamp.org/news/what-every-react-developer-should-know-about-state/)
- [A Thoughtful Way To Use React’s useRef() Hook](https://www.smashingmagazine.com/2020/11/react-useref-hook/)
- [useState in React: A complete guide](https://blog.logrocket.com/a-guide-to-usestate-in-react-ecb9952e406c/)
- [How to Add to an Array in React State using Hooks](https://javascript.plainenglish.io/how-to-add-to-an-array-in-react-state-3d08ddb2e1dc)
- [Updating and Merging State Object using useState Hook in React Functional Component](https://medium.com/@omnia.yehia/updating-object-state-using-usestate-hook-in-react-functional-component-6cd3101962bf)

### **useRef**

#### What is it

- stores and persists a value despite function component re-runs to re-render display
- updating the value _does not_ trigger component re-run

#### How to use it

- accepts one argument as initial value and returns a reference

```
function MyComponent() {
  const reference = useRef(initialValue);
  const someHandler = () => {
    // Access reference value:
    const value = reference.current;
    // Update reference value:
    reference.current = newValue;
  };
  // ...
}
```

#### References:

- [The Complete Guide to useRef() and Refs in React](https://dmitripavlutin.com/react-useref-guide/)

## Controlled vs Uncontrolled Components for Forms

1. [Controlled vs. uncontrolled components in React](https://blog.logrocket.com/controlled-vs-uncontrolled-components-in-react/)

- controlled component -> using state within component to handle form data
- uncontrolled component -> DOM handles form data by itself in the component

### **useContext + useReducer**

#### References:

- [A Guide to React Context and useContext() Hook](https://dmitripavlutin.com/react-context-and-usecontext/)
- [An Easy Guide to React useReducer() Hook](https://dmitripavlutin.com/react-usereducer/)
- [The best Couple: useContext + useReducer !](https://dev.to/jackent2b/the-best-couple-usecontext-usereducer-4e65)
-

## Misc References

1. [Understanding Rendering in React](https://dev.to/teo_garcia/understanding-rendering-in-react-i5i)
2. [How State Works in React – Explained with Code Examples](https://www.freecodecamp.org/news/what-is-state-in-react-explained-with-examples/)
