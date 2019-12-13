##### 会改变原数组的方法：
- push()：末端添加一个或多个元素，并返回新的长度。，该方法会改变原数组；
- pop()：删除数组最后一个元素，并且返回它删除的元素的值，该方法会改变原数组；
- unshift()：数组第一个位置增加元素，并返回新的长度。，该方法会改变原数组；
- shift()：删除数组第一个元素，并返回第一个元素的值。，该方法会改变原数组；
- reverse()：颠倒数组中元素的顺序，该方法会改变原数组；
- splice()：用于删除或替换原数组的一部分成员，splice的第一个参数是删除的起始位置（从0开始），第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素，注意，该方法会改变原数组。
- sort()：对数组成员进行排序，原数组将被改变

```js
// 用法
let a = ['a', 'b', 'c'];

a.unshift('x'); // 4
a // ['x', 'a', 'b', 'c']
```
 

---
##### 不会改变原数组的方法，需要定义新变量接收：
- valueOf():方法返回数组本身。
- toString():返回数组的字符串形式。
- join()：以参数作为分隔符，将所有数组成员组成一个字符串返回。
- slice()：提取原数组的一部分，返回一个新数组，原数组不变。

```js
let a = ['a', 'b', 'c'];

a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]
```
- concat()：多数组的合并，组成新数组，该方法不会改变原数组；
- map():组成新数组，不会改变原数组；
- filter():组成新数组，不会改变原数组；

---
- indexOf():返回给定元素在数组中第一次出现的位置，如果没有出现则返回-1;
- lastIndexOf():返回给定元素在数组中最后一次出现的位置，如果没有出现则返回-1


# 一、Array的迭代方法

`every()` 、`filter()` 、`forEach()` 、`map()` 、`some()`

　　ES5定义了五个迭代方法，每个方法都接收两个参数：要在每一项上运行的函数和运行该函数的作用域对象（可选的），作用域对象将影响this的值。传入这些方法中的函数会接收三个参数：数组的项的值、该项在数组中的位置和数组对象本身。
　　
- map():返回一个新的Array，每个元素为调用func的结果

- filter():返回一个符合func条件的元素数组

- some():返回一个boolean，判断是否有元素是否符合func条件

- every():返回一个boolean，判断每个元素是否符合func条件

- forEach():没有返回值，只是针对每个元素调用func

#### 1.every() 和 some()

`every()`是对数组中的每一项运行给定函数，如果该函数对每一项都返回true，则返回true。

`some()`是对数组中的每一项运行给定函数，如果该函数对任一项返回true，则返回true。

`every()`和`some()`很相似，他们都用于查询数组中的项是否满足某个条件，对`every()`来说，传入的函数必须对每一项都返回true，这个方法才返回true；否则，则返回false。而`some()`方法则只要传入的函数对数组中的某一项返回true，就会返回true。

例如：
```js
let numbers=[1,2,3,4,5,4,3,2,1];

//三个参数：当前成员、当前位置 和 数组本身
let everyResult=numbers.every(function(item,index,array){

    return (item>2);

});

alert(everyResult);//false

let someResult=numbers.some(function(item,index,array){

return (item>2);

});

alert(someResult);//true
```


以上代码调用了every()和some(),传入的函数只要给定项大于2就会返回true。对于every()，它返回的是false，因为只有部分数组符合条件 ; 而对于some()，结果就是true，因为至少有一项是大于2的。

 

#### 2.filter()

filter()是对数组中的每一项运行给定函数，返回该函数会返回true的项所组成的数组。它利用指定的函数确定是否在返回的数组中包含某一项。

例如：
```js
let numbers=[1,2,3,4,5,4,3,2,1];

let filterResult=numbers.filter(function(item,index,array){

return (item>2);

});

alter(filterResult); //[3,4,5,4,3];
```


此例子中，传入的函数要返回一个所有数值都大于2的数组，通过调用filter()方法创建并返回了包含3/4/5/4/3的数组，因为传入的函数对它们的每一项都返回true。这个方法对查询符合某些条件的所有数组项非常有用。

#### 3.map()

map()是对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。这个数组的每一项都是在原始数据中的对应项上运行传入函数的结果.

例如：

```js
let numbers=[1,2,3,4,5,4,3,2,1];

//一个参数
let c = numbers.map(function(n){
    return n+1;
});
console.log(c);//[ 2, 3, 4, 5, 6, 5, 4, 3, 2 ]

//三个参数：当前成员、当前位置 和 数组本身
let mapResult=numbers.map(function(item,index,array){

    return item*2;

});

alert(mapResult); //[2,4,6,8,10,8,6,4,2]
```


