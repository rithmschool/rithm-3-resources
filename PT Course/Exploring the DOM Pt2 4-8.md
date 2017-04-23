* When using querySelector, you will need to include the actual element you are selecting (ie if selecting an 'id', need to include the '#')

* difference between using `children` and `childnodes` when wanting to get the elements inside another

* Alternatively can use `document.querySelectorAll` to get all of the child nodes

* Difference between DOMContentLoaded and window.onload

* window.onload waits for all assets to load, so it can be slower if you have a lot of assests. DOMContentLoaded just cares about the structure of the DOM

* `Math.floor` will always round down to the nearest whole number

* When trying to access an index on jQuery object, cannot use bracket notation, instead you can use `.eq()`

```javascript
Vanilla JS
document.addEventListener('DOMContentLoaded', function(){

  var container = document.querySelector(".container");

  container.style.color = "#A4B107";

  //This works
   var list1 = document.getElementById("list1");
   var list1Items = list1.children;

  for(var i = 0; i < list1Items.length; i++) {
    list1Items[i].style.fontSize = Math.random() * 50 + "px"
  }

  //This also works!
  var list2Items = document.querySelectorAll("#list2 li");

  for(var i = 0; i < list2Items.length; i++){
    list2Items[i].addEventListener('click', function(e){
      e.target.classList.toggle('clicked')
    });
  }

var btn1 = document.getElementById("btn1");
var btn2 = document.getElementById("btn2");

btn1.addEventListener('click', function(){
  var randomColor = getRandomColor();
  var body = document.querySelector('body');
  body.style.backgroundColor = randomColor;
  });

btn2.addEventListener('click', function(){
  container.innerHTML = '';
});

function getRandomColor(){
    var hexDigits = "0123456789ABCDEF"
    var hexCode = "#"
    for(var i = 0; i < 6; i++){
      var randomIdx = Math.floor(Math.random() * hexDigits.length)
      hexCode += hexDigits[randomIdx]
    }
    return hexCode;
  }
});

```

### 4 Common Requests
* Get
* Post
* Patch/Put: edit something
* Delete

* Can issue requests from command line using `curl` command