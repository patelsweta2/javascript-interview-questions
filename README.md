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

```
<details>
  ``` javascript
  // output 
  1 101 0 0
  ```
</details>
