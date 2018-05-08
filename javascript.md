## Javascript The Good Parts - Douglas Crockford ##

- **NUMBER** - JavaScript has a single number type. Internally, it is represented as 64-bit floating point, the same as Java's double. Unlike most other programming languages, there is no separate integer type, so 1 and 1.0 are the same value. The value NaN is a number value that is the result of an operation that cannot produce a normal result. NaN is not equal to any value, including itself. You can detect NaN with the isNaN( number ) function.

- When used inside of a function, the var statement defines the function's private variables.

- Unlike many other languages, blocks in JavaScript do not create a new scope, so variables should be defined at the top of the function, not in blocks.

- The values produced by *typeof* are 'number', 'string', 'boolean', 'undefined', 'function', and 'object'. If the operand is an array or null, then the result is 'object', which is wrong.

- The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects. Numbers, strings, and booleans are object-like in that they have methods, but they are immutable. Objects in JavaScript are mutable keyed collections. In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.

- An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string. A property value can be any JavaScript value except for undefined.

- The prototype link has no effect on updating. When we make changes to an object, the object's prototype is not touched. The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

- The prototype relationship is a dynamic relationship. If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype.

- The *delete* operator can be used to remove a property from an object. It will remove a property from the object if it has one. It will not touch any of the objects in the prototype linkage. Removing a property from an object may allow a property from the prototype linkage to shine through.

- *Functions* in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function's context and the code that implements the function's behavior.

- Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: *this* and *arguments*. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: *the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern*. The patterns differ in how the bonus parameter *this* is initialized.

- If a function is invoked with the *new* prefix, then a new object will be created with a hidden link to the value of the function's prototype member, and this will be bound to that new object. The new prefix also changes the behavior of the *return* statement. 

- A function always returns a value. If the *return* value is not specified, then *undefined* is returned. If the function was invoked with the new prefix and the *return* value is not an object, then *this* (the new object) is returned instead.

- Because of a design error, *arguments* is not really an array. It is an *array-like* object. arguments has a length property, but it lacks all of the array methods.

- The good news about scope is that inner functions get access to the parameters and variables of the functions they are defined within (with the exception of *this* and *arguments*).

- There is a serious hazard with the use of constructor functions. If you forget to include the *new* prefix when calling a constructor function, then this will not be bound to a new object. Sadly, this will be bound to the global object, so instead of augmenting your new object, you will be clobbering global variables. That is really bad. There is no compile warning, and there is no runtime warning. 

- We can use *functions* and *closure* to make modules. A module is a function or object that presents an interface but that hides its state and implementation. By using functions to produce modules, we can almost completely eliminate our use of global variables, thereby mitigating one of JavaScript's worst features.

- Array *length* can be set explicitly. Making the length larger does not allocate more space for the array. Making the length smaller will cause all properties with a subscript that is greater than or equal to the new length to be deleted.

### Reference ###
- https://github.com/iteles/Javascript-the-Good-Parts-notes

* * *

## The Principles of Object Oriented JavaScript - Nicholas C. Zakas ##

- While other programming languages distinguish between primitive and reference types by storing primitives on the stack and references in the heap, JavaScript does away with this concept completely: It tracks variables for a particular scope with a variable object. Primitive values are stored directly on the variable object, while reference values are placed as a pointer in the variable object, which serves as a reference to a location in memory where the object is stored.

- In JavaScript, as in many other languages, a variable holding a primitive directly contains the primitive value (rather than a pointer to an object). When you assign a primitive value to a variable, the value is copied into that variable. This means that if you set one variable equal to another, each variable gets its own copy of the data.

- **Identifying Primitive Types** - The best way to identify primitive types is with the typeof operator, which works on any variable and returns a string indicating the type of data. The typeof operator works well with strings, numbers, Booleans, and
undefined.

- The best way to determine if a value is null is to compare it against *null* directly, like this: console.log(value === null);

- Despite the fact that they’re primitive types, strings, numbers, and Booleans actually have *methods*. (The null and undefined types have no methods.)

- Reference types do not store the object directly into the variable to which it is assigned, so the object variable doesn’t actually contain the object instance. Instead, it holds a pointer (or reference) to the location in memory where the object exists. This is the primary difference between objects and primitive values, as the primitive is stored directly in the variable. When you assign an object to a variable, you’re actually assigning a pointer. That means if you assign one variable to another, each variable gets a copy of the pointer, and both still reference the same object in memory.

