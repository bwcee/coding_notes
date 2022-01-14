# React

## useState

1. [How to Add to an Array in React State using Hooks](https://javascript.plainenglish.io/how-to-add-to-an-array-in-react-state-3d08ddb2e1dc)
   - react state is immutable... => cannot be changed...
   - the only way to update state is to replace it w a new string/array/object... the orig string/array/object cannot be modified...
   - cannot use push() cos it returns length of the array
   - must use concat cos it returns a new array tt is the modified old array
   - can also make use of spread operator to clone e old arr & add new element to array
   - recommended to use callback func in set state function rather than passing in new state directly. since it is a callback func, state is accessed when the re-render actually occurs, not at some other time
2. [Updating and Merging State Object using useState Hook in React Functional Component](https://medium.com/@omnia.yehia/updating-object-state-using-usestate-hook-in-react-functional-component-6cd3101962bf)
   - have to careful in updating if react state is an object
   - if only updating part of the object, still need to use spread operator to make a copy of the old object and update the relevant key:value pairs
3. [useState in React: A complete guide](https://blog.logrocket.com/a-guide-to-usestate-in-react-ecb9952e406c/)
   - comprehensive guide to useState

## Controlled vs Uncontrolled Components for Forms

1. [Controlled vs. uncontrolled components in React](https://blog.logrocket.com/controlled-vs-uncontrolled-components-in-react/)
   - controlled component -> using state within component to handle form data
   - uncontrolled component -> DOM handles form data by itself in the component
