#ES 2015
------------

### Let
```javascript
for(var i = 0; i < 5; i++){
	setTimeout(function(){
		console.log(i)
	}, 1000*i
}

// returns 5 printed 5x
// would the numbers 1-5 printed instead due to setTimeout
// setTimeout is an example of an async function 
// The for loop has already run before the setTimeout function can run. The for loop is blocking the setTimeout from running.

//This can be solved by changing var to let so:

for(let i = 0; i < 5; i++)

//You would not be able to access the 'i' keyword outside of the block due to scoping 
```
* When using the keyword `let`, you are creating a block scope. Code block is defined as in between `{ }`

### Constants
* Cannot take the value of a constant and redefine it
* When you manipulate one object, but it has reference to another object, you change the other (passing by reference)


```javascript
object.assign({}, {name:"Elie"}, {job:"instructor"})

If you want to create a brand new object with a brand new reference in memory, you have to:

var tim = Object.assign({}, elie)
tim.name = "Tim" // "Tim"

elie.name // "Elie"

function assign(obj1,obj2){
	var blankObj = {}
	
	for(var key1 in obj1){
		blankObj[key1] = obj[key1]
	}
	
	for(var key2 in obj2){
	blankObj[key2] = obj[key1]
	}
	return blankObj
}
```
* Good way of making copies of objects and being able to assign them to different keys and passing them in as a reference without changing the value

* We can do this similarly with arrays by using `slice` to make copies of an array

### Arrow Functions
```javascript
Pre ES2015 way of defining functions:

function declaration(){}

var expression = function(){}
```

```javascript
[1,2,3,4].map(function(val){
	return val*2
	}

ES2015 Version:	
[1,2,3,4].map(v => v * 2)	
```

* When you use arrow functions you don't get the keyword `this` or using arguments
* This means that if you are using the keyword `this` in an arrow function, it tries to find the most recent parent element


* if the key and value are same name, javascript will evaluate them both as the same thing

### Spread(Rest) Operator

```javascript
	function AddElieToArguments(){
		var args = Array.from(arguments)
		args.push("Elie")
		return args
	}
	
	//previously array.prototype.slice.call(arguments)
	//taking the array protype, using call to copying it (using slice), you are doing this on the arguments array
```
* Array.from will convert array like objects into an array. In this case, it converts arguments into an array to allow us to add the string elie to args

```javascript
function AddElieToArguments(...args){
	return args.concat("elie")
	}

addElieToArguments(1,2,3) // [1,2,3, "Elie"]	
	
	//nice for getting the rest of the arguments if you are using multiple arguments in a function. You are speading out all of the values you want passed through your function
```

```javascript
function add(a,b){
	return a + b
}
```

### Default Arguments

```javascript
function sum(a,b){
	a = a || 5;
	b = b || 5;
	return a + b;
}
//this doesn't work because if you invoke sum(0,0) you get 10. "0" is not falsey value

//Better way of doing this with default args:

function sum(a = 5,b= 5){
	a = a || 5;
	b = b || 5;
	return a + b;
}
```

### Template Strings

```javascript
var firstName = "Elie"
var lastName = "Schoppik"

ES5
"Hi " + firstname + " " + lastName

ES2015
`Hi ${firstName} ${lastName}`
```

### Exponentiation operator

```javascript
ES5
Math.pow(4,10) // 1048567

ES2016
4**10 // 1048567
```

### Includes

```javascript
[].includes
[1,2,3,4].includes(3) //true
```

### Async Functions
```javascript
function movieData(){
var movieData = await $.getJSON("https....")


console.log("first")
moviedata()
console.log("second")

//returns code asynchronously, but if you use the await keyword, it will run as if it is synchronous
```
* Asynchronous code: code that does not block
* To manage async code you can use `.then`
* By detault they will always return a promise to you. If you use the keyword `await`, your code will wait, as if it reads synchronously, so on the next line you can do the nex operation