以上代码返回的数组中包含每个数乘以2之后的结果，这个方法适合创建包含的项与另一个数组一一对应的数组。


map方法不会跳过undefined和null，但是会跳过空位。
```js
let f = function(n){ return n + 1 };

[1, undefined, 2].map(f) // [2, NaN, 3]
[1, null, 2].map(f) // [2, 1, 3]
[1, , 2].map(f) // [2, , 3]
```



map方法不仅可以用于数组，还可以用于字符串，用来遍历字符串的每个字符。但是，不能直接使用，而要通过函数的call方法间接使用，或者先将字符串转为数组，然后使用。

```js
let upper = function (x) {
  return x.toUpperCase();
};

[].map.call('abc', upper)
// [ 'A', 'B', 'C' ]

// 或者
'abc'.split('').map(upper)
// [ 'A', 'B', 'C' ]
```




#### 4.forEach()

forEach() 是多数组中的每一项运行给定函数，这个方法没有返回值。它只是对数组中的每一项运行传入的函数，没有返回值。本质上与使用for循环迭代数组一样。


```js
let numbers=[1,2,3,4,5,4,3,2,1];

numbers.forEach(function(iterm,index,array){

//执行某些操作

});
```

forEach方法会跳过数组的空位。

```js
let log = function (n) {
 console.log(n + 1);
};

[1, undefined, 2].forEach(log)
// 2
// NaN
// 3

[1, null, 2].forEach(log)
// 2
// 1
// 3

[1, , 2].forEach(log)
// 2
// 3
```
forEach方法也可以用于类似数组的对象和字符串。

```js
let obj = {
  0: 1,
  a: 'hello',
  length: 1
}

Array.prototype.forEach.call(obj, function (elem, i) {
  console.log( i + ':' + elem);
});
// 0:1

let str = 'hello';
Array.prototype.forEach.call(str, function (elem, i) {
  console.log( i + ':' + elem);
});
// 0:h
// 1:e
// 2:l
// 3:l
// 4:o
```





>**注意**:forEach方法无法中断执行，总是会将所有成员遍历完。如果希望符合某种条件时，就中断遍历，要使用for循环。

总结：这些数组方法通过执行不同的操作可以大大方便处理数组的任务，支持这些迭代方法的浏览器有IE9+、Firfox2+、Safari3+、Opera9.5、Chrome。


# 二、Js遍历数组的方式及其性能对比

Js数组遍历，基本有`for`、`for..in`、`forEach`、`for..of`、map等一些方法，下面进行对比分析:

#### 1、普通for循环
最简单一种，使用频率高，性能不差，但仍然有优化空间。　

```js
let arr = ['wukong', 'bajie', 'shaseng' ]
for(let i = 0; i < arr.length; i++) {
   console.log(arr[i])
} 
```
#### 2、优化版for循环

优化后将长度缓存起来，避免重复获取长度，当数据较大时，回报比较明显。
**性能上基本算最高**。　　

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
let len = arr.length;
for(let i = 0; i < len; i++) {
   console.log(arr[i])
} 
```
#### 3、弱化版for循环
这种方法其实严格上也属于for循环，只不过是没有使用length判断，而使用变量本身判断

实际上，这种方法的性能要远远小于普通for循环

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
for(let i = 0; arr[i]!=null; i++) {
   console.log(arr[i])
}
```




#### 4、forEach循环
数组自带的forEach,使用频率高，实际性能比普通for循环弱

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
arr.forEach(function(e)) {
   console.log(e);
} 
```

#### 5、foreach变种
由于foreach是Array型自带的，对于一些非这种类型的，无法直接使用(如NodeList)，所以才有了这个变种，使用这个变种可以让类似的数组拥有foreach功能。

实际性能要比普通foreach弱
```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
Array.prototype.forEach.call(arr,function(e){  
   console.log(e);
});
```


#### 6、for..in循环
效率最低

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
for(i in arr){
    console.log(arr[i]) 
})
```
>**注**:for..in常用于遍历对象，可遍历出所有存在于该对象的属性(Object.hasOwnProperty("a") 为true)，但只能遍历出对象中可枚举的属性（enumerable 为true）.


#### 7、map
使用比较广泛，虽然优雅，但是效率其实还不如forEach

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
arr.map(function(e)) {
   console.log(e);
} 
```
#### 8、for..of循环遍历
这种方式是es6里面用到的，性能要好于forin，但仍然比不上普通for循环

```js
let arr = ['wukong', 'bajie', 'shaseng' ]；
for(let value of arr){
    console.log(value) 
} 
```
综合而言，forin最慢，优化后的for循环最快。







