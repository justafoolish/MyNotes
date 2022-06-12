---
title: Diary
date: 2022-03-17
updated: 2022-06-11
---



---

> **[11/06/2022]** React snippset update

* **rfce**

```jsx
import React from 'react'

function (|) {
    return ( | );
}

export default |;
```
> Typora switching source: **`cmd + /`**




---

> **[30/05/2022]** JS Array method

* reduce

```js
const result = array.reduce((prevValue, curValue, curIndex), initValue);

const num = [1,2,3,4];
const total = num.reduce((prev, cur) => prev += cur, 0); 

console.log(total) // 10
```

* filter

```js
const filter = array.filter((item, index, arr) => condition)

const num = [1,2,3,4];
const filter = num.filter((item) => item > 2);

console.log(filter) // [3,4]
```

* some

```js
const some = array.some((item, index, arr) => condition) // true or false

const num = [1,2,3,4];
const some = array.some(item => item > 3);

console.log(some) // true

const some = array.some(item => item < 0)

console.log(some) // false
```

* every

```js
const every = array.every((item, index, arr) => condition) //true or false

const num = [1,2,3,4];
const some = array.every(item => item > 3);

console.log(some) // false

const some = array.every(item => item > 0)

console.log(some) // true
```



----

> **[28/05/2022] ** React snippset

**ffc - Function Component**

```jsx
function (|) {
    return ( | );
}

export default |;
```

**sfc - Stateless Function Component (Arrow function)**

```jsx
const | = props => {
  return ( | );
};

export default |;
```

**uef - useEffect Hook**

```jsx
useEffect(() => {
  |
}, []);
```



-----

> **[17/03/2022] Vi/Vim/Nvim Command**
>
> Mar. 17, 2022, 11:00 pm



```
$ : start line
0 : end line
```



```
gg : start file
G : end file
```



```
v : visual mode
y : copy
d : cut

yy : copy current line
dd : cut current line
```

