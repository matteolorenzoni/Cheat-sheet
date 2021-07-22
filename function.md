# Index

- [Superior level function](#Superior-level-function)
- [Generator](#Generator)

## Superior level function

```javascript
let duplicate = function(x) => 2*x;

console.log(duplicate(3)); // 6
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br></br></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Generator

```javascript
function* createIterator() {
  yield 1;
  yield 2;
  yield 3;
}

let iterator = createIterator();
console.log(iterator.next()); // {value: 1, done: false}
console.log(iterator.next()); // {value: 2, done: false}
console.log(iterator.next()); // {value: 3, done: false}
console.log(iterator.next()); // {value: undefined, done: true}
```

```javascript
function* createIterator() {
  console.log("step1");
  console.log("ciao");
  yield 1;

  console.log("aaaa");
  yield 2;
  yield 3;
}

let iterator = createIterator();

iterator.next();

console.log("pausina");

iterator.next();

//print
//----step1
//----ciao
//----pausina
//----aaaa
```
