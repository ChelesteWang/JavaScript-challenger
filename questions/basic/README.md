# JavaScript 基础

ex1. 例子(添加题目模板)

### 题目：1. 两数相加

题目要求：
实现一个函数实现两数相加

测试用例：
[input]:a = 1 , b = 2  
[output]:3

<details>
<summary>ex1. 答案</summary>

```js
function add(a,b){
  return a+b
}
```
</details>

### 题目：2. 快速排序（2022百度前端校招第三批一面）

题目要求：
用JS实现一个快速排序



<details>
<summary>ex1. 答案</summary>

```js
function swap(A, i, j) {
  const t = A[i];
  A[i] = A[j];
  A[j] = t;
}

/**
 *
 * @param {*} A  数组
 * @param {*} p  起始下标
 * @param {*} r  结束下标 + 1
 */
function divide(A, p, r) {
  const x = A[r - 1];
  let i = p - 1;

  for (let j = p; j < r - 1; j++) {
    if (A[j] <= x) {
      i++;
      swap(A, i, j);
    }
  }

  swap(A, i + 1, r - 1);

  return i + 1;
}

/**
 * 
 * @param {*} A  数组
 * @param {*} p  起始下标
 * @param {*} r  结束下标 + 1
 */
function qsort(A, p = 0, r) {
  r = r || A.length;

  if (p < r - 1) {
    const q = divide(A, p, r);
    qsort(A, p, q);
    qsort(A, q + 1, r);
  }

  return A;
}
```
</details>

