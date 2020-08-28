
> [JavaScript / ECMAScript](https://en.wikipedia.org/wiki/JavaScript) (by [Brendan Eich](https://en.wikipedia.org/wiki/Brendan_Eich) 1995) is an ECMA standard since 1997, [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) is the official name of the language.


| ES version | ECMA | Name |
|---|---|---|
| ES5  | - | [ECMAScript 2009](https://www.w3schools.com/js/js_es5.asp) |
| ES6  | - | [ECMAScript 2015](https://www.w3schools.com/js/js_es6.asp) |
| ES7  | - | ECMAScript 2016 |
| ES8  | - | ECMAScript 2017 |
| ES9  | - | ECMAScript 2018 |
| ES10 | ECMA-262 | [ECMAScript 2019](https://www.ecma-international.org/ecma-262/10.0/index.html) |


<br/>


<details><summary><strong>Transpile via Babel</strong></summary>

[Babel](https://babeljs.io/repl) is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments. 

          ES6        |      ES5
    -----------------+--------------------
    const a = 123;   |  "use strict";
                     |  var a = 123;
    -----------------+--------------------
    
</details>


<details><summary><strong>Values: primitive / reference</strong></summary>
	
* _Primitive values_ are immutable and **shared by copy**: 
[undefined](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/undefined), 
[String](https://developazer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/String), 
[Number](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Number), 
[Boolean](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Boolean), 
[Symbol](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Symbol), 
[BigInt](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/BigInt)

* _Reference value_ are mutable and **shared by reference**: 
[Object](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Object), 
[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array), 
[Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)

</details>

<details><summary><strong>debug via console API</strong></summary>

* console.clear(): clear console
* console.log() / .debug() / .warn() / .error(): use **%c** directive to apply CSS style
```javascript
console.warn("abc");
console.log("%s %d", "int", 1.555);
console.log("%s %.1f", "float", 1.555);
console.error("Error %o: ", { keyA: 'valA', keyB: 123, keyC: ["a", "b", "c"] } );
console.log('%c big ABC', 'font-size:x-large;color:#f00;')
```
* console.table():
```javascript
console.table({ keyA: 'valA', keyB: 123, keyC: ["a", "b", "c"] } );
```
* console.dir(): prints interactive list of object properties
```javascript
console.dir({ keyA: 'valA', keyB: ["a", "b", "c"] } );
```
* console.group() / .groupEnd() / .groupCollapsed():
```javascript
console.log("START");
console.groupCollapsed("group 1") ; console.log("1 a") ; console.log("1 b") ; console.groupEnd();
console.log("END");
```
* console.count() / .countReset(): log number of times this line has been called (with the given label)
```javascript
console.count("count a");
```
* console.time() / .timeEnd()
```javascript
const longArray = Array.from({ length: 10000000 }, (_, i) => i);

console.time("forof-loop");
for (const value of longArray) {;}
console.timeEnd("forof-loop");

console.time("for-loop");
for (let i = 0; i < longArray.length; i++) {;}
console.timeEnd("for-loop");

console.time("foreach-loop");
longArray.forEach(element => {;});
console.timeEnd("foreach-loop");
```
* console.memory: heap size status

[developer.mozilla.org - Console](https://developer.mozilla.org/en-US/docs/Web/API/Console/)

</details>


<details><summary><strong>var, let and const</strong></summary>

> Before ES6: only _var_ was available!
Since ES6 _const_ and _let_: let is block scoped, no need for _var_ anymore! 

That means that a variable created with the let keyword is available inside the “block” that it was created in as well as any nested blocks. When I say “block”, I mean anything surrounded by a curly brace {} like in a for loop or an if statement.

+ var: function scoped ; undefined when accessing a variable before it's declared
+ let: block scoped ; ReferenceError when accessing a variable before it's declared
+ const: block scoped ; ReferenceError when accessing a variable before it's declared ; can't be reassigned

</details>


<details><summary><strong>Arrow => functions</strong></summary>

Arrow functions are a concise method of declaring anonymous functions in JS.

Arrow function inherit _this_ from the scope they were defined in.

```javascript
// vanilla anonymous function
someMethod(1, function () {    // has no name
   console.log('called');
});

// anonymous arrow function
someMethod(1, () => {          // has no name
   console.log('called');
});
```

</details>


<details><summary><strong>this keyword</strong></summary>

_this_ points to the surrounding execution context == "on what the function was called"

```javascript
const myButton = document.querySelector('some-button');

myButton.addEventListener('click', function() {
  console.log(this);  // => this refer to the element on which the event occurs
});
```

</details>


<details><summary><strong>Visibility of variables - scope</strong></summary>

* **global**:   variables defined outside of any function or block statement

* **function**: var variables defined inside of a function

* **block**:    let / const variables defined inside an block


</details>


<details><summary><strong>Closure</strong></summary>

> In JavaScript every function closes over its environment on creation

**Anonymous Closures**
A anonymous function which executes immediately. All code that runs inside the function lives in a closure, which provides privacy and state throughout the lifetime of the application.

```javascript
(function () {
	// ... all vars and functions are in this scope only
	// still maintains access to all globals
}());
```

```javascript
var test;

function fDelay() {
   setTimeout(function () {
      alert('test=' + test);
   }, 2222);
}

test = 'abc';
fDelay();
test = 'xyz';

// => alert: test=xyz
// because the value is looked up when needed and not when the closure is created
```

</details>


<details><summary><strong>Callback, promises, async/await</strong></summary>

JavaScript is single-threaded, that means only capable of doing one thing at the same time -> asynchronous tasks are handled by it's environment (web browser, NodeJS runtime, ...)

The biggest advantage of Promises over callbacks is readability and chainability.

An async function is 'just' a fancy promise wrapper, which means, the async/await code and the Promise code, are functionally equivalent.

```javascript
setTimeout(callFunction, 5000);   // callback function handed over to the web browser


      Promises                 |      pure callback
-------------------------------+------------------------------------
fetch('data.com/abc')          |  fetch('data.com/abc')
   .then(response => {         |     response => {
      return response.json();  |        response.json(data => {
   })                          |           console.log(data);
   .then(data => {             |           // other nested callbacks
      console.log(data);       |        });
   })                          |      },
   .catch(e => {               |      e => {
      console.error(e);        |         console.error(e);
   });                         |      }
                               |   ); 
-------------------------------+------------------------------------

async function makeHttpRequest(url) { ... }
try {
   const data = await makeHttpRequest('data.com/abc');
   console.log(data);
} catch (e) {
   console.error(e);
}
```

</details>


<details><summary><strong>Iterating DOM elements</strong></summary>

* __for loop__: supported in all browsers
```javascript
const allimg = document.querySelectorAll("img");
const allimgLen = allimg.length;
for (var i = 0; i < allimgLen; i++) {
   console.log('image: ', allimg[i]);
}
```


* __forEach loop__: supported in modern browsers, but not in IE11 and below
```javascript
const allimg = document.querySelectorAll("img");
allimg.forEach(actimg => {
   console.log('image: ', actimg);
});
```


* __for-of loop__: in modern browsers, but not in IE11 and below
```javascript
const allimg = document.querySelectorAll("img");
for (const actimg of allimg) {
   console.log('image: ', actimg);
}
```

* __for-of {values()|entries()|keys()} loop__: iterators are ES2015 specific
```javascript
const allimg = document.querySelectorAll("img");
for (const actimg of allimg.values()) {
   console.log('image: ', actimg);
};
```

</details>


<details><summary><strong>Iterating objects</strong></summary>


* __for…in loop__ => fastest version
```javascript
for (const key in obj) {
  if (obj.hasOwnProperty(key)) {
     console.log(key + " -> " + obj[key]);     
  }
}
```

* __Object.keys__ => slower than for…in
```javascript
Object.keys(obj).forEach(function (key) {
   console.log(key + " -> " + obj[key]);
});
Object.keys(obj).forEach(key => {
   console.log(key + " -> " +   obj[key]);     
});
```

* __Object.entries__ => slowest
```javascript
Object.entries(obj).forEach(entry => {
   console.log(entry[0]+ " -> " + entry[1]);
});
```

* __Object example__
```javascript
var obj= { 
   keyA: 'valueA',  
   keyB: 'valueB',
   keyC: 123,
   fPrintData: function() {
      for (const key in obj) {
         if (obj.hasOwnProperty(key)) {
            if ((typeof obj[key] === 'string') || (typeof obj[key] === 'number')) {
               console.log(key + " -> " +  obj[key]);     
            }
         }
      }
   }
};
// ---
var keyName1="myKey1";
var obj= { 
   [keyName1]: 'valueA',  
   keyB: 'valueB',
   keyC: 123,
   keyD: ["a", "b", "c"]
};

console.table(obj);
console.log(JSON.stringify(obj,null,2));
console.log(obj);
```

</details>


<details><summary><strong>Float Precision</strong></summary>

```javascript
var a=-0.34;
var b=1.20;

x=(a+b);
alert(x);
alert(x.toPrecision(10));
alert((x.toPrecision(10)).replace(/0*$/, ''));
```

</details>


<details><summary><strong>Load image and set background of element</strong></summary>

```javascript
var aElem, elemStyle, imgSrc, image;

aElem = document.getElementById("someElementId");
elemStyle = elem.style;
imgSrc = "someImageWithPath.jpeg";
image = new Image();
image.onload = function () {
   setTimeout(function () {
      elemStyle.backgroundImage = "url(" + imgSrc + ")";
      elemStyle.backgroundPosition = "0 0";
      image = null;
   }, 111);
};
image.src = imgSrc;
```

</details>


<details><summary><strong>Event delegation on non-bubbling events</strong></summary>

events like focus, blur, load, unload, change, reset, scroll,... need third argument of addEventListener "useCapture" to capture events that happen in the parent. Following example does not work without true at the end!
```javascript
document.addEventListener('focus', function (event) {
   console.log('something came into focus: ' + event.target);
}, true);
```
[JavaScript events](https://developer.mozilla.org/en-US/docs/Web/Events)


</details>


<details><summary><strong>Vanilla JavaScript version of "run on DOM ready"</strong></summary>

```javascript
function fVanillaJsDomReady(fn) {
   if (document.attachEvent ? document.readyState === "complete" : document.readyState !== "loading") {
      fn();
   } else {
      document.addEventListener("DOMContentLoaded", fn);
   }
}

fVanillaJsDomReady(function () { 
   console.log("DOM ready ...");
}
```

</details>


<details><summary><strong>Testing existence of property</strong></summary>

// BAD: This will cause an error in code when foo is undefined  
```javascript
if (foo) {  
   doSomething();  
}  
```
 
// GOOD: This doesn't cause any errors. However, even when  
// foo is set to NULL or false, the condition validates as true  
```javascript
if (typeof foo != "undefined") {  
   doSomething();  
} 
```
 
// BETTER: This doesn't cause any errors and in addition  
// values NULL or false won't validate as true  
```javascript
if (window.foo) {  
   doSomething();  
}  
```

</details>


<details><summary><strong>Passing arguments for function</strong></summary>

JavaScript [arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)

```javascript
function fDoSomething() {
   if (!arguments[0]) {   // leave if nothing is passed
      return false;
   }

   var oArgs = arguments[0],
       arg0 = oArgs.arg0 || "NO-ARG0",
       arg1 = oArgs.arg1 || "NO-ARG1",
       arg2 = oArgs.arg2 || -1,
       arg3 = oArgs.arg3 || [],
       arg4 = oArgs.arg4 || false;

    console.log("arg0=", arg0, "  arg1=", arg1, "  arg2=", arg2, "  arg3=", arg3, "  arg4=", arg4);
}

fDoSomething({
   arg1: "foo",
   arg2: 5,
   arg4: false
}); 
```

</details>


<details><summary><strong>"random" numbers</strong></summary>

```javascript

let maxVal = 99;
for (let i = 0; i < 11; i++) {
   setTimeout(() => console.log("random value " + i + ": " + (new Date() % maxVal) + "  /  " + (Math.floor(Math.random()*maxVal))), 1000)
}
```

</details>




<details><summary><strong>events bound in all elements on page</strong></summary>
	
```javascript
Array.from(document.querySelectorAll('*'))
  .reduce(function(pre, dom){
    var evtObj = getEventListeners(dom)
    Object.keys(evtObj).forEach(function (evt) {
      if (typeof pre[evt] === 'undefined') {
        pre[evt] = 0
      }
      pre[evt] += evtObj[evt].length
    })
    return pre
  }, {})
```

</details>





<details><summary><strong>Date / toLocaleString </strong></summary>
	
```javascript
var dm= Date.now();  // number of milliseconds elapsed since January 1, 1970 00:00:00 UTC.
var d= new Date();
var opt = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric', hour: 'numeric', minute: 'numeric', second: 'numeric', hour12: false };
opt.timeZone = 'UTC';
opt.timeZoneName = 'short';

console.log(": milliseconds since 1.1.1970 ", dm);
console.log(": current Date()=", d);
console.log(": UTC time zone diff to local machine time=", d.getTimezoneOffset()); 
console.log(": A: ", d.toLocaleString(navigator.language || 'de-DE', opt));
console.log(": B: ", d.toString());
console.log(": C: ", d.toDateString());
console.log(": D: ", d.toGMTString());
console.log(": E: ", d.toLocaleDateString());
console.log(": F: ", d.toISOString());
console.log(": G: ", d.toTimeString());
```

+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString

</details>



<details><summary><strong>format numbers (currency)</strong></summary>
	
```javascript
var number = 123456.78987654321;
console.log(number.toLocaleString('de-DE', { style: 'currency', currency: 'EUR', maximumFractionDigits: 4 }));
```

+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString

</details>


<details><summary><strong>External documentation</strong></summary>
	
+ https://www.w3schools.com/js/
+ https://plainjs.com/
+ https://air.ghost.io/js-things-i-never-knew-existed/amp/
+ https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
+ [A list of funny and tricky JavaScript examples](https://github.com/denysdovhan/wtfjs/blob/master/README.md#-motivation)
+ [JAMstack WTF](https://jamstack.wtf/)
+ https://mbeaudru.github.io/modern-js-cheatsheet/
+ https://v8.dev/blog/cost-of-javascript-2019
+ [Creating a Promise around an old callback API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises#Creating_a_Promise_around_an_old_callback_API)

+ Chrome Snippets
	+ https://developers.google.com/web/tools/chrome-devtools/javascript/snippets
	+ https://bgrins.github.io/devtools-snippets/
	+ https://github.com/bahmutov/code-snippets

</details>

<br/><br/>

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/JavaScript-logo.png/240px-JavaScript-logo.png)

---

<details>
<summary><strong>Markdown test</strong> (click to expand)</summary>
<p>

[github md guide](https://guides.github.com/features/mastering-markdown/)

[:smile: :confused: :thumbsup: :thumbsdown: :globe_with_meridians: :stopwatch: :calling: :computer: :keyboard: :blue_book: :email: :memo: :arrow_up: :arrow_right: :top: :end: :bangbang: :white_check_mark: :keycap_ten: :red_circle: :large_orange_diamond: :heavy_check_mark: ](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)

# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

**bold** *italic* ~~strikethrough~~
<span style="color:#e11d21;">Color Syntax</span>

> block quote
>> block quote (2 depth)
>>> block quote (3 depth)

* list
    * list indented
1. ordered
2. list
    1. ordered list
    2. indented

- [ ] task
- [x] list completed

`inline code`

    code block
```js
console.log("fenced code block");
```
<pre>**HTML block**</pre>

| table | head |
| ----  | ---- |
| table | body |
</p>
</details>

