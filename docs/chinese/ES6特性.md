从我的测试中发现，它支持 __部分__ ES6特性！


拼接数组
------

```javascript
var array = [1, 2, 3]
f(...array)
```

```javascript
var a = [1, 2, 3, 4]
var b = [5, 6, 7, 8]
var concated = [...a, ...b]

concated
#    => [1, 2, 3, 4, 5, 6, 7, 8]
```


数组和对象的解构
------------------------------

```javascript
var a = 1
var b = 2

[a, b] = [b, a]
#    => [2, 1]

a
#    => 2
b
#    => 1
```

```javascript
var object = { cat: 1, dog: 2 }
var { cat, dog } = object

cat
#    => 1
dog
#    => 2
```
