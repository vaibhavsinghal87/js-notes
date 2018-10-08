# Web Performance

- Loading and execution - JavaScript performance in the browser is arguably the most important usability issue facing developers. The problem is complex because of the blocking nature of JavaScript, which is to say that nothing else can happen while JavaScript code is being executed. In fact, most browsers use a single process for both user interface (UI) updates and JavaScript execution, so only one can happen at any given moment in time. The longer JavaScript takes to execute, the longer it takes before the browser is free to respond to user input.

- On a basic level, this means that the very presence of a script tag is enough to make the page wait for the script to be parsed and executed. Whether the actual JavaScript code is inline with the tag or included in an external file is irrelevant; the page download and rendering must stop and wait for the script to complete before proceeding. This is a necessary part of the page’s life cycle because the script may cause changes to the page while executing

- Any time spent by the browser executing a page’s JavaScript is time that it cannot spend responding to other user events. It is therefore vital that any JavaScript in a page execute as fast as possible. Otherwise, the web page and the browser itself may become sluggish or freeze up entirely.

- When the browser encounters a script tag, as in this HTML page, there is no way of knowing whether the JavaScript will insert content into the p, introduce additional elements, or perhaps even close the tag. Therefore, the browser stops processing the page as it comes in, executes the JavaScript code, then continues parsing and rendering the page. The same takes place for JavaScript loaded using the src attribute; the browser must first download the code from the external file, which takes time, and then parse and execute the code. Page rendering and user interaction are completely blocked during this time.

- Although it’s clear that scripts must be executed sequentially, there’s no reason they have to be downloaded sequentially.

- Script positioning - Keep in mind that browsers don’t start rendering anything on the page until the opening <body> tag is encountered. Putting scripts at the top of the page in this way typically leads to a noticeable delay, often in the form of a blank white page, before the user can even begin reading or otherwise interacting with the page. Because scripts block downloading of all resource types on the page, it’s recommended to place all script tags as close to the bottom of the <body> tag as possible so as not to affect the download of the entire page.

- Data Access - Accessing information from array items and object members is more expensive. The general advice is to use literal values and local variables whenever possible and limit use of array items and object members where speed of execution is a concern.

- Caching Object Member Values - Generally speaking, if you’re going to read an object property more than one time in a function, it’s best to store that property value in a local variable. The local variable can then be used in place of the property to avoid the performance overhead of another property lookup. This is especially important when dealing with nested object members that have a more dramatic effect on execution speed. Local variables are faster to access than out-of-scope variables because they exist in the first variable object of the scope chain. The further into the scope chain a variable is, the longer it takes to access. Global variables are always the slowest to access because they are always last in the scope chain.

- Another way of updating page contents using DOM methods is to clone existing DOM elements instead of creating new ones

- When a DOM change affects the geometry of an element (width and height)—such as a change in the thickness of the border or adding more text to a paragraph, resulting in an additional line—the browser needs to recalculate the geometry of the element as well as the geometry and position of other elements that could have been affected by the change. The browser invalidates the part of the render tree that was affected by the change and reconstructs the render tree. This process is known as a reflow. Once the reflow is complete, the browser redraws the affected parts of the screen in a process called repaint. Repaints and reflows are expensive operations and can make the UI of a web application less responsive. As such, it’s important to reduce their occurrences whenever possible. Reflows and repaints can be expensive, and therefore a good strategy for responsive applications is to reduce their number. In order to minimize this number, you should combine multiple DOM and style changes into a batch and apply them once.

- Event Delegation - A simple and elegant technique for handling DOM events is event delegation. It’s based on the fact that events bubble up and can be handled by a parent element. With event delegation, you attach only one handler on a wrapper element to handle all events that happen to the children descendant of that parent wrapper.

- Loops - it’s recommended to avoid the for-in loop unless your intent is to iterate over an unknown number of object properties.

- There are multiple ways to create objects and arrays in JavaScript, but nothing is faster than creating object and array literals.

- Excessive use of the add-by-value operator involving large quantities of text can become inefficient. If you are experiencing slow performance when accumulating large strings, try pushing your string segments into items of an array. Then use the array's join() method to generate the resulting large string value.

- Always use native methods when available, especially for mathematical calculations and DOM operations.

- About the console time API - The console.time() method allows developers to have an understanding of what code affects performance and what doesn't. The console.time() method delivers results based on not only what browser you're using, but also what operating system and system hardware you're using.

- A lint is, simply put, a code-validation checker. It allows a developer to point to a code file and check for errors or potential issues ranging from spacing issues to pure code errors.


- Using the debugger keyword


