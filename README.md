# Javascript Evaluation

1. What is a potential pitfall with using typeof bar === "object" to determine if bar is an object? How can this pitfall be avoided?

I think because of the ambiguity of "object" in javascript many things that in other languages has itw own definition in js are trated like 'objects',
so if you need to know the type of an array it will return an "object", so you can try the 'instanceof' or to evaluate a specific property from that object
if it is undefined or not.

2. What will the code below output to the console and why?
   
```javascript
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);
        console.log("outer func:  self.foo = " + self.foo);
        (function() {
            console.log("inner func:  this.foo = " + this.foo);
            console.log("inner func:  self.foo = " + self.foo);
        }());
    }
};
myObject.func();
```
The result will be:
outer func:  this.foo = bar
outer func:  self.foo = bar

inner func:  this.foo = undefined
inner func:  self.foo = bar

The reason is that in the first function the scope is related to the object and the object has a property this,
and in the anonymous function is not happening, the 'self' var was previously declared so the function can access it,
but 'this' is not defined in the anonymous function scope.


3. What is the significance of wrapping the entire content of a JavaScript source file in a function block?

The answer is because of the scopes, when you wrap all the content of a library or a module in a function block you create a 
closure and this will create a namespace for this block, you can avoid name clashes.


4. What will the code below output to the console and why?
```javascript
 (function(){
    return typeof arguments;
  })();
```

It is returning the type of arguments property and it is 'object', 
arguments are referred to the ones passed to the anonymous function,
but it is not doing a print to the console.


5. What will the code below output to the console and why?
```javascript
  var foo = {
    bar: function() { return this.baz; },
    baz: 1
  };
  (function(){
    return typeof arguments[0]();
  })(foo.bar);
```

It will not output anything to the console,
It will output an undefined,
because of the anonymous function, foo.bar it is using as the first argument for the function
and because of the scope 'this' is not working, if you use call the function directly with 'foo.bar()' inside
the anonymous function it will return 1.


6. What will the code below output to the console and why?
```javascript
  var x = 1;
  if (function f(){}) {
    x += typeof f;
  }
  x;
```

It will output a result '1undefined',
because in the if statement you are verifying if the function is declare, so it is because you are declaring it right there.
the seconde, you are doing a sum, but first 1 is a Number but it is doing an automatic casting from Number to String
because of the 'typeof f' return value, it is a string so it is doing a concatenation.


7. What will the code below output to the console and why?
```javascript
/^(ab)$/.test('(ab)')
/^aa|bb$/.test('aaxx')
```

It will return false and true,
the first one because of the parenthesis, on the regex you are telling it that the only string that matches the word inside the parentheses but 
not including the parentheses,
the second one needs that 'aa' is for the first two letters or 'bb' for the last two letters


8. What is `use strict` used for?

You use it because of many things,
the first one is to tell javascript to throw some exceptions, that in normal functionality it will not do,
the second one is to optimize,
and the third one is that you can not assign a new value to a var that is has not been defined globally


9. Rewrite the following code as Ecmascript Arrow Function
```
var double = function (i) {
  return i * 2;
};
```
The function:
```
var double = (i) => {
    return i * 2;
}
```

10. Using the following code
    ```
    
    function Logger(level){
        this.level = level
    }
    
    Logger.prototype.log = function(msg){
        console.log(this.level + ' ' +msg)
    }
    ```
    
    print to the console the text: `INFO Message`
    
var logger = new Logger('INFO');
logger.log('Message');


11. Explain the difference between classical inheritance and prototypal inheritance.

The prototypal inheritance is used in javascript, it is a dynamic language and it has no classes (until now) like other languages as C++ or java.
The difference is that you can do a prototype inheritance on any object that is available on javascript, you can inherite properties or functions.
In javascript the classes are treated as objects and any object has a link to its own prototype. Almost any object in javascript are instances from the 
object 'Object'.

So if you try to access a property from a member and it is not declared on the object itself, it will go and look at his prototype link.


