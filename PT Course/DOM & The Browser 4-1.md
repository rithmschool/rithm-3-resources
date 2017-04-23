# Rithm PT(4/1): DOM & The Browser

## Objectives

* How the web works
* Selectors: class, id, direct child, distant child
* Modifying the DOM
* Handling browser events
 
-----

* Get request just gives us back HTML
* Sees HTML and slowly makes the DOM, building nodes line by line
* When you reach a script tag, code is immediately executed


```html
<ul class="firstul">
	<div>
		<li> 111 </li>
	</div>
</ul>

css

.firstul li { }
vs
.firstul > li { }			

// the > is saying to only look for direct descendants of the ul class firstul 
```

* Difference between ID and Classes
	* ID's are globally unique
		* Can select them in CSS using '#'
	* Classes can be used multiple times
		* Can be selected using '.'

* Wrapping your JS in a callback function is a way to solve loading JS on page 

`getElementByID`: returns a reference to the element by its ID

`getElementsByClassName`: returns an array-like object of all child elements which have all of the given class names

`querySelector`: returns first element in the document that matches the specified group of selectors

`querySelectorAll`: gives you an array of things that match that selector	

```javascript
DOM Exercises .js file:

document.addEventListener("DOMContentLoaded", function(){

var ul = document.getElementsByClassName("secondul") //getElementsByClassName returns an array like object, so if we just want to append one item in that array, we need to specify the index
var li = document.createElement("li")
var text = document.createTextNode("Dawgs");
li.appendChild(text);
ul[0].appendChild(li);

var myButton = document.querySelector('#clearli');
  myButton.addEventListener('click', function(){
    var myLIs = document.querySelectorAll('li');
    myLIs.forEach(function(li){
      li.remove();
    })

    //Alternative Option
      for(var i = 0; i < myLIs.length; i++){
       myLIs[i].remove(); 
		}
  });

});

```

Here is how `forEach` works under the hood: 

```javascript
forEach(array, callback) {
	for(var i = 0; i < array.length; i++){
		callback(array[i], i, array)
		}
	}
```		