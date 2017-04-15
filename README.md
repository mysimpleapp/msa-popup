# msa-popup
MySimpleApp component to create popups.

## CLIENT API

### Function: MsaPopup.createConfirm
From: `msa-popup.html`

This function creates a popup asking a question, and allowing user to respond.

![Example](/doc/confirm.png)

```javascript
// Simple example
MsaPopup.createConfirm("Are you sure ?", function(){
    console.log("You confirmed to be sure.")
})

// Complex example
// You can also benefits from all MsaPopup.create arguments
MsaPopup.createConfirm("Are you sure ?", {
  onConfirm: function() {
    console.log("You are sure.")
  },
  buttons: [{
    text: "Yes, I am !",
    act: "confirm"
  }]
})
```

* __MsaPopup.createConfirm__: `Function(text [, args]) -> popup`
  * __*text__: `String`, text that will appear on the popup.
  * __args__: `Function()` or `Object`
    * if  `Function` : used as callback if user confirmed the question.
    * if `Object` : same as __MsaPopup.create__'s one, with some additional properties:
      * __onConfirm__ : `Function()`, callback when user confirm the question.
      * __buttons[].act__ : other possible value is `"confirm"`.
  * __popup__ : `DOM Element`, returned created popup.

### Function: MsaPopup.createInput
From: `msa-popup.html`

This function creates a popup allowing user to fill an input.

![Example](/doc/input.png)

```javascript
// Simple example
MsaPopup.createInput("Give me your name:", function(name){
    console.log("Your name is:", name)
})

// Complex example
// You can also benefits from all MsaPopup.create arguments
MsaPopup.createInput("What is your birthday:", {
  input: {
    type: "date",
    style: { color: "red" }
  },
  onInput: function(date) {
    console.log("Your birthday is:", date)
  },
  buttons: [{
    text: "OK",
    act: "input"
  }]
})
```

* __MsaPopup.createInput__: `Function(text [, args]) -> popup`
  * __*text__: `String`, text that will appear on the popup, before the input.
  * __args__: `Function(value)` or `Object`
    * if  `Function` : used as callback if user validated the input.
    * if `Object` : same as __MsaPopup.create__'s one, with some additional properties:
      * __input__ : `Object`, used to update input DOM element.
      * __onInput__ : `Function(value)`, callback when user validates the input.
      * __buttons[].act__ : other possible value is `"input"`.
  * __popup__ : `DOM Element`, returned created popup.

### Function: MsaPopup.create
From: `msa-popup.html`

This function creates a generic popup.

![Example](/doc/generic.png)

```javascript
// Simple example
MsaPopup.create("my-webcomponent")

// Complex example
var el = document.createElement("div")
MsaPopup.create(el, {
  onCancel: function() {
    console.log("User canceled popup.")
  },
  onClose: function() {
    console.log("bye bye !")
  },
  buttons: [{
    text: "OK",
    act: function() {
      console.log("User clicked on OK.")
    }
  },{
    text: "Cancel",
    act: "cancel"
  }]
})
```

* __MsaPopup.createConfirm__: `Function(el [, args]) -> popup`
  * __*el__: `String` or `DOM Element`, element from which the popup will be created.
    * if `String` : tag name from which the element (and popup) will be created.
    * if `DOM Element` : the element will be changed into a popup (without cloning).
  * __args__: `Object`, the possible properties are:
    * __onCancel__ : `Function()`, callback when user choose to cancel popup.
    * __onClose__ : `Function()`, callback when popup is closed (whatever the choice of the user).
    * __addCloseIcon__ : `Bool`, determines if a close icon is present at the top right of the popup (default: true).
    * __buttons__ : `Array<Object>`, describes the list of buttons of the popup. The possible properties of each object are :
      * __*text__ : `String`, text of the button.
      * __act__ : `String` or `Function()`.
        * if `Function` : callback used when user clicks on button.
        * if `String` : shortcut to predefined callback. Possible value is `"cancel"`.
      * __closePopup__ : `Bool`, determines if popup is closed when button is clocked (default: true).
  * __popup__ : `DOM Element`, returned created popup.

## LICENSE
MIT