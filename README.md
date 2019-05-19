# Treemap-Diagram

*A simple treemap layout*

This is an app that allows you to create a treemap layout for your data.


...

**Home Page**

<img src="/TreeMap.PNG" title="home page" alt="home page" width="500px">

---


## Table of Contents 

> Sections
- [Sample Code](#Sample_Code)
- [Installation](#installation)
- [Features](#features)
- [Contributing](#contributing)
- [Team](#team)
- [FAQ](#faq)
- [Support](#support)
- [License](#license)


---

## Sample Code

```javascript
// treemap layout
var url1= "https://cdn.rawgit.com/freeCodeCamp/testable-projects-fcc/a80ce8f9/src/data/tree_map/kickstarter-funding-data.json";
var url2= " https://cdn.rawgit.com/freeCodeCamp/testable-projects-fcc/a80ce8f9/src/data/tree_map/movie-data.json";
var url3= "https://cdn.rawgit.com/freeCodeCamp/testable-projects-fcc/a80ce8f9/src/data/tree_map/video-game-sales-data.json";
var myObj1={};
var myObj2="";
var myObj3="";

var ajax1= $.getJSON(url1,
                   function(par){
                myObj1= Object.assign(par)
                   }
                  );

  var ajax2= $.getJSON(url2,function(par){
    myObj2= Object.assign(par);
});

var ajax3= $.ajax({dataType: 'json',
                   url: url3,
                   success: function(par){
                   myObj3= Object.assign(par);
   
                    }
                  });
  
  $.when(ajax2).done(function(){

    var h=600;
    var w=1000;
 
    const svg= d3.select('body')
                 .append('svg')
                 .attr("height",h)
                 .attr("width",w);
    
    const tooltip= d3.select('body')
                     .append('div')
                     .attr("class", 'tooltip')
                     .attr("id", 'tooltip')
                     .style('opacity',0);
    
    var treeMapLayout= d3.treemap()
                         .size([w,h])
                         .paddingInner(1);
    
    var root = d3.hierarchy(myObj2)
                 .sum(function(d) {
                   return d.value;
                 })
                 .sort(function(a, b) {
                   return b.height - a.height || b.value - a.value;
                   });
    
    treeMapLayout(root);
  //alert(Object.keys(root.leaves()[1]))
    var categories = root.leaves().map(function(par) {
      return par.data.category;
    }); //alert(Array.isArray(categories))alert(categories)
    var categoriesArr=[];
    for(var i=0;i<categories.length;i++){
      if (!categoriesArr.includes(categories[i])){
        categoriesArr.push(categories[i]);
      }
    }

    var legendColors = [
      ["Action", "#4db8ff"],
      ["Adventure", "#b3ecff"],
      ["Comedy", "#ff8533"],
      ["Drama", "#6c71c4"],
      ["Animation", "#00b33c"],
      ["Family", "#99e699"],
      ["Biography", "#ff3333"]
    ];

    var colorFill = function(category){
      for(var i=0; i<legendColors.length; i++){
        if (category == legendColors[i][0]){
          return legendColors[i][1];
        }
      }
    };

    var cell = svg.selectAll("g")
                  .data(root.leaves())
                  .enter()
                  .append("g")
                  .attr("transform", function(d) {
                     return "translate(" + d.x0 + "," + d.y0 + ")";
                   });

     var tile = cell.append("rect")
                    .attr("width", d => d.x1 - d.x0)
                    .attr("height", d => d.y1 - d.y0)
                    .attr("fill", d => colorFill(d.data.category))
                    .attr("data-category", d => d.data.category)
                    .attr("data-name", d => d.data.name)
                    .attr("data-value", d => d.data.value)
                    .attr("class", "tile")
                    .on("mouseover", function(d) {
                      tooltip.transition()
                             .duration(200)
                             .style("opacity", 0.7);
                      tooltip.attr("data-value", d3.select(this).attr("data-value"))
                             .html("<b>Name: </b>" + d3.select(this).attr("data-name") + "</br><b>Category: </b>" + d3.select(this).attr("data-category") + "</br><b>Value: </b>$" + d3.select(this).attr("data-value"))
                             .style("left", d3.event.pageX + 0 + "px")
                             .style("top", d3.event.pageY + 0 + "px");
                     })
    .on("mouseout", function(d) {
      tooltip.transition()
             .duration(200)
             .style("opacity", 0.0);
    });

    cell.append("text")
      .attr("class", "tile-text")
      .selectAll("tspan")
      .data(d => d.data.name.split("/(?=[A-Z][^A-Z])/g"))
      .enter()
      .append("tspan")
      .attr("x", 6)
      .attr("y", (d, i) => 10 + i * 10)
      .text(d => d)
      .style("font-size", 9);    

  var legend = svg.append("g")
                  .attr("class", "legend")
                  .attr("id", "legend");

  legend.selectAll("rect")
        .data(legendColors)
        .enter()
        .append("rect")
        .attr("id", "legend")
        .attr("class", "legend-item")    
        .attr("width", 10)
        .attr("height", 10)
        .attr("x", 15)
        .attr("y", (d, i) => h + i * 15)
        .attr("fill", d => d[1]);

  legend.selectAll("text")
        .data(legendColors)
        .enter()
        .append("text")
        .attr("x", 15)
        .attr("y", (d, i) => h + i * 15)
        .text(d => d[0])
        .style("font-size", 9);
    
    })


```

---

## Installation
## Features
## Usage (Optional)
## Documentation (Optional)
## Tests (Optional)
## Contributing
## Team

> Contributors/People

| [**seansangh**](https://github.com/seansangh) |
| :---: |
| [![seansangh](https://avatars0.githubusercontent.com/u/45724640?v=3&s=200)](https://github.com/seansangh)    |
| [`github.com/seansangh`](https://github.com/seansangh) | 

-  GitHub user profile

---

## FAQ

- **Have any *specific* questions?**
    - Use the information provided under *Support* for answers

---

## Support

Reach out to me at one of the following places!

- Twitter at [`@sean13nay`](https://twitter.com/sean13nay?lang=en)
- Github at [`seansangh`](https://github.com/seansangh)

---

## Donations (Optional)

- If you appreciate the code provided herein, feel free to donate to the author via [Paypal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4VED5H2K8Z4TU&source=url).

[<img src="https://www.paypalobjects.com/webstatic/en_US/i/buttons/cc-badges-ppppcmcvdam.png" alt="Pay with PayPal, PayPal Credit or any major credit card" />](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4VED5H2K8Z4TU&source=url)

---

## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2019 © <a>S.S.</a>
