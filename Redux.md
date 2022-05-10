reducers should be pure functions,which means their return values should not be dependent on anuthing beside their given aruments:
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
