# JavaScript Fundamentals Cheat Sheet

## Error Handling

### Throw Statement

 - `throw` statement will stop execution of the script, unless you handle it

```javascript
throw new Error('something went wrong')
```

### Error Object

```javascript
const myError = new Error('This is the error message');
console.log(myError.name); // Error
console.log(myError.message); // This is the error message
```
 - `Error` instances have name and message properties.

```javascript
// this:
const x = Error('I was created using a function call!');
​​​​// has the same functionality as this:
const y = new Error('I was constructed via the "new" keyword!');
```
 - When `Error` is used like a function -- without `new`, it will return an `Error` object. Therefore, a mere call to `Error` will produce the same output that constructing an `Error` object via the `new` keyword would

### Try...Catch...Finally Statement

```javascript
function f() {
  try {
    console.log(0);
    throw 'bogus';
  } catch(e) {
    console.log(1);
    return true; // this return statement is suspended
                 // until finally block has completed
    console.log(2); // not reachable
  } finally {
    console.log(3);
    return false; // overwrites the previous "return"
    console.log(4); // not reachable
  }
  // "return false" is executed now  
  console.log(5); // not reachable
}
console.log(f()); // 0, 1, 3, false
```
 - When logging errors to the console inside a `catch` block, using `console.error()` rather than `console.log()` is advised for debugging as it formats the message as an error and adds it to the list of error messages generated by the page
 - The `finally` block executes whether or not an exception is thrown.
 - If the `finally` block returns a value, this value becomes the return value of the entire  `try-catch-finally` production, regardless of any return statements in the `try` and `catch` blocks
 - Overwriting of return values by the `finally` block also applies to exceptions thrown or re-thrown inside of the `catch` block

## Getters / Setters

```javascript
const currentYear = new Date().getFullYear();

let car = {
    yearPurchased : 2001,

    get yearsOwned() {
        return currentYear - this.yearPurchased;
    },

    set yearsOwned(years) {
        this.yearPurchased = currentYear - years;
    }
}

console.log(car.yearPurchased);
console.log(car.yearsOwned);

car.yearsOwned = 5;

console.log(car.yearPurchased);
```

## ES6 Features

```javascript
let person = {
    firstName : "Randy",
    lastName: "Beltran",

    get fullName() {
        return `${this.firstName} ${this.lastName}` // String Literal
    },

    set fullName(name) {
        [this.firstName, this.lastName] = name.split(' '); // Destructuring Assignment
    }
}

console.log(person.fullName);

person.fullName = "Jason Humphrey";

console.log(person.firstName);
console.log(person.lastName);


// Use of Promises
const myPromise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('Data was returned');
    }, 3000);
});

myPromise
    .then(data => {
        console.log(data);
    });
```
## Sync vs Async

```javascript
console.log('Start!');

const myPromise = new Promise(function(resolve, reject) {
    setTimeout(function() {
        resolve('Data was returned');
    }, 3000);
});

myPromise
    .then(function(data) {
        console.log(data);
    })

console.log('End!');
```

## Scope and Closure

```javascript
function closureStart() {
    var topic = 'closure';

    function display() {
        alert(topic);
    }

    return display;
}

var myClosure = closureStart();

myClosure();
```

## Arrays and Objects

```javascript
let myString = 'Hello';
let myString2  = "Hello World";
let myString3 = `Hi ${myString}`;

let myNum = 4;

let isGood = true;

let myShoppingList = ['Flour', 'Sugar', 'Eggs'];
let myShoppingList2 = {
  0: 'Flour',
  1: 'Sugar',
  2: 'Eggs'
};
let myInformation = {
  street: 'Main St',
  phone: '(555) 555-5555',
  state: 'CA'
};
let myPoints = [
  {
    x: 1,
    y:1
  },
  
];
let myPoints2 = [
  [1,1]
];

let myFriendsList = [
  {
    name: 'Sally',
    list: [{
      product: 'Cake',
      brand: 'Betty Crocker'
    }]
  }
];

let storeCustomers = {
  Walmart: myFriendsList
  
};

let scores = {
  2009: [89, 79]
};
let scores2 = [[89, 79], [88, 78]];
```