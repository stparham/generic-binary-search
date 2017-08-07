# Generic Binary Search
It really surprised me that there wasn't already a built-in binary search function for the Array in JavaScript, so with some help from Google and Stack Overflow (it's been a while since I wrote a binary search algorithm from scratch), I wrote this code snippet.

The snippet adds a generic binary search function to the JavaScript Array prototype.  The function takes a value to find as the first parameter and a comparator function as the second parameter.  The comparator works just like it would for Array.prototype.sort function.

You can load the bin-search.js file alongside your own files or just copy and paste the function somewhere in your code.

I wrote some tests for the examples below, but I'll try to add some more edge case ones as well.  Please let me know if you come across some unexpected behavior.

*There are probably a few steps that I could take to improve the performance of the algorithm, but I haven't looked into it too heavily yet.  This [SO answer](https://stackoverflow.com/a/29018745) suggests that recursion is excessive and unnecessary in a binary search algorithm, but I used it anyway because recursion is cool and it was used when I was first taught about binary search.*

## The basic number array example
---
If you need to search an array of numbers super quickly, here you go.
```
var arr = [1, 4, 98, 101, 888];

function myComparator(a, b) {
  return a - b; // this is how the cool kids compare numbers
}

var idx = arr.binarySearch(101, myComparator);
console.log(idx); // 3
idx = arr.binarySearch(204, myComparator);
console.log(idx); // -1
```

## Comparing strings
---
Since you are in charge of the comparison code, you can search whatever kind of array you want to search.
```
var arr = ["apple", "banana", "kiwi", "orange", "starfruit"];

function myComparator(a, b) {
  if (a == b) return 0;
  if (a > b) return 1;
  return -1;
}

var idx = arr.binarySearch("banana", myComparator);
console.log(idx); // 1
idx = arr.binarySearch("turnip", myComparator);
console.log(idx); // -1
```

## Comparing two different types
---
You can even make a comparator function that compares two different things (like a string and object).  Imagine you're trying to find an object that has a particular string as its ```name``` property.  You can just pass the string in as the value to find because you can do whatever you want in the comparator!  Any and all arrays will tremble at your uncanny ability to traverse them at O(log(n)) speeds!
```
var arr = [
  {
    "name": "Dat Boi",
    "info": {}
  },
  {
    "name": "Dis Boi",
    "info": {}
  },
  {
    "name": "Mad Boi",
    "info": {}
  },
  {
    "name": "Oh Boi",
    "info": {}
  },
  {
    "name": "Ya Boi",
    "info": {}
  }
];

// comparator function
function myComparator(nameToFind, arrObj) {
  if (nameToFind == arrObj.name) return 0;
  if (nameToFind > arrObj.name) return 1;
  return -1;
}

var idx = arr.binarySearch("Ya Boi", myComparator);
console.log(idx); // 4
idx = arr.binarySearch("That Dude", myComparator);
console.log(idx); // -1
```
