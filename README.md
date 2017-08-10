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

The Javascript interpreter workd by searching up the prototype tree until the property is found.  The interpreter will look for the property on an object.  If it can't find it there, it will look at the object's prototype, and so on.  If no property is ever found, it returns undefined.

**The last stop at the very top of the prototype tree is Object.prototype, from which all reference types inherit by default.**

See list of available list of Object.prototype properties and methods.  These are properties and methods available out of the box for all objects we create.

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)

```javascript
var parentObj = {
	a:1,
	b:2
}
```
parentObj.a   //returns 1

parentObj.hasOwnProperty('a')   //returns true

Where did this hasOwnProperty property come from?

```javascript
var childObj = Object.create(parentObj);
childObj.b = 3;
childObj.c = 4
```
What do you think will be returned for:
* childObj.c
* childObj.b
* childObj.a
* childObj.d

How did we get a value for childObj.a without explicitly stating an "a" property for childObj?

Inhertance from parentObj.

How come childObj.b returned 3 and not 2?

Property shadowing.

![prototypes diagram](protoimage.png).