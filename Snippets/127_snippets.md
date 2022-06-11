# 127 Useful JavaScript Snippets You Can Understand in 30 Seconds


[127 Useful JavaScript Snippets You Can Understand in 30 Seconds](https://morioh.com/p/a76bc7d72226)

----------------------------------------------------

JavaScript is one of the most popular languages you can learn. As many people say: “If you’re going to learn just one programming language, go for JavaScript.”


If this sounds compelling to you, here’s a list of 127 beneficial snippets taken from this project that you can learn and use immediately.

* * *

1\. all
-------

This snippet returns `true` if the predicate function returns `true` for all elements in a collection and `false` otherwise. You can omit the second argument `fn`if you want to use `Boolean`as a default value.

```javascript

    const all = (arr, fn = Boolean) => arr.every(fn);
    
    all([4, 2, 3], x => x > 1); // true
    all([1, 2, 3]); // true
    
```
2\. allEqual
------------

This snippet checks whether all elements of the array are equal.

```javascript

    const allEqual = arr => arr.every(val => val === arr[0]);
    
    allEqual([1, 2, 3, 4, 5, 6]); // false
    allEqual([1, 1, 1, 1]); // true
    
```
3\. approximatelyEqual
----------------------

This snippet checks whether two numbers are approximately equal to each other, with a small difference.

```javascript

    const approximatelyEqual = (v1, v2, epsilon = 0.001) => Math.abs(v1 - v2) < epsilon;
    
    approximatelyEqual(Math.PI / 2.0, 1.5708); // true
    
```
4\. arrayToCSV
--------------

This snippet converts the elements to strings with comma-separated values.

```javascript

    const arrayToCSV = (arr, delimiter = ',') =>
      arr.map(v => v.map(x => `"${x}"`).join(delimiter)).join('\n');
      
    arrayToCSV([['a', 'b'], ['c', 'd']]); // '"a","b"\n"c","d"'
    arrayToCSV([['a', 'b'], ['c', 'd']], ';'); // '"a";"b"\n"c";"d"'```
    
```
5\. arrayToHtmlList
-------------------

This snippet converts the elements of an array into `<li>` tags and appends them to the list of the given ID.

```javascript

    const arrayToHtmlList = (arr, listID) =>
      (el => (
        (el = document.querySelector('#' + listID)),
        (el.innerHTML += arr.map(item => `<li>${item}</li>`).join(''))
      ))();
      
    arrayToHtmlList(['item 1', 'item 2'], 'myListID');
    
```
6\. attempt
-----------

This snippet executes a function, returning either the result or the caught error object.

```javascript

    const attempt = (fn, ...args) => {
      try {
        return fn(...args);
      } catch (e) {
        return e instanceof Error ? e : new Error(e);
      }
    };
    var elements = attempt(function(selector) {
      return document.querySelectorAll(selector);
    }, '>_>');
    if (elements instanceof Error) elements = []; // elements = []
    
```
7\. average
-----------

This snippet returns the average of two or more numerical values.

```javascript

    const average = (...nums) => nums.reduce((acc, val) => acc + val, 0) / nums.length;
    average(...[1, 2, 3]); // 2
    average(1, 2, 3); // 2
    
```
8\. averageBy
-------------

This snippet returns the average of an array after initially doing the mapping of each element to a value using a given function.

```javascript

    const averageBy = (arr, fn) =>
      arr.map(typeof fn === 'function' ? fn : val => val[fn]).reduce((acc, val) => acc + val, 0) /
      arr.length;
      
    averageBy([{ n: 4 }, { n: 2 }, { n: 8 }, { n: 6 }], o => o.n); // 5
    averageBy([{ n: 4 }, { n: 2 }, { n: 8 }, { n: 6 }], 'n'); // 5
    
```
9\. bifurcate
-------------

This snippet splits values into two groups and then puts a truthy element of `filter`in the first group, and in the second group otherwise.

You can use `Array.prototype.reduce()`and `Array.prototype.push()`to add elements to groups based on `filter`.

```javascript

    const bifurcate = (arr, filter) =>
      arr.reduce((acc, val, i) => (acc[filter[i] ? 0 : 1].push(val), acc), [[], []]);
    bifurcate(['beep', 'boop', 'foo', 'bar'], [true, true, false, true]); 
    // [ ['beep', 'boop', 'bar'], ['foo'] ]
    
```
10\. bifurcateBy
----------------

This snippet splits values into two groups, based on a predicate function. If the predicate function returns a truthy value, the element will be placed in the first group. Otherwise, it will be placed in the second group.

You can use `Array.prototype.reduce()`and `Array.prototype.push()`to add elements to groups, based on the value returned by `fn`for each element.

```javascript

    const bifurcateBy = (arr, fn) =>
      arr.reduce((acc, val, i) => (acc[fn(val, i) ? 0 : 1].push(val), acc), [[], []]);
      
    bifurcateBy(['beep', 'boop', 'foo', 'bar'], x => x[0] === 'b'); 
    // [ ['beep', 'boop', 'bar'], ['foo'] ]
    
```
11\. bottomVisible
------------------

This snippet checks whether the bottom of a page is visible.

```javascript

    const bottomVisible = () =>
      document.documentElement.clientHeight + window.scrollY >=
      (document.documentElement.scrollHeight || document.documentElement.clientHeight);
    
    bottomVisible(); // true
    
```
12\. byteSize
-------------

This snippet returns the length of a string in bytes.

```javascript

    const byteSize = str => new Blob([str]).size;
    
    byteSize('😀'); // 4
    byteSize('Hello World'); // 11
    
```
13\. capitalize
---------------

This snippet capitalizes the first letter of a string.

```javascript

    const capitalize = ([first, ...rest]) =>
      first.toUpperCase() + rest.join('');
      
    capitalize('fooBar'); // 'FooBar'
    capitalize('fooBar', true); // 'Foobar'
    
```
14\. capitalizeEveryWord
------------------------

This snippet capitalizes the first letter of every word in a given string.

```javascript

    const capitalizeEveryWord = str => str.replace(/\b[a-z]/g, char => char.toUpperCase());
    
    capitalizeEveryWord('hello world!'); // 'Hello World!'
    
```
15\. castArray
--------------

This snippet converts a non-array value into array.

```javascript

    const castArray = val => (Array.isArray(val) ? val : [val]);
    
    castArray('foo'); // ['foo']
    castArray([1]); // [1]
    
```
16\. compact
------------

This snippet removes false values from an array.

```javascript

    const compact = arr => arr.filter(Boolean);
    
    compact([0, 1, false, 2, '', 3, 'a', 'e' * 23, NaN, 's', 34]); 
    // [ 1, 2, 3, 'a', 's', 34 ]
    
```
17\. countOccurrences
---------------------

This snippet counts the occurrences of a value in an array.

```javascript

    const countOccurrences = (arr, val) => arr.reduce((a, v) => (v === val ? a + 1 : a), 0);
    countOccurrences([1, 1, 2, 1, 2, 3], 1); // 3
    
```
18\. Create Directory
---------------------

This snippet uses `existsSync()` to check whether a directory exists and then `mkdirSync()` to create it if it doesn’t.

```javascript

    const fs = require('fs');
    const createDirIfNotExists = dir => (!fs.existsSync(dir) ? fs.mkdirSync(dir) : undefined);
    createDirIfNotExists('test'); 
    // creates the directory 'test', if it doesn't exist
    
```
19\. currentURL
---------------

This snippet returns the current URL.

```javascript

    const currentURL = () => window.location.href;
    
    currentURL(); // 'https://medium.com/@fatosmorina'
    
```
20\. dayOfYear
--------------

This snippet gets the day of the year from a `Date`object.

```javascript

    const dayOfYear = date =>
      Math.floor((date - new Date(date.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);
    
    dayOfYear(new Date()); // 272
    
```
21\. decapitalize
-----------------

This snippet turns the first letter of a string into lowercase.

```javascript

    const decapitalize = ([first, ...rest]) =>
      first.toLowerCase() + rest.join('')
    
    decapitalize('FooBar'); // 'fooBar'
    decapitalize('FooBar'); // 'fooBar'
    
```
22\. deepFlatten
----------------

This snippet flattens an array recursively.

```javascript

    const deepFlatten = arr => [].concat(...arr.map(v => (Array.isArray(v) ? deepFlatten(v) : v)));
    
    deepFlatten([1, [2], [[3], 4], 5]); // [1,2,3,4,5]
    
```
23\. default
------------

This snippet assigns default values for all properties in an object that are _undefined_.

```javascript

    const defaults = (obj, ...defs) => Object.assign({}, obj, ...defs.reverse(), obj);
    
    defaults({ a: 1 }, { b: 2 }, { b: 6 }, { a: 3 }); // { a: 1, b: 2 }
    
```
24\. defer
----------

This snippet delays the execution of a function until the current call stack is cleared.

```javascript

    const defer = (fn, ...args) => setTimeout(fn, 1, ...args);
    
    defer(console.log, 'a'), console.log('b'); // logs 'b' then 'a'
    
```
25\. degreesToRads
------------------

This code snippet can be used to convert a value from degrees to radians.

```javascript

    const degreesToRads = deg => (deg * Math.PI) / 180.0;
    
    degreesToRads(90.0); // ~1.5708
    
```
26\. difference
---------------

This snippet finds the difference between two arrays.

```javascript

    const difference = (a, b) => {
      const s = new Set(b);
      return a.filter(x => !s.has(x));
    };
    
    difference([1, 2, 3], [1, 2, 4]); // [3]
    
```
27\. differenceBy
-----------------

This method returns the difference between two arrays, after applying a given function to each element of both lists.

```javascript

    const differenceBy = (a, b, fn) => {
      const s = new Set(b.map(fn));
      return a.filter(x => !s.has(fn(x)));
    };
    
    differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [1.2]
    differenceBy([{ x: 2 }, { x: 1 }], [{ x: 1 }], v => v.x); // [ { x: 2 } ]
    
```
28\. differenceWith
-------------------

This snippet removes the values for which the comparator function returns `false`.

```javascript

    const differenceWith = (arr, val, comp) => arr.filter(a => val.findIndex(b => comp(a, b)) === -1);
    
    differenceWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0], (a, b) => Math.round(a) === Math.round(b)); 
    // [1, 1.2]
    
```
29\. digitize
-------------

This snippet gets a number as input and returns an array of its digits.

```javascript

    const digitize = n => [...`${n}`].map(i => parseInt(i));
    
    digitize(431); // [4, 3, 1]
    
```
30\. distance
-------------

This snippet returns the distance between two points by calculating the Euclidean distance.

```javascript

    const distance = (x0, y0, x1, y1) => Math.hypot(x1 - x0, y1 - y0);
    
    distance(1, 1, 2, 3); // 2.23606797749979
    
```
31\. Drop Elements
------------------

This snippet returns a new array with `n` elements removed from the left.

```javascript

    const drop = (arr, n = 1) => arr.slice(n);
    
    drop([1, 2, 3]); // [2,3]
    drop([1, 2, 3], 2); // [3]
    drop([1, 2, 3], 42); // []
    
```
32\. dropRight
--------------

This snippet returns a new array with `n` elements removed from the right.

```javascript

    const dropRight = (arr, n = 1) => arr.slice(0, -n);
    
    dropRight([1, 2, 3]); // [1,2]
    dropRight([1, 2, 3], 2); // [1]
    dropRight([1, 2, 3], 42); // []
    
```
33\. dropRightWhile
-------------------

This snippet removes elements from the right side of an array until the passed function returns `true`.

```javascript

    const dropRightWhile = (arr, func) => {
      while (arr.length > 0 && !func(arr[arr.length - 1])) arr = arr.slice(0, -1);
      return arr;
    };
    
    dropRightWhile([1, 2, 3, 4], n => n < 3); // [1, 2]
    
```
34\. dropWhile
--------------

This snippet removes elements from an array until the passed function returns `true`.

```javascript

    const dropWhile = (arr, func) => {
      while (arr.length > 0 && !func(arr[0])) arr = arr.slice(1);
      return arr;
    };
    
    dropWhile([1, 2, 3, 4], n => n >= 3); // [3,4]
    
```
35\. elementContains
--------------------

This snippet checks whether the parent element contains the child.

```javascript

    const elementContains = (parent, child) => parent !== child && parent.contains(child);
    
    elementContains(document.querySelector('head'), document.querySelector('title')); // true
    elementContains(document.querySelector('body'), document.querySelector('body')); // false
    
```
36\. Filter Duplicate Elements
------------------------------

This snippet removes duplicate values in an array.

```javascript

    const filterNonUnique = arr => arr.filter(i => arr.indexOf(i) === arr.lastIndexOf(i));
    
    filterNonUnique([1, 2, 2, 3, 4, 4, 5]); // [1, 3, 5]
    
```
37\. findKey
------------

This snippet returns the first key that satisfies a given function.

```javascript

    const findKey = (obj, fn) => Object.keys(obj).find(key => fn(obj[key], key, obj));
    
    findKey(
      {
        barney: { age: 36, active: true },
        fred: { age: 40, active: false },
        pebbles: { age: 1, active: true }
      },
      o => o['active']
    ); // 'barney'
    
```
38\. findLast
-------------

This snippet returns the last element for which a given function returns a truthy value.

```javascript

    const findLast = (arr, fn) => arr.filter(fn).pop();
    
    findLast([1, 2, 3, 4], n => n % 2 === 1); // 3
    
```
39\. flatten
------------

This snippet flattens an array up to a specified depth using recursion.

```javascript

    const flatten = (arr, depth = 1) =>
      arr.reduce((a, v) => a.concat(depth > 1 && Array.isArray(v) ? flatten(v, depth - 1) : v), []);
    
    flatten([1, [2], 3, 4]); // [1, 2, 3, 4]
    flatten([1, [2, [3, [4, 5], 6], 7], 8], 2); // [1, 2, 3, [4, 5], 6, 7, 8]
    
```
40\. forEachRight
-----------------

This snippet executes a function for each element of an array starting from the array’s last element.

```javascript

    const forEachRight = (arr, callback) =>
      arr
        .slice(0)
        .reverse()
        .forEach(callback);
        
    forEachRight([1, 2, 3, 4], val => console.log(val)); // '4', '3', '2', '1'
    
```
41\. forOwn
-----------

This snippet iterates on each property of an object and iterates a callback for each one respectively.

```javascript

    const forOwn = (obj, fn) => Object.keys(obj).forEach(key => fn(obj[key], key, obj));
    forOwn({ foo: 'bar', a: 1 }, v => console.log(v)); // 'bar', 1
    
```
42\. functionName
-----------------

This snippet prints the name of a function into the console.

```javascript

    const functionName = fn => (console.debug(fn.name), fn);
    
    functionName(Math.max); // max (logged in debug channel of console)
    
```
43\. Get Time From Date
-----------------------

This snippet can be used to get the time from a `Date`object as a string.

```javascript

    const getColonTimeFromDate = date => date.toTimeString().slice(0, 8);
    
    getColonTimeFromDate(new Date()); // "08:38:00"
    
```
44\. Get Days Between Dates
---------------------------

This snippet can be used to find the difference in days between two dates.

```javascript

    const getDaysDiffBetweenDates = (dateInitial, dateFinal) =>
      (dateFinal - dateInitial) / (1000 * 3600 * 24);
      
    getDaysDiffBetweenDates(new Date('2019-01-13'), new Date('2019-01-15')); // 2
    
```
45\. getStyle
-------------

This snippet can be used to get the value of a CSS rule for a particular element.

```javascript

    const getStyle = (el, ruleName) => getComputedStyle(el)[ruleName];
    
    getStyle(document.querySelector('p'), 'font-size'); // '16px'
    
```
46\. getType
------------

This snippet can be used to get the type of a value.

```javascript

    const getType = v =>
      v === undefined ? 'undefined' : v === null ? 'null' : v.constructor.name.toLowerCase();
      
    getType(new Set([1, 2, 3])); // 'set'
    
```
47\. hasClass
-------------

This snippet checks whether an element has a particular class.

```javascript

    const hasClass = (el, className) => el.classList.contains(className);
    hasClass(document.querySelector('p.special'), 'special'); // true
    
```
48\. head
---------

This snippet returns the `head` of a list.

```javascript

    const head = arr => arr[0];
    
    head([1, 2, 3]); // 1
    
```
49\. hide
---------

This snippet can be used to hide all elements specified.

```javascript

    const hide = (...el) => [...el].forEach(e => (e.style.display = 'none'));
    
    hide(document.querySelectorAll('img')); // Hides all <img> elements on the page
    
```
50\. httpsRedirect
------------------

This snippet can be used to redirect from HTTP to HTTPS in a particular domain.

```javascript

    const httpsRedirect = () => {
      if (location.protocol !== 'https:') location.replace('https://' + location.href.split('//')[1]);
    };
    
    httpsRedirect(); // If you are on http://mydomain.com, you are redirected to https://mydomain.com
    
```
51\. indexOfAll
---------------

This snippet can be used to get all indexes of a value in an array, which returns an empty array, in case this value is not included in it.

```javascript

    const indexOfAll = (arr, val) => arr.reduce((acc, el, i) => (el === val ? [...acc, i] : acc), []);
    
    indexOfAll([1, 2, 3, 1, 2, 3], 1); // [0,3]
    indexOfAll([1, 2, 3], 4); // []
    
```
52\. initial
------------

This snippet returns all elements of an array except the last one.

```javascript

    const initial = arr => arr.slice(0, -1);
    
    initial([1, 2, 3]); // [1,2]const initial = arr => arr.slice(0, -1);
    initial([1, 2, 3]); // [1,2]
    
```
53\. insertAfter
----------------

This snippet can be used to insert an HTML string after the end of a particular element.

```javascript

    const insertAfter = (el, htmlString) => el.insertAdjacentHTML('afterend', htmlString);
    
    insertAfter(document.getElementById('myId'), '<p>after</p>'); // <div id="myId">...</div> <p>after</p>
    
```
54\. insertBefore
-----------------

This snippet can be used to insert an HTML string before a particular element.

```javascript

    const insertBefore = (el, htmlString) => el.insertAdjacentHTML('beforebegin', htmlString);
    
    insertBefore(document.getElementById('myId'), '<p>before</p>'); // <p>before</p> <div id="myId">...</div>
    
```
55\. intersection
-----------------

This snippet can be used to get an array with elements that are included in two other arrays.

```javascript

    const intersection = (a, b) => {
      const s = new Set(b);
      return a.filter(x => s.has(x));
    };
    
    intersection([1, 2, 3], [4, 3, 2]); // [2, 3]
    
```
56\. intersectionBy
-------------------

This snippet can be used to return a list of elements that exist in both arrays, after a particular function has been executed to each element of both arrays.

```javascript

    const intersectionBy = (a, b, fn) => {
      const s = new Set(b.map(fn));
      return a.filter(x => s.has(fn(x)));
    };
    
    intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor); // [2.1]
    
