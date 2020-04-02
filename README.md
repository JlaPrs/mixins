# mixins
Some useful mixins for scss


Color Theming
Das Mixin dient dazu mehrere Farb-Varianten einer Website einfach umzusetzen. Man hat zum Beispiel eine Headline, die immer die gleiche Schrift und Schriftgröße hat aber je nach Seiten-Theme mal rot oder mal Blau sein kann.

### Color Theming
#### Mixin
```scss
// @param {String} $name - name of the theme
// @param {String} $color - CSS color value

 @mixin theme($name, $color) {
  $theme-color: $color;
  $theme-shade: darken($color, 10%);
 
  .#{$name} {
    .element {
      color: $theme-color;
    }
 
    .other-element {
      border-color: $theme-color;
      box-shadow: 0 2px 5px rgba($theme-shade, .5);
    }
  }
}
```
#### Usage
```scss
.anotherBrand {
  @include theme(themeName, #00e4f9);
  display: flex;
  padding: 15px;
  ...
  ..
}

```
___

### Font (very useful)
> Das Mixin erstellt die Basis-Font-Styles für ein Website. Das ist vor allem dann nützlich, wenn man kein Framework wie Bootstrap oder Foundation Sites im Hintergrund hat, was diese Aufgabe übernimmt. Damit das Mixin funtioniert, benötigt man eine SCSS-Map in dem man die verschiedenen Werte definiert.

> Additional information: You don't have to use all mappings which are in the following mixin (e.g. letter-spacing or text-transform aren't used that often, so its not necessary) and in this case a font-base is already declared, so if there won't declare a font-family this mixin already has a fallback and use $font-base as the font-family.

#### Mixin
```scss
// variables for breakpoints have to be declared
// @param {Map|String} - Font family or setting map

$screen-sm-min: 768px;
$screen-md-min: 1024px;
$screen-lg-min: 1280px;
$screen—xl-min: 1520px;
$ci-font-base: arial;
$fontFamily: helvetica;
 
@mixin gkk-font($font: (font: $ci-font-base)) {
  margin: 0;
  font-family: $fontFamily;
  font-weight: normal;
  
  @if (map-has-key($font, "font")) {
    font-family: map-get($font, "font");
  }
  
  @if (map-has-key($font, "letter-spacing")) {
    letter-spacing: map-get($font, "letter-spacing");
  }
  
  @if (map-has-key($font, "text-transform")) {
    text-transform: map-get($font, "text-transform");
  }
  
  @if (map-has-key($font, "line-height")) {
    line-height: map-get($font, "line-height");
  }
  
  // min 375px
  @if (map-has-key($font, "size-xs")) {
    font-size: map-get($font, "size-xs");
  }
 
 // min 768px
  @if (map-has-key($font, "size-sm")) {
    @media (min-width: $breakpoint—sm-min) {
      font-size: map-get($font, "size-sm");
    }
  }
 
  // min 1024px
  @if (map-has-key($font, "size-md")) {
    @media (min-width: $breakpoint—md-min) {
      font-size: map-get($font, "size-md");
    }
  }
 
  // min 1280px
  @if (map-has-key($font, "size-lg")) {
    @media (min-width: $breakpoint—lg-min) {
      font-size: map-get($font, "size-lg");
    }
  }
 
  // min 1520px
  @if (map-has-key($font, "size-xl”)) {
    @media (min-width: $screen—xl-min) {
      font-size: map-get($font, "size-xl”);
    }
  }
}
```
#### Usage
```scss
.product-headline {
  @include gkk-font((size-sm: 20px, size-md: 40px, size-lg: 70px));
  margin-bottom: 30px;
  ...
  ..
}
```
___

### Retine Images

> Das Mixin wird benutzt um bei Retina-Screens andere Bilder zu laden. Die alternativen Bilder sollten in den Dimensionen doppelt so hoch und breit sein, wie die Originale, die Auflösung von 72 DPI bleibt jedoch bestehen.

#### Mixin
```scss
// Retina images
//
// @param {String} $image - Path to image file
// @param {Number} $width - Image width
// @param {Number} $height - Image height
 
@mixin retina($image, $width, $height) {
  @media (min--moz-device-pixel-ratio: 1.3),
         (-o-min-device-pixel-ratio: 2.6/2),
         (-webkit-min-device-pixel-ratio: 1.3),
         (min-device-pixel-ratio: 1.3),
         (min-resolution: 1.3dppx) {
    background-image: url($image);
    background-size: $width $height;
  }
}
```

#### Usage
```scss
.logo {
  @include retina(“logo2x.png", 100px, 25px);
  background: url("logo.png") no-repeat;
}
```
___

### Media queries
> You can go mobile first too. Its up to you.

#### Mixin
```scss
@mixin breakpoint($size) {
  $desktop: '(min-width: 1024px)';
  $tablet: '(min-width: 768px) and (max-width: 1023px)';
  $mobile: '(max-width: 767px)';

  @if $size == desktop {
    @media only screen and #{$desktop} {
      @content;
    }
  } @else if $size == tablet {
    @media only screen and #{$tablet} {
      @content;
    }
  } @else if $size == mobile {
    @media only screen and #{$mobile} {
      @content;
    }
  } @else {
    @media only screen and #{$size} {
      @content;
    }
  }
}
```
#### Usage
```scss
.wrapper {
  margin: 0 auto;
  width: 100%;
  
  @include breakpoint('tablet') {
    width: 90%;
  }
  
  @include breakpoint('desktop') {
    width: 85%;
  }  
}
```
___

### Pseudo
#### Mixin
```scss
@mixin pseudo($display: block, $pos: absolute, $content: ''){
    content: $content;
    display: $display;
    position: $pos;
}
```
#### Usage
```scss
.someClass {
  @include pseudo;
  ...
  ..
}
```
___

< Some more helpful mixins will be added asap. :D
