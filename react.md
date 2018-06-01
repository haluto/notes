[TOC]

# React生命周期
* [参考1](https://www.cnblogs.com/gdsblog/p/7348375.html)
* [参考2](http://www.css88.com/react/docs/react-component.html)

![life-cycle](.\images\react\life-cycle.jpg)

# React Tips

## Import images.
```
import ic_settings from "./icons/ic_settings.png";
```

### Using image for background
```
<Button 
  type="primary" shape="circle" 
  style={{backgroundImage: `url(${ic_settings})`}}
></Button>
```

### Using image for &lt;img&gt;
```
<img src={ic_settings}></img>
```

## Ref

### Using ref as string
```
<canvas ref="imageCanvas">
```

### Using ref as callback
```
var items = [];
      this.state.imageList.map((listItem, i) => {
          items.push(
              <div className="image-list-item" key={i}
                  ref={child => this._child=child}
                  onClick={(value, virtualDomElement, index) => this.handleImageClick(listItem, this._child, i)}
              >
......
......
```
通过ref={child => this._child=child}可以得到virtual dom，再通过onClick将virtualDomElement传出，需要使用时用ReactDOM.findDOMNode()即可获得element。

## transitioned
transitionend在某些情况下不会触发，所以react会废弃transitionend。
[参考](https://developer.mozilla.org/en-US/docs/Web/Events/transitionend)

# JS Tips

## JS数组方法
### join()
// TODO:

### push(), pop()
// TODO:

### shift(), unshift()
// TODO:

### sort()
// TODO:

### reverse()
// TODO:

### concat()
将参数添加到原数组中。这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。
```js
var arr = [1,3,5,7];
var arrCopy = arr.concat(9,[11,13]);
console.log(arr); // [1,3,5,7]
console.log(arrCopy); // [1,3,5,7,9,11,13]
```

### slice()
返回从原数组中指定开始下标到结束下标之间的项组成的新数组。
slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。
在只有一个参数的情况下， slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。
```js
var arr = [1,3,5,7,9,11];
var arrCopy = arr.slice(1);
var arrCopy2 = arr.slice(1,4);
var arrCopy3 = arr.slice(1,-2);
var arrCopy4 = arr.slice(-4,-1);
console.log(arr); //[1, 3, 5, 7, 9, 11](原数组没变)
console.log(arrCopy); //[3, 5, 7, 9, 11]
console.log(arrCopy2); //[3, 5, 7]
console.log(arrCopy3); //[3, 5, 7]
console.log(arrCopy4); //[5, 7, 9]
```

### splice()
splice()方法可以实现删除、插入和替换。
* 删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。例如， splice(0,2)会删除数组中的前两项。
* 插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、 0（要删除的项数）和要插入的项。例如，splice(2,0,4,6)会从当前数组的位置 2 开始插入4和6。
* 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。例如，splice (2,1,4,6)会删除当前数组位置 2 的项，然后再从位置 2 开始插入4和6。

splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项，如果没有删除任何项，则返回一个空数组。
```js
var arr = [1,3,5,7,9,11];
var arrRemoved = arr.splice(0,2);
console.log(arr); //[5, 7, 9, 11]
console.log(arrRemoved); //[1, 3]
var arrRemoved2 = arr.splice(2,0,4,6);
console.log(arr); // [5, 7, 4, 6, 9, 11]
console.log(arrRemoved2); // []
var arrRemoved3 = arr.splice(1,1,2,4);
console.log(arr); // [5, 2, 4, 4, 6, 9, 11]
console.log(arrRemoved3); //[7]
```

### indexOf(), lastIndexOf()
// TODO:

### forEach()
// TODO:

### map()
// TODO:

### filter()
// TODO:

### every()
// TODO:

### some()
// TODO:

### reduce(), reduceRight()
// TODO: