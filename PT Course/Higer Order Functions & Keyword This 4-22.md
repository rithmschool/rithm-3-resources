# Higher Order Functions & 'This' 4/22

### For loop vs For Each:
* Rule of thumb: If you are looping over a string stick with a for loop, it is likely more efficient

* Imperative programming: docus on how we get there, step by step procedure, breaking down piece by piece

* Declarative programming: concerned with getting what you need, usually results in less pieces of code, but it is more complex

* Every declarative always has some imperative; you abstract the imperative so you can give an an simple answer

### Higher Order Functions:
* ForEach - undefined
* Filter - []
* Map - []
* reduce: :)
* some - boolean
* every - boolean
* find
* findIndex

## Imperative vs Declarative
```javascript
var arr = [1,2,3,4,5]

Imparative
for( var i = 0; i< arr.legnth; i++) {
console.log(arr[i])
}

Declarative
arr.forEach(function(val){
console.log(val)
})

another example:

//Return new array [2,4,6,8,10]
Imperative
//Side affect: mutates the original array
for(var i = 0; i <arr.length; i++){
arr[i] *= 2
}


Declarative
// Pure function, it creates a new array
arr.map(function(val){
return val * 2
})
```

## forEach
```javascript
[].forEach(function(val, index, array){
// iterate through an array
// run a callback for each value in the array
// returns undefined (return value is ALWAYS undefined bc function does not have a return keyword)
}

example:
function each(arr,callback){
// iterate through an array
	for(var i = 0; i < arr.length; i++){
// run a callback for each value in the array
	callback(arr[i])
	}
	return undefined;
}

each([1,2,3]), console.log)
//1
//2
//3

// Very easy to mutate a forEach function and thus it is not often considered not a pure function
```
## Each
```javascript
//For example:
newArr = []
each(arr, function(val){
newArr.push(arr.val * 2)
}
// mutates the array each time that you run this function

function map(arr, callback){
//Make a new array
var newArr = [];
//Iterate through the array
for(var i = 0; i < arr.length; i++){
//Push the result of the callback being run on each value
//into the new array
newArr.push(callback(arr[i], i , arr))
}
//return the new array
return newArr;

// when you map over an array, you will ALWAYS get back an array with the same length

[1,2,3,4,5,6].map(function(val){

// return val % 2 !== 0; (more declarative approach)
if(val %2 !==0){
	return val;
	}
})
// returns [1,3,5]
// this will only give you the truthy values because the falsey values are undefined and filter with remove these out of the return value


//Function Composition: chaining our functions together
var doNotChangeMe = [1,2,3,4]
.map(map(map(doNotChangeMe, function(val){
return val * 10
}), function(val) {
return val * 10
)}, function(val) {
return val * 10
)}
// 1000, 2000, 3000, 4000
```
## Filter
```javascript
[1,2,3,4].filter(function(){
	//ALWAYS be evaluated to a BOOLEAN
		// if(true -> add it to a new array
		// otherwise....move along
}

function filter(arr, callback){
	var newArr = [];
	for (var i = 0; i < arr.length; i++){
		if(callback(arr[i])){
			newArr.push(arr[i])
		}
		return newArr;
	} 
}
//returns undefined

example:
var doNotChangeMe = [1,2,3,4]
filter(map(doNotChangeMe, function(val)
return val * 10
}), function(val){
return val < 30
})
//returns 10,20
```

```javascript
[1,2,3,4,5].some(function(val){
	return val < 5
})
// true

vs 

[1,2,3,4,5].every(function(val){
	return val < 5
})
// false

function some (arr, callback){
	//Return a boolean
	for(var i = 0; i < arr.length; i++){
		//check to see if the callback returns true
		if(callback(arr[i]) === true){
			return true;
			}
		}
	//If there are no elements in the array....that satisfy the 	callback (which we assume will return true or false)
		return false;
}


function every (arr, callback){
	for(var i = 0; i < arr.length; i++){
		if(callback(arr[i]) === false){
			return false;
			}
		}
		return true;
	}
```

```javascript
[1,2,3,4,5,6].find(function(val){
return val === 6
}
//6

function find(arr, callback){
	//iterate through the array
	for(var i = 0; i < arr.length; i++){
		//run the callback on the value in the array
		if(callback(arr[i]) === true){
			// if it is true, return the value in the array
			return arr[i]
		}
	}
}

function findIndex(arr, callback){
	//tells you where the value is in the array
	for(var i = 0; i < arr.length; i++){
		//run the callback on the value in the array
		if(callback(arr[i]) === true){
			// if it is true, return the index, otherwise return -1
			return i
		}
	}
		return -1;
}
```
## Reduce
* Can reduce any collection into any data type

