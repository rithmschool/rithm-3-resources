# Rithm 3/25 JS Fundamentals


## Truthy vs Falsey Values in JS

```
function truthyTest(val){
    if(val){
        return "truthy!"
    } else{
        return "falsey"
    }
}
```

Besides finite list below, everything else in JS is "truthy"

#### Falsey values:

* 0
* null
* NaN
* Undefined
* False
* " "


```javascript
function addWithDefaults(a,b){
    a = a || 10;
    b = b || 10;
    return a + b;
}


addWithDefaults(12,6) //returns 18
addWithDefaults(0,0) //returns 20 (rather than '0' due to falsey value of '0')

```

```javascript
if (person.hometown === undefined){
	console.log("it's undefined!")
	}
```		

```javascript
"4" === 4 //returns false b/c one is a string & one is a num, strict equals operator does not allow conversion between types
```

```javascript
true == 1 //returns true bc true gets converted to a number
```

* Double equals allows for type conversion
* Triple equals checks value & type	

```javascript
[] == [] // returns false bc it is asking if some array in memory is equal to maybe to a similar array stored in diff memory
```
### Arrays

Instance where two arrays could be equal:

```javascript
	var arr = [1,2,3];
	var arr2 = [1,2,3];
	var arr3 = arr;

	
	Where arr3 = arr

 //returns true since arr3 is pointing to arr. whatever you do to one will also change the other if they both point to same array. Arrays and objects are called reference types bc you are assigning references to certain values in memory

```	
passing by value vs passing by reference ** look this up more**

```javascript
var letters =["a","b", "c", "d"]
function addTo(arr,val){
    arr.push(val)
    return arr
}

other soln:

function addTo(arr,val){
    return arr.concat(val)
}

//original array does not mutate when using concat or slice, second soln would be more functional

//slice can also take two arguments, first arg takes the index you start from, second argument tells you how long you want to slice for; slicing w/ neg # will slice from end of array

letters.spice(4,0,"e") // will return [], and add "e" after index 4

letters.splice(-1,1)[0]

spice(num1,num2) // first arg is starting index, second arg is how many items to remove; always will return an array of what is removed

//push returns the length of the new array, we then want to return the new length of the array
```


### Array Mutations

|  | Front   | Back | What it returns |
--- | --- | --- | --- | 
| **Add**   | unshift | push | returns length
| **Remove** | shift | pop | returns removed value

`letters.join("-")` --Join takes an array and converts to a string with "-" by using the .toString() method and places the dash between each item in the array

`letters.split("b")` --Will take a string and return an array on each use of the string "b"

```javascript
var arr = ["a", "b", "c"]

arr.indexOf("a") //returns 0
arr[0] // returns "a"
arr.indexOf("d") //returns -1

arr.includes("d") //returns false

//how would you find indeces of multiple values in same array

//Using *While* loops may be more advantageous over for loop when you don't know how long you have to iterate
```

```javascript
function pirateCount(str){
    var arr = str.split("");
    var count = 0;
    for(var i=0;i< arr.length;i++){
        if(arr[i].toLowerCase() ==="r"){
            count++
        }
    }
    return count;
}

vs.

function pirateCount(str){
    var count = 0;
    for(var i=0;i< arr.length;i++){
        if(str[i].toLowerCase() ==="r"){
            count++
        }
    }
    return count;
}

"hello".splice(0,2) 

//returns TypeError --> can't mutate a primative datatype, they are immutable

//If you want to mutate the string, you can turn it into a string, mutate the array and then convert it back or...


var name = matt
var FormalName = name[0].toUpperCase() + name.slice(1)
formalName //returns Matt
```

* Difference between [] & dot notation:
 expression you pass in will get evaluated first in bracket notaion vs in dot notation

##### Undestanding difference:

```javascript
obj.newkey = 'value 1' //no evaluation happening, you are assining new value to the key

obj[newKey] = 'value 2' //evaluating a variable, finding a variable and then assinging that new value to that variable's key

obj['newkey'] = 'value 3' //reassigning value for the key 'newKey'
```

* To remove a key from an object, you can use the 'delete' keyword

when trying to loop through objects:

`for(var key in obj){
	console.log(key + ": "+ obj[key])
} //will log the key + value`


You can check to see if a key exists in an object a few diff ways:

"name" in obj // 'in' keyword will check and will return a boolean value to you

```javascript
object.keys(obj).indexOf("name")
//returns an index, if not -1, you will know that it exists, but not reccomended option
```

### Reg expressions

"Elie".match(/[aeiou]/gi)

## Higher Order Functions

```javascript
function higherOrderFunction(cb){
	cb();
	}

function helloWorld(){
	alert("hello world!");
	}

higherOrderFunction(helloWorld)

typeOf(helloWorld) // returns undefined, function does not return anything so implicitly a function that does not return anything becomes undefined

[1,2,3,4].map(function(num){
	return 2* num;
	})
	//returns [2,4,6,8] function which itself returns another function and ; pure function that does not mutate the original array
	
function customMap(arr,callback){
	var newArr=[];
	for(var i=0; i <arr.length; i++){
		newArr.push(callback(arr[i]))		
		}
	}		
	
//stack, heap and queue
//heap holds async code
//setTimeout sends things to queue 

###Closure

When a function si able to access variables from an outer function that has already returned.

```javascript
function outer() {
	var myFavoriteNumber = 10;
	return function inner(){
		return "My favorite number is: " + myFavoriteNumber;
	}
}

//inner function preserves access to variables that were in the outside scope even though the outer function has already run
```

### Hoisting
```javascript
function example(){
	console.log(name);
	var name = "Topher"
	}
	
what is happening:

function example(){
	var name;
	console.log(name);
	name = "Matt"
	}	
```	
	