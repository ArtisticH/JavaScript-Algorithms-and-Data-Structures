# Object Oriented Programming

### Make Code More Reusable with the this Keyword
The last challenge introduced a method to the duck object. It used `duck.name` dot notation to access the value for the name property within the return statement:
```
sayName: function() {return "The name of this duck is " + duck.name + ".";}
```
While this is a valid way to access the object's property, there is a pitfall here.  
If the variable name changes, any code referencing the original name would need to be updated as well.  
In a short object definition, it isn't a problem, but if an object has many references to its properties there is a greater chance for error.

A way to avoid these issues is with the `this` keyword:
```
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + this.name + ".";}
};
```
n the current context, `this` refers to the object that the method is associated with: `duck`.  
If the object's name is changed to mallard, it is not necessary to find all the references to duck in the code. It makes the code reusable and easier to read.

### Define a Constructor Function
Constructors are *functions* that create *new objects*.  
They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.
```
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}

let blueBird = new Bird();
```
This constructor defines a Bird object with properties `name`, `color`, and `numLegs` set to Albert, blue, and 2, respectively.  
Constructors follow a few conventions:
- Constructors are defined with a capitalized name to distinguish them from other functions that are not constructors.
- Constructors use the keyword `this` to set properties of the object they will create. Inside the constructor, `this` refers to the new object it will create.
- Constructors define properties and behaviors instead of returning a value as other functions might.  
  
`this` inside the constructor always refers to the object being created.  
  
Notice that the `new` operator is used when calling a constructor.  
This tells JavaScript to create a new instance of `Bird` called `blueBird`.  
Without the `new` operator, `this` inside the constructor would not point to the newly created object, giving unexpected results.  
Now `blueBird` has all the properties defined inside the `Bird` constructor.

### Extend Constructors to Receive Arguments
notice that all Birds that are created with the Bird constructor are automatically named Albert, are blue in color, and have two legs.  
What if you want birds with different values for name and color? It's possible to change the properties of each bird manually but that would be a lot of work:
```
let swan = new Bird();
swan.name = "Carlos";
swan.color = "white";
```
Suppose you were writing a program to keep track of hundreds or even thousands of different birds in an aviary.  
It would take a lot of time to create all the birds, then change the properties to different values for every one.  
To more easily create different Bird objects, you can design your Bird constructor to accept parameters:
```
function Bird(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}
```
The constructor is more flexible. It's now possible to define the properties for each Bird at the time it is created, which is one way that JavaScript constructors are so useful.  
They group objects together based on shared characteristics and behavior and define a blueprint that automates their creation.

### Verify an Object's Constructor with instanceof
Anytime a constructor function creates a new object, that object is said to be an instance of its constructor.  
JavaScript gives a convenient way to verify this with the `instanceof` operator.  
`instanceof` allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor. Here's an example:
```
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // true
```
If an object is created without using a constructor, `instanceof` will verify that it is not an instance of that constructor:
```
let canary = {
  name: "Mildred",
  color: "Yellow",
  numLegs: 2
};

canary instanceof Bird; // false
```

### Understand Own Properties
In the following example, the `Bird` constructor defines two properties: `name` and `numLegs`:
```
function Bird(name) {
  this.name = name;
  this.numLegs = 2;
}

let duck = new Bird("Donald");
let canary = new Bird("Tweety");
```
`name` and `numLegs` are called own properties, because they are defined directly on the instance object.  
That means that `duck` and `canary` each has its own separate copy of these properties.  
In fact every instance of Bird will have its own copy of these properties.  
  
The following code adds all of the own properties of duck to the array ownProps:
```
let ownProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}

console.log(ownProps); // ["name", "numLegs"]
```

### Use Prototype Properties to Reduce Duplicate Code
Since `numLegs` will probably have the same value for all instances of `Bird`, you essentially have a duplicated variable `numLegs` inside each `Bird` instance.

This may not be an issue when there are only two instances, but imagine if there are millions of instances. That would be a lot of duplicated variables.

A better way is to use the `prototype` of `Bird`. Properties in the prototype are shared among ALL instances of Bird. Here's how to add numLegs to the Bird prototype:
```
Bird.prototype.numLegs = 2;
```
Now all instances of `Bird` have the `numLegs` property.
```
console.log(duck.numLegs);
console.log(canary.numLegs);
```
Since all instances automatically have the properties on the `prototype`, think of a prototype as a "recipe" for creating objects.  
Note that the `prototype` for `duck` and `canary` is part of the `Bird` constructor as `Bird.prototype`.

### Iterate Over All Properties
You have now seen two kinds of properties: own properties and prototype properties.  
Own properties are defined directly on the object instance itself. And prototype properties are defined on the prototype.
```
function Bird(name) {
  this.name = name;  //own property
}

Bird.prototype.numLegs = 2; // prototype property

let duck = new Bird("Donald");
```

Here is how you add `duck`'s own properties to the array ownProps and prototype properties to the array prototypeProps:
```
let ownProps = [];
let prototypeProps = [];

for (let property in duck) { // for in은 own / prototype properties
  if(duck.hasOwnProperty(property)) { // hasOwnProperty는 own만
    ownProps.push(property);
  } else {
    prototypeProps.push(property);
  }
}

console.log(ownProps); // ["name"]
console.log(prototypeProps); // ["numLegs"]
```

### Understand the Constructor Property
There is a special `constructor` property located on the object instances `duck` and `beagle` that were created in the previous challenges:
```
let duck = new Bird();
let beagle = new Dog();

console.log(duck.constructor === Bird); 
console.log(beagle.constructor === Dog);
```
  
Note that the `constructor` property is a reference to the constructor function that created the instance.  
The advantage of the constructor property is that it's possible to check for this property to find out what kind of object it is.  
Here's an example of how this could be used:
```
function joinBirdFraternity(candidate) {
  if (candidate.constructor === Bird) {
    return true;
  } else {
    return false;
  }
}
```
Note: Since the `constructor` property can be overwritten (which will be covered in the next two challenges) it’s generally better to use the `instanceof` method to check the type of an object.

### Change the Prototype to a New Object
Up until now you have been adding properties to the prototype individually:
```
Bird.prototype.numLegs = 2;
```
This becomes tedious after more than a few properties.
```
Bird.prototype.eat = function() {
  console.log("nom nom nom");
}

Bird.prototype.describe = function() {
  console.log("My name is " + this.name);
}
```
A more efficient way is to set the `prototype` to a new object that already contains the properties. This way, the properties are added all at once:
```
Bird.prototype = {
  numLegs: 2, 
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

### Remember to Set the Constructor Property when Changing the Prototype
There is one crucial side effect of manually setting the prototype to a new object. It erases the `constructor` property!  
This property can be used to check which constructor function created the instance, but since the property has been overwritten, it now gives false results:
```
duck.constructor === Bird; // false
duck.constructor === Object; // true
duck instanceof Bird; // true
```

To fix this, whenever a prototype is manually set to a new object, remember to define the `constructor` property:
```
Bird.prototype = {
  constructor: Bird,
  numLegs: 2,
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name); 
  }
};
```

### Understand Where an Object’s Prototype Comes From
Just like people inherit genes from their parents, an object inherits its `prototype` directly from the constructor function that created it.  
For example, here the `Bird` constructor creates the `duck` object:
```
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald");
```
`duck` inherits its prototype from the `Bird` constructor function. You can show this relationship with the `isPrototypeOf` method:
```
Bird.prototype.isPrototypeOf(duck); // true
```

### Understand the Prototype Chain
