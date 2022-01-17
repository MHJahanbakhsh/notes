* one otherway to return multiple jsx elements from one component,rather than having a wrapper element is to put them in array! we already know array of jsx is a legit thing for react comp to return(we use map()) the only downside to this approach is that you have to set unique keys for each element 
* other way is to create a wrapper component and in that component simply just return props.children
---
### React Portals:
with correct styling ,technichally a modal still might work in react ,no matter how deeply nested it is. but semsntically is not right to put an overlay component deep in somewhere it does not belong.

Portals only affect the HTML DOM structure and not impact the React components tree.which means modal component can still be deeply nested inside but when rendering it will be on top level next to root div

![Screenshot (70)](https://user-images.githubusercontent.com/50621975/149794847-9951f7c4-5671-4f14-b702-903a2dcfca2d.png)

sidebar's z-index gets compared to positioned's z-index.

what happens with portals is : based on where  your states are or personal prefrence you define your modal component.let say very deep; we don't care as long as that modal component returns its jsxs as portal
