#### aync await


```
/**AjAX using async await */
const fetchPosts = async () => {
  try {
    const url = 'https://jsonplaceholder.typicode.com/posts';
    const response = await fetch(url); // fetch returns a promise
    const data = await response.json(); //.json() returns a promise
    return data;
  } catch (e) {
    console.log('err', e);
  }
};

fetchPosts().then((data) => console.log(data));
```