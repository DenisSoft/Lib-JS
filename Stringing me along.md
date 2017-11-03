Create a function that will allow you to pass in a string, with the ability to add to this with more function calls. When it is finally passed an empty argument return the full concatinated string of all arguments pased previously.

For example: createMessage("Hello")("World!")("how")("are")("you?")();

This will return the following: "Hello World! how are you?"

function createMessage() {
    var string = arguments[0] || '';
    return function f(){
        string += arguments[0] ? " " + arguments[0] : '' ;
        return  arguments[0] ?  f : string;
    }
}

Best Solution

function createMessage(str) {
    return function(next){
      if (next === undefined) {return str;}
      return createMessage(str + " "+ next);
    }
}

Best solution #2

let createMessage = (msg) => m => m? createMessage(msg+' '+m) : msg ;

Best solution #3

function createMessage(s) {
  var parts = []
  var f = (s) => s ? (parts.push(s), f) : parts.join(" ")
  return f(s)
}