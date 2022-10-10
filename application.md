# Cro Metrics Experiment Engineer Application

Thanks for your interest in working with us! To apply:

- Create a new *secret* gist (link in github header once you're logged in) with the Raw Text of this .md file (**do not fork this gist**). Please name your gist `application.md` so that it's formatted correctly (not a .txt file)
- Answer the following questions in the spaces provided respond to the email that linked you here with a link to your gist.
- Once we receive your submission and all looks well, we’ll reach out for next steps. If you have any questions / concerns about the process please reach out to joshua.sperry@crometrics.com. We're happy to address anything before you apply.
- One last note, this is a new version of our gist and you're lucky enough to be one of the first to try it out!  If you come across anything that doesn't make sense, or if you find yourself spending more than 90 minutes completing the exercise, please reach out to joshua.sperry@crometrics.com.  We're constantly experimenting with our processes and would love to hear any feedback that you might have.

---

For questions 1-4, consider the following HTML:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <style>
            [data-color="red"] { color: red; }
            [data-color="blue"] { color: blue; }
            [data-color="green"] { color: green; }
            [data-color="orange"] { color: orange; }
            [data-color="purple"] { color: purple; }
        </style>
        <script>
            window.myHandler = () => {
                console.log("Click!");
            };

            window.getRandomNumber = (max) => {
                return Math.floor(Math.random() * max);
            };

            const colors = ["red", "blue", "green", "orange", "purple"];
            window.changeHeadlineColor = (croHeadline) => {
                const colorIndex = window.getRandomNumber(colors.length);
                const newColor = colors[colorIndex];
                const newTimeoutMillis = window.getRandomNumber(5000);

                setTimeout(() => {
                    croHeadline.setAttribute("data-color", newColor);
                    window.changeHeadlineColor(croHeadline);
                }, newTimeoutMillis);
            };
        </script>
        <script defer>
            ////////////////////
            /* YOUR CODE HERE */
            ////////////////////
        </script>
    </head>
    <body>
        <div id="myDiv">OMG Click me!</div>
        <script>
            const myDiv = document.querySelector("#myDiv");
            myDiv.addEventListener("click", window.myHandler);

            const newTimeoutMillis = window.getRandomNumber(5000);
            setTimeout(() => {
                myDiv.insertAdjacentHTML("beforebegin", `<h1 id="cro-headline" data-color="red">Cro Metrics</h1>`);

                const croHeadline = document.querySelector("#cro-headline");
                window.changeHeadlineColor(croHeadline);
            }, newTimeoutMillis);
        </script>
    </body>
</html>
```

## Handling Clicks

**Question 1:**

What would you write in the `YOUR CODE HERE` section to **_add a new click handler_** to the `#myDiv` element? 

The handler should use `console.log()` to tell us something interesting about your development background, for example:

`console.log("I know FORTRAN lol long story");`.

Your response:
```javascript
window.onload = function(){
    document.getElementById("myDiv").addEventListener("click", ()=>{
        console.log("Hi, I am Fullstack Developer and waiting to hear from CROmetrics Front-End Engineering Application");
    })
```

---

**Question 2:**

Rewrite your solution to Question 1. Make sure your `console.log()` executes every time a visitor clicks `#myDiv`, but **_do not add a new handler_** and retain the original behavior. Monkey patching is acceptable.

Your response:
```javascript
var _myHandler = window.myHandler;
                window.myHandler = function() {
                _myHandler();
                console.log('In college, I taught myself PHP...');
                }
```

---

## Modifying an element

**Question 3:**

Write code in `YOUR CODE HERE` that changes the Cro Metrics headline text with another string of your choosing. 

Your response:
```javascript
function updateText() {
    if (document.getElementById('cro-headline')) {
        const title = document.querySelector("#cro-headline");
        title.innerHTML = "Test"
    } else {
      window.requestAnimationFrame(updateText);
    }
  }
  updateText();
```

---


**Question 4:**

Write code in `YOUR CODE HERE` that logs the current and previous values of the data-color attribute on the #cro-headline element each time that the attribute changes.  Your log statement should look something like this:  
```console.log(`Current color: ${currentColor} | Previous Color: ${previousColor}`);```

Your response:
```javascript
function displayColorName(){
    if (document.getElementById('cro-headline')) {
        var element = document.querySelector('#cro-headline');
        setTimeout(function() {
          element.getAttribute('data-color');
        }, 5000)
        
        let initColor = "red"
        var observer = new MutationObserver(function(mutations) {
          mutations.forEach(function(mutation) {
            if (mutation.type === "attributes") {
           console.log(`Current color: ${element.getAttribute('data-color')} | Previous Color: ${initColor}`)
           initColor = element.getAttribute('data-color')
            }
          });
        });
        
        observer.observe(element, {
          attributes: true //configure it to listen to attribute changes
        });
    }
    else {
        window.requestAnimationFrame(displayColorName)
    }
}
displayColorName()
```

## Regex fu

**Question 5:**

Our client, chairdelivery.com, is launching a test on all product pages. Write a JavaScript function that takes in a URL, evaluates the URL for a regex match, and returns true or false depending on whether or not the URL matches your regex string.  

The first 3 URLs passed into your function should return true, and the last 4 URLs should return false.

Your code should look something like this example:
```javascript
const myRegexFunction = (url) => {
  // Your code here
}

// Should return true
console.log(`1 - ${myRegexFunction("www.chairdelivery.com/weekly-chair-delivery/")}`);
console.log(`2 - ${myRegexFunction("www.chairdelivery.com/daily-chair-delivery/")}`);
console.log(`3 - ${myRegexFunction("www.chairdelivery.com/chair-of-the-month-club/")}`);

// Should return false
console.log(`4 - ${myRegexFunction("www.chairdelivery.com/")}`);
console.log(`5 - ${myRegexFunction("www.chairdelivery.com/?some_param")}`);
console.log(`6 - ${myRegexFunction("www.chairdelivery.com/about/")}`);
console.log(`7 - ${myRegexFunction("www.chairdelivery.com/contact-us/")}`);
```

Your response:
```javascript
/(www.chairdelivery.com)(\/)(.*(chair).*)(\/)/
```

---

## Stylin'

**Question 6:**

Share a link to an original CodePen/JSFiddle that implements this:

![Boxes with hover animation](http://uploads.crometrics.com/7P8x/4F9VmEDq.gif)

Don't worry about pixel perfection; just eyeball it.

Your response:
```javascript
https://codepen.io/samk12323/pen/jOxQGXj
```

---

## jQueryin'

**Question 7:**

How could you improve the following code?  Be sure that you don't change any functionality.

```javascript
$(document).ready(() => {
  $(".foo #bar").css("color", "red");
  $(".foo #bar").css("border", "1px solid blue");
  $(".foo #bar").text("new text!");
  $(".foo #bar").click(function() {
    $(this).attr("title", "new title");
    $(this).width("100px");
  });

  $(".foo #bar").click();
});
```

Your response:
```javascript
let $fooBar = $('.foo #bar');         
                    $fooBar.css({                         
                    'color' : 'red',
                    'border' : '1px solid blue'
                    })
                    .text('new text!');                   
                    $fooBar.click(function() {
                    $(this).attr('title', 'new title')
                        .width('100px');               
                    });
            $fooBar.click();
```

Re-write your solution using plain JavaScript:
```javascript
var x = document.querySelector('.foo #bar');
            x.style.color="red";
            x.style.border="1px solid blue";
            x.innerHTML="new text!";
            x.addEventListener("click",()=>{
                x.setAttribute('title', "new title")
                x.setAttribute("width","100px")
            })
```


---

## Behaviors

**Question 8:**

What code could run before the following statement that would make it evaluate to true?

```javascript
"bc".prefix("a") === "abc";
```

Your response:
```javascript
String.prototype.prefix = function(preString) {
    return preString + this;
};
"bc".prefix("a") === "abc" ===> This will return True
```
