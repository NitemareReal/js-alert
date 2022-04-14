# js-alert2
A simple JavaScript alert manager.

#### Changes in this fork: ####
#### v1.0.5 ####
* Clicking outside the dialog doesn't dismiss the dialog
* Buttons only react when clicked with left button
* Solved a legacy dependency problem in package.json


## Use from the browser

The simplest way to use from the browser is to include the minified script:

``` html
<script src="https://unpkg.com/js-alert2/dist/jsalert2.min.js"></script>
```


## Use from Node

To use this library in your node web app, first install the dependency:

```
npm install --save js-alert2
```

Then you can use it in your project:

``` javascript
var JSAlert2 = require("js-alert2");
```


## Usage examples

See all tests [here](https://rawgit.com/jjv360/js-alert/master/tests.html).

``` javascript
// Show a plain alert
JSAlert2.alert("This is an alert.");
```

``` javascript
// Show an alert with a title and custom dismiss button
JSAlert2.alert("Your files have been saved successfully.", "Files Saved", "Got it");
```

``` javascript
// Show multiple alerts (alerts are automatically queued)
JSAlert2.alert("This is the first alert.");
JSAlert2.alert("This is the second alert.");
JSAlert2.alert("This is the third and final alert.");
```

``` javascript
// Automatically dismiss alert
JSAlert2.alert("This will only last 10 seconds").dismissIn(1000 * 10);
```

``` javascript
// Event when dismissed
JSAlert2.alert("This one has an event listener!").then(function() {
    console.log("Alert dismissed!");
});
```

``` javascript
// Show a confirm alert
JSAlert2.confirm("Are you sure you want to delete this file?").then(function(result) {

    // Check if pressed yes
    if (!result)
        return;
    
    // User pressed yes!
    JSAlert2.alert("File deleted!");

});
```

``` javascript
// Create an alert with custom buttons
var alert = new JSAlert2("My text", "My title");
alert.addButton("Yes").then(function() {
    console.log("Alert button Yes pressed");
});
alert.addButton("No").then(function() {
    console.log("Alert button No pressed");
});
alert.show();
```


## Building the library

To create a minified build of this library, run this:

```
npm run build
```

A built version of the library will be saved to the dist folder.
