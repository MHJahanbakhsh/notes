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

![image](https://user-images.githubusercontent.com/50621975/153896461-8b71a57d-4fde-4f97-b471-ecad53b42b43.png)

![image](https://user-images.githubusercontent.com/50621975/153896402-7ea9aa7a-815f-4b52-a24b-071d751b3479.png)     

for 'undefined' and 'null' , types & values are the same:
```typescript
    let nothingMuch:null = null;
    const nothing:undefined = undefined
```
