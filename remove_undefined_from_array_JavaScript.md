To remove undefined elements from array in JavaScript

eg: 
```
var list = [1, 2, undefined, 4]
list = list.filter(ele => ele)

console.log(list)   #[1, 2, 4]
```
