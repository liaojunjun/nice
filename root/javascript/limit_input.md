1. 考虑中文输入
2. 模板中传正则表达式字符串

<iframe data-src="https://liaojunjun.github.io/nice/root/javascript/limit_input_demo.html" width="100%" height="200"></iframe>

#### 组合键

```ts
function runOnKeys(fn, ...keys) {
  const keyObj = {};
  function clear() {
    keys.forEach((key) => {
      keyObj[key] = false;
    });
  }
  clear();

  document.addEventListener(
    "keydown",
    (e) => {
      if (keys.includes(e.code)) {
        keyObj[e.code] = true;
      }
      if (Object.values(keyObj).every(Boolean)) {
        clear();
        fn();
      }
    },
    false
  );
  document.addEventListener("keyup", clear, false);
}

runOnKeys(() => alert("Hello!"), "KeyQ", "KeyW");
```
