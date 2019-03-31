Given a credit card number we can determine who the issuer/vendor is with a few basic knowns.

Complete the function getIssuer() that will use the values shown below to determine the card issuer for a given card number. If the number cannot be matched then the function should return the string Unknown.

| Card Type  | Begins With          | Number Length |
|------------|----------------------|---------------|
| AMEX       | 34 or 37             | 15            |
| Discover   | 6011                 | 16            |
| Mastercard | 51, 52, 53, 54 or 55 | 16            |
| VISA       | 4                    | 13 or 16      |

Examples

getIssuer(4111111111111111) == "VISA"
getIssuer(4111111111111) == "VISA"
getIssuer(4012888888881881) == "VISA"
getIssuer(378282246310005) == "AMEX"
getIssuer(6011111111111117) == "Discover"
getIssuer(5105105105105100) == "Mastercard"
getIssuer(5105105105105106) == "Mastercard"
getIssuer(9111111111111111) == "Unknown"

Solution 1

function getIssuer(n) {
  var s = n.toString();
  if (/^3[4|7]\d{13}$/.test(s)) return "AMEX";
  if (/^6011\d{12}$/.test(s)) return "Discover";
  if (/^5[1-5]\d{14}$/.test(s)) return "Mastercard";
  if (/^4(\d{12}|\d{15})$/.test(s)) return "VISA";
  return "Unknown";
}

Solution 2

const getIssuer = number => /^3(4|7)[0-9]{13}$/g.test(number) ? "AMEX" : 
  /^6011[0-9]{12}$/g.test(number) ? "Discover" : 
  /^5[1-5][0-9]{14}$/g.test(number) ? "Mastercard" : 
  /^4([0-9]{12}|[0-9]{15})$/g.test(number) ? "VISA" : "Unknown";
  
  Solution 3
  
  function getIssuer(number) {
var num = number.toString();
var num1 = num.substr(0, 2);
var num2 = num.substr(0, 4);
var num3 = num.substr(0, 1);
if ((num1 == '34' || num1 == '37') && num.length == 15) {
  return 'AMEX';
}
else if (num1 >= '51' && num1 <= '55'&& num.length == 16){
  return 'Mastercard';
}
else if (num2 == '6011'&& num.length == 16){
  return 'Discover';
}
else if (num3 == '4' && (num.length == 13 || num.length == 16) ){
  return 'VISA';
}
else {
 return 'Unknown';
}
}
  
  
