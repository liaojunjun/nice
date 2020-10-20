```ts
function exchangeCombination(arr) {
  const len = arr.length;
  if (len >= 2) {
    const len0 = arr[0].length;
    const len1 = arr[1].length;
    const items = new Array(len0 * len1);
    let index = 0;
    for (let i = 0; i < len0; i++) {
      for (let j = 0; j < len1; j++) {
        if (Array.isArray(arr[0][i])) {
          items[index] = arr[0][i].concat(arr[1][j]);
        } else {
          items[index] = [arr[0][i]].concat(arr[1][j]);
        }
        index++;
      }
    }
    const newArr = new Array(len - 1);
    for (let i = 2; i < arr.length; i++) {
      newArr[i - 1] = arr[i];
    }
    newArr[0] = items;
    return exchangeCombination(newArr);
  } else {
    return arr[0];
  }
}
```

<iframe src="https://liaojunjun.github.io/nice/root/javascript/product_specification_combination_demo.html" width="100%" height="800"></iframe>