```
57\. intersectionWith
---------------------

This snippet can be used to return a list of elements that exist in both arrays by using a comparator function.

```javascript

    const intersectionWith = (a, b, comp) => a.filter(x => b.findIndex(y => comp(x, y)) !== -1);
    
    intersectionWith([1, 1.2, 1.5, 3, 0], [1.9, 3, 0, 3.9], (a, b) => Math.round(a) === Math.round(b)); // [1.5, 3, 0]
    
```
58\. is
-------

This snippet can be used to check if a value is of a particular type.

```javascript

    const is = (type, val) => ![, null].includes(val) && val.constructor === type;
    
    is(Array, [1]); // true
    is(ArrayBuffer, new ArrayBuffer()); // true
    is(Map, new Map()); // true
    is(RegExp, /./g); // true
    is(Set, new Set()); // true
    is(WeakMap, new WeakMap()); // true
    is(WeakSet, new WeakSet()); // true
    is(String, ''); // true
    is(String, new String('')); // true
    is(Number, 1); // true
    is(Number, new Number(1)); // true
    is(Boolean, true); // true
    is(Boolean, new Boolean(true)); // true
    
```
59\. isAfterDate
----------------

This snippet can be used to check whether a date is after another date.

```javascript

    const isAfterDate = (dateA, dateB) => dateA > dateB;
    
    isAfterDate(new Date(2010, 10, 21), new Date(2010, 10, 20)); // true
    
