```scss
/**
 * USAGE:
 *	@include screenSize(240)  { }
 *	@include screenSize(320)  { }
 *	@include screenSize(480)  { }
 *	@include screenSize(768)  { }
 *	@include screenSize(1024) { }
 *	@include screenSize(1140) { }
 *	@include screenSize(1280) { }
 *  @include screenSize(1500) { }
 *
 * .header {
 * 	  @include screenSize(320)  { display: none; }
 * }
 */
@mixin screenSize($point) {
  @if $point==240 {
    @media (min-width: 240px) {
      @content;
    }
  }
  @if $point==320 {
    @media (min-width: 320px) {
      @content;
    }
  }
  @if $point==480 {
    @media (min-width: 480px) {
      @content;
    }
  }
  @if $point==600 {
    @media (min-width: 600px) {
      @content;
    }
  }
  @if $point==768 {
    @media (min-width: 768px) {
      @content;
    }
  }
  @if $point==1024 {
    @media (min-width: 1024px) {
      @content;
    }
  }
  @if $point==1140 {
    @media (min-width: 1140px) {
      @content;
    }
  }
  @if $point==1280 {
    @media (min-width: 1280px) {
      @content;
    }
  }
  @if $point==1500 {
    @media (min-width: 1500px) {
      @content;
    }
  }
}
```
