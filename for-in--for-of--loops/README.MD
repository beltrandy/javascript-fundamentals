# `for in`/`for of` Loops
```javascript

let obj = {
  make: "Toyota",
  model: "Camry",
  year: 2014
};

// for in - used to iterate over all non-Symbol, enumerable properties of an object
for (var key in obj) {
  console.log(key);
}

// for of - used to iterate over iterable objects (strings, arrays, arguments, etc)
let name = "Randy";

for (var char of name) {
  console.log(char, 'char');
}
```