## JavaScript Prototypes and Prototypal Inheritance

### 1. **Introduction to Prototypes**
Hello everyone, Today we will walk through the concept of **Prototypal Inheritance** in JavaScript. Before diving into inheritance, let's first understand **what a prototype is** and **prototype chaining**.

In JavaScript, almost everything is an object, and every object has an internal link to another object called its **prototype**. This connection forms a chain, commonly referred to as the **prototype chain**. Through this chain, objects can access properties and methods of their prototypes.

### 2. **What is a Prototype?**
Whenever you create an object in JavaScript, the JavaScript engine automatically links it to a prototype object. The prototype is an object from which other objects inherit properties and methods. This is crucial because it allows objects to share behaviors without defining them on each individual object.

For example, if you create an array:
```javascript
let arr = ['Akshay', 'Aditya'];
```
The array `arr` has access to built-in methods like `push`, `forEach`, `map`, etc., even though we didn't define them. This is possible because `arr` is linked to the **Array prototype**, which contains these methods. You can access this prototype using:
```javascript
console.log(arr.__proto__);
```

### 3. **Prototype Chaining**
JavaScript allows objects to inherit from other objects, forming a chain of prototypes. This chain can be visualized as:
```
arr -> Array.prototype -> Object.prototype -> null
```
- `arr.__proto__` is `Array.prototype`.
- `Array.prototype.__proto__` is `Object.prototype`.
- `Object.prototype.__proto__` is `null`, which marks the end of the chain.

This chain is what we call the **prototype chain**. If you try to access a property or method on an object, JavaScript will look for it on the object itself. If it doesn't find it, it will check the object's prototype and continue up the chain until it either finds the property or reaches `null`.

### 4. **Prototypal Inheritance**
Prototypal inheritance allows one object to inherit properties and methods from another. When you access a property on an object, and it isn't found on the object itself, JavaScript checks the prototype chain.

For example:
```javascript
let obj1 = {
  name: 'Akshay',
  city: 'Dehradun',
  getIntro: function() {
    return `${this.name} from ${this.city}`;
  }
};

let obj2 = {
  name: 'Aditya'
};

// Set the prototype of obj2 to obj1
obj2.__proto__ = obj1;

console.log(obj2.getIntro()); // "Aditya from Dehradun"
```
In the above code, `obj2` inherits the `getIntro` method from `obj1`. When `obj2.getIntro()` is called, the method is found on `obj1`, and the `this` keyword refers to `obj2`.

### 5. **Modifying the Prototype (Don't Do This!)**
While you can modify the prototype of an object directly using `__proto__`, **this is not recommended** as it can lead to performance issues and unexpected behavior. Instead, you should use **Object.create** or **class inheritance** for setting prototypes properly:
```javascript
Object.setPrototypeOf(obj2, obj1); // Preferred way to set the prototype
```

### 6. **Prototype Chain Example**
Let's break down an example of prototype chaining:
```javascript
let arr = ['Akshay', 'Aditya'];
console.log(arr.__proto__); // Array.prototype
console.log(arr.__proto__.__proto__); // Object.prototype
console.log(arr.__proto__.__proto__.__proto__); // null
```
Here, `arr.__proto__` refers to the `Array.prototype`, which contains methods like `push`, `forEach`, etc. The prototype of `Array.prototype` is `Object.prototype`, which contains methods like `toString` and `hasOwnProperty`. Finally, the prototype of `Object.prototype` is `null`, which ends the chain.

### 7. **Prototypes in Functions**
Even functions in JavaScript are objects, and they also have prototypes. Every function has a `prototype` property, which is used when creating new objects through a constructor:
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return `Hello, my name is ${this.name}`;
};

let person1 = new Person('Akshay');
console.log(person1.greet()); // "Hello, my name is Akshay"
```
In this example, `Person.prototype` contains the `greet` method, and any new `Person` object will inherit it.

### 8. **Prototype Chain in Functions**
Functions also have their own prototype chains:
```javascript
function greet() {}
console.log(greet.__proto__); // Function.prototype
console.log(greet.__proto__.__proto__); // Object.prototype
```
Just like arrays and objects, functions inherit from `Function.prototype`, which itself inherits from `Object.prototype`.

### 9. **Conclusion**
Prototypal inheritance is one of the most important concepts in JavaScript. Unlike classical inheritance in languages like Java or C++, where classes inherit from other classes, JavaScript uses objects to inherit from other objects. This is known as **object-based inheritance**. By understanding how prototypes and prototype chains work, you'll gain a deep insight into how JavaScript functions under the hood.

Make sure to use prototypal inheritance effectively, and remember not to directly manipulate `__proto__`. Instead, use proper methods like `Object.create` or ES6 `classes`.

That's all for today. Thanks for watching, and I hope this helps you better understand JavaScript prototypes and prototypal inheritance!
