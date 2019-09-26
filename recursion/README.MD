# Recursion

- Termination condition - If the input is bad, this prevents the recursion from running
- Base case - the condition that signifies the completion of the recursion and stops it
- The Recursion - when the function calls itself
```javascript
function factorial(x) {
    // TERMINATION
    if (x < 0) return;
    // BASE
    if (x === 0) return 1;
    // RECURSION
    return x * factorial(x - 1);
}
factorial(3);
// 6

// Another simple recursion example
let countdown = (num) => {
    if (num <= 0) return;
    console.log(num);
    countdown(num - 1);
}

countdown(10);
```