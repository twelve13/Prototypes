# Prototypes

### Learning Objectives

* Demonstrate a use case that explains prototypal inheritance and what kind of flexibility it gives to programmers
* Use namespaces to organize application code
* Define a custom constructor method that sets one or more properties of a new object

### Intro

Let's say we want to design a bunch of Lego Minifigures.

![Assorted Lego Minifigures](minifigures.jpg)

Many traits in common:
* yellow head
* removable hair
* movable limbs
* same size/shape

To design each new Minifigure you can go off of a template Minifigure that has the properties that all Minifigures should have.  Then you can further customize each Minifigure as you want.  This template Minifigure can be considered the Minifigure prototype.

![typical Lego man](legoman.jpg) 

**In programming, a prototype is an object that supplies base behavior to a second object.**
The second object inherits the base behavior and can then further customize the base behavior.  This second object in turn could be the prototype for a third object and so on, forming a **prototype tree**. 

When looking for a property on an object, the Javascript interpreter works by searching up the prototype tree until the property is found.  The interpreter will look for the property on an object.  If it can't find it there, it will look at the object's prototype, and so on.  If no property is ever found, it returns undefined.

**The last stop at the very top of the prototype tree is Object.prototype, from which all reference types inherit by default.**

See list of available list of Object.prototype properties and methods.  These are properties and methods available out of the box for all objects we create.

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)

```javascript
var parentObject = {
	a:1,
	b:2
}
```
parentObject.a   //returns 1

parentObject.hasOwnProperty('a')   //returns true

Where did this hasOwnProperty property come from?

```javascript
var childObject = Object.create(parentObject);
childObject.b = 3;
childObject.c = 4
```
What do you think will be returned for:
* childObject.c
* childObject.b
* childObject.a
* childObject.d

How did we get a value for childObject.a without explicitly stating an "a" property for childObject?

Inhertance from parentObject.

How come childObject.b returned 3 and not 2?

Property shadowing.

![prototypes diagram](protoimage.png)

### Constructors

```javascript
var chocChip = {
	category: "dessert",
	"base-ingredients": ["flour", "sugar", "eggs"],
	extras: "chocolate chips",
	time: "20 min",
	directions: function(){
		console.log(`Mix ${this["base-ingredients"][0]}, ${this["base-ingredients"][1]}, 
		and ${this["base-ingredients"][2]}, then add in ${this.extras}.  Bake for ${this.time}.`)
	}
}
```

```javascript
var peanutButter = {
	category: "dessert",
	"base-ingredients": ["flour", "sugar", "eggs"],
	extras: "peanut butter",
	time: "25 min",
	directions: function(){
		console.log(`Mix ${this["base-ingredients"][0]}, ${this["base-ingredients"][1]}, 
		and ${this["base-ingredients"][2]}, then add in ${this.extras}.  Bake for ${this.time}.`)
	}
}
```

```javascript
function Cookie(extras, time) {
  this.category = "dessert";
  this["base-ingredients"] = ["flour", "sugar", "eggs"]
  this.extras = extras;
  this.time = time;
  this.directions = function() {
    console.log(`Mix ${this["base-ingredients"][0]}, ${this["base-ingredients"][1]}, 
    and ${this["base-ingredients"][2]}, then add in ${this.extras}.  Bake for ${this.time}.`)
  }
}
```

```javascript
var cChip = new Cookie("choco chips", "20 min");
var pButter = new Cookie("peanut butter", "24 min");
```

**Constructors are like regular functions, but we call them with the "new" keyword to create new objects from the same prototype.**  A constructor is useful when you want to create multiple similar objects with the same properties and methods.  It's a convention to capitalize the name of constructors to distinguish them from regular functions.

When we use the "new" keyword, we create a new instance of Cookie and assign it to a variable.  The constructor assigns the received parameters (for example, extras and time) to the properties of the current instance.

Sidenote about "this":
* In Javascript, "this" is the object that "owns" the Javascript code.
* The value of "this", when used in a function, is the object that "owns" the function.
* The value of "this", when used in an object, is the object itself.
* The "this" keyword in an object constructor does not have a value.  It is only a substitute for the new object.
* The value of "this" will become the new object when the constructor is used to create a new object.

It is a good idea to use namespacing to organize code.  A namespace is a context in which variables can exist without conflicting with other variables of the same name elsewhere.  You can avoid naming conflict by encapsulating your code in an object that is unlikely to collide with other objects.

