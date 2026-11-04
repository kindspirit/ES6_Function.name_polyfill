# ES6_Function.name_polyfill
As an exercise I made this polyfill for ES6'S [Function: name](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/name) for use with Internet Explorer 9-11 and potentially other old browsers. The idea was to make it configurable in the same way that Function: name is configurable in ES6+.

# Other polyfills:
```
Date.name // 'Date'

Date.bind().name // ''

Object.getOwnPropertyDescriptor(Date, 'name') // undefined
```

# This polyfill:
```
Date.name // 'Date'

Date.bind().name // 'bound Date'

Object.getOwnPropertyDescriptor(Date, 'name') // {value: 'Date', writable: false, enumerable: false, configurable: true}

Less than 1.3K minified

```

# Caveat:
In ES6 `delete Date.name` would result in the name being deleted. In this polyfill if it is configurable `delete Date.name` returns true and the name just goes back to the original name of 'Date'.

To mimic ES6 behavior of functions having an own 'name' property, I had to monkey patch the following methods:
* `Object.getOwnPropertyDescriptor()`
* `Object.getOwnPropertyNames()`
* `Object.defineProperty()`
* `Object.defineProperties()`
* `Object.preventExtensions()`
* `Object.prototype.hasOwnProperty()`
* `Function.prototype.bind()` (to add 'bound ' prefix)
