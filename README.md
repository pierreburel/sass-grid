# Grid

Proportional, responsive and (eventually) semantic grid with (optional) IE7 compatibility  

**Work in progress**  

Demo : http://labs.pierreburel.com/sass/grid/  
<<<<<<< HEAD
Inspired by https://github.com/mattberridge/Proportional-Grids  
=======
Inspired by https://github.com/mattberridge/Proportional-Grids   
>>>>>>> 1a67bcf46071289a45aafc45d6ae8d80a5137787

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
      <div class="grid">
        <div class="grid-unit three-quarters">
          Content
        </div>
        <div class="grid-unit quarter">
          Sidebar
        </div>
      </div>
      <div class="grid thirds no-gutters">
        <div class="grid-unit">
          Footer #1
        </div>
        <div class="grid-unit">
          Footer #2
        </div>
        <div class="grid-unit">
          Footer #3
        </div>
      </div>
    </div>
    
## Mobile first grid example

With IE7 compatibility thanks to https://github.com/scottjehl/Respond

### SCSS
    @import "grid";
    
    $grid-wrapper-name: "columns"; // ... and .columns instead of .grid-wrapper
    $grid-unit-name: "column"; // We prefer .column instead of .grid ...
    $grid-number: 2; // We only full and half grids on mobile
    $grid-oldie: true; // We need IE7 compatibility
    
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
      @extend %grid;
    }
      .media-item {
        @extend %grid-unit, %half, %tablet-third, %tablet-quarter;
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

    $grid-wrapper-name

Name of the wrapper element (ex. `cols`, `columns`, `grid`). `grid` by default.

    $grid-unit-name

Name of the grid element (ex. `col`, `column`, `grid__unit` or `false` for using direct descendant). `grid-unit` by default.  

    $grid-prefix

Set a prefix for all modifiers (ex. `grid-` for writing "grid grid-no-gutters grid-tablet-halves"). Empty by default.  

    $grid-gutter

Gutter size (in `px`, `em` or `%`). `20px` by default.

    $grid-number

Number of proportions to generate (up to `12`). `4` by default when using `.` selector to prevent bloat.

    $grid-pushpull

Generate `push` and `pull` classes. `false` by default when using `.` selector to prevent bloat.
    
    $grid-oldie

Use CSS expressions for IE7 compatibility. `false` by default.

### Mixin
    
    @mixin grid($namespace, $gutter, $number, $pushpull);
