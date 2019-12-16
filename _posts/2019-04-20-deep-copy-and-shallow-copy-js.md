---
layout: post
title: Deep copy và shallow copy trong Javascript
tags: [deep copy, shallow copy, javascript]
comments: true
---

<!-- Content here -->
Phân biệt deep copy và shallow copy trong Javascript
<!-- ![copy logo](/img/copy-160128_1280.png) -->
<div class="flex justify-center">
  <img src="/img/copy-160128_1280.png" height="300">
</div>

**Shallow copy**: Chỉ copy object cha, các property phía trong vẫn được reference về object cũ
```javascript
const src = { p1: { c1: 1, c2: '2' }, p2: 'p2' }
const dist = Object.assign({}, src);
src.p1 === dist.p1 //true
src.p1.c1 = 2
console.log(dist.p1.c1) //2
```

**Deep copy**: Copy hết tất tần tật các property bên trong, dù nó có nesting bao nhiêu đi chăng nữa
```javascript
// import _ from 'lodash'
const src = { p1: { c1: 1, c2: '2' }, p2: 'p2' }
const dist = _.cloneDeep(src);
src.p1 === dist.p1 //false
src.p1.c1 = 2
console.log(dist.p1.c1) //1
```

### jQuery
```javascript
// Shallow copy
var newObject = jQuery.extend({}, oldObject);

// Deep copy
var newObject = jQuery.extend(true, {}, oldObject);
```

### Lodash
```javascript
// Shallow copy
var newObject = _.clone(oldObject);

// Deep copy
var newObject = _.cloneDeep(oldObject);
```

### JSON.stringify
```javascript
// Deep copy
var newObject = JSON.parse(JSON.stringify(oldObject));
// => Bad performance
// => Lost prototype
// => Error khi có property tham chiếu lẫn nhau
```

### Object.assign
```javascript
// Shallow copy
var newObject = Object.assign({}, oldObject);
```

### Spread operator
```javascript
// Shallow copy
var newObject = {...oldObject};
var newArray = {...oldArray};
```