```
60\. isAnagram
--------------

This snippet can be used to check whether a particular string is an anagram with another string.

```javascript

    const isAnagram = (str1, str2) => {
      const normalize = str =>
        str
          .toLowerCase()
          .replace(/[^a-z0-9]/gi, '')
          .split('')
          .sort()
          .join('');
      return normalize(str1) === normalize(str2);
    };
    
    isAnagram('iceman', 'cinema'); // true
    
```
61\. isArrayLike
----------------

This snippet can be used to check if a provided argument is iterable like an array.

```javascript

    const isArrayLike = obj => obj != null && typeof obj[Symbol.iterator] === 'function';
    
    isArrayLike(document.querySelectorAll('.className')); // true
    isArrayLike('abc'); // true
    isArrayLike(null); // false
    
```
62\. isBeforeDate
-----------------

This snippet can be used to check whether a date is before another date.

```javascript

    const isBeforeDate = (dateA, dateB) => dateA < dateB;
    
    isBeforeDate(new Date(2010, 10, 20), new Date(2010, 10, 21)); // true
    
```
63\. isBoolean
--------------

This snippet can be used to check whether an argument is a boolean.

```javascript

    const isBoolean = val => typeof val === 'boolean';
    
    isBoolean(null); // false
    isBoolean(false); // true
    
