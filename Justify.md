Your task in this Kata is to emulate text justification in monospace font. You will be given a single-lined text and the expected justification width. The longest word will never be greater than this width.

Here are the rules:

    Use spaces to fill in the gaps between words.
    Each line should contain as many words as possible.
    Use '\n' to separate lines.
    Gap between words can't differ by more than one space.
    Lines should end with a word not a space.
    '\n' is not included in the length of a line.
    Large gaps go first, then smaller ones: 'Lorem---ipsum---dolor--sit--amet' (3, 3, 2, 2 spaces).
    Last line should not be justified, use only one space between words.
    Last line should not contain '\n'
    Strings with one word do not need gaps ('somelongword\n').

Example with width=30:

Lorem  ipsum  dolor  sit amet,
consectetur  adipiscing  elit.
Vestibulum    sagittis   dolor
mauris,  at  elementum  ligula
tempor  eget.  In quis rhoncus
nunc,  at  aliquet orci. Fusce
at   dolor   sit   amet  felis
suscipit   tristique.   Nam  a
imperdiet   tellus.  Nulla  eu
vestibulum    urna.    Vivamus
tincidunt  suscipit  enim, nec
ultrices   nisi  volutpat  ac.
Maecenas   sit   amet  lacinia
arcu,  non dictum justo. Donec
sed  quam  vel  risus faucibus
euismod.  Suspendisse  rhoncus
rhoncus  felis  at  fermentum.
Donec lorem magna, ultricies a
nunc    sit    amet,   blandit
fringilla  nunc. In vestibulum
velit    ac    felis   rhoncus
pellentesque. Mauris at tellus
enim.  Aliquam eleifend tempus
dapibus. Pellentesque commodo,
nisi    sit   amet   hendrerit
fringilla,   ante  odio  porta
lacus,   ut   elementum  justo
nulla et dolor.


/**
 * @param {String} str - inital string
 * @param {Number} len - line length
 */
var justify = function(str, len) {
	var arrayOfWords = str.split(' ');
	var lines = [];

	while (arrayOfWords.length > 0) {
		var line = [];
		var length = -1;
		while (arrayOfWords.length > 0 && length + arrayOfWords[0].length < len) {
			var word = arrayOfWords.shift();
			line.push(word);
			length += word.length + 1;
		}
		var spaces = line.length - 1;

		var each = 1;
		var head = 0;
		if (len - length > 0 && arrayOfWords.length>0) {
			each += ~~((len - length) / spaces);
			head = (len - length) % spaces;
		}
		lines.push(line
			.map(w=> w + (head-->0?' ':''))
			.join(' '.repeat(each)));
	}
	
	return lines.join('\n');
};

Best Solution

/**
 * @param {String} str - inital string
 * @param {Number} len - line length
 */
function justify(str, len) {
  var words = str.split(' ');
  var lines = [];
  var lastLine = words.reduce(function(line, word) {
    if (line) {
      if (line.length + word.length + 1 <= len)
        return line + ' ' + word;
      lines.push(line);
    }
    return word;
  });
  lines = lines.map(function(line) {
    if (line.indexOf(' ') >= 0)
      for (var lineLen = line.length; lineLen < len; )
        line = line.replace(/ +/g, function(spaces) {
          return spaces + (lineLen++ < len ? ' ' : '');
        });
    return line;
  });
  lastLine && lines.push(lastLine);
  return lines.join('\n');
}

Best solution #2

/**
 * @param {String} str - inital string
 * @param {Number} len - line length
 */
var justify = function(str, len) {
  var words = str.split(' ');
  var output = [];
  while (words.length){
    // Collect as many words as possible for the current line
    var lineWords = [];      
    while (words.length>0 && (lineWords+','+words[0]).length <= len)
      lineWords.push(words.shift());

    if (words.length){  // No last line, so justify it
     // Compute the holes between the words
     var spaces = len - (''+lineWords).length;
     for (var i=0; i<spaces; i++)
       lineWords[i % (lineWords.length-1)] += ' ';
    }

    // Build the line
    output.push(lineWords.join(' '));
  }

  return output.join('\n');
};