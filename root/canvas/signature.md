1. 监听 canvas 的 mousedown、mousemove
2. 监听 window 的 mouseup
3. 组合前后点坐标

```ts
mousedown.pipe(
  switchMap((e) =>
    mousemove.pipe(
      takeUntil(mouseup),
      startWith({
        x: e.offsetX,
        y: e.offsetY,
      })
    )
  ),
  map((e) => ({
    x: e.offsetX,
    y: e.offsetY,
  })),
  pairwise()
);
```

<iframe src="./canvas/signature_demo.html" width="100%" height="350"></iframe>
