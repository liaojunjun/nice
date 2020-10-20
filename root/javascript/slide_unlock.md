window 上监听 mousemove、mouseup 而不是滑块或滑板上

```ts
const mousedown = fromEvent(unlock_slide, "mousedown");
const mousemove = fromEvent(window, "mousemove");
const mouseup = fromEvent(window, "mouseup");
```

<iframe src="https://liaojunjun.github.io/nice/root/javascript/slide_unlock_demo.html" width="100%" height="620"></iframe>
