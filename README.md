# javascript-interview-questions

### 1.Explain the result of output:
``` javascript
(function main() {
  var factory = function () {
    var a = [];
    a[Array.prototype.pop.apply(arguments)] = 1;
    return a;
  };
  console.log(
    factory(0).length,
    factory(100).length,
    factory(Infinity).length,
    factory(null).length
  );
})();
// output 1 101 0 0

```
<details>
  <summary> Explanation </summary>
  <p style="padding-left: 8px">Array.prototype.pop is a method that removes the last element from an array and returns that element.</p>
  <p style="padding-left: 8px">apply(arguments) calls the pop method on the arguments object (which is array-like but not a true array). This removes and returns the last argument passed to factory.</p>
  <h4> 1. factory(0): </h4>
  <p style="padding-left: 8px">arguments is [0]</p>
  <p style="padding-left: 8px">Array.prototype.pop.apply(arguments) returns 0 </p>
  <p style="padding-left: 8px">a[0] = 1, so a becomes [1] </p>
 <p style="padding-left: 8px">a.length is 1</p>
  <h4> 2. factory(100): </h4>
 <p style="padding-left: 8px"> arguments is [100] </p>
 <p style="padding-left: 8px">Array.prototype.pop.apply(arguments) returns 100 </p>
 <p style="padding-left: 8px">a[100] = 1, so a becomes an array with 101 elements, with 1 at the 100th index.</p>
  <p style="padding-left: 8px">a.length is 101</p>
  <h4>3. factory(Infinity):</h4>
  <p style="padding-left: 8px">a.length is 0 because setting an element at an index of Infinity does not change the array's length.</p>
  <h4>4. factory(null): </h3>
  <p style="padding-left: 8px">a.length is 0 because setting an element at an index of null does not change the array's length.</p>
</details>

### 2. Explain the result of output:

``` javascript
function* number() {
  for (let i = 0; i < 3; i++) {
    console.log(i);
    yield i;
  }
}
const y = number();
number().next();
number().next();
number().next();

// output:- 0
//          0
//          0
```
### 3. Explain the result of output:
``` javascript
(function test() {
  console.log(
    {}.constructor === arguments.constructor,
    [].constructor === arguments.constructor
  );
})();

// output:- true false
```
<details>
  <summary>Explanation</summary>
  <ul>
    <li>{}.constructor === arguments.constructor compares Object to Object. This is true because both refer to the same constructor.</li>
    <li>[].constructor === arguments.constructor compares Array to Object. This is false because Array and Object are different constructors.</li>
    <li>In non-strict mode `arguments.constructor`:- object where as strict-mode it is not an instance of object.</li>
  </ul>
</details>

### 4. Explain the result of output:
``` javascript
(function test (arguments) {
	console.log(arguments[0]);
})(100);

// output:- undefined
```
<details>
  <summary>Explanation</summary>
  <p>undefined(argument is num i.e 100) not an array</p>
</details>
