## Website Performance Optimization portfolio

Project is about optimizing the critical rendering path and make webpage render as quickly as possible.

### How Its Done.

####Part 1: Optimizing PageSpeed Insights score for index.html

The PageSpeed Insight showed problems Mainly in
  * Images Compression.
  * Way of use of Google Fonts API.
  * Render Blocking CSS.
  * Render Blocking JS.
  * Leverage browser caching.

Image compression was done online on [kraken.io](https://kraken.io/web-interface) website.

Google Fonts was used in a different way by directly using fonts in CSS

       @font-face {
              font-family: OpenSans;
              src: url(href="//fonts.googleapis.com/css?family=Open+Sans:400");
              font-weight: normal;
            }
   
 CSS File `print.css` was linked to `index.html` with attribute `media = "print`.
 
 Critical parts of `style.css` was inlined.
 
 Attribute `async` was added to JavaScript used for Analytics.
 
 To experience the web page [Click Here](https://vasudev-ps.github.io/performance-optimization/).
 
####Part 2: Optimizing Frames per Second in pizza.html

To optimize views/pizza.html, modified views/js/main.js so that frames per second rate is 60 fps and Time to resize pizzas is less than 5 ms.

* The Timeline showed Problems while scrolling.
  
  In the function `resizePizzas` the functions `changePizzaSizes` and `determineDx` were causing recalculate style and forced reflow.
  
  so modified these function with.
  
    ` var allPizzas = document.getElementsByClassName("randomPizzaContainer");
      for (i = 0; i < allPizzas.length; i++){
      allPizzas[i].style.width = newwidth + "%";
      }`
      
   which solved the Problem.
   
* The Timeline also highligted Problem while resizing the pizza.

  In the function `updatePositions` the for loop line
  
  `var phase = Math.sin((document.body.scrollTop / 1250) + (i % 5));`
  
   was creating problems. by calculating `document.body.scrollTop / 1250` for every itteration.
   
   Replaced by creating a variable for `document.body.scrollTop / 1250` outside for loop and hence calculating only once.
   
      `var items = document.querySelectorAll(".mover");
       var a = document.body.scrollTop / 1250;
        for ( i = 0; i < items.length; i++){
        phase = Math.sin(a + i % 5),items[i].style.left = items[i].basicLeft + 100 * phase + "px";
        }`

 To experience the web page [Click Here](https://vasudev-ps.github.io/performance-optimization/views/pizza.html).
 
Feel Free to Suggest any more optimization tips.
