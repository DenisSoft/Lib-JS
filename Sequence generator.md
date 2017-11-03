Implement function sequence, which returns new n-size Array filled according to pattern.

pattern may be:

    a function that takes two: (element, index), one: (element) or any arguments (similar to map function), then filled running this function, in other words: function describes sequence,
    number, string or any other object, then filled by copying, this object n-times.

Examples:

sequence(3, 4); // [4, 4, 4]
sequence(5, []); // [[], [], [], [], []]
sequence(2, "s"); // ["s", "s"]
sequence(5, (x, idx) => idx%2) // [0, 1, 0, 1, 0];
sequence(10, (x, idx) => idx+1) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

Note: Sequences are great to work with functional methods like map, reduce, forEach, every or any. For example:

// sum of numbers 1-10
let sum = sequence(10, (x, idx) => idx+1).reduce((sum, num) => sum + num);

function sequence(n, pattern) {
    let result = [];
    pattern = pattern ? pattern :  pattern = null;
    for (let i = 0; i < n; i++) {
        result[i] = typeof(pattern) === "function" ? pattern(n, i) : pattern;
    }
    return result;
}

Best Solution

function sequence(n, pattern) {
  return Array.from({length: n}, typeof pattern === "function" ? pattern : () => pattern)
}

Best solution #2

function sequence(len, fun) {
  return Array.from({length:len}, fun && fun.call ? fun : _ => fun )
}