JavaScript programs are written using the Unicode character set.

JavaScript is a case-sensitive language.

Functions that are written to be used (with the new operator) to initialize a newly created object are known as constructors. 

JavaScript variables are untyped: you can assign a value of any type to a variable, and you can later assign a value of a different type to the same variable.

The JavaScript number format allows you to exactly represent all integers between −9007199254740992 (−253) and 9007199254740992 (253), inclusive. If you use integer values larger than this, you may lose precision in the trailing digits.

* * *
Arithmetic in JavaScript does not raise errors in cases of overflow, underflow, or division by zero. When the result of a numeric operation is larger than the largest representable number (overflow), the result is a special infinity value, which JavaScript prints as Infinity. Similarly, when the absolute value of a negative value becomes larger than the absolute value of the largest representable negative number, the result is negative infinity, printed as -Infinity.
Division by zero is not an error in JavaScript: it simply returns infinity or negative infinity. There is one exception, however: zero divided by zero does not have a well-defined value, and the result of this operation is the special not-a-number value, printed as NaN. NaN also arises if you attempt to divide infinity by infinity, or take the square root of a negative number or use arithmetic operators with non-numeric operands that cannot be converted to numbers.

The not-a-number value has one unusual feature in JavaScript: it does not compare equal to any other value, including itself. This means that you can’t write x == NaN to determine whether the value of a variable x is NaN. Instead, you should write x != x. That expression will be true if, and only if, x is NaN. The function isNaN() is similar. It returns true if its argument is NaN, or if that argument is a non-numeric value such as a string or an object.
* * *
JavaScript uses the UTF-16 encoding of the Unicode character set, and JavaScript strings are sequences of unsigned 16-bit values. The most commonly used Unicode characters (those from the “basic multilingual plane”) have codepoints that fit in 16 bits and can be represented by a single element of a string. Unicode characters whose codepoints do not fit in 16 bits are encoded following the rules of UTF-16 as a sequence (known as a “surrogate pair”) of two 16-bit values. This means that a JavaScript string of length 2 (two 16-bit values) might represent only a single Unicode character:
```
var p = "π"; // π is 1 character with 16-bit codepoint 0x03c0
var e = "e"; // e is 1 character with 17-bit codepoint 0x1d452
p.length     // => 1: p consists of 1 16-bit element
e.length     // => 2: UTF-16 encoding of e is 2 16-bit values: "\ud835\udc52"
```
The various string-manipulation methods defined by JavaScript operate on 16-bit values, not on characters. They do not treat surrogate pairs specially, perform no normalization of the string, and do not even ensure that a string is well-formed UTF-16.
* * *

