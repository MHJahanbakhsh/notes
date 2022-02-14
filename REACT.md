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


Once React knows which virtual DOM objects have changed, then React updates those objects, and only those objects, on the real DOM

vanillajs approach id imperative but react with use of jsx is declarative:
document.createElement('div').append(document.getElementById('root') vs jsx approach
---
whenever you combine components you're using composition

when to use props.children? custom made components unlike

why  in react we can't use this:
```
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
 comprehensive guide to useRef: https://www.youtube.com/watch?v=t2ypzz6gJm0;
---
Note:don't forget 
```
React.creatElemet()
```
for interviews
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


![image](https://user-images.githubusercontent.com/50621975/153897548-5f40594b-95a9-4e7a-8b56-707a9076ea3c.png)

useEffect cleanup function: useEffect can return one thing and one thing only;which is a function. this function would invoke at next render(not first one)
