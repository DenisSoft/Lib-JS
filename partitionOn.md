Write a function which partitions a list of items based on a given predicate.

After the partition function is run, the list should be of the form [ F, F, F, T, T, T ] where the Fs (resp. Ts) are items for which the predicate function returned false (resp. true).

NOTE: the partitioning should be stable; in other words: the ordering of the Fs (resp. Ts) should be preserved relative to each other.

For convenience and utility, the partition function should return the boundary index. In other words: the index of the first T value in items.

For example:

var items = [1, 2, 3, 4, 5, 6];
function isEven(n) {return n % 2 == 0}
var i = partitionOn(isEven, items);
// items should now be [1, 3, 5, 2, 4, 6]
// i     should now be 3


function partitionOn(pred, items) {
  var result = 0;
  for(var item in items) {
    if(!pred(items[item])) {
      items.splice((result++), 0, items.splice(item, 1)[0]);
    }
  }
  return result;
}

Best Solution

function partitionOn(pred, items) {
  var f = items.filter( function(e) { return !pred(e); } ); 
  var t = items.filter(pred); 
  items.length = 0;
  for(var i = 0; i < f.length; i++) { items.push(f[i]); }
  for(var i = 0; i < t.length; i++) { items.push(t[i]); }
  
  return f.length;
  
}

Best solution #2

function partitionOn(pred, items) {
  var truthies = items.filter(pred);
  var falsies = items.filter(function (a) {return !pred(a)});
  items.length = 0;
  items.push.apply(items, falsies.concat(truthies));
  return falsies.length;
}