
When comparing complex objects, they are equal only when they reference the same object (i.e. have the same address). Two variables 
containing identical objects, are not equal to each other since they do not actually point at the same object.

```
var objectFoo = {same: 'same'};
var objectBar = {same: 'same'};
// logs false, JS does not care that they are identical and of the same object type
console.log(objectFoo === objectBar);
// how complex objects are measured for equality
var objectA = {foo: 'bar'};
var objectB = objectA;
console.log(objectA === objectB); // logs true because they reference the same object
```
