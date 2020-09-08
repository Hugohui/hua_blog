---
title: 【拿下JS算法】：快速排序
date: 2020-09-08 16:22:52
tags: 拿下算法
---

> 实现面试中最常问到的快速排序。

##### 基本思想   
- 在一组数组中，选取一个基准元素
- 将所有小于等于基准的元素都放到左边新数组，将大于基准的元素都放到右边新数组
- 对左边新数组和右边新数组重复前两部，知道数组只剩一个元素

##### 思想重现   
现在有数组[12, 2 , 13, 23, 4, 45], 分步骤执行   
- 第一步   
选择基准元素13   
- 第二步   
将小于等于13的放入左侧数组，大于13放入右侧数组，得到   
[12, 2, 4] (13) [23, 45]   
- 第三步   
对左右两个数组重复第一步和第二部，知道数组只有一个元素。   
(2) [12, 4] 13 (23) [45]   
2 [4] (12) 13 23 45   
2 4 12 13 23 45   

##### 代码实现   
- 定义`quickSort`函数，接受一个数组作为参数。   
```javascript
function quickSort(arr) {
}
```
- 对参数类型进行判断   
```javascript
function quickSort(arr) {
  if ( !Array.isArray(arr)) {
  throw new Error('参数类型错误，请传入数组')
    return
  }
}
```
- 检查数组元素个数，小于等于1，则返回原数组。   
```javascript
function quickSort(arr) {
  if ( !Array.isArray(arr)) {
  throw new Error('参数类型错误，请传入数组')
    return
  }

  if (arr.length <= 1) {
    return arr
  }
}
```

- 选择基准元素，然后定义左侧数组和右侧数组   
```javascript
function quickSort(arr) {
  if ( !Array.isArray(arr)) {
  throw new Error('参数类型错误，请传入数组')
    return
  }

  if (arr.length <= 1) {
    return arr
  }

  const middleNum = arr.splice(Math.floor(arr.length /2), 1)[0]

  const left = [],
        right = [];
}
```

- 遍历数组，将小于等于基准的元素放入`left`数组，大于基准的元素放入`right`数组。   
```javascript
function quickSort(arr) {
  if ( !Array.isArray(arr)) {
  throw new Error('参数类型错误，请传入数组')
    return
  }

  if (arr.length <= 1) {
    return arr
  }

  const middleNum = arr.splice(Math.floor(arr.length /2), 1)[0]

  const left = [],
        right = [];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] <= middleNum) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }
}
```

- 递归重复第一步和第二步，最终的到排序后的数组。   
```javascript
function quickSort(arr) {
  if ( !Array.isArray(arr)) {
    throw new Error('参数类型错误，请传入数组')
    return
  }

  if (arr.length <= 1) {
    return arr
  }

  const middleNum = arr.splice(Math.floor(arr.length / 2), 1)[0]

  const left = [],
        right = [];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] <= middleNum) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }

  return quickSort(left).concat([middleNum], quickSort(right))
}
```

##### 技术点   
数组方法请移步：[Javascript对象之【Array】](https://zhuanlan.zhihu.com/p/165482743)   
- Math   
- splcie   
- concat   
- 递归   