# KoLite
**KoLite** contains a set of helpers to aid in creating MVVM applications using JavaScript and Knockout. Including:

1. asyncCommand
2. activity
3. dirtyFlag

## Current Version
1.0.3

##NuGet
Also available on NuGet at https://nuget.org/packages/KoLite

## Quick start
### asyncCommand 
demo: http://jsfiddle.net/johnpapa/FhLvf/
<pre>
&lt;button data-bind="command: saveCommand">Save&lt;/button>
</pre>
<pre>
self.saveCommand = ko.asyncCommand({
    execute: function(callback) {
        $.ajax({
            complete: callback,
            data: { name: self.name() },
            type: 'POST',
            url: '/save/',
                    
            success: function(result) {
                alert('Name saved:' + result)
            }
        })
    },
        
    canExecute: function(isExecuting) {
        return !isExecuting && self.name()
    }
})
</pre>


### asyncCommand - event other than click
<pre>
&lt;div data-bind="command: {onmouseover: tooltipCommand}">Information&lt;/div>
</pre>



### asyncCommand and activity
<pre>
&lt;button data-bind="activity: saveCommand.isExecuting, command: saveCommand">Save&lt;/button>
</pre>

### dirtyFlag
<pre>
// Your model
var Person = function () {
	var self = this;
	self.id = ko.observable();
	self.firstName = ko.observable().extend({ required: true });
	self.lastName = ko.observable().extend({ required: true });
	self.dirtyFlag = new ko.DirtyFlag([self.firstName,self.lastName]);
	return self;
};
</pre>

Hook these into your viewmodel ...

<pre>

//Property on your view model. myPerson is an instance of Person.
//Did it Change?
isDirty = ko.computed(function () {
	return myPerson().dirtyFlag().isDirty();
}),
</pre>

<pre>
//Resync Changes
dirtyFlag().reset();
</pre>



## Depends on
&gt;= jQuery 1.4.4

&gt;= KnockoutJS 2.0.0



## Authors

**Hans Fjällemark**

+ http://twitter.com/hfjallemark

**John Papa**

+ http://twitter.com/John_Papa

## Credits
Inspired by http://KnockoutJS.com


## Copyright

Copyright © 2012 [Hans Fjällemark](http://twitter.com/hfjallemark) & [John Papa](http://twitter.com/John_Papa).

## License 

KoLite is under MIT license - http://www.opensource.org/licenses/mit-license.php