```javascript
['Elie','Tim','matt'].reduce(function(previousValue, nextValue){
	//accumulate or build up something
	//whatever you return to the callback, will be the next value in 	//following interation
	return previousValue + ' ' + nextValue;
}, '')
// returns "Elie Tim Matt"

//depending on what starting value is, you can mutate value of what you are reducing

function reduce(array, callback, initialValue){
	// see if there is an initial value
	// is there a third parameter passed to this function? If there isn't, that is what the need for the 'i++' in our if statement
	// If that isn't there, we end up having arr[0] used as both the previous and next value
	var accumulator = initialValue === undefined ? undefined : initialValue

for(var i = 0; i < arr.length; i++){
	if(accumulator === undefined){
		i++
		accumulator = arr[0]
	}
	accumulator += callback(accumulator, arr[i], i, arr)
	}
	return accumulator;
}
```
## This
* Its value gets determined at function exectution
* 4 ways to determine value:
 - Global: think of this as the window object, when keyword 'this' is not inside a parent object, it will always refer to global object
 
 ```javascript
 function determineThis(){
 	return this;
 	
 	//if function is not inside a parent object, keyword this will always refer to the window
 	//"Use Strict" mode will throw errors when you write sloppy code and help us avoid making mistakes in JS
 ```
 - Implicit: when it is inside a function and that function is inside a parent object. This refers to the parent object

 ```javascript
	var obj = {
		name: "Elie",
		info: function(){
			return this
		}
	obj.info() === obj // true
	
	var instructor = {
		firstName: "Elie",
		lastName: "Schoppik",
		fullName: function(){
			return this.firstName + " " + this.lastName
		}
	}
	
	instructor.FullName() // "Elie Schoppik"
 ```
 
 - Explicit: call, apply, bind (all methods that can be accessed on functions). When you want control over what the value of keyword 'this' is
 
  ```javascript
	var instructorOne = {
		firstName: "Elie",
		SayHi: function(){
			return "Hello " + this.firstName
		}
	}
	// this refers to instructorOne, returns Hello Elie
	
	var instructorTwo = {
    firstName: "Matt",
    sayHi: function(){
        return "Hello " + this.firstName
    }
}
 ```
 ## Call, Apply, Bind
 ```javascript
	call(thisArg, a,b,c  ): invoke function right away
	apply(thisArg,[a,b,c] ): invoke function right away
	bind(thisArg, a,b,c) : returns a new function
	
	instructorOne.sayHi.call(instructorTwo) // hello Matt
	instructorOne.sayHi.apply(instructorTwo) // hello Matt
	
	var instructorOne = {
	firstName: "Elie",
	addNumbers: function(a,b,c){
		return this.firstName + " adds " + (a+b+c);
	}
}

	var instructorTwo = {
    firstName: "Matt"
    }
    //we want to borrow addNumbers function from instructorOne for instructorTwo
    
    Bad Way
    instructorOne.addNumbers.call(instructorTwo) //returns Matt adds NaN because we never passed in parameters for addNumbers
    
    Good Way
    instructorOne.addNumbers.call(instructorTwo,1,2,3)
    instructorOne.addNumbers.apply(instructorTwo,[1,2,3])
    
    callMeLater= instructorOne.addNumbers.bind(instructorTwo, 1) // returns new function you can assign as a new variable
    
    //when you invoke bind, you dont have to specify your parameters
    //This is great when you don't know all of your parameters, you can invoke your code later on in the function. This is the idea of partial application. You partially call the function.   
 ```
 
```javascript
	Use case for bind:
		
	var obj = {
	    firstName: "Elie",
	    sayHiLater: function(){
	        setTimeout(function(){
	            console.log("Hello " + this.firstName)
	        }.bind(this),1000)
	    }
	}
	
	//.bind(this) --> refers to obj. Forces this.firstName to also bind to obj
	
	obj.sayHiLater() // Hello Elie
	
	
	function bind (fn, thisArg){
		//takes arguments array like object and turns it into an array (aka Array.prototype)
		var outerArgs = [].slice.call(arguments, 2)
		return function(__){
			var innerArgs = [].slice.call(arguments)
			fn.apply(thisArg, outerArgs.concat(innerArgs))
		}
	}
	
	example:
	
	function add(a,b){
		return a + b;
	}
	
	bind(add, this, 1)(2) // 3
```

 - New

