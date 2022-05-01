## standard module pattern & revealing module pattern:
so this is exclusively for javascript.before es6 and introduction of modules system ,this was the way to seperate code and make some properties and methods private.but now es6 has a better implementation for this;however let see whats the fuss about it:
```javascript
//the convetion is to do this pattern by IIFE but you can also use function declaration and expression and invoke them later


//Standard module pattern:
/* the basic structure is:
(function UICtrl(){
  <Declare private method and properties>
  
  <Decalre other methods and properties whom uses private ones>
  
  return{
    <return the public ones in a object.(however if you wanna return only one thing ,object is not neccessary)>
  }
})
*/

(function UICtrl(){
  let _text = "Hello World"
  
  const _changeUI = function(){
    const element = document.querySelector('h1')
    element.textContent = text;
  }
  
  return {
    callChangeUi = function(){
      _changeUI();
    }
  }
  
})


//Revealing module pattern:
  (function itemCtrl(){
    let _data = []
    
    function add(item){
      _data.push(item)
      console.log('item added')
    }
    
    function get(id){
      _data.find(item=> return item.id === id)
    }
    
    return {add, get}
  })

```
__Note1:__ undescrore `_` is just a convention for private variables not neccessary.
__Note2:__ diffrence between revealing and standard is in revealing you reveal your methods! nut in standard try to encapsulate the original logic
