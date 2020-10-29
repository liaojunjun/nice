1. debounceTime 节流操作信号
2. switchMapTo 转 of(0) 并延时 time 分钟,信号发出时间在 time 内阻止发出 0,否则将发出 0
3. 如果最后发出 0，则用户下线了

```ts
function userOffline(time = 15) {
  return merge(
    fromEvent(document, "mousemove"),
    fromEvent(document, "click"),
    fromEvent(document, "keydown")
  ).pipe(debounceTime(1000), switchMapTo(of(0).pipe(delay(time * 60 * 1000))));
}
```

<iframe data-src="https://liaojunjun.github.io/nice/root/rxjs/user_offline_demo.html" width="100%" height="50"></iframe>
