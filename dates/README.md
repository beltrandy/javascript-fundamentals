# Timezones

- By default, almost every date method (except one) gives you a date/time in local time.
- You only get UTC if you specify UTC.

# Creating a Date

## The date-string method

```javascript
new Date('1988-03-21') // ISO 8601 Extended format 'YYYY-MM-DDTHH:mm:ss:sssZ'
```
- If `Z` is present, date is set to UTC. If it is not there, it will be Local Time if time is provided.
- date-string method is not the recommened way to create dates. Using arguments or timestamps is preferred.

## Creating dates with arguments

```javascript
new Date(2017, 3, 22, 5, 23, 50)

// This date can be easily read if you follow the left-right formula.
// Year: 2017,
// Month: April (because month is zero-indexed)
// Date: 22
// Hours: 05
// Minutes: 23
// Seconds: 50
```
To create a date in UTC:
```javascript
// 11th June 2019, 12am, UTC.
new Date(Date.UTC(2019, 5, 11))
```

## Creating dates with timestamps

- A timestamp is the amount of milliseconds elapsed since 1 January 1970 (aka Unix Epoch Time)
- You rarely use timestamp method to create dates. It's mostly used to compare different dates.

```javascript
// 11th June 2019, 8am (in my Local Time, Singapore)
new Date(1560211200000)

// Using no arguments, you get current time in Local Time
new Date()
```

# Formatting a date

```javascript
const date = new Date(2019, 0, 23, 17, 23, 42)
```
- `toString` gives you `Wed Jan 23 2019 17:23:42 GMT+0800 (Singapore Standard Time)`
- `toDateString` gives you `Wed Jan 23 2019`
- `toLocaleString` gives you `23/01/2019, 17:23:42`
- `toLocaleDateString` gives you `23/01/2019`
- `toGMTString` gives you `Wed, 23 Jan 2019 09:23:42 GMT`
- `toUTCString` gives you `Wed, 23 Jan 2019 09:23:42 GMT`
- `toISOString` gives you `2019-01-23T09:23:42.079Z`

To make custom formatting you'll need to use the following methods:
- `getFullYear`: Gets 4-digit year according to local time
- `getMonth`: Gets month of the year (0-11) according to local time. Month is zero-indexed.
- `getDate`: Gets day of the month (1-31) according to local time.
- `getDay`: Gets day of the week (0-6) according to local time. Day of the week begins with Sunday (0) and ends with Saturday (6).
- `getHours`: Gets hours (0-23) according to local time.
- `getMinutes`: Gets minutes (0-59) according to local time.
- `getSeconds`: Gets seconds (0-59) according to local time.
- `getMilliseconds`: Gets milliseconds (0-999) according to local time.

# Comparing dates

You can compare date objects directly using `<`, `>`, `>=`, and `<=`, but you can't use `==` or `===`
```javascript
const earlier = new Date(2019, 0, 26)
const later = new Date(2019, 0, 27)

console.log(earlier < later) // true
```
To check if 2 dates fall on the exact same time. use `getTime`
```javascript
const isSameTime = (a, b) => {
  return a.getTime() === b.getTime()
}

const a = new Date(2019, 0, 26)
const b = new Date(2019, 0, 26)
console.log(isSameTime(a, b)) // true
```
To check whether two dates fall on the same day, you can check their `getFullYear`, `getMonth` and `getDate` values
```javascript
const isSameDay = (a, b) => {
  return a.getFullYear() === b.getFullYear() &&
    a.getMonth() === b.getMonth() &&
    a.getDate()=== b.getDate()
}

const a = new Date(2019, 0, 26, 10) // 26 Jan 2019, 10am
const b = new Date(2019, 0, 26, 12) // 26 Jan 2019, 12pm
console.log(isSameDay(a, b)) // true
```

# Getting a date from another date

## Setting a specifc date and time
You can use these methods to set a date/time from another date:
- `setFullYear`: Set 4-digit year in Local Time.
- `setMonth`: Set month of the year in Local Time.
- `setDate`: Set day of the month in Local Time.
- `setHours`: Set hours in Local Time.
- `setMinutes`: Set minutes in Local Time.
- `setSeconds`: Set seconds in Local Time.
- `setMilliseconds`: Set milliseconds in Local Time.
```javascript
const d = new Date(2019, 0, 10)
const newDate = new Date(d)
newDate.setMonth(5)

console.log(d) // 10 January 2019
console.log(newDate) // 10 June 2019
```

## Adding/Subtracting delta from another date

### The set approach
```javascript
const today = new Date(2019, 2, 28)
const finalDate = new Date(today)
finalDate.setDate(today.getDate() + 3)

console.log(finalDate) // 31 March 2019
```

### The new Date approach
```javascript
const today = new Date(2019, 2, 28)

// Getting required values
const year = today.getFullYear()
const month = today.getMonh()
const day = today.getDate()

// Creating a new Date (with the delta)
const finalDate = new Date(year, month, day + 3)

console.log(finalDate) // 31 March 2019
```

# Automatic date correction

If you provide Date with a value that's outside of its acceptable range, JavaScript recalculates the date for you automatically.
```javascript
// 33rd March => 2nd April
new Date(2019, 2, 33)
```
```javascript
// 33rd March => 2nd April
new Date(2019, 2, 30 + 3)
```