# mixins
Some useful mixins for scss


Color Theming
Das Mixin dient dazu mehrere Farb-Varianten einer Website einfach umzusetzen. Man hat zum Beispiel eine Headline, die immer die gleiche Schrift und Schriftgröße hat aber je nach Seiten-Theme mal rot oder mal Blau sein kann.

Mixin Color Theming
```scss
// Color theming
//
// @param {String} $name - name of the theme
// @param {String} $color - CSS color value
//
// @example usage
// @include itl-theme(itl, #00e4f9);
//
// @example output
// .itl .element { color: #00e4f9; }
//
// .itl .other-element {
//   border-color: #00e4f9;
//   box-shadow: 0 2px 5px rgba(0, 181, 198, 0.5);
// }
 
 
 @mixin itl-theme($name, $color) {
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
CI Font Mixin
Das Mixin erstellt die Basis-Font-Styles für ein Website. Das ist vor allem dann nützlich, wenn man kein Framework wie Bootstrap oder Foundation Sites im Hintergrund hat, was diese Aufgabe übernimmt. Damit das Mixin funtioniert, benötigt man eine SCSS-Map in dem man die verschiedenen Werte definiert.

Mixin CI Font
// CI Font
//
// @param {Map|String} - Font famaily or setting map
 
@mixin ci-font($font: (font: $ci-font-base)) {
  margin: 0;
 
  $fontFamily: $ci-font-base;
    @if (map-has-key($font, "font")) {
      $fontFamily: map-get($font, "font");
    }
 
  font-family: $fontFamily;
  font-weight: normal;
 
  @if (map-has-key($font, "size-xs")) {
    font-size: map-get($font, "size-xs");
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
    @media (min-width: $breakpoint—sm) {
      font-size: map-get($font, "size-xl”);
    }
  }
}
Retine Images
Das Mixin wird benutzt um bei Retina-Screens andere Bilder zu laden. Die alternativen Bilder sollten in den Dimensionen doppelt so hoch und breit sein, wie die Originale, die Auflösung von 72 DPI bleibt jedoch bestehen.

Mixin Retina Images
// Retina images
//
// @param {String} $image - Path to image file
// @param {Number} $width - Image width
// @param {Number} $height - Image height
//
// @example
// .logo {
//   @include retina(“logo2x.png", 100px, 25px);
//   background: url("logo.png") no-repeat;
// }
 
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
