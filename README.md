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
        <div class="grid three-quarters">
          Content
        </div>
        <div class="grid quarter">
          Sidebar
        </div>
      </div>
      <div class="grid-wrapper thirds no-gutters">
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
    
    $grid-name: "column"; // We prefer .column instead of .grid ...
    $grid-wrapper-name: "columns"; // ... and .columns instead of .grid-wrapper
    $grid-number: 2; // We only full and half grids on mobile
    
    @include grid; // Mobile-first
    @media only screen and (min-width: 481px) {
      $grid-number: 3; // We want thirds grids on tablet
      @include grid(tablet); // Tablet and up
    }
    @media only screen and (min-width: 769px) {
      $grid-number: 4; // We want quarters grids on desktop
      $grid-pushpull: true; // We want to use pull and push on desktop
      @include grid(desktop); // Desktop and up
    }

### HTML
    <div class="columns">
      <div class="column tablet-two-thirds desktop-three-quarters desktop-push-quarter">
        Content
      </div>
      <div class="column tablet-third desktop-quarter desktop-pull-three-quarters">
        Sidebar
      </div>
    </div>
    <div class="columns tablet-halves desktop-quarters">
      <div class="column">
        Footer #1
      </div>
      <div class="column">
        Footer #2
      </div>
      <div class="column">
        Footer #3
      </div>
      <div class="column">
        Footer #4
      </div>
    </div>
    
## Semantic responsive grid
### SCSS
    @import "grid";
    
    $grid-selector: "%";
    $grid-gutter: 10px;
    
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

    $grid-selector

Use normal (`.`) or placeholder (`%`) class selector. `.` by default.

    $grid-name

Name of the grid element (ex. `col`, `column`). `grid` by default.

    $grid-wrapper-name

Name of the wrapper element (ex. `cols`, `columns`). `grid-wrapper` by default.

    $grid-gutter

Gutter size (in `px`, `em` or `%`). `20px` by default.

    $grid-number

Number of proportions to generate (up to `12`). `4` by default.

    $grid-pushpull

Generate `push` and `pull` classes. `false` by default when `$grid-selector` is `.` to prevent bloat.
    
    $grid-oldie

Use CSS expressions for IE7 compatibility. `true` by default

### Mixin
    
    @mixin grid($namespace, $gutter, $number, $pushpull);