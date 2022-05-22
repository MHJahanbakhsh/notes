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
it takes away all the sweat of creating action creators and reducers seperate and connecting them together.
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
