# JavaScript

首先理解一下
### 赋值  
1.基本数据类型(字符串,数值,数组,对象,布尔值) es6新增(null,undefined,symbol)赋值，赋值之后两个变量互不影响
2.引用数据类型:两个变量具有相同的引用，指向同一个对象，相互之间有影响
```
let a = "original"
let b = a
console.log(b) // original

a = "change"
console.log(a) // change

console.log(b) // original

```
对于引用类型进行操作即使是改变a中的基本类型变量也会影响变量b
```
// saucxs
let a = {
    name: "saucxs",
    book: {
        title: "You Don't Know JS",
        price: "45"
    }
}
let b = a;
console.log(b);
// {
// 	name: "saucxs",
// 	book: {title: "You Don't Know JS", price: "45"}
// } 

a.name = "change";
a.book.price = "55";
console.log(a);
// {
// 	name: "change",
// 	book: {title: "You Don't Know JS", price: "55"}
// } 

console.log(b);
// {
// 	name: "change",
// 	book: {title: "You Don't Know JS", price: "55"}
// }
```
### 浅拷贝
源对象和拷贝后的对象的基本类型属于不同的field所以改变源对象的基本类型不会影响拷贝，但是引用类型refObj仍然是同一个对象，拷贝的就是***内存地址***
`Object.assign()`
```
// saucxs
let a = {
    name: "saucxs",
    book: {
        title: "You Don't Know JS",
        price: "45"
    }
}
let b = Object.assign({}, a);
console.log(b);
// {
// 	name: "saucxs",
// 	book: {title: "You Don't Know JS", price: "45"}
// } 

a.name = "change";
a.book.price = "55";
console.log(a);
// {
// 	name: "change",
// 	book: {title: "You Don't Know JS", price: "55"}
// } 

console.log(b);
// {
// 	name: "saucxs",
// 	book: {title: "You Don't Know JS", price: "55"}
// }
```
### 深拷贝
两个变量之间互相不影响，但是速度较慢并且花销较大
