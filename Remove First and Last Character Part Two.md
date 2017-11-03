This is a spin off of my first Kata, you are given a list of characters as a comma separated string. Write a function to return a string containing all except the first and last characters, separated by spaces. If the input string is empty, or the removal of the first and last items would cause the string to be empty, return null value.

Arrays are joined by adding a single space between each consecutive array element.

function array(arr) {
    arr = arr.split (',');
    arr.shift();
    arr.pop();
    arr = arr.toString().replace(/,/g, ' ');
   return arr.length < 1 ? null : arr;
}

Best Solution

function array(arr){
  return arr.split(",").slice(1,-1).join(" ") || null;
}

Best solution #2

function array(arr){
var data = arr.split(',');
data.pop()
data.shift();
return data.length ? data.join(' ') : null;
}