```
64\. isBrowser
--------------

This snippet can be used to determine whether the current runtime environment is a browser. This is helpful for avoiding errors when running front-end modules on the server (Node).

```javascript

    const isBrowser = () => ![typeof window, typeof document].includes('undefined');
    
    isBrowser(); // true (browser)
    isBrowser(); // false (Node)
    
```
65\. isBrowserTabFocused
------------------------

This snippet can be used to determine whether the browser tab is focused.

```javascript

    const isBrowserTabFocused = () => !document.hidden;
    
    isBrowserTabFocused(); // true
    
```
66\. isLowerCase
----------------

This snippet can be used to determine whether a string is lower case.

```javascript

    const isLowerCase = str => str === str.toLowerCase();
    
    isLowerCase('abc'); // true
    isLowerCase('a3@$'); // true
    isLowerCase('Ab4'); // false
    
```
67\. isNil
----------

This snippet can be used to check whether a value is `null` or `undefined`.

```javascript

    const isNil = val => val === undefined || val === null;
    
    isNil(null); // true
    isNil(undefined); // true
    
```
68\. isNull
-----------

This snippet can be used to check whether a value is `null`.

```javascript

    const isNull = val => val === null;
    
    isNull(null); // true
    
```
69\. isNumber
-------------

This snippet can be used to check whether a provided value is a number.

```javascript

    const isNumber = val => typeof val === 'number';
    
    isNumber('1'); // false
    isNumber(1); // true
    
