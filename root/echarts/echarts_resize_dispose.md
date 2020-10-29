1. 去抖动
2. 图表 init、resize、dispose

```ts
function debounce(fn, ms = 300) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(fn.bind(this, args), ms);
  };
}

function chartsResize(chartsInstance, opts) {
  const resize = debounce(chartsInstance.resize.bind(null, opts));

  window.addEventListener("resize", resize, false);

  return () => {
    window.removeEventListener("resize", resize);
    chartsInstance.dispose();
  };
}

window.cancel = chartsResize(chart);
```

<iframe data-src="https://liaojunjun.github.io/nice/root/echarts/echarts_resize_dispose_demo.html" width="100%" height="500"></iframe>
