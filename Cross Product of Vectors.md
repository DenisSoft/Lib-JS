Make a function called crossProduct that takes two 3 dimensional vectors (in the form of two arrays) and returns their cross product. You need to check if the passed arguments are of the expected format, otherwise throw the message: "Arguments are not 3D vectors!".

crossProduct([1,0,0],[0,1,0]) //should return [0,0,1]
crossProduct('gobbledigook', [1,1,1]) //should throw the string "Arguments are not 3D vectors!"

Your function should handle non integers.

function crossProduct(a, b) {
    if (arguments.length < 2 ||
        isNaN(parseInt(a[0])) || isNaN(parseInt(a[1])) || isNaN(parseInt(a[2]))
        || isNaN(parseInt(b[0])) || isNaN(parseInt(b[1])) || isNaN(parseInt(b[2]))) {
        throw ('Arguments are not 3D vectors!');
    }
    return [a[1] * b[2] - a[2] * b[1], a[2] * b[0] - a[0] * b[2], a[0] * b[1] - a[1] * b[0]];
}

Best Solution

function crossProduct (vector1, vector2) {
  if (!(vector1 instanceof Array) || !(vector2 instanceof Array) || vector1.length !== 3 || vector2.length!==3) {
    throw "Arguments are not 3D vectors!"
  }
  
  return [(vector1[1]*vector2[2] - vector2[1]*vector1[2]), (vector1[2]*vector2[0] - vector2[2]*vector1[0]), (vector1[0]*vector2[1] - vector2[0]*vector1[1])]
}

Best solution #2

function crossProduct (vector1, vector2) {
  if(Array.isArray(vector1) && Array.isArray(vector2)&& vector1.length ===3 && vector2.length ===3) {
     return [ vector1[1] * vector2[2] - vector1[2] * vector2[1], vector1[2] * vector2[0] - vector1[0] * vector2[2], vector1[0] * vector2[1] - vector1[1] * vector2[0] ]; 
  }
  else {
    throw "Arguments are not 3D vectors!";
  }
}