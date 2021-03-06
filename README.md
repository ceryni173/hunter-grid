![Cattle Grid](https://usecattlegrid.com/assets/images/logo-type-small.png)

Extremely lightweight, basic flex grid built from a simple mixin

## Demo

[Cattle Grid Example](https://usecattlegrid.com)   


## Getting Started

Cattle grid contains not only a very simple (under 20kb) grid as well as a small suite of extra settings I've collected over the years of doing Front End. Unlike most frameworks, this grid is easy to isolate and use on it's own - the rest is just for sheer aesthetics and laziness!

To isolate the grid, navigate to [grid.scss](https://gitlab.com/Ceryni/cattle-grid/blob/master/assets/scss/base/_grid.scss) and add this to your own project! Simple.

If you wish to use the entire project, the folder structure is very simple.

#### Base
General contains all files needed to set up a new site, from colours, helpers, form elements and mixins

#### Site
Site contains files related to the project you're about to build.

_I use an autoprefixer on my scss!_

---

### Defining Variables

```
$grid-gutter-medium: 30px !default;
$grid-gutter-small: 20px !default;
$global-width: 1200px;
$grid-max-width: $global-width + ($grid-gutter-medium * 2) !default;
$grid-columns: 12 !default;

$breakpoint-small: 767px !default;
$breakpoint-medium: 992px !default;
$breakpoint-large: 1200px !default;
$breakpoint-xlarge: 1440px !default;
```

### Using Breakpoint Mixin

```
@mixin breakpoint($media) {
	@media #{$media} {
		@content;
	}
}
```

### Using Grid Markup

```
<div class="container">
	<div class="row">
		<div class="small-12 medium-6 large-3 columns">column</div>
		<div class="small-12 medium-6 large-3 columns">column</div>
		<div class="small-12 medium-6 large-3 columns">column</div>
		<div class="small-12 medium-6 large-3 columns">column</div>
	</div>
</div>
```

---

## Extra mixins & Settings

These are just tidbits that come in handy when starting out a new build!


### Sizings
```
$small-space: 5px;
$medium-space: 20px;
$large-space: 40px;
$xlarge-space: 60px;
$hundred: ($large-space + $xlarge-space);
$input-height: $large-space;
$border-radius: 3px;
```


### Text Alignments
To be able to align text left, right or centrally within the markup, there are 4 classes available!

_To use_
```
<div class="small-text-center medium-text-right large-text-left xlarge-text-center">Align me!</div>
```

### Atom Users!

If you use Atom - this handy snippet allows for easy autofill of sizes! Be a faster dev

```
'.source.css.scss':
  '5px':
    'prefix': '5px'
    'body': '$small-space';
  '10px':
    'prefix': '10px'
    'body': '($small-space * 2)';
  '15px':
    'prefix': '15px'
    'body': '($small-space * 3)';
  '20px':
    'prefix': '20px'
    'body': '$medium-space';
  '25px':
    'prefix': '25px'
    'body': '($small-space * 5)';
  '30px':
    'prefix': '30px'
    'body': '($xlarge-space / 2)';
  '40px':
    'prefix': '40px'
    'body': '$large-space';
  '50px':
    'prefix': '50px'
    'body': '($small-space * 10)';
  '60px':
    'prefix': '60px'
    'body': '$xlarge-space';
```


### Crayola

```
$palette: (
	primary: #8eb8ba,
	primaryText: #fcf8f4,
	secondary: #ebc7ba,
	secondaryText: #697280,
	success: #c9e4bf,
	error: #d38a8a,
	alert: #d38a8a,
	warning: #d29075,
	light-grey: #c4c5c5
);

// shorthand
$primary: map-get($palette, primary);
$primaryText: map-get($palette, primaryText);
$secondary: map-get($palette, secondary);
$secondaryText: map-get($palette, secondaryText);
$light: map-get($palette, light-grey);
```

_To use_

```
background-color: $primary;
color: $primaryText;
```

### Buttons

```
@mixin button-bg($bg, $txt) {
	background: $bg;
	border: $bg;
	color: $txt;
	&:hover,
	&:focus {
		background:darken($bg,10%);
		border:darken($bg, 10%);
		transition: all 0.3s ease;
	}
}
```

_To use:_

```
@include button-bg(#000000, #ffffff);
```

### Hollow Buttons

```
@mixin button-hollow($border, $txt) {
	background: transparent;
	border: 1px solid $border;
	color: $txt;
	&:hover,
	&:focus {
		border: 1px solid darken($border, 10%);
		transition: all 0.3s ease;
		color: darken($txt, 10%);
	}
}
```

_To use:_

```
@include button-hollow(#000000, #000000);
```

### Pseudos

```
@mixin pseudo($display: block, $pos: absolute, $content: ''){
	content: $content;
	display: $display;
	position: $pos;
}
```

_To use:_

```
@include pseudo;
```

### Placeholders

```
@mixin input-placeholder {
	&.placeholder { @content; }
	&:-moz-placeholder { @content; }
	&::-moz-placeholder { @content; }
	&:-ms-input-placeholder { @content; }
	&::-webkit-input-placeholder { @content; }
}
```

_To use:_

```
@include input-placeholder {
	color: $grey;
}
```

### Headlines

```
@mixin heading {
	color: inherit;
	font-weight: 500;
	font-style: normal;
	text-rendering: optimizeLegibility;
	margin-top: 0;
	margin-bottom: 0.5rem;
	line-height: 1.4;
	padding: 0;
}

@mixin h1 {
	@include heading;
	font-size: rem-calc(40);
	@include breakpoint($small-only) {
		font-size: rem-calc(30);
	}
}
```

_To use:_

```
@include h1;
```


### Font sizes

```
// Rem Calc
@function rem-calc($font-size) {
	$rem-size: $font-size / 16;
	@return #{$rem-size}rem;
}

```

_To use:_

```
font-size: rem-calc(12)
```


### Z Indexes

```
$z-index: (
	modal: 200,
	navigation: 100,
	footer: 10,
	header: 50,
	main: 10,
);

@function z-index($key) {
	@return map-get($z-index, $key);
}
@mixin z-index($key) {
	z-index: z-index($key);
}
```

_To use:_

```
@include z-index(header);
```

### Fades

```
@mixin fade($type) {
	@if $type == 'hide' {
		visibility: hidden;
		opacity: 0;
		transition: visibility 1s, opacity 1s;
	}
	@else if $type == 'show' {
		visibility: visible;
		opacity: 1;
		transition: visibility 1s, opacity 1s;
	}
}
```

_To use:_

```
@include fade(hide)
@include fade(show)
```


---


## Extends

### Alignment & Positioning

```
// Columns in a flex grid can be aligned horizontal or vertical inside of their parent.
	.align-all {
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
		text-align: center;
	}

	.align-middle {
	    align-items: center;
	}

	.align-center {
	    justify-content: center;
	}

// Columns in a flex grid can be aligned horizontal or vertical individually also
	.align-self-bottom {
		align-self: flex-end;
	}

	.align-self-middle {
		align-self: center;
	}

	.align-self-top {
		align-self: flex-start;
	}

// Elements can be absolutely positioned inside of it's relative parent
	.horizontal-center {
		position: absolute;
		left: 50%;
		top: auto;
		transform: translateX(-50%);
	}

	.vertical-center {
		position: absolute;
		left: auto;
		top: 50%;
		transform: translateY(-50%);
	}

	.absolute-center {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
```

_To use:_

```
@extend .align-all;
@extend .horizontal-center;
@extend .vertical-center;
@extend .absolute-center;

<div class="container">
	<div class="row align-all">
		<div class="small-12 medium-6 columns align-self-top">column</div>
		<div class="small-12 medium-6 columns align-self-middle"> column</div>
		<div class="small-12 medium-6 columns align-self-bottom">column</div>
	</div>
	<div class="row">
		<div class="small-12 columns">
			<div class="box horizontal-center align-all">
				horizontal-center
			</div>
			<div class="box vertical-center align-all">
				vertical-center
			</div>
			<div class="box absolute-center align-all">
				absolute-center
			</div>
		</div>
	</div>
</div>
```
---

## Markup Elements

### Drawer

_To use:_

```

// Will sit to the top right of the page
// The Drawer will open from the right


<a href="#main-menu" role="button" id="main-menu-toggle" class="menu-toggle"
	aria-expanded="false"
	aria-controls="main-menu"
	aria-label="Open main menu">
	<span class="fa fa-bars" aria-hidden="true"></span>
</a>
<nav id="main-menu" role="navigation" class="main-menu" aria-expanded="false" aria-label="Main menu">
	<a href="#main-menu-toggle" role="button" id="main-menu-close" class="menu-close"
		aria-expanded="false"
		aria-controls="main-menu"
		aria-label="Close main menu">
		<span class="fa fa-close" aria-hidden="true"></span>
	</a>
	<ul class="drawerMenu">
		<li><a href="#>Link</a></li>
	</ul>
</nav>
<a href="#main-menu-toggle" class="menuBg" tabindex="-1" aria-hidden="true" hidden></a>

```

---

## Authors

* **Ceryni** - *Initial work* - [Ceryni173](https://github.com/Ceryni173)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Inspired by Foundation 6 markup
