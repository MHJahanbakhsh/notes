## python:
so basically stack is where address of the variables is stored and heap is the actual Reservior.
for premitive types such as string and numbers the stack address for one value is the same for example:
```python
  s = "Hello"
  ss = "Hello"
  
  print(id(s));
  print(id(ss));
  # id method gives the sack address and you will see their stack address are the same;
  
  print(s == ss)  #>> this will return true:
  
```
![Screenshot (54)](https://user-images.githubusercontent.com/50621975/148685860-9f68ccf6-1ceb-4b03-826a-d66b04f0aa6b.png);

## However
 ```python
  list_1 =[1,2,3,4]
  list_2 = [1,2,3,4]
  print(id(list_1))
  print(id(list_2))
  #this will return two diffrent addresses
  #but if you run the comparison function you will see unlike javascript it will return true! so we can culminate that '==' is not comparing stack adresses
  print(list_1 == list_2)  #>> true
 ```
 if we change s to 'hi' the stack address will competly change but if we mutate the list (ex:append another number) the stack address remains the same
 
 [video 1 link](https://www.youtube.com/watch?v=OdQSWuG78Sk)
 
 [video 2 link](https://www.youtube.com/watch?v=F6u5rhUQ6dU)
 
 ---
 ## javascript:
 we start by defining two use cases:
 ```javascript
  let age = 30;
  let oldAge = age;
  age = 31
  
  console.log(age) //>> 31
  console.log(oldAge) //>> 30
 ```
 we can say this makes sense cause we defined oldAge after the age and changes to age shouldn't effect oldAge
 
 now lets see similar case but this time for objects:
 ```javascript
 const me = {
 name:'james',
 age:28
 }
 const friend = me
 friend.age = 27;
 console.log(friend.age) //>>27;
 console.log(me.age) //>>27 !!whaaat
 ```

### ok back to our two cases: 
it's important to know that javascript engine has two component: 
* a call stack
* and a heap.
  * call stack is where functions are executed and premitive type values are stored(fancy term:premitive types are stored in the execution context which they are declared
  * and heap is where refrence type values are stored(becasue refrence type data such as objects,arrays,functions,.. tend to take much more space and heap has A LOT!).
 
another important note to remember is that when we assign some variable to somthing for example const age = 30 ; in fact age refers to an address in stack which that points to value 30

![Screenshot (56)](https://user-images.githubusercontent.com/50621975/148692311-0b47d2e3-fb5c-4b78-8be5-529ebc1f0463.png)
so for both refrence and premitive types when we create new values with '=' based on another value ,js just use one piece of memory for both of them(makes sense) but the main diffrence is for premitives when we say age = 31, js allocate new part of stack with new address and value.
however in the case of refrence types,it doesn't bother hmself and when we change friend.age, javascript won't make new room for friend and simply mutate the original object!

even when we have two diffrent values,with their own initialization for premitive types js will use same memory stack address:
```javascript
  const samAge = 32;
  const markAge = 32;
  //both samAge and markAge identifirs point to same memory
```

#### note:the whole immutable values with 'const' thing is only for premitive types not refrence types why?
#### cause what needs to stay constant is the value in the call stack so when we change a refrence type,what is changed is the value in heap not the value in callstack(which is address for heap) and 'const' or 'let' doesn't give a shit.
#### but premitive types their values are only stored in callstack and changing them will irritate 'const'

```javascript
  const jessica ={
  age:32,
  weight:60
  }
  
  jessica.age =30 // ok because does not change value in the call stack
  jessica = {}  //not ok cause it will create new allocation of memory in heap and in the call stack(heap's address)
```

**Question:** how to solve this issue in refrence types and how to properly copy instead of using '=' ?
__Answer:__ there are many ways such as ```object.assign({} , me}```, spread operator ```{...me}``` and ```JSON.parse(JSON.stringify(me))``` also lodash has some methodes for this
but things to conside is **shallow copy** and  **deep copy**:

```javascript
let person = {
    firstName: 'John',
    lastName: 'Doe',
    address: {
        street: 'North 1st street',
        city: 'San Jose',
        state: 'CA',
        country: 'USA'
    }
};


let copiedPerson = Object.assign({}, person);

copiedPerson.firstName = 'Jane'; // disconnected

copiedPerson.address.street = 'Amphitheatre Parkway'; // connected
copiedPerson.address.city = 'Mountain View'; // connected

/*firsName in Person object wont change because its in first level but street and city in address will change becase its nested and copiedPerson uses the same address object as Person uses in heap */ 
```
---

### memory leak:
is a situation when a garbage collector fails to remove a value that is no longer needs to be
---
we have 3 paradigm in programming and javascript and python can do all:
* oop
* functional
* procederal programming => kosekhari neveshtan

---
### General terms:
__thread:__ 
  in computing,thread is just a set of instructions that get executed in cpu.on other words are the code is in one place.
  __python__ and __javascript__ are single threaded but __java__ is multithread language
  
__concurency or concurency model__:
is how a programming language handles multiple tasks happening at the same time

__so since js is single thread it have to to somthing in order to get non-blocking performance otherwise for example: fetching a data from a server that takes a long time;will block other instructions.__
__javascript does this with EVENT LOOP:  event loop essentially executes long-running-tasks in "background" and puts them back in the main thread once they are finished__

---
## diffrence between compiler and intrepeter:
interpretaion is slower than compilation by defualt becuase executes line by line.
js used to be an interprator language but since slow speed is not acceptable anymore,modern js is JIT which is very fast and similar to compilition.
diffrence between compile and JIT is machine code in the middle is not portable and will execute immediatly(i ain't got it bu thats what is written)
![Screenshot (57)](https://user-images.githubusercontent.com/50621975/148735561-0fcfa202-0de2-4a62-88cb-06092934d3f7.png)
 
 #### more elaboration on JIT:
 when peice of js code enters the engine , the first step is to parse the code(essentially means read) and code get transforms to somthing called AST 
 __AST:__ abstract syntax tree works by first spliting the meaningfull parts of the code such as 'const' and 'function' keywords.and then saves all the pieces into the tree in a structured way .this step also checks if there is any syntax error .the resulting tree will later be used to generate a machine code.
 we dont need to know everything about AST .its somthing inside js engine.
 also it has nothing to do with DOM tree.
 next step is to compile AST to machine code (and we already know in JIT machine code gets executed immediatly)
 
 __note about Execution:__ first the rencently machine code gets executed immediatly but that is not the end! machine code gets optimized and executes again(during ongoing execution)
 
 parsing,compiling and optimizing happens in a special thread that we can not access from code.(main thread is in call stack)
 diffrent engines might implement this slighlty diffrent but this is how v8 works in a nutshell
 ![Screenshot (58)](https://user-images.githubusercontent.com/50621975/148744512-bf49bf6a-c385-462f-8bf9-2e4b301ceab6.png)
---
### what is javascript runtime?
__its a package in order to run and use javascript. for example: all modern browsers or nodejs__
other than js engines runtime include other tools too. in browser it hs web apis and in nodejs it has c++ bindings & thread poll
![Screenshot (59)](https://user-images.githubusercontent.com/50621975/148745231-90812562-6d4f-4703-a8f0-0a6e4af49d1d.png)
![Screenshot (60)](https://user-images.githubusercontent.com/50621975/148745258-6bbba351-86e5-4eb2-92e6-caaf74e50a5f.png)

---
# function declaration:
```javascript
  function doStuff(){}
```

# function expression:
```javascript
  const doStuff = function(){} 
  //or 
  const doStuff = ()=>{}
```
## IIFE(imediately invoked function expressions):
only possible with function expression 
```javascript
 (function(){})()
```
or 

```javascript
 (()=>{})()
```

# Hoisting:
Hoisting refers to the availability of functions and variables “at the top” of your code, as opposed to only after they are created. The objects are initialized at compile time and available anywhere in your file.
__Function declarations are hoisted but function expressions are not(for function expression if we use ```var``` we get undefined, if we use ```let``` or ```const``` we get uninitialized in temporal dead zone ,so in both cases is useless) __
![Screenshot (64)](https://user-images.githubusercontent.com/50621975/149287711-feb07501-b2c3-41e1-9b61-47f04c652e49.png)


```javascript
doStuff();
function doStuff(){}
//code above does not throw an error  
```
```javascript
doStuff();
const doStuff = ()=>{} //or function(){}
/*but this code will throw an error.a refrence error actually:we cant access 'doStuff' before initialization.and that is exactly same error we get if we defie anything else with ```let``` or ```const``` ,rather than a function(it is in tdz) */
```
### the case for function expression:
It might seem like function declarations, with their powerful hoisting properties, are going to edge out function expressions for usefulness. But choosing one over the other requires thinking about when and where the function is needed. Basically, who needs to know about it?
Function expressions are invoked to __avoid polluting the global scope__. Instead of your program being aware of many different functions, when you keep them anonymous, they are used and forgotten immediately.

```javascript
function mapAction(item) {
  // do stuff to an item
}
array.map(mapAction)

```
he problem here is that ```mapAction``` will be available to your entire application — there’s no need for that. If that callback is a function expression, it will not be available outside of the function that uses it:

```javascript
array.map(item => { //do stuff to an item })
```
### or

```javascript
const mapAction = function(item) {
  // do stuff to an item
}
array.map(mapAction)
```
### summary:
In short, use function declarations when you want to create a function on the global scope and make it available throughout your code. Use function expressions to limit where the function is available, keep your global scope light, and maintain clean syntax.
---
a video from jonas javascript tutorial was very good=> name: 5.Execution Contexts and Call Stack
---
## diffrent types of scope:
![Screenshot (61)](https://user-images.githubusercontent.com/50621975/148844061-e0cc7504-dabe-4339-8bbb-1f31f6e5610d.png)

important thing to note here is block scope is somthing that introduced in es6 and ```var``` dar behtarin halat is function scoped
ex:
```javascript
function first(){
  if(bluh bluh){
    let x = 'hello';
    var y = 'by';
  }
}

//x is in block scope of if-block but var is in the scope of first() function
```

![Screenshot (63)](https://user-images.githubusercontent.com/50621975/148846975-75d6aa50-c16e-483e-a036-07ba3aa5dd39.png)

__note:__ if we use 'strict mode'.the function declarations will also be block scoped for ex:
```javascript
'use strict';

function first(){
  if(myAge>= 18 && myAge<=30){
    function addFunc(){
      return 2+3
      }
}
addFunc() //this is ok becuase programm is in strict mode.otherwise function would not be accessible in here
}
```
__important note about polymorphism:__ we would get a diffrent result if we __change__ or we __define__ the existing variable in parent scope from child scope:
```javascript
  function first(){
    let output = "hi"
    
    function second(){
      output = "Hello" //since inner function access the outer variables,this code would change the ```output``` variable we defined above
      let output = "Hello" //but this code will create a new putput variable in ```second``` functions scope,so the ```output``` variable in first function remains intact
    }
  
  }
```

### About Temporal Dead Zone:
![image](https://user-images.githubusercontent.com/50621975/149310280-4e317ba9-34fd-4df9-99c8-5a8d10a6bfac.png)
son in both cases we get error and the result is more or less the same.son dont sweat too much on it

##### Hositing in practice:
```javascript
console.log(job)  //>> undefined
console.log(firstName)  //>> ReferenceError: Cannot access 'firstName' before initialization
console.log(year) // >> ReferenceError: Cannot access 'year' before initialization



let firstName = 'jack'
const year = 1994;
var job = 'teacher'
```
we get unedfined for the ```var``` variable becuase ```var``` is hoisted.(well, kind of hoisted actually.not as good as function declarations)  

#### wtf fact: 
__ if we use ```var``` for declaring a variable, that variable goes to ```window``` object!__

---

0 is a falsey value

### ABOUT ```this``` keyword:
![Screenshot (67)](https://user-images.githubusercontent.com/50621975/149319081-8e796b8e-f905-4288-a9a4-f1c221ace540.png)
### Lessons 11 and 12 in js under the hood section for ```this``` keyword are also brilliant! so in total:videos #5 #11 #12

for building methods, arrow functions are not suggested becuase their ```this``` would not refer to that object
---

we have a data structure called "Heap" but it has nothing to do with Heap Memory.completely diffrent things.
and we also have a data structure called stack; it has some similarties with stack memory
and also 

---

js tip of the day:
```javascript
if(+enteredAge <1){do somthing}
//'plus sign before variable makes forced conversion to number.although if enteredAge is a string like "4", js is smart enough to presume its a number before comparing to 1'
```
note:even number type inputes return those numbers as string;

####conditionally render element in react ,based on one value:
```javascript
{error && <errorModal/>}
```
---
### [complete guide to reducer function in javascript](https://www.javascripttutorial.net/javascript-array-reduce/)
---

```
{expression1} && {expression2}
```
javascript will return expression2 if only and only expression1 is truthy expression.this is called short circuiting

---
in javascript/typescript we dont have shits around numbers(float,integer,..) we only have "number" type for all that/

---
## First-Class Functions vs Higher-Order Functions:
first class functions is just a concept that either a programming language has it or not.it is not a real thing! it implies on this fact that functions are value and we can treat them as such for example we can call methods on function like we can call methods on array,object ... (ex: `bind`).
however higher-order function is a function that accept another function as a value or return another function or even both. 
```javascript
document.body.addEventListner('click' , onClickHandler)
```
`addEventlistner` is a higher order function cuase it recieves a function(as a callback.harja callback didi bedoon functione parentesh higher ordere). 
all array methods who recieve a callback are higher order functions(map, foreach , filter , reduce ...)
the important note is; in javascript higher-order functions are possible becuase js supports first-class function

---
intresting destructuring:
```javascript
const str = 'hello lads how you doing?'
//lets get the first word:
const [first , ...others] = str.split(' ') //totaly legit
```
__why callback functions are so important? __
__becuase they allow us to create abstractions__
### abstraction in programming:
essentially means hiding details of a code implementaion that we don't really need it. for example we dont need to know how Handler function works in a addEventListner function
 and this allows us to think at higher order or abstract level

---
`this` keyword really depends on where it is called.specially in functions    
### `call` , `apply` and `bind` function methods and partial design pattern:

call and apply mutate the original function but bind creates a new function
call takes arguments one by one.apply take them as an list


---
for object use `for in` and for arrays use `for of`   

callback que is not part of v8 engine.it is kind of an addon    

      
dont you think that everytime we use callback it is about some asynchronus shit.for example `setTimeout` is a function that is provided by browsers and node and it uses the callback function in an asynchronus way(calling it later) BUT functions such as `foreach` and `map` also use callback function and they implement them in a synchronus way.

__timer API is unique and like a miracle.__  we can simulate another anync actions like fetching data from server,with this api      
in functions the position of arguments matters ;not the name of them


### Callback example:
```javascript
  const geocode = (address)=>{
    
    setTimeout(()=>{
     const data = {
     longtitide:1,  //imagine this is a requested coordinate data based non address you provided  
     latitude:0
     }
     return data
      },2000)
      
   }
   
   console.log(geocode('philadelphia'))  // ->this returns nothing becuase the return is for inner function in setTimeout;not the geocode function
   
   
   //we have to use callback pattern for this to work:
   const geocode(address,callback)=>{
   setTimeout(()=>{
    const data={
    latitude:1,
    longtitude:0}
    callback(data)
   },2000)
   }
   
   
   console.log('philadelphia',(data)=>console.log(data)) //->this returns the data
   
```

if you console.log an asynchronous funtion,it logs:`AsyncFunction` .so it is really diffrent from a regular function.(as stephan said)

## another callback example:
using callback gives us more control when we call the function.in this case we can define how to use response and error.we can log them or...
```javascript
const forcast = (address,callback)=>{
    axios.get('http://api.weatherstack.com/current',{
    params:{
        access_key:'75eabb2336e0c10a53ba7a347abbbdbc',
        query:address,
        units:'f'
    }
}).then(response => {
    if(response.data.error){ //handling high level errors. for example server responded 200 status but there is no data for that city
        callback(`------ ${response.data.error.info}--------`)
    }else{
        callback(undefined,`it is currently ${response.data.current.temperature} out. it feels like ${response.data.current.feelslike} out`)
    }
    
}).catch(error => {  // this is usually for low-level errors such as network problems
    callback('some low level shit happend');
});
}

forcast('austin',(err,res)=>{
    console.log('ERROR: ', err);
    console.log('RESPONSE: ', res)
})
```
callbacks are usually designed to run after the completion of other tasks in that function
### importance of default params:
```javascript
//let say we expect input of a function to be object and we use destructring :

function todo(address,{name,time,color}){
}

//but this code leads to an error if,second parameter is missing and the error is like: "connot read name attribute of undefined"
// so we make the parameter to have a default value,just in case:
function todo(address,{name,time,color}={}){
}
```

### what the hell is Symbol?
__it is a new premitive type in javascript.behind the scenes it represents a unique id like `9823487236487232892739`__


in javascript Functions are objects. They have properties and methods. But this type of objects can be called.    
we can not return anything from terneary expression.means: `x===4?return 0` is wrong!


### Generators:
![image](https://user-images.githubusercontent.com/50621975/167612025-e8719a3f-d6f5-4767-a9cd-01b0484497c7.png)   
Calling a generator function does not execute it at once; instead, it returns an iterator object. When we call the `next()` method on iterator object, function body is executed until it sees the next `yield` keyword.

`next()` method returns an object with a “value” property which has the value that has been returned by `yield` and a “done” property which stands for whether a function has completed execution or not.   
`yield` is similar to await;in terms of waiting for an async thing to finish for ex:
```javascript
fynction* gen(){
  const fin = yield fetch(...)
}
```
__note about functions in general:__ when we don not explicitly return somthing from a function,that function actually returns undefined


## canvas api, audio and video api , blob and URL api .... all these apis are not part of javascript itself

## HUGE IMPORTANT NOTE IN OOP:
diffrence between static method.public fields and public methods:
```javascript
class Person{

constructor(){
this.choob = 'choob'
}
pelastik = 'pelastik'
//choob & pelastik are exactly the same in terms of defining and their position in instances.they are avalable in each instance 
}

//but this is not the case for methods(functions).javascript classes by default try to store methods in prototype(this is the right way).unless you explicitly define //your methods in contructor.which means:
class Material(){
constructor(){
this.getMe = function(){} //this method is not going to prototype
  }
  
getYou(){} //this is going to in prototype
}

```
__what about static methods(or even attributes)? they are going to be in the constructor function of the class! see below:__
```javascript
class Person{
    constructor(){
        this.getMe = function(){return null}
        this.choob = 'choob'
    }
  static ker = 'ker'
    static kossherSaz = function(){}

  pelastik=  'pelastik'

  getYou(){}
}

const ava = new Person()
console.log(ava)
```
![screenpng](https://user-images.githubusercontent.com/50621975/179822240-bf8cbbb0-a3a4-4a80-aaab-fd3f8bc0b7ec.png)
and this is why instances cant access to static methods(and attr),becuase they are not in the prototype chain!

if u want to use your script tag in html head instead of end of body, put `defer` sttribute in the script tag
```html
<script src='...' defer></script>
```

---
# javascript,understanding the wierd parts:
* 1)`console.log(typeof [1,2,3])` >>> object 
fix: console.log(Object.prototype.toString.call([1,2,3) >>> [object Array]

similar to `typeof` we have `instanceOf` which requires no pranethesis or dots for usage:
only use it for an instance of a class. if you write somthing like `[1,2] instanceof Array` it will give you false cause `[1,2]` is not instance of the Array its just using its prototype methods in prototype chain if needed

strict mode: as the name suggest impose stricter rules to javascript engine in compiling:
```javascript
person = {} //believe it or not this will not lead to and error

//but it we enable strict mode it requires a declaration(let,var,const) before initialization
'use strict'
const person = {} //should
```
also it does not have to be at global scope .you can impose strict rules only for one function in a file:
```javascript
function loggerr(){
"use strict"
let person;
persom = {} //lead to error in function call
}

abdoli = 'abdoli' //fine becuase strict mode won't apply to this
```
## what is 'syntax parser'?
__a programm that reads your code and determines what it does and if its grammer is valid(essentially a compiler)__   
your code is not magic.someone else wrote a programm to translate it for the computer.it's important to know your code is not the exact thing that goes to the computer ,but the translation of it which could contain extra stuff
![image](https://user-images.githubusercontent.com/50621975/179918023-3722dc02-01e3-4e82-a329-83dad6c10eaa.png)


## what is 'lexical environment'?
__where somthing sits physically in the code you write__    
'lexical' means having to do with words or grammer.a lexical environment exists in programming languages in which __wher__ you write something is important.    
in simple for the compiler is important where your variables are. (for defining scopes and shit..)  

## what is execution context?
__a wrapper to help manage the code that is running__     
there are lots of lexical environments.which one is currently running is managed via execution contexts.it can contain things beyond what you've written in your code.(that extra stuff) 
![image](https://user-images.githubusercontent.com/50621975/180510586-e080565c-1e4c-4b10-b054-65a0bbb58064.png)
either we did wrote any code or not,javascript engine creates these two at the begining ;and in the global context `this` is equals to `window` object.   
in browser global object is window.in nodejs is diffrent in bunjs too and so on...      
esseintially global means :not inside any function or scope


---
a name may be defined more than once, but only can have one value in any given context.   
in javascript __objects__ are just collections of name-value pairs    

## hoisting:
you already have some idea about hoisting from jonas.let anthony alicia clarifies more:   

```
console.log(a)
b()

var a = 'hello world'

function b(){
    console.log('fuck off')
}
/*>>> the result is:
undefined
hello world
*/
```
so why for function b is completely hoisted but for variable a kinda hoisted?(if it wasn't hoisted at all you would get an error instead of undefined)    
so what happens is; javascript engine before executing codes one by one take a quick glampse at it and allocate memory for function and variables . for function does this completely but for variables does this partially .kinda like this:  
```javascript
var a;
//this is a simulation-like example for before code start to execute
//js engine sets the value of a to 'undefined' to see what comes next
```

## Single Threaded:
javascript is a single threaded language ,which means can only do one command at a time(no parallel)(however under the hood of browser maybe not!)     

## synchronus:
essentially the same thing as being single threaded

## let see what happens when you invoke a function (in terms of execution context and call stack)
consider code below:
```js
function a(){
    b();
    var c;
}

function b(){
    var d;
}
a();
var d;
```
lets walkthrough this codes execution:      
1. first before executing anything,js engine creates a __global execution context__ and set aside memory for each variable and function![image](https://user-images.githubusercontent.com/50621975/181321215-c99eb27c-d8cc-40f3-b6a2-c28bf6e4909d.png)

2. then it starts line by line ,it would not create new execution context UNTILL one function gets invoke.in this case is function a
3. and in that point we have a execution stack![image](https://user-images.githubusercontent.com/50621975/181323838-c1971946-bcdb-4bfa-8a87-e79805c00424.png)
4. intrestingly inside function `a`, function `b` gets invoked,so another execution context (for `b`) gets created on top of `a`![image](https://user-images.githubusercontent.com/50621975/181328644-1de28c9b-7f79-46b3-beae-8ded0f0528a3.png)
5. now only when `b` finishes to run,it's execution context will pop off from the execution stack and `a` continous to run(in this case declare `c`) and so on...

__NOTE:__ what matters in execution stack is the hierarchical order of 'function calls',not their declaration or so to speak lexical environment

### Question: 
what is the result of running code below?
```js
function b(){
    console.log(myVar)
}

function a(){
    var myVar = 2;
    b()
}

var myVar = 1
a()
```
>>> th result is 1! despite the fact `b` is invoked isnide `a`; but `b` is not defined inside `a` (in that case it would have benn 2)
