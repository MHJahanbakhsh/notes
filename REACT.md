* one otherway to return multiple jsx elements from one component,rather than having a wrapper element is to put them in array! we already know array of jsx is a legit thing for react comp to return(we use map()) the only downside to this approach is that you have to set unique keys for each element 
* other way is to create a wrapper component and in that component simply just return props.children
---
### React Portals:
with correct styling ,technichally a modal still might work in react ,no matter how deeply nested it is. but semsntically is not right to put an overlay component deep in somewhere it does not belong.

Portals only affect the HTML DOM structure and not impact the React components tree.which means modal component can still be deeply nested inside but when rendering it will be on top level next to root div

![Screenshot (70)](https://user-images.githubusercontent.com/50621975/149794847-9951f7c4-5671-4f14-b702-903a2dcfca2d.png)

sidebar's z-index gets compared to positioned's z-index.

what happens with portals is : based on where  your states are or personal prefrence you define your modal component.let say very deep; we don't care as long as that modal component returns its jsxs as portal.and if you do that,every time it renders rather than appearing as a direct child of root,it will be rendered in related div.

---
## useRef:
used to store variables when they really dont need to be stored in state.
such as input values.(updating input value and run function to setState,just to finally read that value is not necessary.)
although we have to bend the rule and break out from "REACT" to browser DOM manipulation.

also unlike states Ref would not force component to rerender in every change. so keep that in mind for storing a variable that we dont neccessarily want to Rerenders our component

---
## useMemo:
it comes from memoization which is essentialy caching variables.
```jsx
import React from "react"
import { Fragment, useState , useMemo} from "react"
import { useEffect } from "react"


export default function App(){
  const [number , setNumber] = useState(0)
  const [dark , setDark] = useState(false)
  const doubleNumber = useMemo(()=>{return slowFunction(number)},[number])
/*
  const themeStyle = {
    backgroundColor : dark? 'black':'white',
    color : dark? 'white': 'black'
  }
  */
  const themeStyle = useMemo(()=>{
    return  {
      backgroundColor : dark? 'black':'white',
      color : dark? 'white': 'black'
    }
  },[dark])
  
  useEffect(()=>{
    console.log('runing useEffect cuase theme Styles changed');
  },[themeStyle ])
  
  return (<Fragment>
    <input type="number" value={number} onChange={(e)=>setNumber(parseInt(e.target.value))} />
    <button onClick={()=>setDark(prevValue=>!prevValue)}>change theme</button>
    <div style={themeStyle}>{doubleNumber}</div>
  </Fragment>)

  function slowFunction(num){
    console.log('running slow function')
    for(let i=0 ; i<=1000000000;i++){}
    
      return num*2
    
  }
}


```
in the example above, `slowFunction` we used 2 momoization:
* as u know updating state cause whole component to reRender,so even when we just click on theme changer button, `doubleNumber` gets reinitialized and slowFunction runs completely unneccarily.so we wrap the value in a useMemo.just like useEffect it has a callback function and a dependancy array.the function only runs when the dependancy array changes.
* we also used useMemo for an object: what happens is below that we have a useEffect that runs everytime "themeStyle" changes; but when since themeStyle is an object and a  refrence type value,in rerenders,its value in callstack changes and cuase useEffect to think it actually changed.so we wrap whole object in a useMemo and since the only variable that object is depends on, is `dark`, we make an arrangement so that only when `dark` varaible change; themStyle change; and hence useEffect runs

### useCallback:   
useMemo: Returns and stores the calculated value of a function in a variable   
useCallBack: Returns and stores the actual function itself in a variable.although their syntax is the same

Once React knows which virtual DOM objects have changed, then React updates those objects, and only those objects, on the real DOM

vanillajs approach is imperative but react with use of jsx is declarative:
document.createElement('div').append(document.getElementById('root') vs jsx approach     

---
whenever you combine components you're using composition

when to use props.children? custom made components unlike

why  in react we can't use this:
```jsx
let title = 'somthing';
function onClickHandler(){
    title = 'somthing else'    
}

function MyComponent(){
    return(
    <div>{title}</div>
    <button onClick={onClickHandler}>click me</button>
    )
}
```
because as you already know jsx are not real dom and they will run once at the start of the mounting component..so when we change the 'title' variable to somthig else ,the change would not be reflected in component becuase is not rerendering with new shit .to put into context:react doesnt care about changing variables inside component if they are not part of state system(either useState or this.setState)

---
Note:all hooks only are accessible inside a react component(function)
-useState(value)  is a funtion that RETURNS two things: that 'value' and a function to reset that value

---
useRef: essentioanlly  ref has two usecase:
first:using as a state reservior which does not force component to render like useStateand 
second:selecting an element instead of using document.queryselector....
 comprehensive guide to useRef: [link](https://www.youtube.com/watch?v=t2ypzz6gJm0);
 
 ### use useRef to acess previous value in states:
 
 ```jsx
import React , {useEffect, useRef, useState} from 'react'

export default function App() {
const [name,setName] = useState('')
const prevName = useRef('')


useEffect(()=>{
  prevName.current = name //why name in here is set to prev value and not the current one? becuase at the time useEffect renders,
}, [name])                //  name is not the new name in state!

  return (
    <div className="App">
      <input value={name} onChange={e=>setName(e.target.value)}/>
      <h2>my name is {name} and it used to be {prevName.current}</h2>
    </div>
  );
}

 ```
 
---
Note:don't forget `React.creatElemet()` for interviews

---
React knows how to work with "array of jsx".thats why we can use map and list rendering;    

---
"div soup" is a term used for having to many unnecessary  divs just for wrapping your jsxes;

---
Intersting note: 
```
function WrapperComponenet(props){
    return props.children    
}
```
this will work even if childrens are not a single element and can stay alongside in this case;
this is what we call wrapper trick ; an alternative to fragment

---

### useEffect cleanup function: 
useEffect can return one thing and one thing only;which is a function. this function would invoke at next render(not initial render)

![Screenshot (168)](https://user-images.githubusercontent.com/50621975/155688587-bb3e0c54-c0a6-4d64-8d8f-bbb3cefcf730.png)
ofcourse the data fetching process results usually shows on screen ;but the process itself is sideEffecrt 

__an example of creating infinite loop if we dont use `useEffect`:__
```jsx
import React, { useState } from 'react';

import Login from './components/Login/Login';
import Home from './components/Home/Home';
import MainHeader from './components/MainHeader/MainHeader';

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
   
  if(localStorage.getItem('isSignedIn')==1){
    setIsLoggedIn(true)
  } //the problem is it creates infinite loop.that's why we need use Effect(to control this process).
  //changing state causes reRender and in every rerender states changes again and so on

  const loginHandler = (email, password) => {
    // We should of course check email and password
    // But it's just a dummy/ demo anyways
    localStorage.setItem('isSignedIn','1')
    setIsLoggedIn(true);
  };

  const logoutHandler = () => {
    setIsLoggedIn(false);
  };

  return (
    <React.Fragment>
      <MainHeader isAuthenticated={isLoggedIn} onLogout={logoutHandler} />
      <main>
        {!isLoggedIn && <Login onLogin={loginHandler} />}
        {isLoggedIn && <Home onLogout={logoutHandler} />}
      </main>
    </React.Fragment>
  );
}

export default App;

```

__another example where useEffect shines:__
in this case the problem is reusing same logic multiple times:
```jsx
import React, { useState } from 'react';

import Card from '../UI/Card/Card';
import classes from './Login.module.css';
import Button from '../UI/Button/Button';

const Login = (props) => {
  const [enteredEmail, setEnteredEmail] = useState('');
  const [emailIsValid, setEmailIsValid] = useState();
  const [enteredPassword, setEnteredPassword] = useState('');
  const [passwordIsValid, setPasswordIsValid] = useState();
  const [formIsValid, setFormIsValid] = useState(false);

  const emailChangeHandler = (event) => {
    setEnteredEmail(event.target.value);

    setFormIsValid(
      event.target.value.includes('@') && enteredPassword.trim().length > 6
    );
  };

  const passwordChangeHandler = (event) => {
    setEnteredPassword(event.target.value);

    setFormIsValid(
      event.target.value.trim().length > 6 && enteredEmail.includes('@')
    );
  };

  const validateEmailHandler = () => {
    setEmailIsValid(enteredEmail.includes('@'));
  };

  const validatePasswordHandler = () => {
    setPasswordIsValid(enteredPassword.trim().length > 6);
  };

  const submitHandler = (event) => {
    event.preventDefault();
    props.onLogin(enteredEmail, enteredPassword);
  };

  return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        <div
          className={`${classes.control} ${
            emailIsValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor="email">E-Mail</label>
          <input
            type="email"
            id="email"
            value={enteredEmail}
            onChange={emailChangeHandler}
            onBlur={validateEmailHandler}
          />
        </div>
        <div
          className={`${classes.control} ${
            passwordIsValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor="password">Password</label>
          <input
            type="password"
            id="password"
            value={enteredPassword}
            onChange={passwordChangeHandler}
            onBlur={validatePasswordHandler}
          />
        </div>
        <div className={classes.actions}>
          <Button type="submit" className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
        </div>
      </form>
    </Card>
  );
};

export default Login;

```
instead of using setFormValid function multiple times,we can set this function as a useEffect callback and set dependencies,which make callback function run when we want

---
### useReducer
one usecase of useReducer is : when updating one state is based on the on other state.in this case you might face a situation that u get the wrong snapshot of the state you want to use.

### Context :
we can still use oldway context in a functional comp(returning a function from consumer tag).it's not like we have to use `useContext`    
the only time that we can use default value is when we have no provider! (by default value i mean `React.createContext({name:value1,age:value2})`).so technichlly we don't have to use provider to access context in react.however 95% of times the value that we access in our consumer, is the one that we passed to the provider.      
__note:__ we always have to use consumer. 
overall there is 3 ways to use context(React.createContext() is already created):
* `theClass.contextType = contextObject` . only works in calss component.and also write this outside of the class scope.in this case the context values.are accessible via `this.context`
* `<contextObject.consumer> {(value)=>return...} </contextObject.consumer>
* useContext

---
briliant way to write all of your props:
```jsx
function Input(props){
return <input {...props}/>
}
```

---
### Forwarding Ref:
we can not pass ref as a prop with "ref" keyword

### server side rendering:
the diffrence is it loads an skeleton preload html from serer and then start the react script. it is exactly a sweet spot between ssg and client side rendering

## things that i missed in interview:
* give an example of how HOC works in react     
* how to implement componentwillunmount in functional componenet
* why usecallback and how functions are in need for usecallback
* There are three categories of lifecycle methods: mounting, updating, and unmounting

