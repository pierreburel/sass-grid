# Proportionnal grids

Work in progress

## Usage
### SCSS
    @import "grid";
    @include grid; // Mobile-first
    @media only screen and (min-width: 480px) {
      @include grid(tablet); // Tablet and up
    }
    @media only screen and (min-width: 768px) {
      @include grid(desktop); // Desktop and up
    }

### HTML
    <div class="grid-wrapper">
      <div class="grid tablet-half desktop-third">
        Content
      </div>
      <div class="grid tablet-half desktop-two-thrids">
        Content
      </div>
    </div>

## Configuration

### Variables

    $grid-name: "grid" !default;
    
    $grid-gutter: 20px !default;
    
    $grid-number: 4 !default; // Number of grids to generate (up to 12)
    
    $grid-pushpull: true !default; // Set to false if you dont use push or pull
    
    $grid-selector: "." !default; // Use normal (.) or placeholder (%) class selector
    
    $grid-oldie: true !default; // Set to true to use css expressions for IE7 compatibility

### Mixin
    
    @mixin grid($namespace, $gutter, $number, $pushpull, $selector, $name);