- JavaScript is a garbage-collected language, so you don’t really need to worry about memory allocations when you use reference types. However, it’s best to dereference objects that you no longer need so that the garbage collector can free up that memory. The best way to do this is to set the object variable to *null*.

- A function is the easiest reference type to identify because when you use the typeof operator on a function, the operator should return "function". Other reference types are trickier to identify because, for all reference types other than functions, typeof returns "object". To identify reference types more easily, you can use JavaScript’s *instanceof* operator.

- If your environment is ECMAScript 5 compliant, Array.isArray() is the best way to identify arrays.

- The number of *arguments* a function expects is stored on the function’s *length* property. Remember, a function is actually just an
object, so it can have properties. The length property indicates the function’s *arity*, or the number of parameters it expects. Knowing the function’s arity is important in JavaScript because functions won’t throw an error if you pass in too many or too few parameters.

-  **Function Overloading** - Most object-oriented languages support function *overloading*, which is the ability of a single function to have multiple signatures. A function signature is made up of the function name plus the number and type of parameters the function expects. Thus, a single function can have one signature that accepts a single string argument and another that accepts two numeric
arguments. The language determines which version of a function to call based on the arguments that are passed in. As mentioned previously, JavaScript functions can accept any number of parameters, and the types of parameters a function takes aren’t specified
at all. That means JavaScript functions don’t actually have signatures. A lack of function signatures also means a lack of function overloading. The fact that functions don’t have signatures in JavaScript doesn’t mean you can’t mimic function overloading. You can retrieve the number of parameters that were passed in by using the arguments object, and you can use that information to determine what to do.

- There are three function methods that allow you to change the value of *this* - *call, apply, bind*.

- There is a difference between the *enumerable* properties returned in a *for-in* loop and the ones returned by *Object.keys()*. The for-in loop also enumerates *prototype properties*, while Object.keys() returns only *own (instance) properties*.

- Not all properties on object are *enumerable*. In fact, most of the native methods on objects have their [[Enumerable]] attribute set to false. You can check whether a property is enumerable by using the *propertyIsEnumerable()* method, which is present on every object.

- There are two different types of properties: *data* properties and *accessor* properties. *Data properties* contain a value. The default behavior of the [[Put]] method is to create a data property. *Accessor properties* don’t contain a value but instead define a function to call when the property is read (called a getter), and a function to call when the property is written to (called a setter). Accessor properties only require either a getter or a setter, though they can have both.
You don’t need to define both a getter and a setter; you can choose one or both. If you define only a getter, then the property becomes read-only, and attempts to write to it will fail silently in nonstrict mode and throw an error in strict mode. If you define only a setter, then the property becomes write-only, and attempts to read the value will fail silently in both strict and nonstrict modes.

- There are two *property attributes* shared between *data and accessor* properties. One is *[[Enumerable]]*, which determines whether you can iterate over the property. The other is *[[Configurable]]*, which determines whether the property can be changed. By default, all properties you declare on an object are both enumerable and configurable. If you want to change property attributes, you can use the *Object.defineProperty()* method.

- Data properties possess two additional attributes that accessors do not - *[[Value]] and [[Writable]]*.

- Accessor properties also have two additional attributes. Because there is no value stored for accessor properties, there is no need for [[Value]] or [[Writable]]. Instead, accessors have *[[Get]] and [[Set]]*, which contain the getter and setter functions respectively.

- f you try to create a property with both data and accessor attributes, you will get an error.

- It’s also possible to define multiple properties on an object simultaneously if you use *Object.defineProperties()* instead of Object.defineProperty(). This method accepts two arguments: the object to work on and an object containing all of the property information.

- If you need to fetch property attributes, you can do so in JavaScript by using *Object.getOwnPropertyDescriptor()*. As the name suggests, this method works only on *own* properties. This method accepts two arguments: the object to work on and the property name to retrieve. If the property exists, you should receive a descriptor object with four properties: configurable, enumerable, and the two others appropriate for the type of property.

- Objects, just like properties, have internal attributes that govern their behavior. One of these attributes is *[[Extensible]]*, which is a Boolean value indicating if the object itself can be modified. All objects you create are extensible by *default*, meaning new properties can be added to the object at any time. By setting [[Extensible]] to false, you can prevent new properties from being added to an object. There are three different ways to accomplish this - *Object.preventExtensions(), Object.seal(), Object.freeze()*.

- One way to create a nonextensible object is with *Object.preventExtensions()*. This method accepts a single argument, which is the object you want to make nonextensible. Once you use this method on an object, you’ll never be able to add any new properties to it again. You can check the value of *[[Extensible]]* by using *Object.isExtensible()*.

