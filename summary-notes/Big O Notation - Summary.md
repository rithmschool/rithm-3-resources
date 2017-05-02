# Big O Notation

## Defining Big O Notation
Big O Notation is used to measure relative growth rate between two functions to determine which function is more efficient.  The definition of Big O is as follows:  
>f(n) = O(g(n)) if there exits some positive constant C such that f is eventually less than C * g

A few things to note:  

*	Big O is concerned with the general shape of a function (the relative growth rate) rather than any specific values.
* 	The 'n' in the function stands for the input of the function.

There are two rules of Big O:

*	Constants are ignored (because constants can be absorbed into 'n')
*	Smaller components are ignored

Some examples of these rules in play are as follows:

~~~
O(500 * n) --> O(n) //constants don't matter.
O(99999999999) --> O(1) //constants don't matter again - anything which is a number value is equay to O()
O(10* n^2 + 5n + 20) --> O( n^2 ) // O ( n^2 ) is the biggest component and the only one that matters.
O(n * n) --> O(n2) // O (n*n) becomes O ( n^2 )
O(n*log(n) + 30000 * n) --> O(n * log(n))
~~~

Broadly speaking, the order of time complexities by Big O notations are as follows (from fastest to slowest, best to worst):

*	O(1) - constant
* 	O(log n) - logarithmic
*  	O(n) - linear
*   	O(n log n)
*	O( n^2 ) - quadratic
* 	O( 2^n ) - exponential
*  	O(!n) - factorial

For a quick cheatsheet regarding Big O complexities, please see: http://bigocheatsheet.com/.

## Time complexity

Time complexity is the relationship between the number of inputs a function takes and the runtime it takes to compute the response.  Please note when comparing two functions, absolute timing cannot be used to determine which function is more efficient.

### O(1) - constant

This is Big O 1 or constant time.  This occurs where the number of function is constant regardless of the size of the input - runtime will not grow beyond some constant size.

**Example**

~~~javascript
function add(num1, num2, num3) {
   return num1 + num2 + num3;
}
~~~

### O(n) - linear

Algorithm are linear time because the data set is iterated over approximately one time.  As a general first rule, if you see one for loop assume that it is O(n) unless otherwise shown.

**Example**

~~~javascript
function sayHello(numberOfTimes) {
    for (var i = 0; i < numberOfTimes; i++) {
        console.log("Hello");
    }
}
~~~

### O( n^2 ) - quadratic

As a general rule, if you see a nested for loop, it is safe to assume that the Big O notation is  O( n^2 ) unless otherwise shown.

**Example**

~~~javascript
function allPairs(arr) {
    var pairs = [];
    for (var i = 0; i < arr.length; i++) {
        for (var j = i + 1; j < arr.length; j++) {
            pairs.push([arr[i], arr[j]]);
        }
    }

    return pairs;
}
~~~

## Space complexity

Space complexity is the relationship between input size of the function and the amount of allocated of memory that is required.  It follows similar rules in time complexity.

**Example 1**

```function double(array){
    for(var i = 0; i < array.length; i++){
        array[i] = array[i]*2;
    }
}
```
* Memory allocated is none.
* No further memory is allocated therefore is constant O(1).

**Example 2**

```javascript
function double(array) {
    var newArray = [];
    for (var i = 0; i < array.length; i++) {
        newArray.push(2 * array[i]);
    }
    return newArray;
}
```
*  Memory for a new array is allocated.
*  The length of the new array is based on the length of the input array, therefore worst case is the size of the array:  O(n).

_Note:_ both above algorithms have the same **time complexity** but different **space complexity**.