---
title: 排序
date: 2018-07-15 09:47:21
tags: 'Vue'
categories: 前端
---


# 算法题  
    如下数字: 35 99 18 76 12  
- 桶排序  
    有[100] for初始化数组  
    将数字放到相应的位置  

    **思想**： 

    ```
    利用数组的下标是有序的,待排序的数字大小在下标的范围内，当数组下标等于要排序的数组时
    用待排序的数字坐桶的下标 给相应项+1 类似于做标记的
    myIdea:当下标等于待排序的数字大小 即输出下标 相当于输出较小的数字 
    ```  

    **时间复杂度:**  
       时间复杂度 循环  
       O(M+N) 一重循环最大值99 100，又一重循环N，  
       之后又有一层循环M 有值的桶子  
       嵌套循环 >= 0 1 2 3有限的，<N   M+N  
         多层循环是最花时间M+N  
         O(M+N+M+N)=O(2*(M+N))  O(M+N)
 
    **缺点:** 占物理内存，因为要分配M个元素的数组  
        
- 冒泡排序  

```js
// 冒泡排序 
// 思想: 比较相邻的元素。如果第一个比第二个大，就交换两数顺序  
const source_arr = [35,18, 99, 18, 76, 12];
function bubbleSort(arr) {
    const len = arr.length;
    for (let i = 0; i < len; i++) {
        for (let j = 0; j < len - 1 - i; j++) {
            if (arr[j] > arr[j+1]) {        // 相邻元素两两对比
                let temp = arr[j+1];        // 元素交换
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}
console.log(bubbleSort(source_arr));
```

- 选择排序  
> 第一重循环默认把 i 个作为最小值与后面 j 循环中的的数进行比较，也就是通过第二重循环与后面的值进行比较
```js
// n^2
// 找到数组中最小的值放在第一位，第二小的放在第二位...
// 基址查询
function SelectSort(arr) {
  let len = arr.length
  for(let i = 0; i < len; i++) {
    let minIndex = i
    // 如果已经选择了， 前面的就一定是有序的
    for( let j = i; j < len; j++) {
      if( arr[j] < arr[minIndex]) {
        // 循环和默认的最小值进行比较， 如果更小纪录下标
        minIndex = j
        console.log(i, j)
      }
    }
    if(minIndex !== i) {
      [arr[minIndex], arr[i]] = [arr[i], arr[minIndex]]
    }
  }
  return arr
}
console.log(SelectSort([45,21,45,12,56,12,67,32,98]))

```

- 快排排序  
   > 因为采用了分治思想，所以快  形象的例子 三个数之间进行排序 a b c 再加递归  

```js
// 简单排序： 冒泡、选择、插入 时间复杂度都是 n^2
// 复杂排序： 快排、堆排、归并排序 时间复杂度都是 (log2^n)* n
// 分治
// 快排 log2(n)* n for循环 n次
  // 1. 随机选择一个数组中的一个数作为一个基准 一般是中点
  // 2. 其余数字跟他比较， 小的放左边 大的放右边
  // 3. 利用递归的思想， 将左右两边的数重复以上两步
function QuickSort(arr) {
  // 这里是出口 当数组长度小于等于1的时候结束递归
  if(arr.length <= 1) {
    return arr
  }
  let pivotIndex = Math.floor(arr.length /2)
  // 把中间基准值从数组提出来
  pivot = arr.splice(pivotIndex, 1)[0]  // 选出相应位置的值
  console.log(pivot)
  let left = [], right = []
  for(let i = 0, len = arr.length ; i < len; i++) {
    if( arr[i] < pivot) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }
  return QuickSort(left).concat(pivot, QuickSort(right))
}
console.log(QuickSort([85, 24, 63, 45, 17, 31, 78, 56]))
```





