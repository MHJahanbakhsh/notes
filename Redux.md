reducers should be pure functions,which means their return values should not be dependent on anything beside their given aruments:
```javascript
function reducer(state,action){
  //BAD!
  return document.querySelector('input')..

  //BAD!
  return axios.get('some api')

//good
return state + action
}
```

# redux-toolikt is a Godsent!
it takes away all the sweat of creating action creators and reducers seperately and connecting them together.
```javascript

import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions  //vahlaa here are the actions

export default counterSlice.reducer //here we go.you have the reducers
```
just to sink in of how awsome it is i should say each key in `redecers` are going to define as an action. Baaam!

[link to a sandbox for redux toolit intro](https://codesandbox.io/s/redux-toolkit-intro-7dp3kn)


# mapDispatchToProps:
essentially we have two forms of mapDispatchToProps:
* function
* object    
in a nutshell we use the function form when we want to have full controll over when dispatches the actions(so that we won't be needing a middlware in this case!! BAAAM).     
object form is probably more intuitive but we dont access to `dispatch` directly and when that action creator is called dispatch fires off automatically.

just to be more clear when i say object form i mean an object of action creator functions.see below     

__Object form:__
```javascript
const mapDispatchToProps = {
  decrement: () => ({ type: "DECREMENT" }),
  increment: () => ({ type: "INCREMENT" })
};
//as you can see there is no dispatch
```
__function form:__
```javascript
const mapDispatchToProps = dispatch => {
  return {
    decrement: () => dispatch({ type: "DECREMENT" }),
    increment: () => dispatch({ type: "INCREMENT" })
  };
};
```
now; with redux thunk it lets each of those acion creators in object form of `mapDispatchToProps` return a function and that function recieves two arguments: `dispatch`&`getState`   
imagine the example above for __object form:__    
```javascript
const mapDispatchToProps = {
  decrement: () =>{
  return function (dispatch,getState){
    //do some shit asynchronus
    dispatch({ type: "DECREMENT" })
  }},
  increment: () => ({ type: "INCREMENT" }) //we can still have normal action creators with redux thunk
};

```
#### redux thunk uses the object-form of mapDispatchToProps and makes it act like a function form

# redux-saga
unlike redux thunk the your action will cross this middleware whether its a function or not.    
the way it works is it can catch every action with functions such as `takeEvery`.and in that function it passes down a callback function which is essentially the actionCreator that is being send to the reducer.  
essentially we have two types of saga :   
* watcher
* worker    
the 'watcher' is responsible for catching the action and delegating it.and 'worker' does the actual asyn job
`put` is like dispatch    
`call` runs a function , if it returns a promise,pauses the saga untill the promise is resolved
`takeEvery` makes queue on every action that is called and forward them respectively    
`takeLatest` acts like debouncing and if the previous action is not dispatched yet ,it will discard it and create a new one to go
[link to the sandbox](https://codesandbox.io/s/redux-saga-nxwzwj?file=/src/sagas/saga.js)     

---
as the stephan showed,with redux thunk we can still have some normal action creators alongside with async functions. but it seems with redux-saga every action goes through saga and you have to write all of your action in 'watcher-worker' form

### what is 'pristine' and 'submitting' in redux-form?      
__pristine__ means that no fields in the form have been modified yet    
__submitting__, as the name suggests, means that the form is in process of submitting.