```
70\. isObject
-------------

This snippet can be used to check whether a provided value is an object. It uses the Object constructor to create an object wrapper for the given value.

If it is already an object, then an object type that corresponds to the given value will be returned. Otherwise, a new object will be returned.

```javascript

    const isObject = obj => obj === Object(obj);
    
    isObject([1, 2, 3, 4]); // true
    isObject([]); // true
    isObject(['Hello!']); // true
    isObject({ a: 1 }); // true
    isObject({}); // true
    isObject(true); // false
    
```
71\. isObjectLike
-----------------

This snippet can be used to check if a value is not `null`and that its `typeof` is “object”.

```javascript

    const isObjectLike = val => val !== null && typeof val === 'object';
    
    isObjectLike({}); // true
    isObjectLike([1, 2, 3]); // true
    isObjectLike(x => x); // false
    isObjectLike(null); // false
    
```
72\. isPlainObject
------------------

This snippet checks whether a value is an object created by the Object constructor.

```javascript

    const isPlainObject = val => !!val && typeof val === 'object' && val.constructor === Object;
    
    isPlainObject({ a: 1 }); // true
    isPlainObject(new Map()); // false
    
```
73\. isPromiseLike
------------------

This snippet checks whether an object looks like a `Promise`.

```javascript

    const isPromiseLike = obj =>
      obj !== null &&
      (typeof obj === 'object' || typeof obj === 'function') &&
      typeof obj.then === 'function';
      
    isPromiseLike({
      then: function() {
        return '';
      }
    }); // true
    isPromiseLike(null); // false
    isPromiseLike({}); // false
    
```
74\. isSameDate
---------------

This snippet can be used to check whether two dates are equal.

```javascript

    const isSameDate = (dateA, dateB) => dateA.toISOString() === dateB.toISOString();
    
    isSameDate(new Date(2010, 10, 20), new Date(2010, 10, 20)); // true
    
```
75\. isString
-------------

This snippet can be used to check whether an argument is a string.

```javascript

    const isString = val => typeof val === 'string';
    
    isString('10'); // true
    
```
76\. isSymbol
-------------

This snippet can be used to check whether an argument is a symbol.

```javascript

    const isSymbol = val => typeof val === 'symbol';
    
    isSymbol(Symbol('x')); // true
    
```
77\. isUndefined
----------------

This snippet can be used to check whether a value is `undefined`.

```javascript

    const isUndefined = val => val === undefined;
    
    isUndefined(undefined); // true
    
```
78\. isUpperCase
----------------

This snippet can be used to check whether a string is upper case.

```javascript

    const isUpperCase = str => str === str.toUpperCase();
    
    isUpperCase('ABC'); // true
    isLowerCase('A3@$'); // true
    isLowerCase('aB4'); // false
    
```
79\. isValidJSON
----------------

This snippet can be used to check whether a string is a valid JSON.

```javascript

    const isValidJSON = str => {
      try {
        JSON.parse(str);
        return true;
      } catch (e) {
        return false;
      }
    };
    
    isValidJSON('{"name":"Adam","age":20}'); // true
    isValidJSON('{"name":"Adam",age:"20"}'); // false
    isValidJSON(null); // true
    
```
80\. last
---------

This snippet returns the last element of an array.

```javascript

    const last = arr => arr[arr.length - 1];
    
    last([1, 2, 3]); // 3
    
```
81\. matches
------------

This snippet compares two objects to determine if the first one contains the same property values as the second one.

```javascript

    const matches = (obj, source) =>
      Object.keys(source).every(key => obj.hasOwnProperty(key) && obj[key] === source[key]);
      
    matches({ age: 25, hair: 'long', beard: true }, { hair: 'long', beard: true }); // true
    matches({ hair: 'long', beard: true }, { age: 25, hair: 'long', beard: true }); // false
    
```
82\. maxDate
------------

This snippet can be used to get the latest date.

```javascript

    const maxDate = (...dates) => new Date(Math.max.apply(null, ...dates));
    
    const array = [
      new Date(2017, 4, 13),
      new Date(2018, 2, 12),
      new Date(2016, 0, 10),
      new Date(2016, 0, 9)
    ];
    maxDate(array); // 2018-03-11T22:00:00.000Z
    
