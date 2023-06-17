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
All objects in JavaScript (with a few exceptions) have a `prototype`. Also, an object’s prototype itself is an object.  
```
function Bird(name) {
  this.name = name;
}

typeof Bird.prototype;
```
Because a `prototype` is an `object`, a `prototype` can have its own `prototype`! In this case, the prototype of `Bird.prototype` is `Object.prototype`:
```
Object.prototype.isPrototypeOf(Bird.prototype); 
```
How is this useful? You may recall the `hasOwnProperty` method from a previous challenge:
```
let duck = new Bird("Donald");
duck.hasOwnProperty("name");
```
The `hasOwnProperty` method is defined in `Object.prototype`, which can be accessed by `Bird.prototype`, which can then be accessed by `duck`.  
This is an example of the prototype chain. In this prototype chain, Bird is the `supertype` for duck, while duck is the `subtype`.  
Object is a `supertype` for both Bird and duck. *Object is a supertype for all objects in JavaScript*. Therefore, any object can use the hasOwnProperty method.

### Use Inheritance So You Don't Repeat Yourself
There's a principle in programming called *Don't Repeat Yourself (DRY)*.  
The reason repeated code is a problem is because any change requires fixing code in multiple places.  
This usually means more work for programmers and more room for errors.  
  
Notice in the example below that the `describe` method is shared by `Bird` and `Dog`:
```
Bird.prototype = {
  constructor: Bird,
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Dog.prototype = {
  constructor: Dog,
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```
The `describe` method is repeated in two places. The code can be edited to follow the DRY principle by creating a `supertype` (or parent) called `Animal`:
```
function Animal() { };

Animal.prototype = {
  constructor: Animal, 
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```
Since `Animal` includes the `describe` method, you can remove it from `Bird` and `Dog`:
```
Bird.prototype = {
  constructor: Bird
};

Dog.prototype = {
  constructor: Dog
};
```
### Inherit Behaviors from a Supertype
In the previous challenge, you created a `supertype` called `Animal` that defined behaviors shared by all animals:
```
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
```
This and the next challenge will cover how to reuse the methods of Animal inside Bird and Dog without defining them again.  
It uses a technique called inheritance.  
This challenge covers the first step: make an instance of the supertype (or parent). You already know one way to create an instance of Animal using the new operator:
```
let animal = new Animal();
```
There are some disadvantages when using this syntax for inheritance, which are too complex for the scope of this challenge.  
Instead, here's an alternative approach without those disadvantages:
```
let animal = Object.create(Animal.prototype);
```
`Object.create(obj)` creates a new object, and sets obj as the new object's `prototype`. Recall that the prototype is like the "recipe" for creating an object.  
By setting the prototype of animal to be the prototype of Animal, you are effectively giving the animal instance the same "recipe" as any other instance of Animal.
```
animal.eat();
animal instanceof Animal; // true
```

### Set the Child's Prototype to an Instance of the Parent
In the previous challenge you saw the first step for inheriting behavior from the supertype (or parent) Animal: making a new instance of Animal.

This challenge covers the next step: set the `prototype` of the subtype (or child)—in this case, `Bird`—to be an instance of `Animal`.
```
Bird.prototype = Object.create(Animal.prototype);
```
In a way, the recipe for `Bird` now includes all the key "ingredients" from `Animal`.
```
let duck = new Bird("Donald");
duck.eat();
```
`duck` inherits all of `Animal`'s properties, including the `eat` method.

### Reset an Inherited Constructor Property
When an object inherits its prototype from another object, it also inherits the supertype's constructor property.
```
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor
```
But `duck` and all instances of `Bird` should show that they were constructed by `Bird` and not `Animal`. To do so, you can manually set the `constructor` property of `Bird` to the Bird object:
```
Bird.prototype.constructor = Bird;
duck.constructor
```

### Add Methods After Inheritance
A constructor function that inherits its `prototype` object from a supertype constructor function can still have its own methods in addition to inherited methods.

For example, `Bird` is a constructor that inherits its `prototype` from `Animal`:
```
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;
```
In addition to what is inherited from `Animal`, you want to add behavior that is unique to `Bird` objects.  
Here, Bird will get a `fly()` function. Functions are added to Bird's prototype the same way as any constructor function:
```
Bird.prototype.fly = function() {
  console.log("I'm flying!");
};
```
Now instances of `Bird` will have both `eat()` and `fly()` methods:
```
let duck = new Bird();
duck.eat(); // nom nom nom 
duck.fly(); // I'm flying!
```

### Override Inherited Methods
In previous lessons, you learned that an object can inherit its behavior (methods) from another object by referencing its prototype object:
```
ChildObject.prototype = Object.create(ParentObject.prototype);
```
Then the ChildObject received its own methods by chaining them onto its prototype:
```
ChildObject.prototype.methodName = function() {...};
```
It's possible to override an inherited method. It's done the same way - by adding a method to `ChildObject.prototype` using the same method name as the one to override.  
Here's an example of `Bird` overriding the `eat()` method inherited from `Animal`:  
```
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};
function Bird() { }

Bird.prototype = Object.create(Animal.prototype);

Bird.prototype.eat = function() {
  return "peck peck peck";
};
```
If you have an instance `let duck = new Bird();` and you call `duck.eat()`, this is how JavaScript looks for the method on the prototype chain of `duck`:
- 1. `duck` => Is `eat()` defined here? No.
- 2. `Bird` => Is `eat()` defined here? => Yes. Execute it and stop searching.
- 3. `Animal` => `eat()` is also defined, but JavaScript stopped searching before reaching this level.
- 4. `Object` => JavaScript stopped searching before reaching this level.  

### Use a Mixin to Add Common Behavior Between Unrelated Objects
As you have seen, behavior is shared through inheritance. However, there are cases when inheritance is not the best solution.  
Inheritance does not work well for *unrelated objects* like `Bird` and `Airplane`. They can both fly, but a `Bird` is not a type of `Airplane` and vice versa.  
  
For unrelated objects, it's better to use mixins. A mixin allows other objects to use a collection of functions.
```
let flyMixin = function(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  }
};
```
The `flyMixin` takes any object and gives it the `fly` method.
```
let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
```
Here `bird` and `plane` are passed into `flyMixin`, which then assigns the `fly` function to each object. Now `bird` and `plane` can both `fly`:
```
bird.fly(); // Flying, wooosh! 
plane.fly(); // Flying, wooosh! 
```
Note how the mixin allows for the same `fly` method to be reused by unrelated objects `bird` and `plane`.

### Use Closure to Protect Properties Within an Object from Being Modified Externally
In the previous challenge, `bird` had a public property name.  
It is considered public because it can be accessed and changed outside of bird's definition.
```
bird.name = "Duffy";
```
Therefore, any part of your code can easily change the name of bird to any value.  
Think about things like passwords and bank accounts being easily changeable by any part of your codebase. That could cause a lot of issues.  
  
The simplest way to make this public property private is by creating a variable within the constructor function.  
This changes the scope of that variable to be within the constructor function versus available globally.  
This way, the variable can only be accessed and changed by methods also within the constructor function.  
```
function Bird() {
  let hatchedEgg = 10;

  this.getHatchedEggCount = function() { 
    return hatchedEgg;
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount();
```
Here `getHatchedEggCount` is a privileged method, because it has access to the private variable `hatchedEgg`.  
This is possible because `hatchedEgg` is declared in the same context as `getHatchedEggCount`.  
In JavaScript, a function always has access to the context in which it was created. This is called `closure`.  
getHatchedEggCount 함수는 Bird constructor안에서  


