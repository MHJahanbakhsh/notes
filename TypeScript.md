# typescript
by default type script will throw an error if you don't specify type for your function parameters.unless you write this in tsconfig.json:
```
{ 
    "compilerOptions": { 
        "noImplicitAny": false 
    } 
}
```

in typescript/javascript ,Object types are function,arrays,objects and classes which means each one has their own type(like with interface that we define our own types) 

![Screenshot (224)](https://user-images.githubusercontent.com/50621975/170809614-34c9c99d-d438-4ef8-9da6-0b33df2b05f2.png)
sometimes we can trick the typescript compiler that a value has a diffent type(in a good way).but this is only possible with refrence types(object types)       
wheter you like it or not,every value in typescript gonna have a type associate with it
* __in "Type annotation", we as developers tell typescript type of a value__
* __in "Type infrence",TypeScript guesses the type__

for 'undefined' and 'null' , types & values are the same:
```typescript
    let nothingMuch:null = null;
    const nothing:undefined = undefined
```

let see how it works with object literals
```typescript
let point : {x:number; y:number} = {  //note that for type we use ";" instead of ','
    x:10,
    y:5
}
```

![image](https://user-images.githubusercontent.com/50621975/153896461-8b71a57d-4fde-4f97-b471-ecad53b42b43.png)
```typescript
//initialization and declration at the same line
let apples = 5   //typescript will guess the type for us and assign apples type to number same as =====> let apples:number = 5

//initialization and declaration on diffrent lines
let apples;
apples = 5 //typescript wont assign any type to apples
```
## if typescript can guess variables for us, when we are going to use type annotaion over indfrence or vice-versa?      
![image](https://user-images.githubusercontent.com/50621975/153896402-7ea9aa7a-815f-4b52-a24b-071d751b3479.png)   
```typescript
//1)when we have a function that returns the any type:
const json = '{"X":10,"Y":5}'
const coords = JSON.parse(json)   //if you hover over it,coords has type of "any"(why?) becuase the JSON.parse is a function that returns "any" 
console.log(coords) //{X:10,Y:5}

//2)when we declare first and init later
let words = ['blue', 'green', 'red']
let foundWord;
for(let i=0; i<words.length; i++){
if (words[i] === 'blue'){foundWord = true}
}

/*3) a variable whose type connot be inferred correctly.for example you wanna conditionally assign a value boolean or number.if you let infrence does its job;you'll face an error */
let numbers = [-10, -1, 12];
let numberAboveZero: boolean|number = false;
for(let i=0; i<numbers.length; i++){
if(numbers[i] >0){numberAboveero = number[i]}else{null}
}
```
quick note on json: as you can see in picture below,the output of `JSON.parse()` is heavily dependent on the input. instead of guessing the output-type TS says "fuck it lets just return any type"
![Screenshot (227)](https://user-images.githubusercontent.com/50621975/170857878-10ee18fe-0e19-4c0c-a485-2ba20607c069.png)
```
JSON.parse('{"value":"5"}') // {value:"5"}
```

### note:avoid variables with "any" type at all cost   
so usually we are going to use type infrence more frequently

type inference for function only tries to guess the return value of the function and not the arguments.which means typescript can never guess types of arguments but nontheless we are not going to use it:
```typescript
const add = (a:number, b:number)=>{
    return a+b                  //becuase we returned 2numbers,type script guess the return value is number
}
//however
const subtract = (a:number, b:number)=>{
    a-b                         //here we forgot to put the return statement so typescript guess the value in a wrong way to  be void
}

//so overall we avoid any type inference in functions
```
### two special types: `void`&`never`       
you already know void, however when a function is explicitly says its returning void, it can also return null or undefined.
about never:
```typescript
function errorLogger(message:string):never{   
    throw new Error(message)     //we use 'never' when a function aaaalways with no condition returns an error.yani: if it has a if statement for it,it should return void instead?
  }
```

### let see how destructuring in a function argument works in typescript:       
```typescript

const todaysWeather = {
date: new Date(),
weather:'sunny'
}
//instead of this:
const logWeather = (forcast:{date:Date,weather:string})=>{
    console.log(forcast.date)
    console.log(forcast.weather)
}
//do this:
const logWeather = ({date,weather}:{date:Date,weather:string})=>{ //notice how destructuring and annotaion portions are seperate from each other
    console.log(date)
    console.log(weather)
}
```

## video 44 and after:
![image](https://user-images.githubusercontent.com/50621975/179449657-1599be2c-32ef-4715-8286-4e2b49dcdb3d.png)
* private method is not accessible in a child class(i mean extended child class.not instance)
* in polymorphism the type of the method can't change 
* by default if u don't put anything;is public      

`public`, `private` & `protected` are not solely for methods,we can use them for attributes too.however instead of implmenting attributes hardcoded like methods we want them to be dynamic via arguments in initialization.

```typescript
//this is ok
class Vehicle {
    color:string = 'red'
}

//but usually:
class Vehicle{
    color:string;
    constructor(color){
    this.color = color
     }
}

//in typescript we can make above statement waaay shorter:
class Vehicle{
    constructor(public color:string){} //exactly same as above!!
}
```
__what happens when we try to init a child extended class of Vehicle when itself has its own dynamic attributes:__
```typescript
class Vehicle{
    constructor(public color:string){} //exactly same as above!!
}

class Car extends Vehicle{
    constructor(public wheels:number, color:string){
    super(color) //whenever we call a constructor in a child class we are REQUIRED to call the construcotr of the parent class too. to do so we HAVE TO call `super`
    }
}
// so essentially `super` is a refrence to constructor method of the parent class

const ford = new Car(4,'blue')
```