- The Timeline panel allows us to detect the overall web page performance with respect to JavaScript; it also allows us to inspect browser rendering events. To use the Timeline panel, all we need to do is click the record button and reload the page in Chrome. In the Timeline inspector, there are four types of events that the Timeline panel shows. These are Loading, Scripting, Rendering, and Painting events. It gives you a look under the hood of how the browser renders web pages and lets you see which processes and resources require more computing power for both rendering and JavaScript load times. This tool allows you to visualize where you need to fine-tune and better optimize your web applications.

- The Loading event
The Loading event handles requests and responses; typically these are loading external scripts and files as well as POST requests for data leaving the page. Loading events also include the initial parsing of HTML code. In Google Chrome's Timeline, these show up in blue.

- The Scripting event
The Scripting event occurs when the browser reads and interprets JavaScript code. In the Timeline panel, you can expand a Scripting event and see at what point a function was received in the browser. Scripting events appear as yellow lines in Google Chrome.

- The Rendering event
The Rendering event occurs when image files and scripts affect the DOM; this can be when an image is loaded without a size specified in an image tag, or if a JavaScript file updates the CSS of a page after the page is loaded.

- The Painting event
The Painting event is the last type of events and typically is used in updating the UI. Unlike Rendering event, the Painting event occurs when the browser redraws an image on the screen. For desktop JavaScript development, Painting events aren't usually a concern, but become strongly concerning when we start looking at mobile web browsers.

- The Profile panel helps a developer analyze a web page's CPU profile and take heap snapshots of the JavaScript used. A CPU profile snapshot is helpful when it comes to checking large complex applications to see what files may cause issues in terms of object size.
A JavaScript heap snapshot is a compiled list of objects found in the page's overall JavaScript. This includes not only the code written by us, but also the code built into the browser, such as the document or console objects, giving an overall list of all possible objects in an application.

- The reality of this is that the equals operator is slow compared to using the === strict comparison operator, which also compares object types as well as the object's value. As the JavaScript interpreter doesn't have to confirm the type before checking the equality, it operates faster than using the double equals operator.


- Batch your DOM changes, especially when updating styles


- Build DOM separately before adding it to the page

- The following tips are derived from the book High Performance Web Sites (O’Reilly) by Steve Souders:
  - Make fewer HTTP requests to reduce object overhead.
  - Use a content delivery network.
  - Add an Expires header.
  - Gzip/compress text components.
  - Put stylesheets at the top in the head.
  - Put scripts at the bottom of the body.
  - Avoid CSS expressions which are CPU-intensive and can be evaluated frequently.
  - Make JavaScript and CSS files external.
  - Reduce Domain Name System (DNS) lookups to reduce the overhead of DNS delay by splitting lookups between two to four unique hostnames.
  - Minify JavaScript.
  - Avoid redirects which slow performance. It’s better to CNAME or alias.
  - Remove duplicate scripts to eliminate extra HTTP requests in Internet Explorer.
  - Configure ETags for sites hosted on multiple servers. FileETag none in Apache removes Etags to avoid improper cache validation.
  - Make Ajax cacheable and small to avoid unnecessary HTTP requests.

# References - 
https://github.com/handsontable/handsontable/wiki/JavaScript-&-DOM-performance-tips <br/>
http://superherojs.com/ <br/>
https://www.monitis.com/blog/2011/05/15/30-tips-to-improve-javascript-performance/ <br/>
http://v8-io12.appspot.com/#54 <br/> 
https://github.com/petkaantonov/bluebird/wiki/Optimization-killers <br/>
https://medium.com/the-javascript-collection/lets-write-fast-javascript-2b03c5575d9e#.6hh0uc81v <br/>
http://home.earthlink.net/~kendrasg/info/js_opt/ <br/>
http://www.webreference.com/programming/javascript/jkm3/index.html <br/>
https://developer.yahoo.com/performance/rules.html <br/>
http://betterexplained.com/articles/how-to-optimize-your-site-with-gzip-compression/ <br/>
https://gtmetrix.com/enable-gzip-compression.html <br/>
http://mrale.ph/blog/2011/12/18/v8-optimization-checklist.html <br/>
https://moz.com/blog/15-tips-to-speed-up-your-website <br/>
http://www.webweaver.nu/html-tips/load-time.shtml <br/>
http://yslow.org/ <br/>
https://developer.yahoo.com/performance/ <br/>
http://blog.crazyegg.com/2013/12/11/speed-up-your-website/ <br/>
https://www.devbridge.com/articles/need-for-speed-how-to-improve-your-website-performance/ <br/>
http://webdesign.tutsplus.com/articles/best-practices-for-increasing-website-performance--webdesign-9109 <br/>
https://css-tricks.com/efficiently-rendering-css/
