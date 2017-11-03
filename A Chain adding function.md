We want to create a function that will add numbers together when called in succession.

add(1)(2);
// returns 3

We also want to be able to continue to add numbers to our chain.

add(1)(2)(3); // 6
add(1)(2)(3)(4); // 10
add(1)(2)(3)(4)(5); // 15

and so on.

A single call should return the number passed in.

add(1); // 1

We should be able to store the returned values and reuse them.

var addTwo = add(2);
addTwo; // 2
addTwo + 5; // 7
addTwo(3); // 5
addTwo(3)(5); // 10

We can assume any number being passed in will be valid whole number.

function add(n){
  var fun = function(x) { 
     return add(n + x); 
  };
  fun.valueOf = function() { 
    return n; 
  };
  return fun;
}

Best Solution

var add = function(n) {
  const f = x => add(n + x)
  f.valueOf = () => n
  return f;
}

Best solution #2

function add(n){
  var sum = n;
  function f (k){
    sum += k;
    return f;
  }
 f.valueOf = function(){return sum}
  return f
}
