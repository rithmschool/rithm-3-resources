# Recursion
## Recursion basics
Recursion is an alternate method to iteration - it is basically running an algorithm by having a function call itself.

Recursion makes use of the callstack to store functions that are then returned in a last in first out (LIFO) structure.

There are two general rules of recursion:

* Every recursive function must have a **base case** - basically when do we stop running the recursive function.  If you don't have a base case you run into stack overflow (which is the recursion version of infinite loops.
*  Every call that you make is working in a different scope - every call that you make can't be the same.  The **input must change everytime**.

### A basic illustration of recursion
Lets take the following function as an example.  

~~~javascript
function factorial(num){
    if (num === 1) {
    	return 1;
    }
    return num * factorial(num - 1);
}

var x = factorial(4);
console.log(x);
~~~
  
  This function is an example of recursion - the factorial function calls itself until the value of num is equal to one in which 1 is returned.

Basically what is happening here is that each function called is being placed in the call stack - once the last one returns - the one previous to it will return etc. etc. until the first function returns.  Imagine a callstack is a series of functions placed in a cup and that cup only starts emptying when it is full (last function returns).

~~~
An illustrated example of the factorial function being returned recursively.
|___f(1)________| f(1) =1
|___f(2)*f(1)___| f(2) = 2
|___f(3)*f(2)___| f(3) = 6
|___f(4)*f(3)___| f(4) = 24

~~~
  
## Other recursion examples
### Fibonacci numbers
Not all recursive functions are efficient, take the following function that solves Fibonacci numbers via recursion:

~~~javascript
function fib(n) {
    if (n <= 2) {
        return 1;
    }
    return fib(n-1) + fib(n-2)
}

fib(5);
~~~
This is an inefficient formula as it relices on a Big O notation of O( 2^n ).

In the future, you will learn about dynamic programming which will me use of advance recursive techniques such as memoization and tabulation that will help solve this problem.

### Palindrome problem (recursive)

~~~javascript
function isPalindrome(string) {
    if(string.length === 0 || string.length === 1) {
        return true;
    }
    if (string[0] !== string[string.length - 1]) {
        return false;
    }
    return isPalindrome(string.substring(1,string.substring-2));
}

isPalindrome("crabby");
isPalindrome("tacocat");
~~~

### Reduce (recursive)

~~~javascript
function reduce(array, callback, acc) {
    if(array.length === 1) {
        if (acc !== undefined) {
            return callback(acc, array[0]);
        } else {
            return array[0];
        }
    }
    return callback(reduce(array.slice(0, array.length -1), callback, acc), array[array.length-1]);
}

var x = [1,2,3,4,5,6];

function addNumber(acc, value) {
    return acc + value;
}

reduce(x,addNumber);
~~~

## Helper functions

In some recursive functions you need to return values that are held and pushed into an array or assigned a key value pair in an object.  However you run into a problem if you declare new variables in a recursive function.  To avoid this, you can code a helper function into the recursive function to server as a nested function.  See the following syntax.

~~~javascript
function toughRecursiveProblem(input){
    
    var arrayToRemember = [];
    
    function helperFunction(){
        arrayToRemember.push('whatever')
        return helperFunction(smaller input)
    }

    return helperFunction(input)
 }
~~~

An example of a recursive function using a helper function is set out below.

~~~javascript
function fromPairs(array){
	var holdingObj = {};
	function helper(array) {
		if (array.length === 0) {
			return;
		}
		holdingObj[array[0][0]] = array[0][1];
		array.shift();
		return helper(array);
	}
	helper(array);
	return holdingObj;
}
~~~