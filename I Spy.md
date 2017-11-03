In testing, a spy function is one that keeps track of various metadata regarding its invocations. Some examples of properties that a spy might track include:

    Whether it was invoked
    How many times it was invoked
    What arguments it was called with
    What contexts it was called in
    What values it returned
    Whether it threw an error

For this kata, implement a spyOn function which takes any function func as a parameter and returns a spy for func. The returned spy must be callable in the same manner as the original func, and include the following additional properties/methods:

    .callCount() — returns the number of times spy has been called
    .wasCalledWith(val) – returns true if spy was ever called with val, else returns false.
    .returned(val) — returns true if spy ever returned val, else returns false

Below is a specific example of how spyOn might work in the wild.

function adder(n1, n2) { return n1 + n2; }
var adderSpy = spyOn( adder );

adderSpy(2, 4); // returns 6
adderSpy(3, 5); // returns 8
adderSpy.callCount(); // returns 2
adderSpy.wasCalledWith(4); // true
adderSpy.wasCalledWith(0); // false
adderSpy.returned(8); // true
adderSpy.returned(0); // false


function spyOn(func) {
  let count = 0;
  let arr = [];
  let result;
  let spy = function (...args) {
     count++;
     arr.push(...args);
     result = func(...args);
     return result;
  }    
  spy.callCount = () => count;
  spy.wasCalledWith = (x) => arr.indexOf(x) != -1;
  spy.returned = (x) => x === result;
  return spy;
}
          
 Best Solution
 
function spyOn(func) {
  let calls = 0
  let all = []
  let val
  
  const spy = function(...args) {
    calls++
    all.push(...args)
    val = func.apply(this, args)
    return val
  }
  
  spy.callCount = () => calls
  spy.wasCalledWith = (x) => all.some((a) => x === a)
  spy.returned = (x) => x === val
  
  return spy
}
  
Best solution #2

function spyOn (func) {
  var callVals  = [],
      returnVals = [],
      callCount = 0;
  function spy () {
    ++callCount;
    callVals = [].concat.apply(callVals, arguments);
    var val = func.apply(this, arguments);
    returnVals.push(val);
    return val;
  };
  spy.callCount = function () { return callCount; };
  spy.wasCalledWith = function (val) { return callVals.indexOf(val) > -1; };
  spy.returned = function (val) { return returnVals.indexOf(val) > -1; };
  return spy;
};   

