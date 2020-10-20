```scss
/**
 *
 * 美化占位符 placeholder 样式
 *
 */

@mixin beauty-placeholder($fz, $color: #999, $align: left) {
  &:-moz-placeholder {
    font-size: $fz;
    color: $color;
    text-align: $align;
  }
  &:-ms-input-placeholder {
    font-size: $fz;
    color: $color;
    text-align: $align;
  }
  &::-webkit-input-placeholder {
    font-size: $fz;
    color: $color;
    text-align: $align;
  }
}

/**
   *
   * IE
   *
   */

@mixin IEInput {
  ::-ms-clear,
  ::-ms-reveal {
    display: none;
  }
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    appearance: none;
    margin: 0;
  }
}
```
