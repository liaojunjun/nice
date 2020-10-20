```scss
/**
 *
 * 实心和空心的三角形
    $position: top | right | bottom | left; 底边的位置
    $color:color; 颜色
    $size:size; 底边长度
 *
 */

@mixin triangle($position, $color, $size) {
  height: 0;
  width: 0;
  border-color: transparent;
  border-style: solid;
  display: inline-block;
  border-width: $size * 2;
  border-#{$position}-color: $color;
}
i.icon-triangle {
  &::before {
    content: "";
    @include triangle(bottom, red, 10px);
  }
}
@mixin arrow($position, $color, $size) {
  width: 0;
  height: 0;
  border: solid $color;
  border-width: 0 2px 2px 0;
  padding: $size;
  display: inline-block;

  @if $position == top {
    transform: rotate(-135deg);
  }

  @if $position == bottom {
    transform: rotate(45deg);
  }

  @if $position == left {
    transform: rotate(135deg);
  }

  @if $position == right {
    transform: rotate(-45deg);
  }
}

i.icon-arrow {
  @include arrow(right, red, 10px);
}
```
