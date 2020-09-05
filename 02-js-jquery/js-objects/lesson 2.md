# Objects

## Lesson Objectives

_After this lesson, students will be able to:_

1. Explain the difference between arrays and objects
1. Store key-value pairs inside an object
1. Access values by key-name
1. Add Object Properties
1. Change Object Properties
1. Explain why we use an object instead of an array
1. Manipulate objects and arrays declared as `const`
1. List common errors made with objects
1. Use object properties with conditionals

## Explain the difference between arrays and objects

We have seen the following datatypes:

* String
* Number
* Boolean
* Arrays

Arrays are a **data structure**. We use them to organize our data: in the case of arrays, we can organize our data into a **sequential list** data structure.

* We can use arrays to store multiple pieces of data as a sequential list:

```javascript
const vehicle = ["blue", 4000, 1989];
```

* Each element has a corresponding index (or place), in sequence.

But with the array above, we don't know what the values mean. Does "blue" refer to the color of the vehicle? To the mood of the owner? Is it the model of the vehicle?

* An object is also a **data structure**, but we can use objects to store data with greater specificity.

* In JavaScript, **objects** are what we use to represent **key-value** pairs.

## Store key-value pairs inside an object

Key-value pair syntax:

```javascript
const car = {
	color: "blue",
	hp: 4000,
	year: 1989
}
```

* Unlike arrays, objects use _named keys_ rather than ordered indexes. Each piece of data is _bound_ to its key, rather than assigned an index. The data is not _sequential_.

* In Javascript, an object is a way to group many pairs of keys and values together

We can console.log the entire object:

```javascript
console.log(car);
```

## Access values by key-name

We can access the values stored in key using dot notation:

```javascript
console.log(car.color)
```

### Question: Ask (5 min)

* What differences do you see between the `vehicle` array and the `car` object syntax?

```javascript
const vehicle = ["blue", 4000, 1989];
const car = { color: "blue", hp: 4000, year: 1989 };
```

## Differences between arrays and objects

* Arrays are declared using the square brackets ` var arr = [];`
* Objects are declared using the curly braces `var obj = {}`

Objects contain _key-value pairs_. They are are the **properties** of the object

A **key** is like an **index** in an array, but it has

* a name
* it is unique

A key is really a string but we can omit the quotes.

A **value** is what a key _refers to_, and can be any datatype.

### Class Exercise: Build an Object

Build an object in detail, demonstrating that:

* We use a colon to separate the key and the value
* We do not put semicolons after our values.
* We separate our key-value pairs with a comma

```javascript
const person = {}
```

#### Investigate
1. What properties should we add to the person object.

1. How can we access these properties.

### Activity (10 min)

#### Dog

* Create an object called `dog` that has the following properties:
	* name (a string, give your dog a name)
	* age (a number, give your dog an age)
	* Remember the correct use of curly braces, colons, and commas! No semicolons!
* Console.log the `dog` object to check if it's correct
* Console.log just the dog's name
* Console.log just the dog's age

#### Celebrity

* Create an object called `celebrity` that has the following properties:
	* name (a string, give the celebrity a name)
	* age (a number, give the celebrity an age)
	* isCurrrentlyTweeting (a boolean)
* Console.log the `celebrity` object
* Console.log just the name of the `celebrity`
* Console.log just the age of the `celebrity`
* Console.log whether or not the `celebrity` is currently tweeting
* Write conditional that will print "Turn off Twitter" if the celebrity is currently tweeting.

## Add Object Properties

You can easily add more properties to a previously declared object:

```javascript
const house = {
	doors: 9
}

console.log(house)
```

> => { doors: 9 }


Add properties to the `house` object by simply adding a key using dot notation and the value using an equals `=`. Our house has no windows. Let's add some in _without_ writing them straight into the object:

```javascript
house.windows = 30
```

When we do it this way, the `windows` key is added to the object.

```javascript
console.log(house);
```

> => { doors: 9, windows: 30 }

Add another property `hasGarden`:

```javascript
house.hasGarden = true;
```

## Change Object Properties

Changing the value of an existing key has the same syntax as creating a new key-value pair:

```javascript
const bicycle = {
	isATricycle: false
}
```

```javascript
bicycle.isATricycle = true
```

### Activity (7 min)

* Create an _empty_ object called `macros`

Do not write in to this empty object. Instead, add keys and values with `macros.keyName = "value"`
After each key-value addition, console.log the `macros` object to make sure the new keys and values show up.

* Add to the object a key `protein` with a value 'tempeh'
* Add to the object a key `carbohydrates` with a value 'spuds'
* Add to the object a key `fats` with a value 'olive oil'
* Console.log the `macros` object to check if all the macros are there

### Activity: 10 minutes

