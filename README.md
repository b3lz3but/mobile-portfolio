## Running Instructions

1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

2. Open a browser and visit localhost:8080
3. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok http 8080
  ```

4. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

### Part 1: Optimize PageSpeed Insights score for index.html

#### What needs to be done?

1. Identify and perform optimizations to achieve a PageSpeed score above 90 on index.html.

#### What did I do?

1. Prevented render blocking JS by making analytics.js async.
2. Prevented render blocking CSS by using media type "print" to print.css.
3. Set Google Fonts to load directly using @font-face.
4. Used grunt-uncss plugin to remove unused css from style.css.
5. Minifed style.css using grunt-contrib-cssmin plugin.
6. Optimized style.css delivery by making it to inline CSS in index.html.
7. Copied pizzeria.jpg to pizzeria100w.jpg and changed its width to 100px.
8. Optimized pizzeria 100w.jpg and profilepic.jpg using the online tool [Optimizilla](http://optimizilla.com/).
9. Minified perfmatters.js using grunt-contrib-uglify plugin.
10. Minified index.html using grunt-contrib-htmlmin plugin.

#### References:

1. [Website Performance Optimization Course](https://www.udacity.com/course/website-performance-optimization--ud884-nd)
2. [Google Fonts using @fontface in your .css](https://coderwall.com/p/5vrdkg/google-fonts-using-fontface-in-your-css)
3. [How to get all font variations for font-face](http://stackoverflow.com/questions/25011533/google-font-api-uses-browser-detection-how-to-get-all-font-variations-for-font)

### Part 2: Optimize Frames per Second in pizza.html

#### What needs to be done?

1. Time to resize pizzas is less than 5ms in pizza.html shown in the browser console.
2. Identify and perform optimizations ensuring a consistent frame rate at 60fps when scrolling in pizza.html.

#### What did I do?

1. Optimized pizza.png and pizzeria.jpg using the online tool [Optimizilla](http://optimizilla.com/).
2. Used grunt-uncss plugin to remove unused css from style.css and bootstrap-grid.css (after this I realized that .mover was removed so I had to add it manually) and moved everything to style.css.

#### For the Pizza Resize Part:

1. Found that determineDx, changePizzaSizes and resizePizzas functions in main.js were making FSL.
2. Removed determineDx function, moved sizeSwitcher logic inside changePizzaSizes and used percentages instead of pixels.
3. Created variables to accomplish DRY.
4. Moved variables outside loops to prevent constant calling or creation.

#### For the 60 FPS on Scroll:

1. Found that updatePositions functions was making FSL.
2. Created a new variable named scrolledTop that handles document.body.scrollTop outside the "for" loop for preventing to be called each time.
3. Set var phase outside the "for" loop to prevent variable creation each time.
4. FSL was gone :) but still having FPS below 60.
5. Realized there was a lot of Painting so, decided to put will-change: transform on the .mover class (because it handles the pizza.png images on the background), job done.
6. Created variables to hold the length outside "for" loops.
7. Reduced the number of pizzas to be shown based on the browser's height.
8. Moved var elem outside the loop, to prevent constant creation.
9. Minifed style.css using grunt-contrib-cssmin plugin.
10. Optimized style.css delivery by making it to inline CSS in pizza.html.
11. Minified main.js to main.min.js using grunt-contrib-uglify plugin.
12. Minified pizza.html using grunt-contrib-htmlmin plugin.

#### Other main.js tasks:

1. Changed querySelectorAll to getElementsByClassName due to its speed.
2. Changed querySelector to getElementById due to its speed.

### Other notes:

1. Inside the main.js file you can find more details of what I did.

#### References:

1. [Browser Rendering Optimization Course](https://www.udacity.com/course/browser-rendering-optimization--ud860-nd)
2. [getElementsByClassName VS querySelectorAll](https://jsperf.com/getelementsbyclassname-vs-queryselectorall/18)
3. [getElementById vs. querySelector](https://jsperf.com/getelementbyid-vs-queryselector/11)

#### Other References in General:

1. [Grunt Tutorial](https://www.youtube.com/watch?v=zfzUH9Keu1s&list=PLpP9FLMkNf55_LqrPuSUxcs84bMvQiPD8)
