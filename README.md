# CEF_Utility
This is a lightweight utility library which creates dynamic GUI pages on the CEF (Chromium Embedded Framework) using the HtmlRenderer framework in Dyalog V.17. This allows for cross-platform compatible GUI pages (Pages generated will be displayed on Windows and Mac OS platforms -- hopefully Linux with V.17.1) To run this, all you need is Dyalog Version 17. You can download the files using acre desktop. Which can be downloaded for free by clicking [here](https://github.com/the-carlisle-group/Acre-Desktop/releases/tag/v5.0.0.074) 

Each folder in this repository represents a namespace in the workspace. #.CEF_Utility.UserFunctions are where the userfunctions are stored for use. Each one of these functions creates a dynamic page given your input. These functions can be used in any one of your functions to prompt for user response, or to simply display some information. There are three classes of functions that are provided:

  * Queries
  * Notifications
  * Graphics
  
  
The goal of each function is to produce a single graphical page. If we called a query function, the function will wait for the user input and then return the information about their response. The specific response returned will be documented by a function by function basis below. Notification pages will not wait for a response, because no response is needed. A simple dialog box is shown to the users. Graphical pages can return references to update the visuals on the page. These pages will not wait for a response either. 

These functions are designed with minimal styling. All these functions take one, optional left argument that is the result of the ‘specifyParams’ function. Use this function to further describe how you want your page styled and other details about the page. 

## UserFunctions Reference

⎕IO is 0 

Parameters enclosed with ‘{}’ are optional arguments.

### PARAMETER FUNCTIONS:

∇ specifyParams ∇

R ←specifyParams args

- R is a namespace containing fields that can be set. The namespace has the following properties
	-	CSS
	-	Coord
	-	Header
	-	JavaScript
	-	Posn
	-	Size
	-	Title

- Args can be defined as key/value pairs. With the key being a defined property in the namespace (see list above) and the value being the value you wish to populate that property with. Examples:

      R← specifyParams (‘Title’ ‘myTitle’)(‘Size’ 30 30)
      R.CSS← 'body{background-color:blue}'
      
R can be universally passed to any functions below as a left argument. This includes Queries, Notifications, and Graphics. All the user functions are limited to only one optional argument, and that argument is the result of the specifyParams function. 

### QUERIES:

∇ AskYesNo ∇

R← {p} AskYesNo msg

- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is the result of the function. R is an Integer. 
  - ¯1 : Page was aborted. The page was closed before a response was submitted. 
  -  0 : ‘No’ was selected
  -  1 : ‘Yes’ was selected
- Msg is the question you wish to ask the user. 

∇ PickDate ∇

R←{p} PickDate labels

- P is the namespace result of the ‘specifyParams’ function. P is optional.  
- R is the result of the function. R is the date returned selected by the User. This date is returned in the 'YYYY-MM-DD' format. R is ¯1 if the page was closed before a response was submitted. R is Character, unless the page was aborted then an Integer ¯1 is returned.  The length of R is equal to the length of labels. 
- Labels is a list of labels that will precede each date picker object. Labels can be a vector of items or a single item. The function will enclose labels by default if there is only one item, so it is treated as a single string, and not an array of characters. 

∇ PromptTextInput ∇

R← {p} PromptTextInput labels

- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is the result of the function. R is the response the user has entered and submit into each text input. R is Character, unless the page was aborted then an Integer ¯1 is returned. The length of R is equal to the length of labels.
- Labels is a list of labels that will precede each text input box. Labels can be a vector of items or a single item. The function will enclose labels by default if there is only one item, so it is treated as a single string, and not an array of characters. 

∇ SelectMultipleCheckbox ∇

R← {p} SelectMultipleCheckbox labels
- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is the result of the function. R is indices of the responses selected. If no response is submitted, then ¯1 is returned. R is Integer.  The length of R is equal to the length of labels.
- Labels is a list of labels that will follow each checkbox. Labels can be a vector of items or a single item. 

∇ SelectOneDropdown ∇

R← {p} SelectOneDropdown options	
- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is the result of the function. R is index of the response selected. If no response is submitted, then ¯1 is returned. R is Integer.  The length of R is 1. 
- Options is a list of options to populate the dropdown list with. Only one can be selected.

∇ SelectOneRadio ∇ 

R ← {p} SelectOneRadio options
- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is the result of the function. R is index of the response selected. If no response is submitted, then ¯1 is returned. R is Integer.  The length of R is 1. 
- Options is a list of options that will follow each radio button.

### NOTIFCATIONS:

∇ NotifyError ∇ 

R ← {p} NotifyError msg
- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is non-existent right now. No result is currently returned. May change this to return a shy result 
- Msg is the message you want displayed in the dialog box. This is a dialog box with a red background and white text color. 

∇ NotifyInfo ∇

R ← {p} NotifyInfo msg

- P is the namespace result of the ‘specifyParams’ function. P is optional.  
- R is nonexistent right now. No result is currently returned. May change this to return a shy result 
- Msg is the message you want displayed in the dialog box. This is a dialog box with a blue background and white text color. 

∇ NotifySuccess ∇

R ← {p} NotifySuccess msg
  * P is the namespace result of the ‘specifyParams’ function. P is optional.  
  * R is nonexistent right now. No result is currently returned. May change this to return a shy result 
  * Msg is the message you want displayed in the dialog box. This is a dialog box with a green background and white text color. 

∇ NotifyWarning ∇

R ← {p} NotifyWarning msg

- P is the namespace result of the ‘specifyParams’ function. P is optional.  
- R is nonexistent right now. No result is currently returned. May change this to return a shy result 
- Msg is the message you want displayed in the dialog box. This is a dialog box with an orange background and white text color. 

### GRAPHICS:

∇ DisplayProgressBar ∇

R← {p} DisplayProgressBar start max

- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- R is namespace containing a ‘setProgress’ function which takes a single integer value which will update the progress bar. 
- Start is the starting value of the progress bar.
- Max is the maximum value of the progress bar. 

## GUI Reference

Inside #.CEF_Utility.UserFunctions is a namespace called 'GUI'. In it is a GUI that helps you build more customized forms. Leveraging the functions in the #.CEF_Utility.UserFunctions.HtmlFormBuilder class, you can build forms with multiple types of input. For example, you can add text fields, date pickers, radio buttons, styling, etc. and capture the result which returns a HtmlFormBuilder object in the namespace, called 'FormObj'. You can then pass this object, along with a form size, to the renderPage function and use it to generate a custom page.
To access these functions from the GUI namespace: 

##.specifyParams

##.##.Utils.renderPage

∇ renderPage ∇

R ← {p} renderPage (size)(FormObj)
- P is the namespace result of the ‘specifyParams’ function. P is optional. 
- Size is a 2 item numeric vector of the Y and X values, respectively, that the form should be displayed at. Note that Coord is set to 'Prop' by default, but this could of course be changed by specifying so in p. 
- FormObj is an HtmlFormBuilder object. If you created a form from the GUI then there will be in object in your GUI namespace called 'FormObj'. You can simply pass this as an argument, or any valid HtmlFormBuilder object. 



