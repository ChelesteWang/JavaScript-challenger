## 实现节流与防抖

防抖函数实现，距离上次执行多少秒之后执行

```js
function debounce(fn, delay) {
  let timer = null;
  return function () {
    if (timer !== null) {
      clearTimeout(timer);
    }
    timer = setTimeout((...args) => {
      fn.apply(this, args);
    }, delay);
  };
}

```
节流函数实现，每多少秒执行一次

