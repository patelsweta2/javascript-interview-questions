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
  #### Array.prototype.pop.apply(arguments):
  Array.prototype.pop is a method that removes the last element from an array and returns that element.
  apply(arguments) calls the pop method on the arguments object (which is array-like but not a true array). This removes and returns the last argument passed to factory.
  ###### 1. factory(0):
  arguments is [0]
  Array.prototype.pop.apply(arguments) returns 0
  a[0] = 1, so a becomes [1]
  a.length is 1
  ##### 2. factory(100):
  arguments is [100]
  Array.prototype.pop.apply(arguments) returns 100
  a[100] = 1, so a becomes an array with 101 elements, with 1 at the 100th index.
  a.length is 101
  ##### 3. factory(Infinity):
  a.length is 0 because setting an element at an index of Infinity does not change the array's length.
  ##### 4. factory(null):
  a.length is 0 because setting an element at an index of null does not change the array's length.
</details>