```
83\. maxN
---------

This snippet returns the `n` largest elements from a list. If `n`is greater than or equal to the list’s length, then it will return the original list (sorted in descending order).

```javascript

    const maxN = (arr, n = 1) => [...arr].sort((a, b) => b - a).slice(0, n);
    
    maxN([1, 2, 3]); // [3]
    maxN([1, 2, 3], 2); // [3,2] 	
    
```
84\. minDate
------------

This snippet can be used to get the earliest date.

```javascript

    const minDate = (...dates) => new Date(Math.min.apply(null, ...dates));
    
    const array = [
      new Date(2017, 4, 13),
      new Date(2018, 2, 12),
      new Date(2016, 0, 10),
      new Date(2016, 0, 9)
    ];
    minDate(array); // 2016-01-08T22:00:00.000Z
    
```
85\. minN
---------

This snippet returns the `n` smallest elements from a list. If `n`is greater than or equal to the list’s length, then it will return the original list (sorted in ascending order).

```javascript

    const minN = (arr, n = 1) => [...arr].sort((a, b) => a - b).slice(0, n);
    
    minN([1, 2, 3]); // [1]
    minN([1, 2, 3], 2); // [1,2]
    
```
86\. negate
-----------

This snippet can be used to apply the not operator (`!`) to a predicate function with its arguments.

```javascript

    const negate = func => (...args) => !func(...args);
    
    [1, 2, 3, 4, 5, 6].filter(negate(n => n % 2 === 0)); // [ 1, 3, 5 ]
    
```
87\. nodeListToArray
--------------------

This snippet can be used to convert a `nodeList` to an array.

```javascript

    const nodeListToArray = nodeList => [...nodeList];
    
    nodeListToArray(document.childNodes); // [ <!DOCTYPE html>, html ]
    
```
88\. pad
--------

This snippet can be used to `pad` a string on both sides with a specified character if it is shorter than the specified length.

```javascript

    const pad = (str, length, char = ' ') =>
      str.padStart((str.length + length) / 2, char).padEnd(length, char);
      
    pad('cat', 8); // '  cat   '
    pad(String(42), 6, '0'); // '004200'
    pad('foobar', 3); // 'foobar'
    
```
89\. radsToDegrees
------------------

This snippet can be used to convert an angle from radians to degrees.

```javascript

    const radsToDegrees = rad => (rad * 180.0) / Math.PI;
    
    radsToDegrees(Math.PI / 2); // 90
    
```
90\. Random Hexadecimal Color Code
----------------------------------

This snippet can be used to generate a random hexadecimal color code.

```javascript

    const randomHexColorCode = () => {
      let n = (Math.random() * 0xfffff * 1000000).toString(16);
      return '#' + n.slice(0, 6);
    };
    
    randomHexColorCode(); // "#e34155"
    
```
91\. randomIntArrayInRange
--------------------------

This snippet can be used to generate an array with `n` random integers in a specified range.

```javascript

    const randomIntArrayInRange = (min, max, n = 1) =>
      Array.from({ length: n }, () => Math.floor(Math.random() * (max - min + 1)) + min);
      
    randomIntArrayInRange(12, 35, 10); // [ 34, 14, 27, 17, 30, 27, 20, 26, 21, 14 ]
    
```
92\. randomIntegerInRange
-------------------------

This snippet can be used to generate a random integer in a specified range.

```javascript

    const randomIntegerInRange = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
    
    randomIntegerInRange(0, 5); // 3
    
```
93\. randomNumberInRange
------------------------

This snippet can be used to return a random number in a specified range.

```javascript

    const randomNumberInRange = (min, max) => Math.random() * (max - min) + min;
    
    randomNumberInRange(2, 10); // 6.0211363285087005
    
```
94\. readFileLines
------------------

This snippet can be used to read a file by getting an array of lines from a file.

```javascript

    const fs = require('fs');
    const readFileLines = filename =>
      fs
        .readFileSync(filename)
        .toString('UTF8')
        .split('\n');
    
    let arr = readFileLines('test.txt');
    console.log(arr); // ['line1', 'line2', 'line3']
```
95\. Redirect to a URL
----------------------

This snippet can be used to do a redirect to a specified URL.

```javascript

    const redirect = (url, asLink = true) =>
      asLink ? (window.location.href = url) : window.location.replace(url);
      
    redirect('https://google.com');
    
```
96\. reverse
------------

This snippet can be used to reverse a string.

```javascript

    const reverseString = str => [...str].reverse().join('');
    
    reverseString('foobar'); // 'raboof'
    
```
97\. round
----------

This snippet can be used to round a number to a specified number of digits.

```javascript

    const round = (n, decimals = 0) => Number(`${Math.round(`${n}e${decimals}`)}e-${decimals}`);
    
    round(1.005, 2); // 1.01
    
```
98\. runPromisesInSeries
------------------------

This snippet can be used to run an array of promises in series.

```javascript

    const runPromisesInSeries = ps => ps.reduce((p, next) => p.then(next), Promise.resolve());
    const delay = d => new Promise(r => setTimeout(r, d));
    
    runPromisesInSeries([() => delay(1000), () => delay(2000)]); 
    // Executes each promise sequentially, taking a total of 3 seconds to complete
    
```
99\. sample
-----------

This snippet can be used to get a random number from an array.

```javascript

    const sample = arr => arr[Math.floor(Math.random() * arr.length)];
    
    sample([3, 7, 9, 11]); // 9
    
