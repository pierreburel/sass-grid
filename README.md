# Proportionnal grids

Work in progress  

Demo : http://labs.pierreburel.com/sass/proportionnal-grids/  
Inspired by https://github.com/mattberridge/Proportional-Grids  

## Simple 960 desktop grid example
### SCSS
    @import "grid";
    
    @include grid;
    
    .container {
      margin: 0 auto;
      padding: 0 10px;
      width: 960px;
    }

### HTML
    <div class="container">
      <div class="grid-wrapper">
        <div class="grid three-quarters push-quarter">
          Content
        </div>
        <div class="grid quarter pull-three-quarters">
          Sidebar
        </div>
      </div>
      <div class="grid-wrapper set-third no-gutters">
        <div class="grid">
          Footer #1
        </div>
        <div class="grid">
          Footer #2
        </div>
        <div class="grid">
          Footer #3
        </div>
      </div>
    </div>
    
## Mobile first grid example
### SCSS
    @import "grid";
    
    $grid-number: 2; // We only full and half grids on mobile
    
    @include grid; // Mobile-first
    @media only screen and (min-width: 481px) {
      $grid-number: 3; // We want thirds grids on tablet
      @include grid(tablet); // Tablet and up
    }
    @media only screen and (min-width: 769px) {
      $grid-number: 4; // We want quarters grids on desktop
      @include grid(desktop); // Desktop and up
    }

### HTML
    <div class="grid-wrapper">
      <div class="grid tablet-two-thirds desktop-three-quarters">
        Content
      </div>
      <div class="grid tablet-third desktop-quarter">
        Sidebar
      </div>
      <div class="grid tablet-half desktop-quarter">
        Footer #1
      </div>
      <div class="grid tablet-half desktop-quarter">
        Footer #2
      </div>
      <div class="grid tablet-half desktop-quarter">
        Footer #3
      </div>
      <div class="grid tablet-half desktop-quarter">
        Footer #4
      </div>
    </div>
    
## Semantic responsive grid
### SCSS
    @import "grid";
    
    $grid-selector: "%";
    $grid-gutter: 10px;
    $grid-pushpull: false;
    
    @include grid; // Mobile first, 10px gutter
    @media only screen and (min-width: 481px) {
      @include grid(tablet, 15px); // Tablet and up, 15px gutter
    }
    @media only screen and (min-width: 769px) {
      @include grid(desktop, 20px); // Desktop and up, 20px gutter
    }
    
    .medias {
      @extend %grid-wrapper;
    }
      .media-item {
        @extend %grid, %half, %tablet-third, %tablet-quarter;
      }
        .media-img {
          display: block;
          width: 100%;
        }

### HTML  
    <ul class="medias">
      <li class="media-item">
        <img src="img.jpg" class="media-img"/>
      </li>
      ...
    </ul>

## Configuration

### Variables

    $grid-gutter: 20px !default; // Gutter size (px, em or %)

    $grid-number: 4 !default; // Number of grids to generate (up to 12)

    $grid-pushpull: true !default; // Set to false if you dont use push or pull

    $grid-name: "grid" !default; // Name of the grid element (ex. "col", "column")

    $grid-wrapper-name: "grid-wrapper" !default; // Name of the wrapper element (ex. "cols", "columns")

    $grid-selector: "." !default; // Use normal (.) or placeholder (%) class selector
    
    $grid-oldie: true !default; // Set to true to use css expressions for IE7 compatibility  

### Mixin
    
    @mixin grid($namespace, $gutter, $number, $pushpull);
