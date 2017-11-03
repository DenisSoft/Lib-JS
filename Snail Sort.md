Snail Sort

Given an n x n array, return the array elements arranged from outermost elements to the middle element, traveling clockwise.

array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
snail(array) #=> [1,2,3,6,9,8,7,4,5]

For better understanding, please follow the numbers of the next array consecutively:

array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
snail(array) #=> [1,2,3,4,5,6,7,8,9]

This image will illustrate things more clearly:

NOTE: The idea is not sort the elements from the lowest value to the highest; the idea is to traverse the 2-d array in a clockwise snailshell pattern.

NOTE 2: The 0x0 (empty matrix) is represented as [[]]


snail = function(array) {
  var result = [];

  while (array.length>0){
    result = result.concat.apply(result,array.splice(0,1));

    for (var i=0;i<=array.length-1;i++)
    {
      result = result.concat(array[i].splice(array.length));
    }

    var temp = [].concat.apply([],array.splice(array.length-1)).reverse();
    result = result.concat.apply(result,temp);

    for (var i=array.length-1;i>=0;i--)
    {
      result = result.concat(array[i].splice(0,1));
    }
  }
  return result; 
}

Best Solution

snail = function(array) {
  var result;
  while (array.length) {
    // Steal the first row.
    result = (result ? result.concat(array.shift()) : array.shift());
    // Steal the right items.
    for (var i = 0; i < array.length; i++)
      result.push(array[i].pop());
    // Steal the bottom row.
    result = result.concat((array.pop() || []).reverse());
    // Steal the left items.
    for (var i = array.length - 1; i >= 0; i--)
      result.push(array[i].shift());
  }
  return result;
}

Best solution #2

snail = function(array) {
  var res = [];
  while(array.length) {
    res = res.concat(array.shift())
    array = expand(array);
  }
  return res;
}


function expand(matrix){
    return matrix.reduce(function(res, arr, i){
        arr.forEach(function(n, j){
            if (!res[j]) res[j] = [];
            res[j][i] = n;
        })
        return res;
    }, []).reverse();
}