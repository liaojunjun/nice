```scss
/**
 * $name 图片名字
 * @return url(...)
 */
@function bgUrl($name) {
  @return url(./assets/images/#{$name});
}

/**
   *
   * 设置背景图片
   * @example @include background("xx.png");
   */

@mixin background($name, $position: center center, $size: contain) {
  background-image: bgUrl($name);
  background-position: #{$position};
  background-size: #{$size};
  background-repeat: no-repeat;
}

/**
   * 设置多图背景
   @example
  // @include multiple-background(image, [ bgUrl("1.png"), bgUrl("2.png"), bgUrl("3.png") ]);
  // @include multiple-background(repeat, [no-repeat, no-repeat, no-repeat]);
  // @include multiple-background(size, [auto 10px, cover, cover]);
  // @include multiple-background(position, [20px 20px, center, center]);
   *
   */

@mixin multiple-background($key, $list) {
  $url_list: ();
  @each $name in $list {
    $url_list: append($url_list, $name, comma);
  }
  background-#{$key}: $url_list;
}
```