* Create an object called `guitar` with the following properties:
	* a key `strings` with value 6
	* a key `isAcoustic` with value true (boolean)  
* _Change_ the value of `strings` to 100
	* console.log the value of `strings` (`guitar.strings`)
* _Change_ the value of `isAcoustic` to false
	* Console.log the value of `isAcoustic`
* Without writing into your object directly, add a key `belongsTo` with the value 'Dimebag Darrell'
	* Console.log the value of `belongsTo`
* _Change_ the value of `belongsTo` to 'Mr. Rogers'
* Console.log the entire `guitar` object

## Explain why we use an object instead of an array

When designing your programs, it is up to you to **choose** how to model your data. We can represent real-life things with our datatypes, but it's a matter of choosing the appropriate datatypes.

If the thing you want to model is just a list, use an **array**.

If the thing want to model has properties, use an **object**.

Using what we know about datatypes so far, which datatype would we use to model:

1. The name of your cat
2. The age of your cat
3. Your cat's favorite things
4. Whether your cat can speak French
5. Whether your cat can solve a Rubik's cube
6. Your cat

## Manipulate objects and arrays declared as `const`

`const` only prevents you from reassigning a variable, it doesn't prevent you from adding or changing elements of arrays or properties of objects.

You can do this:

```javascript
const mogwai  = {}

mogwai.name = 'Gizmo';
```

Cannot do this:

```javascript
const mogwai = {}

mogwai = { name: 'Gizmo' }
```

## Object literal shorthand

If variable names outside the object will correspond to the keys in the object, you can write shorthand like this for the `mogwai` object:

```javascript
const name = 'Gizmo';
const age = 1;

const mogwai = { name, age }

console.log(mogwai);
```

> => { name: 'Gizmo', age: 1 }


This is equivalent to the longhand:

```javascript

const name = 'Gizmo';
const age = 1;

const mogwai = { name: name, age: age }

console.log(mogwai);
```

> => { name: 'Gizmo', age: 1 }

## List common errors made with objects

### Unique Keys

It just makes sense that keys ought to be unique within an object. Values, however, can be whatever.

An object can not have more than one key with the same name. If it does, the value will default to the last key with the same name, and the prior properties will be excluded on creation.

```javascript
const borough = {
	name: "Brooklyn",
	name: "The Bronx"
}
```

```javascript
console.log(borough);

=> Object { name: "The Bronx" }
```

Conclusion: keys should be unique within an object. Values, however, are not unique.

### Accessing and Naming Keys Using Brackets and Quotes

You can create and access any key with square brackets and quotes.

```javascript
const goblin = { badGuy: true };
```

```javascript
console.log(goblin['badGuy']);
=> true
```

With square brackets and quotes, you can make key names with spaces and special characters, because the key is _coerced_ into a string. _But_ you then have to access the value from here on out with square brackets and quotes.

```javascript
const strangeObj = {}

strangeObj['a key with spaces'] = 999;

console.log(strangeObj)
=> Object { 'a key with spaces': 999 }
```

You would need also to access that key with the square brackets and quotes:

```javascript
console.log(strangeObj['a key with spaces']);

=> 999
```

You could not access that key using dot notation.

Square brackets are nice if you need to programmatically generate a key name:

```javascript
const obj = {};
for (var i = 0; i < 10; i++) {
    obj['key'+i] = 'foo'
}
console.log(obj);
```

### Keys That Are Numbers

If a key is just a number, that number will be coerced into a string, which is fine.

```javascript
const obj = {
	1: "one",
}
```

```javascript
console.log(obj);
=> Object { '1': 'one' }
```

But, you cannot access, add, or change numbered keys with dot notation.

```javascript
console.log(obj.1)
```

```javascript
obj.2 = "hey"

console.log(obj2);
```

There is another way to access key-values using square brackets and quotes `obj['1']`

### Activity

* Create an _empty_ object called `testObject`
* Give `testObject` a key called 'this is a test' with the value "test"
	* Console.log the value of the key 'this is a test'
* Give test object a key called `2` with the value "I'm just messing around with objects"
	* Console.log the value of the key `2`

## Use object properties with conditionals

You can use object properties with conditionals, loops, etc

```javascript
const obj = {
	whatevs: 'hi',
	count:4
}
if (obj.whatevs == "hi") {
	console.log('ok');
}

for (var i = 0; i < obj.count; i++) {
	console.log(i);
}
```

You can test to see if a property exists on an object:

```javascript
const obj = {
	something:'wuttt'
}

if (obj.something) {
	console.log('ok');
}
if (obj.anotherthing){
	console.log('ok');
} else {
	console.log('no go');
}
```

This is because accessing a property that doesn't exist on an object gives you `undefined` which is treated as `false`.