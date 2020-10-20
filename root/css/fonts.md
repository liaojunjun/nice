```scss
/**
 *
 * 艺术字
 * @include font-gradient(rgba(254, 255, 138, 1), rgba(255, 131, 224, 1));
 */

@mixin font-gradient($from, $to) {
  background: -webkit-linear-gradient(#{$from}, #{$to});
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/**
   *
   * 单行与多行截断
   *
   */

$line-map: (1, 2, 3);

%text-over {
  overflow: hidden;
  text-overflow: ellipsis;
}

@each $k in $line-map {
  @if $k == 1 {
    .text-over {
      @extend %text-over;
      white-space: nowrap;
    }
  } @else {
    .text-line-#{$k} {
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: $k;
    }
  }
}

/**
   *
   * 禁止文本被选择
   *
   */

@mixin user-select {
  user-select: none;
}

/**
   *
   * px 转rem
   *
   */

@function calculateRem($size) {
  $remSize: $size / 16px;
  @return $remSize * 1rem;
}
```
