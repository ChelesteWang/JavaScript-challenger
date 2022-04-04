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

### 实现 Promise API

实现 Promise.all

```js
function myPromiseAll(promiseList) {
  return new Promise((resolve, reject) => {
    let result = [];
    for (promise of promiseList) {
      Promise.resolve(promise)
        .then((res) => {
          result.push(res);
        })
        .catch((err) => {
          reject(err);
        });
    }
    resolve(res);
  });
}

```

实现 Promise.race

```js
function myPromiseRace(promiseList) {
  return new Promise((resolve, reject) => {
    for (promise of promiseList) {
      Promise.resolve(promise)
        .then((res) => {
          resolve(res);
        })
        .catch((err) => {
          reject(err);
        });
    }
  });
}
```

## 数组扁平化

```js
function flat(arr) {
  return arr.reduce((pre, cur) => {
    return pre.concat(Array.isArray(cur) ? flat(cur) : cur);
  }, []);
}
```

## 深拷贝

```js
function deepClone(obj, hash = new WeakMap()) {
    if (hash.has(obj)) {
        return obj;
    }
    let res = null;
    const reference = [Date, RegExp, Set, WeakSet, Map, WeakMap, Error];

    if (reference.includes(obj?.constructor)) {
        res = new obj.constructor(obj);
    } else if (Array.isArray(obj)) {
        res = [];
        obj.forEach((e, i) => {
            res[i] = deepClone(e);
        });
    } else if (typeof obj === "object" && obj !== null) {
        res = {};
        for (const key in obj) {
            if (Object.hasOwnProperty.call(obj, key)) {
                res[key] = deepClone(obj[key]);
            }
        }
        hash.set(obj, res);
    } else {
        res = obj;
    }
    return res;
}
```
