#Command Pattern

Command Pattern is one of the Behavioral Design Pattern and it’s used to implement lose coupling in a request-response model. In command pattern, the request is send to the invoker and invoker pass it to the encapsulated command object. Command object passes the request to the appropriate method of Receiver to perform the specific action.

The command pattern is different from a normal function in several ways: it provides the ability to parameterize and pass around a method call, which can then be executed whenever you need it to be. It also allows you to decouple the object invoking the action from the object implementing it, thus providing a huge degree of flexibility in swapping out concrete classes. The command pattern can be used in many different situations, but it is very useful in creating user interfaces, especially when an unlimited undo action is required. This pattern can also be used in place of a callback function, as it allows greater modularity in passing the action from object to object.

This pattern is different from the Chain of Responsibility in a way that, in the earlier one, the request passes through each of
the classes before finding an object that can take the responsibility. The command pattern however finds the particular object 
according to the command and invokes only that one.

It’s like there is a server having a lot of services to be given, and on Demand (or on command), it caters to that service for that particular client.

A classic example of this is a restaurant. A customer goes to restaurant and orders the food according to his/her choice. The waiter/ waitress takes the order (command, in this case) and hands it to the cook in the kitchen. The cook can make several types of food and so, he/she prepares the ordered item and hands it over to the waiter/waitress who in turn serves to the customer.

Command design pattern provides the options to queue commands, undo/redo actions and other manipulations.

This pattern works very well in GUI code, but it can be applied wherever it is possible and worthwhile to make operations reversible. For example, you could use it to undo filesystem changes, or database transactions. Commands can fail, and roll-back is easily implemented, so the system can make a best-effort to stay in a valid state.

Imagine a scenario where we have a web page will multiple menus in it. One way of writing this code is to have multiple if else condition and executing the actions on each click of the menu. We have to execute the actions based on the action 
string. To resolve this problem the Command pattern is here to rescue.

It can be used to encapsulate a callback function, for use in an XHR call or some other delayed-invocation situation. Instead of passing a callback function, you can pass a callback command, which allows you to encapsulate multiple function calls in a single package. Command objects also make it almost trivial to implement an undo mechanism in your application. By pushing executed commands to a stack, you can have an unlimited undo. This command logging can be used to implement undo even for actions that are not inherently reversible. It can also be used to restore the entire state of any app after a crash.


