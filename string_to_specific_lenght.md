#### To modify the string to specific length

```
var requiredLenght = 6 

var title = "Gopala rao"
var modifiedTitle = ''

if(title.length < requiredLenght) {
  console.log("adding spaces")
  var spacesToAdd = requiredLenght - title.length
  modifiedTitle = title + ' '.repeat(spacesToAdd)
} else if (title.length > requiredLenght) {
  console.log("slicing title")
  modifiedTitle = title.slice(0, requiredLenght) 
} else {
  console.log("doing nothing")
  modifiedTitle = title
}

console.log(modifiedTitle, modifiedTitle.length)
```
