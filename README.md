knockout-x-editable
===================

knockout binding handler for x-editable - See **http://vitalets.github.com/x-editable**

**NOTE: to use the select options, you need my fork of x-editable (http://github.com//brianchance/knockout-x-editable) that allows the list source to be set to a function**

##Simple Usage
**NOTE: set any editable defaults before calling ko.applyBindings**

for a view model:
```javascript
var viewModel = function(){
  var self = this;
  self.id = ko.observable();
  self.firstName = ko.observable();
  self.lastName = ko.observable();
  self.gender = ko.observable();
  
  self.genders = ko.observableArray();
}
```
and binding:
```html
<span data-bind="editable: firstName"></span>
```

will set editable options value (value of firstName) and name to firstName. Your observable is updated to the new value in the save event.

##Advanced
You can pass through any editable options with: 
```html
<span data-bind="editable: firstName, editableOptions: {name: 'first', pk: id, url: '/save'}"></span>
```

Note the pk can be an observable since x-editable just calls it as a function

###Select options
For select, you can pass options just as you would to knockout:
```html
<span data-bind="editable: gender, editableOptions: {pk: id, options: genders, optionsText: 'text', optionsValue: 'id'}"></span>
```

optionsCaption is used to set editable.prepend