- You can use the *Object.seal()* method on an object to seal it. When that happens, the *[[Extensible]]* attribute is set to *false*, and all properties have their *[[Configurable]]* attribute set to *false*. You can check to see whether an object is sealed using *Object.isSealed()*.

- The last way to create a *nonextensible* object is to freeze it. If an object is frozen, you can’t *add or remove* properties, you can’t change properties’ types, and you can’t write to any data properties. In essence, a frozen object is a *sealed object where data properties are also read-only*. Frozen objects can’t become *unfrozen*, so they remain in the state they were in when they became frozen. You can freeze an object by using *Object.freeze()* and determine if an object is frozen by using *Object.isFrozen()*.

- Frozen objects are simply snapshots of an object at a particular point in time. They are of limited use and should be used rarely.

- *Strict mode* doesn’t assign *this* to the global object. Instead, *this* remains undefined, and an error occurs whenever you attempt to create a property on undefined.

- An *instance* keeps track of its *prototype* through an internal property called *[[Prototype]]*. This property is a pointer back to the prototype object that the instance is using. When you create a new object using *new*, the constructor’s prototype property is assigned to the [[Prototype]] property of that new object. 

- You can read the value of the *[[Prototype]]* property by using the *Object.getPrototypeOf()* method on an object. You can also test to see if one object is a *prototype* for another by using the *isPrototypeOf()* method.

- The *shared nature of prototypes* makes them ideal for defining methods once for all objects of a given type. Because methods tend to do the same thing for all instances, there’s no reason each instance needs its own set of methods. It’s much more efficient to *put the methods on the prototype* and then use this to access the current instance.

- Perhaps the most interesting aspect of the relationships among *constructors, prototypes, and instances* is that there is no direct link between the instance and the constructor. There is, however, a direct link between the instance and the prototype and between the prototype and the constructor. This nature of this relationship means that any disruption between the instance and the prototype will also create a disruption between the instance and the constructor.

- The ability to modify the *prototype* at any time has some interesting repercussions for *sealed* and *frozen* objects. When you use Object.seal() or Object.freeze() on an object, you are acting solely on the object instance and the own properties. You can’t add new own properties or change existing own properties on frozen objects, but you can certainly still add properties on the prototype and continue extending those objects.

- Object literals have *Object.prototype* set as their [[Prototype]] implicitly, but you can also explicitly specify [[Prototype]] with the *Object.create()* method.

- It is fairly common to override supertype methods with new functionality in the subtype, but what if you still want to access the supertype method? In other languages, you might be able to say super.toString(), but JavaScript doesn’t have anything similar. Instead, you can directly access the method on the supertype’s prototype and use either call() or apply() to execute the method on the subtype object. 

* * *

## Object-oriented Javascript - Stoyan Stefanov, Kumar Chetan Sharma ##

- When you use a number-like string (for example "1") as an operand in an arithmetic operation, the string is converted to a number behind the scenes. This works for all arithmetic operations except addition, because of its ambiguity.

- A lazy way to convert any number-like string to a number is to multiply it by 1 (another way is to use a function called parseInt()).

- If you use a logical operator on a non-Boolean value, the value is converted to Boolean behind the scenes.

- Just because if *somevar* returns false doesn't mean that *somevar* is not defined. It could be that *somevar* is defined and initialized but contains a falsy value like *false* or *0*. A better way to check if a variable is defined is to use *typeof*. *typeof* always returns a string, and you can compare this string with the string *"undefined"*.
```
var result = "";
if (typeof somevar !== "undefined") {
    result = "yes";
}
result;
""
```
- As you know, in JavaScript, there is no curly braces scope, but there is function scope. A variable defined in a function is not visible outside the function, but a variable defined in a code block (for example an if or a for loop) is visible outside
the block.

- When your JavaScript program execution enters a new function, all the variables declared anywhere in the function are moved (or elevated, or hoisted) to the top of the function. This is an important concept to keep in mind. Further, only the declaration is hoisted, meaning only the presence of the variable is moved to the top. Any assignments stay where they are.

