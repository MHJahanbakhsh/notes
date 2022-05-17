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
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```
just to sink in of how awsome it is i should say each key in `redecers` are going to define as an action. Baaam!
