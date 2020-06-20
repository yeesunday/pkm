## 冒泡排序

算法步骤

- 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
- 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
- 针对所有的元素重复以上的步骤，除了最后一个。
- 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。

```
function bubbleSort(arr) {
  let l = arr.length
  while(l > 0) {
    for(i = 0; i < l; i++) {
      if(arr[i] > arr[i+1]) {
        [arr[i], arr[i+1]] = [arr[i+1], arr[i]]
      }
    }
    l--
  }
  return arr
}
```

## 快速排序

算法步骤

- 从数组中选择一个元素作为基准点
- 排序数组，所有比基准值小的元素摆放在左边，而大于基准值的摆放在右边。每次分割结束以后基准值会插入到中间去。
- 最后利用递归，将摆放在左边的数组和右边的数组在进行一次上述的 1 和 2 操作。

```
// 简单版，占用较多内存
var quickSort = function(arr) {
  if (arr.length <= 1) {
    return arr;
  }
  var pivotIndex = Math.floor(arr.length / 2);
  var pivot = arr.splice(pivotIndex, 1)[0];
  var left = [];
  var right = [];

  for (var i = 0; i < arr.length; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }
  return quickSort(left).concat([pivot], quickSort(right));
};

// 原地排序
function quickSort(array, left, right) {
  left = typeof left === 'number' ? left : 0
  right = typeof right === 'number' ? right : array.length - 1
  
  // 只有一个元素的数组不用排序
  if (array.length === 1) {
    return array
  }
  // 结束递归条件
  if (left >= right) {
    return false
  }

  const target = array[left]
  let i = left + 1, j = right

  while(i < j) {
    // 交换排序
    while (i < j && array[j] >= target) {
      j--
    }
    while(i < j && array[i] < target) {
      i++
    }
    [array[i], array[j]] = [array[j], array[i]]
  }
  // ij相遇
  if (array[i] < target) {
    [array[left], array[i]] = [array[i], array[left]]
  }
  
  quickSort(array, left, i - 1)
  quickSort(array, i + 1, right)
  return array
}
```

[js算法-快速排序(Quicksort)](https://segmentfault.com/a/1190000017814119)