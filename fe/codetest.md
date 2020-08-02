## 字符串压缩
给定由普通英文字母组成的非空字符串s1，要求将连续出现的字符压缩成字符和该字符连续出现的次数，并返回新的字符串s2。s1字符串的长度不超过100。

输入描述: 
全部由普通英文字符组成的长度不超过100的字符串 。
输出描述: 
由英文字符和数字组成的字符串，其中数字表示它前面的字符在输入字符串中连续出现的次数。

示例

输入：
aabccccaaa 

输出：
a2bc4a3 

```js
function strZip(str) {
  if (str === '') {
    return '';
  }
  
  let pre = str[0], 
      count = 1,
      ans = '', 
      n = str.length;

  for (let i = 1; i < n; i++) {
      if (str[i] !== pre) {
          ans += count === 1 ? pre : pre + count;
          pre = str[i]
          count = 1;
      } else {
          count++;
      }
  }

  ans += count === 1 ? pre : pre + count;
  
  return ans;
}
```

## 版本号比对

```js
var compareVersion = function(version1, version2) {
  let list1 = version1.split('.');
  let list2 = version2.split('.');
  let n = Math.max(list1.length, list2.length);
  for(let i = 0; i < n; i++) {
      let cur1 = parseInt(list1[i] || 0);
      let cur2 = parseInt(list2[i] || 0);
      if (cur1 > cur2) {
          return 1;
      }
      if (cur2 > cur1) {
          return -1;
      }
  }
  return 0;
};
```

## [扔鸡蛋问题](https://leetcode-cn.com/problems/super-egg-drop/)