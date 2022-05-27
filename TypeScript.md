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
![image](https://user-images.githubusercontent.com/50621975/153896461-8b71a57d-4fde-4f97-b471-ecad53b42b43.png)

![image](https://user-images.githubusercontent.com/50621975/153896402-7ea9aa7a-815f-4b52-a24b-071d751b3479.png)
