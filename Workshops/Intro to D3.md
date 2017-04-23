#D3
---

* You do not select things in DOM right away, you can select elements that don't exist and then create them after


```javascript
d3.select("body")
  .selectAll("p")
  .data(quotes)
  .enter()
  .append("p")
  .text(function(d) {
    return d;
  });
  
  //enter says go through dom and find mismatch between elements we have in dataset. If p's don't exist, append them
  // we appeneded to the document, the number of quotes that are in our dataset
  // Enter is the thing that creates new <p> tags if they need to be created
  
```


```javascript
d3.select("body")
  .selectAll("p")
  .data(quotes)
  .enter()
  .append("p")
  .text(function(d) {
    return d.quote;
  })
  .style("color", function(d){
    return d.color;
  })
  .style("font-size", function(){
    return (Math.round(Math.random() * 40)+ 60) + " px";
  })

```

```javascript
<svg height="250" width="300">
  <g stroke="black" stroke-width="3">
    <circle cx=55 cy=55 r=50 fill="#006BB6"/>
    <rect x=100 y=100 width=100 height=100 fill="#FDB927"/>
    <triangle x=100 y=100 width=300 height=200 />
  <path d = "M80 150 L80 80 L150 150Z"
    fill= "rgb(0,225,0)"
    stroke="black" />
  </g>
</svg>
```


```
var width = 500;
var height = 500;
var svg = d3.select("svg")
            .attr("width", width)
            .attr("height", height);

var data = [[250, 250], [0, 0], [100, 150], [400, 200], [700, 250]];

var xMin = d3.min(data, function(d) {
  return d[0];
});

var xMax = d3.max(data, function(d) {
  return d[0];
});

var yMin = d3.min(data, function(d) {
  return d[1];
});

var yMax = d3.max(data, function(d) {
  return d[1];
});

var padding = 10;

var xScale = d3.scaleLinear()
               .domain([xMin, xMax])
               .range([padding, width - padding]);

var yScale = d3.scaleLinear()
               .domain([yMin, yMax])
               .range([height-padding, padding]);

svg.selectAll('circle')
  .data(data)
  .enter()
  .append('circle')
  .attr('cx', function(d) { return xScale(d[0]); })
  .attr('cy', function(d) { return yScale(d[1]); })
  .attr('r', function() { return 10; });

```