To include a string literally in a JavaScript program, simply enclose the characters of the string within a matched pair of single or double quotes (' or "). Double-quote characters may be contained within strings delimited by single-quote characters, and single-quote characters may be contained within strings delimited by double quotes. 

Remember that strings are immutable in JavaScript. Methods like replace() and toUpperCase() return new strings: they do not modify the string on which they are invoked.

null and undefined both indicate an absence of value and can often be used interchangeably. The equality operator == considers them to be equal. (Use the strict equality operator === to distinguish them.) Both are falsy values—they behave like false when a boolean value is required. Neither null nor undefined have any properties or methods. In fact, using . or [] to access a property or method of these values causes a TypeError.

* * *
**Wrapper Objects**
```
var s = "hello world!";                             // A string
var word = s.substring(s.indexOf(" ")+1, s.length); // Use string properties
```
Primitive strings are not objects, though, so why do they have properties? Whenever you try to refer to a property of a string s, JavaScript converts the string value to an object as if by calling new String(s). This object inherits (see Inheritance) string methods and is used to resolve the property reference. Once the property has been resolved, the newly created object is discarded. (Implementations are not required to actually create and discard this transient object: they must behave as if they do, however.)
Numbers and booleans have methods for the same reason that strings do: a temporary object is created using the Number() or Boolean() constructor, and the method is resolved using that temporary object. There are no wrapper objects for the null and undefined values: any attempt to access a property of one of these values causes a TypeError.
Consider the following code and think about what happens when it is executed:
```
var s = "test";         // Start with a string value.
s.len = 4;              // Set a property on it.
var t = s.len;          // Now query the property.
```
When you run this code, the value of t is undefined. The second line of code creates a temporary String object, sets its len property to 4, and then discards that object. The third line creates a new String object from the original (unmodified) string value and then tries to read the len property. This property does not exist, and the expression evaluates to undefined. This code demonstrates that strings, numbers, and boolean values behave like objects when you try to read the value of a property (or method) from them. But if you attempt to set the value of a property, that attempt is silently ignored: the change is made on a temporary object and does not persist.
The temporary objects created when you access a property of a string, number, or boolean are known as wrapper objects, and it may occasionally be necessary to distinguish a string value from a String object or a number or boolean value from a Number or Boolean object. Usually, however, wrapper objects can be considered an implementation detail and you don’t have to think about them. You just need to know that string, number, and boolean values differ from objects in that their properties are read-only and that you can’t define new properties on them.
Note that it is possible (but almost never necessary or useful) to explicitly create wrapper objects, by invoking the String(), Number(), or Boolean() constructors:
```
var s = "test", n = 1, b = true;  // A string, number, and boolean value.
var S = new String(s);            // A String object
var N = new Number(n);            // A Number object
var B = new Boolean(b);           // A Boolean object
```
JavaScript converts wrapper objects into the wrapped primitive value as necessary, so the objects S, N, and B above usually, but not always, behave just like the values s, n, and b. The == equality operator treats a value and its wrapper object as equal, but you can distinguish them with the === strict equality operator. The typeof operator will also show you the difference between a primitive value and its wrapper object.
* * *


**Immutable Primitive Values and Mutable Object References**

There is a fundamental difference in JavaScript between primitive values (undefined, null, booleans, numbers, and strings) and objects (including arrays and functions). Primitives are immutable: there is no way to change (or “mutate”) a primitive value. This is obvious for numbers and booleans—it doesn’t even make sense to change the value of a number. It is not so obvious for strings, however. Since strings are like arrays of characters, you might expect to be able to alter the character at any specified index. In fact, JavaScript does not allow this, and all string methods that appear to return a modified string are, in fact, returning a new string value. For example:
```
var s = "hello";   // Start with some lowercase text
s.toUpperCase();   // Returns "HELLO", but doesn't alter s
s                  // => "hello": the original string has not changed
```
Primitives are also compared by value: two values are the same only if they have the same value. This sounds circular for numbers, booleans, null, and undefined: there is no other way that they could be compared. Again, however, it is not so obvious for strings. If two distinct string values are compared, JavaScript treats them as equal if, and only if, they have the same length and if the character at each index is the same.
Objects are different than primitives. First, they are mutable—their values can change:
```
var o = { x:1 };     // Start with an object
o.x = 2;             // Mutate it by changing the value of a property
o.y = 3;             // Mutate it again by adding a new property

var a = [1,2,3]      // Arrays are also mutable
a[0] = 0;            // Change the value of an array element
a[3] = 4;            // Add a new array element
```
Objects are not compared by value: two objects are not equal even if they have the same properties and values. And two arrays are not equal even if they have the same elements in the same order:
```
var o = {x:1}, p = {x:1};  // Two objects with the same properties
o === p                    // => false: distinct objects are never equal
var a = [], b = [];        // Two distinct, empty arrays
a === b                    // => false: distinct arrays are never equal
```
Objects are sometimes called reference types to distinguish them from JavaScript’s primitive types. Using this terminology, object values are references, and we say that objects are compared by reference: two object values are the same if and only if they refer to the same underlying object.
```
var a = [];   // The variable a refers to an empty array.
var b = a;    // Now b refers to the same array.
b[0] = 1;     // Mutate the array referred to by variable b.
a[0]          // => 1: the change is also visible through variable a.
a === b       // => true: a and b refer to the same object, so they are equal.
```
As you can see from the code above, assigning an object (or array) to a variable simply assigns the reference: it does not create a new copy of the object. If you want to make a new copy of an object or array, you must explicitly copy the properties of the object or the elements of the array. This example demonstrates using a for loop (for):
```
var a = ['a','b','c'];              // An array we want to copy
var b = [];                         // A distinct array we'll copy into
for(var i = 0; i < a.length; i++) { // For each index of a[]
    b[i] = a[i];                    // Copy an element of a into b
}
```
Similarly, if we want to compare two distinct objects or arrays, we must compare their properties or elements. This code defines a function to compare two arrays:
```
function equalArrays(a,b) {
    if (a.length != b.length) return false; // Different-size arrays not equal
    for(var i = 0; i < a.length; i++)       // Loop through all elements
        if (a[i] !== b[i]) return false;    // If any differ, arrays not equal
    return true;                            // Otherwise they are equal
}
```
* * *


Keep in mind that convertibility of one value to another does not imply equality of those two values. If undefined is used where a boolean value is expected, for example, it will convert to false. But this does not mean that undefined == false. JavaScript operators and statements expect values of various types, and perform conversions to those types. The if statement converts undefined to false, but the == operator never attempts to convert its operands to booleans.


To convert an object to a string, JavaScript takes these steps:
If the object has a toString() method, JavaScript calls it. If it returns a primitive value, JavaScript converts that value to a string (if it is not already a string) and returns the result of that conversion. Note that primitive-to-string conversions are all well-defined in Table 3-2.
If the object has no toString() method, or if that method does not return a primitive value, then JavaScript looks for a valueOf() method. If the method exists, JavaScript calls it. If the return value is a primitive, JavaScript converts that value to a string (if it is not already) and returns the converted value.
Otherwise, JavaScript cannot obtain a primitive value from either toString() or valueOf(), so it throws a TypeError.
To convert an object to a number, JavaScript does the same thing, but it tries the valueOf() method first:
If the object has a valueOf() method that returns a primitive value, JavaScript converts (if necessary) that primitive value to a number and returns the result.
Otherwise, if the object has a toString() method that returns a primitive value, JavaScript converts and returns the value.
Otherwise, JavaScript throws a TypeError.


When you declare a global JavaScript variable, what you are actually doing is defining a property of the global object (The Global Object). If you use var to declare the variable, the property that is created is nonconfigurable (see Property Attributes), which means that it cannot be deleted with the delete operator. We’ve already noted that if you’re not using strict mode and you assign a value to an undeclared variable, JavaScript automatically creates a global variable for you. Variables created in this way are regular, configurable properties of the global object and they can be deleted:
```
var truevar = 1;     // A properly declared global variable, nondeletable.
fakevar = 2;         // Creates a deletable property of the global object.
this.fakevar2 = 3;   // This does the same thing.
delete truevar       // => false: variable not deleted
delete fakevar       // => true: variable deleted
delete this.fakevar2 // => true: variable deleted
```

A property has a name and a value. A property name may be any string, including the empty string, but no object may have two properties with the same name. The value may be any JavaScript value, or (in ECMAScript 5) it may be a getter or a setter function (or both). We’ll learn about getter and setter functions in Property Getters and Setters. In addition to its name and value, each property has associated values that we’ll call property attributes:
The writable attribute specifies whether the value of the property can be set.
The enumerable attribute specifies whether the property name is returned by a for/in loop.
The configurable attribute specifies whether the property can be deleted and whether its attributes can be altered.
Prior to ECMAScript 5, all properties in objects created by your code are writable, enumerable, and configurable. In ECMAScript 5, you can configure the attributes of your properties.


In addition to its properties, every object has three associated object attributes:
An object’s prototype is a reference to another object from which properties are inherited.
An object’s class is a string that categorizes the type of an object.
An object’s extensible flag specifies (in ECMAScript 5) whether new properties may be added to the object.


An object literal is an expression that creates and initializes a new and distinct object each time it is evaluated. The value of each property is evaluated each time the literal is evaluated. This means that a single object literal can create many new objects if it appears within the body of a loop in a function that is called repeatedly, and that the property values of these objects may differ from each other.

In ECMAScript 3, the identifier that follows the dot operator cannot be a reserved word: you cannot write o.for or o.class, for example, because for is a language keyword and class is reserved for future use. If an object has properties whose name is a reserved word, you must use square bracket notation to access them: o["for"] and o["class"]. ECMAScript 5 relaxes this restriction (as do some implementations of ECMAScript 3) and allows reserved words to follow the dot.


There is one exception to the rule that a property assignment either fails or creates or sets a property in the original object. If o inherits the property x, and that property is an accessor property with a setter method (see Property Getters and Setters), then that setter method is called rather than creating a new property x in o. Note, however, that the setter method is called on the object o, not on the prototype object that defines the property, so if the setter method defines any properties, it will do so on o, and it will again leave the prototype chain unmodified.


The delete operator only deletes own properties, not inherited ones. (To delete an inherited property, you must delete it from the prototype object in which it is defined. Doing this affects every object that inherits from that prototype.)


The for/in loop runs the body of the loop once for each enumerable property (own or inherited) of the specified object, assigning the name of the property to the loop variable. Built-in methods that objects inherit are not enumerable, but the properties that your code adds to objects are enumerable.