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

```js
function throttle(fn, delay) {
  let lastTime = 0;
  return function (...args) {
    let now = +new Date();
    if (now - lastTime > delay) {
      lastTime = now;
      func.apply(this, args);
    }
  };
}

```

## 实现 new 函数

最简版

```js

function myNew(cfn, ...args) {
  let newObj = Object.create(cfn.prototype);
  let res = newObj.apply(this, args);
  return typeof res == "object" ? res : newObj;
}

```

## 实现 Ajax

简易版

```js
function myAjax(url, ...args) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url, false);
    xhr.onreadystatechange = function () {
      if (xhr.readyState == 4 && xhr.status == 200) {
        resolve(xhr.responseText);
      } else {
        reject("请求失败");
      }
    };
    xhr.send();
  });
}

```