```
100\. sampleSize
----------------

This snippet can be used to get `n`random elements from unique positions from an array up to the size of the array. Elements in the array are shuffled using the [Fisher-Yates algorithm](https://morioh.com/redirect?l=https%3A%2F%2Fgithub.com%2F30-seconds%2F30-seconds-of-code%23shuffle).

```javascript

    const sampleSize = ([...arr], n = 1) => {
      let m = arr.length;
      while (m) {
        const i = Math.floor(Math.random() * m--);
        [arr[m], arr[i]] = [arr[i], arr[m]];
      }
      return arr.slice(0, n);
    };
    
    sampleSize([1, 2, 3], 2); // [3,1]
    sampleSize([1, 2, 3], 4); // [2,3,1]
    
```
101\. scrollToTop
-----------------

This snippet can be used to do a smooth scroll to the top of the current page.

```javascript

    const scrollToTop = () => {
      const c = document.documentElement.scrollTop || document.body.scrollTop;
      if (c > 0) {
        window.requestAnimationFrame(scrollToTop);
        window.scrollTo(0, c - c / 8);
      }
    };
    
    scrollToTop();
    
```
102\. serializeCookie
---------------------

This snippet can be used to serialize a cookie name-value pair into a Set-Cookie header string.

```javascript

    const serializeCookie = (name, val) => `${encodeURIComponent(name)}=${encodeURIComponent(val)}`;
    
    serializeCookie('foo', 'bar'); // 'foo=bar'
    
```
103\. setStyle
--------------

This snippet can be used to set the value of a CSS rule for a particular element.

```javascript

    const setStyle = (el, ruleName, val) => (el.style[ruleName] = val);
    
    setStyle(document.querySelector('p'), 'font-size', '20px');
    // The first <p> element on the page will have a font-size of 20px
    
```
104\. shallowClone
------------------

This snippet can be used to create a shallow clone of an object.

```javascript

    const shallowClone = obj => Object.assign({}, obj);
    
    const a = { x: true, y: 1 };
    const b = shallowClone(a); // a !== b
    
```
105\. show
----------

This snippet can be used to show all the elements specified.

```javascript

    const show = (...el) => [...el].forEach(e => (e.style.display = ''));
    
    show(...document.querySelectorAll('img')); // Shows all <img> elements on the page
    
```
106\. shuffle
-------------

This snippet can be used to order the elements of an array randomly using the [Fisher-Yates algorithm](https://morioh.com/redirect?l=https%3A%2F%2Fgithub.com%2F30-seconds%2F30-seconds-of-code%23shuffle).

```javascript

    const shuffle = ([...arr]) => {
      let m = arr.length;
      while (m) {
        const i = Math.floor(Math.random() * m--);
        [arr[m], arr[i]] = [arr[i], arr[m]];
      }
      return arr;
    };
    
    const foo = [1, 2, 3];
    shuffle(foo); // [2, 3, 1], foo = [1, 2, 3]
    
```
107\. similarity
----------------

This snippet can be used to return an array of elements that appear in two arrays.

```javascript

    https://medium.com/better-programming/127-helpful-javascript-snippets-you-can-learn-in-30-seconds-or-less-part-6-of-6-862a6403d334
    
```
108\. sleep
-----------

This snippet can be used to delay the execution of an asynchronous function by putting it into sleep.

```javascript

    const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));
    
    async function sleepyWork() {
      console.log("I'm going to sleep for 1 second.");
      await sleep(1000);
      console.log('I woke up after 1 second.');
    }
    
```
109\. smoothScroll
------------------

This snippet can be used to smoothly scroll the element on which it is called into the visible area of the browser window.

```javascript

    const smoothScroll = element =>
      document.querySelector(element).scrollIntoView({
        behavior: 'smooth'
      });
      
    smoothScroll('#fooBar'); // scrolls smoothly to the element with the id fooBar
    smoothScroll('.fooBar'); // scrolls smoothly to the first element with a class of fooBar
    
```
110\. sortCharactersInString
----------------------------

This snippet can be used to alphabetically sort the characters in a string.

```javascript

    const sortCharactersInString = str => [...str].sort((a, b) => a.localeCompare(b)).join('');
    
    sortCharactersInString('cabbage'); // 'aabbceg'
    
```
111\. splitLines
----------------

This snippet can be used to split a multi-line string into an array of lines.

```javascript

    const splitLines = str => str.split(/\r?\n/);
    
    splitLines('This\nis a\nmultiline\nstring.\n'); // ['This', 'is a', 'multiline', 'string.' , '']
    
```
112\. stripHTMLTags
-------------------

This snippet can be used to remove HTML/XML tags from a string.

```javascript

    const stripHTMLTags = str => str.replace(/<[^>]*>/g, '');
    
    stripHTMLTags('<p><em>lorem</em> <strong>ipsum</strong></p>'); // 'lorem ipsum'
    
```
113\. sum
---------

This snippet can be used to find the sum of two or more numbers or arrays.

```javascript

    const sum = (...arr) => [...arr].reduce((acc, val) => acc + val, 0);
    
    sum(1, 2, 3, 4); // 10
    sum(...[1, 2, 3, 4]); // 10
    
```
114\. tail
----------

This snippet can be used to get an array with all the elements of an array except for the first one. If the array has only one element, then that an array with that element will be returned instead.

```javascript

    const tail = arr => (arr.length > 1 ? arr.slice(1) : arr);
    
    tail([1, 2, 3]); // [2,3]
    tail([1]); // [1]
    
```
115\. take
----------

This snippet can be used to get an array with `n`elements removed from the beginning.

```javascript

    const take = (arr, n = 1) => arr.slice(0, n);
    
    take([1, 2, 3], 5); // [1, 2, 3]
    take([1, 2, 3], 0); // []
    
