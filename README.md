# js-alert
A simple JavaScript alert manager.

#### Changes in this fork: ####

#### v1.0.9 ####

* Added classes to all items to allow customization
#### v1.0.8 ####

* When an alert is created WITHOUT buttons, "clickOutsideDismiss" behavior is ALWAYS **true** to allow closing the dialog box

#### v1.0.7 ####
* function "clickOutsideDismiss" renamed to "setClickOutsideDismiss" and changed default value to **false**

#### v1.0.6 ####
* Added function "clickOutsideDismiss" to allow changing clicking outside behavior

#### v1.0.5 ####
* Clicking outside the dialog doesn't dismiss the dialog
* Buttons only react when clicked with left button
* Solved a legacy dependency problem in package.json


## Use from the browser

The simplest way to use from the browser is to include the minified script:

``` html
<script src="https://unpkg.com/js-alert2/dist/jsalert.min.js"></script>
```


## Use from Node

To use this library in your node web app, first install the dependency:

```
npm install --save js-alert2
```

Then you can use it in your project:

``` javascript
var JSAlert = require("js-alert2");
```

## Methods

| Static Methods (called on JSAlert class)                                       | Params                        
| ------------------------------------------------------------------------------ | --------
| alert(text, title, icon, closeText)                                            | `string text` The text shown in alert<br>`string title` The title for the alert. Default: ""<br>`null\|boolean\|string icon` Icon for the alert box. If set to **false** no icon is shown, if set to **null**, default (Information) icon is shown. If used as string, it's a base 64 image string. There are some inbuilt icons that can be referenced with a variable (see Icons below). Default: **null**<br>`string closeText` Text for alert box button, default: **Close** 
| confirm(text, title, icon, acceptText, rejectText)                              | `string text` The text shown in alert<br>`string title` The title for the alert. Default: ""<br>`null\|boolean\|string icon` Icon for the alert box. If set to **false** no icon is shown, if set to **null**, default (Question) icon is shown. If used as string, it's a base 64 image string. There are some inbuilt icons that can be referenced with a variable (see Icons below). Default: **null**<br>`string acceptText` Text for alert box 'Accept' button, default: **Ok**<br>`string rejectText` Text for alert box 'Cancel' button, default: **Cancel**
| prompt(text, defaultText, placeholderText, title, icon, acceptText, rejectText) | `string text` The text shown in alert<br>`string defaultText` default value for alert input box. Default: ""<br>`string placeholderText` text shown as alert input box placeholder. Default: ""<br>`string title` The title for the alert. Default: ""<br>`null\|boolean\|string icon` Icon for the alert box. If set to **false** no icon is shown, is set to **null** default (Question) icon is show. If used as string, it's a base 64 image string. There are some inbuilt icons that can be referenced with a variable (see Icons below). Default: **null**<br>`string acceptText` Text for alert box 'Accept' button, default: **Ok**<br>`string rejectText` Text for alert box 'Cancel' button, default: **Cancel** 
| loader(text, cancelable)                                                        | `string text` The text shown in loader box<br>`boolean cancelable` whether the loader box can be closed by user or not

| Methods (called on a JSAlert object)       | Description                       | Params 
| ------------------------------------------ | --------------------------------- | ---
| setIcon(icon)                              | Sets an icon for the alert        | `string icon` either a URL or one of `JSAlert.Icons` strings
| addButton(text, value, type)               | Adds a button. Returns a Promise that is called if the button is clicked | `string text` The button text<br>`string value` The value sent to promise function when button is pressed<br>`string type` Type of the button, e.g: 'cancel', 'normal', 'default'
| addTextField(value, type, placeholderText) | Adds a text field. Returns a Promise that will be called when the dialog is dismissed, but not cancelled. | `string value` The initial value of input control<br>`string type` Type of input control e.g: 'text', 'password', 'checkbox', ...<br>`string placeholderText` placeholder text shown in control
| getTextFieldValue(index)                   |  Gets a text field's value        | `int index` index of input control to get value from
| show()                                     | Shows the alert                   |
| then(func)                                 | A 'then' function, to allow chaining with Promises | `function func` a function to be called when alert is closed
| dismiss(result)                            | Dismisses the alert               | `boolean result` value sent to promise function when closing the alert
| dismissIn(time)                            | Dismisses the alert some time in the future | `int time` milliseconds to wait after dismissing the alert
| setClickOutsideDismiss(value)              | Set behavior when clicking outside alert | `boolean value` if set to **true**, clicking outside the alert box will dismiss the alert box. Default: **false**

## Usage examples

``` javascript
// Show a plain alert
JSAlert.alert("This is an alert.");
```

``` javascript
// Show an alert with a title and custom dismiss button
JSAlert.alert("Your files have been saved successfully.", "Files Saved", null, "Got it");
```

``` javascript
// Show an alert with a title and no icon
JSAlert.alert("Alert with no icon.", "The title", false);
```

``` javascript
// Show multiple alerts (alerts are automatically queued)
JSAlert.alert("This is the first alert.");
JSAlert.alert("This is the second alert.");
JSAlert.alert("This is the third and final alert.");
```

``` javascript
// Automatically dismiss alert
JSAlert.alert("This will only last 10 seconds").dismissIn(1000 * 10);
```

``` javascript
// Event when dismissed
JSAlert.alert("This one has an event listener!").then(function() {
    console.log("Alert dismissed!");
});
```

``` javascript
// Show a confirm alert
JSAlert.confirm("Are you sure you want to delete this file?").then(function(result) {

    // Check if pressed yes
    if (!result)
        return;
    
    // User pressed yes!
    JSAlert.alert("File deleted!");

});
```

``` javascript
// Create an alert with custom buttons and 'Deleted' icon
var alert = new JSAlert("My text", "My title");
alert.addButton("Yes").then(function() {
    console.log("Alert button Yes pressed");
});
alert.addButton("No").then(function() {
    console.log("Alert button No pressed");
});
alert.setIcon(JSAlert.Icons.Deleted)
alert.show();
```

``` javascript
// Create an alert that closes (dismisses) when clicking outside
var alert = new JSAlert("My text", "My title");
alert.addButton("Close", null);
alert.setClickOutsideDismiss(true);
alert.show();
```
## Icons

| Const string              | Icon                                                    |
| ------------------------- |:-------------------------------------------------------:|
| JSAlert.Icons.Information | ![Information](res/Information.svg "Information Icon")  |
| JSAlert.Icons.Question    | ![Question](res/Question.svg "Question Icon")           |
| JSAlert.Icons.Success     | ![Success](res/Success.svg "Success Icon")              |
| JSAlert.Icons.Warning     | ![Warning](res/Warning.svg "Warning Icon")              |
| JSAlert.Icons.Failed      | ![Failed](res/Failed.svg "Failed Icon")                 |
| JSAlert.Icons.Deleted     | ![Deleted](res/Deleted.svg "Deleted Icon")              |
## Building the library

To create a minified build of this library, run this:

```
npm run build
```

A built version of the library will be saved to the dist folder.
