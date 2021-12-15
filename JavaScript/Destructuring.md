### Destructuring:

unpacking elements from an array or properties from an object and assigning to new variables   

1. array destructuring
2. object destructuring

if variables are in same count as values
```
const [a, b] = [1, 2];
console.log(a) // 1
console.log(b) // 2
```
if variables are more than values
```
const [a, b] = [1];
console.log(a) // 1
console.log(b) // undefined
```

if variables are less than values
```
const [a, b] = [1, 2, 3];
console.log(a) // 1
console.log(b) // 2
```

assigning after decleration

```
let a = 1,
  b = 2;
[a, b] = [10, 20, 30];
console.log(a); // 10
console.log(b); // 20
```

with default values

```
const [a = 1, b = 2] = [10, 20, 30];
console.log(a); // 10
console.log(b); // 20
```

```
const [a = 1, b = 2] = [10];
console.log(a); // 10
console.log(b); // 2
```

with rest operator:
```
const [a, ...b] = [1, 2, 3, 4, 5];
console.log(a) // 1
console.log(b) // [2, 3, 4, 5]
```

ignoring elements:
```
const [a, , c] = [1, 2, 3];
console.log(a); // 1
console.log(c); // 3
```

### Object destructuring:
```
let emp = {
  name: 'Gopal',
  age: 20,
};

const { name, age } = emp;
console.log(name); // Gopal
console.log(age); // 20
console.log(email); // Error: email is not defined
```

with spread operator:
```
let emp = {
  name: 'Gopal',
  age: 20,
  email: 'g@gmail.com',
};

const { name, ...otherDetails } = emp;
console.log(name); // Gopal
console.log(otherDetails); // {age: 20, email: "g@gmail.com"}

```


### combined (array + object destructing)
```
let employees = [
  {
    name: 'Gopal',
    age: 20,
    email: 'g@gmail.com',
  },
  {
    name: 'Ram',
    age: 10,
    email: 'r@gmail.com',
  },
  {
    name: 'Siva',
    age: 20,
    email: 's@gmail.com',
  },
];

const [gopal, , { name }] = employees;
console.log(gopal); // {name: "Gopal", age: 20, email: "g@gmail.com"}
console.log(name); // Siva
```