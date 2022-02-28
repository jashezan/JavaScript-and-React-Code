# javascript-learned-hardway 🥲

## <script> File Place:
1. We have to put <script> at the end of HTML file to do DOM MANIPULATION, else it won't find that HTML element if we put in in the head or before that element.
2. Though we can put <script> tag in the head with attribute ( async/defer ).

## Be aware of Case-sensitivity
1. Got "XMLhttpRequest is not defined" at noon. After trying many thing,Found it was XMLHttpRequest() whole time at night. just writing 'H' as 'h' can ruin your day.
2. If even got stuck, then look for simole mistake first. Try case-sensitivity and semicolon or Syntax error (Though semicolon is not necessary in new line in JavaScript.

## Callback Function =>
1. If a function is passed as parameter in anaother function, then first bracket () should not be there with parameter or these will call the parameter function immediately.
2. Function should be called with only name or the whole function should be defined as parameter.

## Non primitive Data types without console.log() doesn't show list
Prtimitve Data Types:
1. Number
2. String
3. Boolean
4. Undefined
5. Null
6. Object
7. Symbol
