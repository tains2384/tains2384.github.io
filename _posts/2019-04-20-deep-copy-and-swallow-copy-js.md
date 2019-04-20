---
layout: post
title: Deep copy và swallow copy trong Javascript
tags: [deep copy, swallow copy, javascript]
comments: true
---

<!-- Content here -->
Phân biệt deep copy và swallow copy trong Javascript
![copy logo](/img/copy-160128_1280.png)

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
var newObject = JSON.parse({}, oldObject);
```

### Spread operator
```javascript
// Shallow copy
var newObject = {...oldObject};
var newArray = {...oldArray};
```