```
116\. takeRight
---------------

This snippet can be used to get an array with `n`elements removed from the end.

```javascript

    const takeRight = (arr, n = 1) => arr.slice(arr.length - n, arr.length);
    
    takeRight([1, 2, 3], 2); // [ 2, 3 ]
    takeRight([1, 2, 3]); // [3]
    
```
117\. timeTaken
---------------

This snippet can be used to find out the time it takes to execute a function.

```javascript

    const timeTaken = callback => {
      console.time('timeTaken');
      const r = callback();
      console.timeEnd('timeTaken');
      return r;
    };
    
    timeTaken(() => Math.pow(2, 10)); // 1024, (logged): timeTaken: 0.02099609375ms
    
```
118\. times
-----------

This snippet can be used to iterate over a callback `n`times.

```javascript

    const times = (n, fn, context = undefined) => {
      let i = 0;
      while (fn.call(context, i) !== false && ++i < n) {}
    };
    
    var output = '';
    times(5, i => (output += i));
    console.log(output); // 01234
    
```
119\. toCurrency
----------------

This snippet can be used to format a number like a currency.

```javascript

    const toCurrency = (n, curr, LanguageFormat = undefined) =>
      Intl.NumberFormat(LanguageFormat, { style: 'currency', currency: curr }).format(n);
      
    toCurrency(123456.789, 'EUR'); // €123,456.79  | currency: Euro | currencyLangFormat: Local
    toCurrency(123456.789, 'USD', 'en-us'); // $123,456.79  | currency: US Dollar | currencyLangFormat: English (United States)
    toCurrency(123456.789, 'USD', 'fa'); // ۱۲۳٬۴۵۶٫۷۹ ؜$ | currency: US Dollar | currencyLangFormat: Farsi
    toCurrency(322342436423.2435, 'JPY'); // ¥322,342,436,423 | currency: Japanese Yen | currencyLangFormat: Local
    toCurrency(322342436423.2435, 'JPY', 'fi'); // 322 342 436 423 ¥ | currency: Japanese Yen | currencyLangFormat: Finnish
    
```
120\. toDecimalMark
-------------------

This snippet uses the `toLocaleString()`function to convert float-point arithmetic to the decimal mark form by using a number to make a comma-separated string.

```javascript

    const toDecimalMark = num => num.toLocaleString('en-US');
    
    toDecimalMark(12305030388.9087); // "12,305,030,388.909"
    
```
121\. toggleClass
-----------------

This snippet can be used to toggle a class for an element.

```javascript

    const toggleClass = (el, className) => el.classList.toggle(className);
    
    toggleClass(document.querySelector('p.special'), 'special'); // The paragraph will not have the 'special' class anymore
    
```
122\. tomorrow
--------------

This snippet can be used to get a string representation of tomorrow’s date.

```javascript

    const tomorrow = () => {
      let t = new Date();
      t.setDate(t.getDate() + 1);
      return t.toISOString().split('T')[0];
    };
    
    tomorrow(); // 2019-09-08 (if current date is 2018-09-08)
    
```
123\. unfold
------------

This snippet can be used to build an array using an iterator function and an initial seed value.

```javascript

    const unfold = (fn, seed) => {
      let result = [],
        val = [null, seed];
      while ((val = fn(val[1]))) result.push(val[0]);
      return result;
    };
    
    var f = n => (n > 50 ? false : [-n, n + 10]);
    unfold(f, 10); // [-10, -20, -30, -40, -50]
    
```
124\. union
-----------

This snippet can be used to find the `union` of two arrays, resulting in an array that has elements that come from both arrays but that do not repeat.

```javascript

    const union = (a, b) => Array.from(new Set([...a, ...b]));
    
    union([1, 2, 3], [4, 3, 2]); // [1,2,3,4]
    
```
125\. uniqueElements
--------------------

This snippet uses ES6 `Set`andthe`…rest`operator to get every element only once.

```javascript

    const uniqueElements = arr => [...new Set(arr)];
    
    uniqueElements([1, 2, 2, 3, 4, 4, 5]); // [1, 2, 3, 4, 5]
    
```
126\. validateNumber
--------------------

This snippet can be used to check whether a value is a number.

```javascript

    const validateNumber = n => !isNaN(parseFloat(n)) && isFinite(n) && Number(n) == n;
    
    validateNumber('10'); // true
    
```
127\. words
-----------

This snippet converts a string into an array of words.

```javascript

    const words = (str, pattern = /[^a-zA-Z-]+/) => str.split(pattern).filter(Boolean);
    
    words('I love javaScript!!'); // ["I", "love", "javaScript"]
    words('python, javaScript & coffee'); // ["python", "javaScript", "coffee"]    
```

Synopsis
--------

These snippets were taken from this [project](https://morioh.com/redirect?l=https%3A%2F%2Fgithub.com%2F30-seconds%2F30_seconds_of_knowledge) in which you can find more JavaScript snippets, and also snippets for other technologies and frameworks.

> _**The**_ [_**Original Article**_](https://morioh.com/redirect?l=https%3A%2F%2Fbetterprogramming.pub%2F127-helpful-javascript-snippets-you-can-learn-in-30-seconds-or-less-part-1-of-6-bc2bc890dfe5) _**can be found on**_ [_**https://github.com**_](https://morioh.com/redirect?l=https%3A%2F%2Fgithub.com%2F30-seconds%2F30-seconds-of-code) 

 Understand in 30 Seconds_files/82bfcc1021.png)](https://morioh.com/@5c42bfb15f2b0c4254e513fb)

