knockout-x-editable
===================

knockout binding handler for x-editable - See **http://vitalets.github.com/x-editable**

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

will set editable options value (value of firstName) and name to firstName. Your observable is updated to the new value in the save event (you can also pass your own save event that gets called after).

##Advanced
You can pass through any editable options with: 
```html
<span data-bind="editable: firstName, editableOptions: {name: 'first', pk: id, url: '/save'}"></span>
```

Note the pk can be an observable since x-editable just calls it as a function.
The option editableOptions.visible can be passed an observable, this sets the x-editable toggle to 'manual', then uses the observable to fire the 'show' method

###select, checklist and typeahead options
For select and checklist, you can pass options just as you would to knockout:
```html
<span data-bind="editable: gender, editableOptions: {pk: id, options: genders, optionsText: 'text', optionsValue: 'id'}"></span>
```

For select only, you can also pass in the `valueUpdate` option (see http://knockoutjs.com/documentation/value-binding.html):
```html
<span data-bind="editable: comment, editableOptions: { /* ... */, valueUpdate: 'keyup'}"></span>
```

optionsCaption is used to set editable.prepend

###knockout.validation
If you are using knockout.validation, I have wired up a call to the observable's isValid for editable.validate. To work, this has to push the new value into the observable, then validate, then revert back. If you have subscribed to changes, you will see them. Not the best choice, but works. 
