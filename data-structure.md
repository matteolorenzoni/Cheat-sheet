# Index

- [Object](#Object)
  - [Pass object as a value](#Pass-object-as-a-value)
  - [Pass an object as a reference](#Pass-an-object-as-a-reference)
- [Set](#Set)
  - [Initialized set with element](#Initialized-set-with-element)
  - [Multiple elements with same value](#Multiple-elements-with-same-value)
  - [Property](#Property)
  - [Iteration](#Iteration)
  - [Trasform a set into an array](#Trasform-a-set-into-an-array)
- [Map](#Map)
  - [Add element](#Addelement)

## Object

#### Pass object as a value

```javascript
let user1 = {
  name = "Manes"
}

let user2 = user1;

console.log(user1);  // Manes
console.log(user2);  // Manes

user2.name = "Luigi";

console.log(user1); // Luigi
console.log(user2); // Luigi
```

#### Pass an object as a reference

```javascript
let user1 = {
  name = "Manes"
}

let user2 = JSON.parse(JSON.stringify(user1));

user2.name = "Luigi";

console.log(user1); // Manes
console.log(user2); // Luigi
```

```javascript
let user1 = {
  name = "Manes"
}

let user2 = Object.assign({}, user1);

user2.name = "Luigi";

console.log(user1); // Manes
console.log(user2); // Luigi
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br></br></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Set

#### Initialized set with element

```javascript
let set = new Set([1, 2, 3, 3, 3, 3, 3]);

console.log(set.size); // 3
```

#### Multiple elements with same value

```javascript
let set = new Set();

set.add(56);
set.add("56");
set.add("test");
set.add("test");
set.add("test");
set.add("test");

console.log(set.size); // 3
```

#### Set Property

```javascript
set.add(56); // add element
set.delete(56); // delete element
set.has(56); // return true or false depending on if set has that value
```

#### Iteration

```javascript
set.forEach((value, key, set) => {
  console.log(value); // value of element
  console.log(key); // key of element
  console.log(set); // size of set
});
```

#### Trasform a set into an array

```javascript
// utils for example to delete duplicates
let set = new Set([1, 2, 3, 3, 3, 3, 3]);
let array = [...set];

console.log(array); // [1, 2, 3]
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br></br></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Map

#### Add element

```javascript
map.set("user1", "Coosimo");
map.set(5, "Veloxey");
```

#### Map Property

```javascript
map.set("user1", "Coosimo"); // add element
map.delete(56); // delete element
map.get("user1"); // return the relative value
map.has("user1"); // return true or false depending on if map has that value
```
