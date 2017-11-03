In JavaScript we can create objects using the new operator.

For example, if you have this constructor function:

function Greeting(name) {
  this.name = name;
}

Greeting.prototype.sayHello = function() {
  return "Hello " + this.name;
};


Greeting.prototype.sayBye = function() {
  return "Bye " + this.name;
};

You can create a Greeting object in this way:

  var greeting = new Greeting('John');

new operator is evil because it produces a highly coupled code, difficult to maintain and test.

Some patterns to reduce coupling are object factories or dependency injection.

These patterns can benefit of the construct() function.

This function receives a constructor function and possibly some arguments and it returns a new object constructed with the function and the passed arguments.

This is another way to create the greeting object:

var greeting = construct(Greeting, 'John');

And a factory could use like this:

  function factory() {
    return {
      createGreeting() {
        return construct(Greeting, arguments);
      }
      ...
    }
  }

Your work is to implement the construct() function.

function construct(Class,...arg) {
    return new Class(...arg);
}

Best Solution

function construct(Class /*, args */) {
  var obj = Object.create(Class.prototype);
  Class.apply(obj, Array.prototype.slice.call(arguments, 1));
  return obj;
}

Best solution #2

function construct(Class) {
  return new (Class.bind.apply( Class, arguments ))()
}


