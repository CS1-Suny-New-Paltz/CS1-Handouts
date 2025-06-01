# String Javadoc

There are quite a few additional methods on the String class, but these are the ones that are going to be relevant this semester. Feel free to print out a copy of this to add to your quiz notes\!

`int length()` \- returns the number of characters (letters) in the String

`boolean equals(String otherString)` \- returns true if the two Strings are equal, false otherwise

`char charAt(int index)` \- returns the letter at the provided (0-indexed) position in the String

`int indexOf(String toFind)` \- returns the starting index of toFind in the String, or \-1 if toFind is not in the String. If toFind occurs multiple times, this returns the **first** instance

`int indexOf(String toFind, int startIndex)` \- similar to the 1-parameter toFind, but starts looking from startIndex instead of the beginning of the String. Note that startIndex is **inclusive**; if you're looping through a String to find every instance of `toFind`, you'll want to increment the previously-found index by 1

`String substring(int startIndex, int endIndex)` \- returns the piece of the String from startIndex up to, but not including, endIndex. Useful mnemonic: substring(0, someNumber) returns the first someNumber letters in the String.

`String replace(char original, char replacement)` \- replaces all instances of 'original' with 'replacement'. Note that this takes in a single char; there are similar methods (such as replaceAll) that use **regular expressions**, which we haven't covered and can cause surprising behavior

`String toUpperCase()` \- returns a version of this String with all letters converted to uppercase

`String toLowerCase()` \- returns a version of this String with all letters converted to lowercase

`String trim()` \- returns a version of this String with any whitespace (spaces, tabs, newlines) removed from the beginning and end (but not middle) of the String.

## Character Javadoc

Much like Integer, Character is a class with a number of **static** methods. All these methods can be called as Character.\<name of method\> (ex: `Character.isDigit(ch)`).

`static boolean isDigit(char ch)` \- returns true if the character is a digit from 0-9

`static boolean isLetter(char ch)` \- returns true if the character is a letter from a-z or A-Z

`static boolean isUpperCase(char ch)` \- returns true if the character is **both** a letter and is uppercase

`static boolean isLowerCase(char ch)` \- returns true if the character is **both** a letter and is lowercase  
 