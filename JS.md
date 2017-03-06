
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

When any object is instantiated, the *constructor* property is created behind the scenes as a property of that object/instance. This points to the constructor function that created the object. The *constructor* property also works on user-defined constructor functions. 

By using the *instanceof* operator, we can determine (true or false) if an object is an instance of a particular constructor function. This works with user-defined objects as well as native objects created with the new operator. The *instanceof* operator will return false when dealing with primitive values that leverage object wrappers (e.g. 'foo' instanceof String //returns false). Had the string 'foo' been created with the new operator, the *instanceof* operator would have returned true. So, keep in mind that *instanceof* really only works with complex objects and instances created from constructor functions that return objects.

In JavaScript, objects can be augmented at any time (i.e dynamic properties). As previously mentioned, and to be exact, JavaScript has mutable objects. This means that objects created from a constructor function can be augmented with properties. Below, I create an instance from the Array() constructor and then augment it with its own property. 
```
var myArray = new Array();
myArray.prop = 'test';
console.log(myArray.prop) // logs 'test'
```

Bracket notation can be very handy when you need to access a property key and what you have to work with is a variable that contains a string value representing the property name. Additionally, bracket notion can come in handy for getting at property names that are invalid JavaScript identifiers.

Only properties that are enumerable (i.e. available when looping over an objects properties) show up with the for in loop. For example, the constructor property will not show up. It is possible to check which properties are enumerable with the propertyIsEnumerable() method.