- Every function can be considered a *closure*. This is because every function maintains a secret link to the environment (the scope) in which it was created. Closure is created when a function keeps a link to its parent scope even after the parent has returned. And,
every function is a closure because, at the very least, every function maintains access to the global scope, which is never destroyed.
Function *parameters* behave like local variables to this function, but they are implicitly created (you don't need to use var for them). You can create a function that returns another function, which in turn returns its parent's parameter

- Function parameters behave like local variables to a function, but they are implicitly created (you don't need to use var for them). You can create a function that returns another function, which in turn returns its parent's parameter.

* * *

Deleting an array element leaves a “hole” in the array and does not change the array’s length. The resulting array is sparse.

All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as Object.prototype. Objects created using the new keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. So the object created by new Object() inherits from Object.prototype just as the object created by {} does. Similarly, the object created by new Array() uses Array.prototype as its prototype, and the object created by new Date() uses Date.prototype as its prototype.

The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript because it allows us to selectively override inherited properties.

for in can distinguish between properties that do not exist and properties that exist but have been set to undefined.

Object serialization is the process of converting an object’s state to a string from which it can later be restored. ECMAScript 5 provides native functions JSON.stringify() and JSON.parse() to serialize and restore JavaScript objects.

The keyword prototype is a property of Function() objects. No other type of objects have this property.

The prototype link has no effect on updating. The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

The standard properties in Object.prototype are all nonenumerable, which is why they do not show up in such a for/in loop.

Invoking a function suspends the execution of the current function, passing control and parameters to the new function.
There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

A function always returns a value. If the return value is not specified, then undefined is returned.

For object a property's name can be any string, including the empty string.

JavaScript does have function scope. That means that the parameters and variables defined in a function are not visible outside of the function, and that a variable defined anywhere within a function is visible everywhere within the function.

Closure - For example, suppose we want to augment String with a deentityify method. Its job is to look for HTML entities in a string and replace them with their equivalents. It makes sense to keep the names of the entities and their equivalents in an object. But where should we keep the object? We could put it in a global variable, but global variables are evil. We could define it in the function itself, but that has a runtime cost because the literal must be evaluated every time the function is invoked. The ideal approach is to put it in a closure, and perhaps provide an extra method that can add additional entities

The length can be set explicitly. Making the length larger does not allocate more space for the array. Making the length smaller will cause all properties with a subscript that is greater than or equal to the new length to be deleted.

parseInt is a function that converts a string into an integer. It stops when it sees a nondigit, so parseInt("16") and parseInt("16 tons") produce the same result.

In Java, the bitwise operators work with integers. JavaScript doesn't have integers. It only has double precision floating-point numbers. So, the bitwise operators convert their number operands into integers, do their business, and then convert them back. In most languages, these operators are very close to the hardware and very fast. In JavaScript, they are very far from the hardware and very slow. JavaScript is rarely used for doing bit manipulation.
JavaScript does not have an integer type, but it does have bitwise operators. The bitwise operators convert their operands from floating-point to integers and back, so they are not nearly as efficient as they are in C or other languages.

JavaScript programs are written using the Unicode character set. JavaScript assumes that the source code it is interpreting has already been normalized and makes no attempt to normalize identifiers, strings, or regular expressions itself.

JavaScript is a case-sensitive language.

Note that JavaScript does not treat every line break as a semicolon: it usually treats line breaks as semicolons only if it can’t parse the code without the semicolons. More formally (and with two exceptions described below), JavaScript treats a line break as a semicolon if the next non space character cannot be interpreted as a continuation of the current statement.

JavaScript types can be divided into two categories: primitive types and object types. JavaScript’s primitive types include numbers, strings of text (known as strings), and Boolean truth values (known as booleans). The special JavaScript values null and undefined are primitive values, but they are not numbers, strings, or booleans.

Functions that are written to be used (with the new operator) to initialize a newly created object are known as constructors. 

The JavaScript interpreter performs automatic garbage collection for memory management. This means that a program can create objects as needed, and the programmer never needs to worry about destruction or deallocation of those objects. When an object is no longer reachable—when a program no longer has any way to refer to it—the interpreter knows it can never be used again and automatically reclaims the memory it was occupying.

JavaScript variables are untyped: you can assign a value of any type to a variable, and you can later assign a value of a different type to the same variable.

Unlike many languages, JavaScript does not make a distinction between integer values and floating-point values. All numbers in JavaScript are represented as floating-point values. JavaScript represents numbers using the 64-bit floating-point format defined by the IEEE 754 standard. The JavaScript number format allows you to exactly represent all integers between −9007199254740992 (−253) and 9007199254740992 (253), inclusive. If you use integer values larger than this, you may lose precision in the trailing digits.

* * *
Arithmetic in JavaScript does not raise errors in cases of overflow, underflow, or division by zero. When the result of a numeric operation is larger than the largest representable number (overflow), the result is a special infinity value, which JavaScript prints as Infinity. Similarly, when the absolute value of a negative value becomes larger than the absolute value of the largest representable negative number, the result is negative infinity, printed as -Infinity.
Division by zero is not an error in JavaScript: it simply returns infinity or negative infinity. There is one exception, however: zero divided by zero does not have a well-defined value, and the result of this operation is the special not-a-number value, printed as NaN. NaN also arises if you attempt to divide infinity by infinity, or take the square root of a negative number or use arithmetic operators with non-numeric operands that cannot be converted to numbers.

The not-a-number value has one unusual feature in JavaScript: it does not compare equal to any other value, including itself. This means that you can’t write x == NaN to determine whether the value of a variable x is NaN. Instead, you should write x != x. That expression will be true if, and only if, x is NaN. The function isNaN() is similar. It returns true if its argument is NaN, or if that argument is a non-numeric value such as a string or an object. Following are treated as false in javascript - 
```
Boolean false
undefined
null
0
-0
NaN
""
```
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
Numbers and booleans have methods for the same reason that strings do: a temporary object is created using the Number() or Boolean() constructor, and the method is resolved using that temporary object. There are no wrapper objects for the null and undefined values: any attempt to access a property of one of these values causes a TypeError. Strings, numbers, and boolean values behave like objects when you try to read the value of a property (or method) from them. But if you attempt to set the value of a property, that attempt is silently ignored: the change is made on a temporary object and does not persist. The temporary objects created when you access a property of a string, number, or boolean are known as wrapper objects, and it may occasionally be necessary to distinguish a string value from a String object or a number or boolean value from a Number or Boolean object. The typeof operator will show you the difference between a primitive value and its wrapper object. If two distinct string values are compared, JavaScript treats them as equal if, and only if, they have the same length and if the character at each index is the same.
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

There are two different types of properties: data properties and accessor properties. Data properties contain a value. The default behavior of the [[Put]] method is to create a data property. Accessor properties don’t contain a value but instead define a function to call when the property is read (called a getter), and a function to call when the property is written to (called a setter). Accessor properties only require either a getter or a setter, though they can have both. You don’t need to define both a getter and a setter; you can choose one or both. If you define only a getter, then the property becomes read-only, and attempts to write to it will fail silently in nonstrict mode and throw an error in strict mode. If you define only a setter, then the property becomes write-only, and attempts to read the value will fail silently in both strict and nonstrict modes.

Data properties possess two additional attributes that accessors do not. The first is [[Value]], which holds the property value. This attribute is filled in automatically when you create a property on an object. All property values are stored in [[Value]], even if the value is a function.
The second attribute is [[Writable]], which is a Boolean value indicating whether the property can be written to. By default, all properties are writable unless you specify otherwise.

Objects, just like properties, have internal attributes that govern their behavior. One of these attributes is [[Extensible]], which is a Boolean value indicating if the object itself can be modified. All objects you create are extensible by default, meaning new properties can be added to the object at any time. You’ve seen this several times in this chapter. By setting [[Extensible]] to false, you can prevent new properties from being added to an object - Object.preventExtensions(), Object.seal(), Object.freeze().

You can also check the type of an instance using the constructor property. Every object instance is automatically created with a constructor property that contains a reference to the constructor function that created it. For generic objects (those created via an object literal or the Object constructor), constructor is set to Object; for objects created with a custom constructor, constructor points back to that constructor function instead. When you create a new object using new, the constructor’s prototype property is assigned to the [[Prototype]] property of that new object.
Even though this relationship exists between an instance and its constructor, you are still advised to use instanceof to check the type of an instance. This is because the constructor property can be overwritten and therefore may not be completely accurate.

Bar.prototype = Foo.prototype doesn’t create a new object for Bar.prototype to be linked to. It just makes Bar.prototype another reference to Foo.prototype, which effectively links Bar directly to the same object to which Foo links: Foo.prototype. This means when you start assigning, like Bar.prototype.myLabel = ..., you’re modifying not a separate object but the shared Foo.prototype object itself, which would affect any objects linked to Foo.prototype. This is almost certainly not what you want. If it is what you want, then you likely don’t need Bar at all, and should just use only Foo and make your code simpler.

Bar.prototype = new Foo() does in fact create a new object that is duly linked to Foo.prototype as we’d want. But, it used the Foo(..) “constructor call” to do it. If that function has any side effects (such as logging, changing state, registering against other objects, adding data properties to this, etc.), those side effects happen at the time of this linking (and likely against the wrong object!), rather than only when the eventual Bar() “descendents” are created, as would likely be expected.




