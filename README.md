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

```javascript
(function test() {
  var arguments;
  console.log(arguments[0]);
})(200);

// output :- 200
```
<details>
	<summary>Explanation</summary>
	<p>The built-in arguments object contains this value.</p>
</details>

``` javascript
(function test() {
   let arguments;
   console.log(arguments[0]);
 })(200);

// output:- TypeError

```
<details>
	<summary>Explanation</summary>
	<p>let var will shadow built-in arguments</p>
</details>

``` javascript
(function test() {
  function sum() {
    var sum = 0,
      i;
    for (i in arguments) {
      sum += i;
    }
    return sum;
  }
  console.log(sum(10, 20, 30, 40, 50, 60));
})();

// output:- 0012345
```
<details>
	<summary>Explanation</summary>
	<ul><h4>Type Coercion in JavaScript:</h4>
		<li>When you use the += operator, JavaScript performs type coercion based on the types of the operands.</li>
		<li>Initially, sum is a number (0).</li>
		<li>When sum += i is executed, i is a string (the index of arguments), so JavaScript converts sum to a string and concatenates i.</li>
	</ul>
</details>

### 5. Explain the result of output:
``` javascript
(function test() {
  console.log(
    function () {} instanceof Object,
    function () {} instanceof Function,
    Function instanceof Object,
    Object instanceof Function
  );
})();
// output:- true true true true

```
<details>
	<summary>Explanation</summary>
	<ul>
		<li>Every function is an instance of both Object and Function.</li>
		<li>The Function constructor is an instance of Object.</li>
		<li>The Object constructor is an instance of Function.</li>
	</ul>
</details>
### 6. Explain the result of output:

``` javascript
(function test() {
  console.log(function () {}.apply.length);
})();

// output :- 2

```
<details>
	<summary>Explanation</summary>
	<p>The apply method is defined to accept two parameters (thisArg and argArray), hence its length property is 2.</p>
</details>

### 7. Explain the result of output:

``` javascript
console.log(
  Function instanceof Function,
  Function.prototype instanceof Function,
  Function.prototype.isPrototypeOf(Function),
  Function === Function.prototype,
  Function === Function.prototype.constructor,
  typeof Function.prototype,
  typeof Function
);

// output :- true false true false true 'function' 'function'

```

``` javascript
(function test() {
  console.log(
    Function === Object.constructor,
    Function === Number.constructor,
    Function === Function.constructor,
    Function === Window.constructor,
    Object === Object.prototype.constructor,
    Number === Number.prototype.constructor,
    Array === Array.prototype.constructor,
    Window === Window.prototype.constructor
  );
})();
// output :- true true true true true true true true

```

``` javascript
(function test() {
  console.log(
    typeof Object.prototype,
    typeof String.prototype,
    typeof RegExp.prototype
  );
})();
// output:- object object object

```
### 8. Async/Await:

#### 8.1:

``` javascript
function intro(name) {
  setTimeout(() => {
    return `my name is ${name}`;
  },1000);
}

const myIntro = intro("Sweta");
console.log(myIntro);
 // output :- undefined

```
<details>
	<summary>Explanation</summary>
	<p>The intro function calls setTimeout, but it doesn't have a return statement that waits for the setTimeout to complete. As a result, intro returns undefined immediately because there is no explicit return value.</p>
</details>

#### 8.1.1:

``` javascript
function intro(name, callback) {
  setTimeout(() => {
    callback(`my name is ${name}`);
  }, 1000);
}

const myIntro = () => {
  intro("Sweta", (result) => {
    console.log(result);
  });
};
myIntro();

// output:- my name is Sweta

```

#### 8.2

``` javascript
function introPromGen(name) {
  return new Promise((resolve, reject) => {
    const condition = false;
    if (condition) {
      setTimeout(() => {
        resolve(`my name is ${name}`);
      }, 1000);
    } else {
      reject("no name found");
    }
  });
}

function cityPromGen(city) {
  return new Promise((resolve, reject) => {
    const condition = true;
    if (condition) {
      setTimeout(() => {
        resolve(`${city}`);
      }, 1000);
    } else {
      reject("no city found");
    }
  });
}

introPromGen("Sweta")
  .then((data) => {
    console.log(data);
    return cityPromGen("Patna");
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => console.log(err));

// output:- no name found

```
#### 8.4

``` javascript
async function test() {}
const output = test();
console.log(output);

// output:- Promise
```
<details>
	<summary>Explanation</summary>
	<p>Js Engine by default convert the output of async function as Promise.</p>
</details>

#### 8.5:

``` javascript
function promiseGen() {
  console.log("inside PromiseGen");
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("this is a resolved promise");
    }, 5000);
  });
}
console.log("start");

async function test() {
  const a = 1;
  console.log("before promise");
  const promiseResult = await promiseGen();
  console.log("after promise");
  console.log(promiseResult);
  console.log(a);
}
console.log("mid");
test();
console.log("end");

// output:-

// start
// mid
// before promise
// inside PromiseGen
// end
// after promise
// this is a resolved promise
// 1
```

#### 8.6

``` javascript
function promiseGen() {
  console.log("Hello how are you?");
  return "Some meaningfull data";
}
console.log("start");
async function test() {
  console.log("before promiseGen");
  const promiseResult = await promiseGen();
  console.log(promiseGen);
  console.log("after promiseGen");
}

test();
console.log("end");
// output:-

// start
// before promiseGen
// Hello how are you?
// end
// Some meaningfull data
// after promiseGen

```
