# sassy-mixins

Just some Sass mixins

- [Mixins](#mixins)
	- [Breakpoint](#breakpoint)
	- [Clearfix](#clearfix)
	- [Embed](#embed)
	- [Font-Face](#font-face)
	- [Hidden](#hidden)
	- [Position](#position)
	- [Text-Truncate](#text-truncate)
- [Functions](#functions)
	- [Font-Size](#font-size)

[Further examples](./tests/)

## Mixins

```scss
@import 'sassy-mixins/mixins';
```

### Breakpoint

Helper to organize your media queries. If you prefer writing lists:

```scss
$breakpoints: (
	'mobile': 'screen and (min-width: #{$mobile})',
	'mobile-down': 'screen and (max-width: #{$mobile - 1px})',
	'tablet': 'screen and (min-width: #{$tablet})',
	'tablet-only': 'screen and (min-width: #{$mobile}) and (max-width: #{$tablet - 1px})',
	'tablet-down': 'screen and (max-width: #{$tablet - 1px})',
	'desk': 'screen and (min-width: #{$desk})',
	'desk-only': 'screen and (min-width: #{$tablet}) and (max-width: #{$desk - 1px})',
	'desk-down': 'screen and (max-width: #{$desk - 1px})',
	'retina': '(-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi), (min-resolution: 2dppx)'
) !default;

.breakpoint {
	@include breakpoint(mobile) {
		background: green;
	}

	@include breakpoint(tablet) {
		background: blue;
	}

	@include breakpoint(desk) {
		background: yellow;
	}

	@include breakpoint(desk-only) {
		background: orange;
	}

	@include breakpoint(mobile-down) {
		background: purple;
	}
}
```

Or if your like a quick min/max solution:

```scss
$mobile: 600px !default;
$tablet: 900px !default;
$desk: 1200px !default;

.breakpoint {
	@include mq($mobile) {
		background: green;
	}

	@include mq($tablet) {
		background: blue;
	}

	@include mq($desk) {
		background: yellow;
	}

	@include mq($tablet, $desk - 1px) {
		background: orange;
	}

	@include mq($max: $mobile - 1px) {
		background: purple;
	}
}
```

Compiles to:

```css
@media screen and (min-width: 600px) {
	.breakpoint {
		background: green;
	}
}

@media screen and (min-width: 900px) {
	.breakpoint {
		background: blue;
	}
}

@media screen and (min-width: 1200px) {
	.breakpoint {
		background: yellow;
	}
}

@media screen and (min-width: 900px) and (max-width: 1199px) {
	.breakpoint {
		background: orange;
	}
}

@media screen and (max-width: 599px) {
	.breakpoint {
		background: purple;
	}
}
```

### Clearfix

```scss
.clearfix {
	@include clearfix();
}
```

Compiles to:

```css
.clearfix::after {
	content: '';
	display: table;
	clear: both;
}
```

### Embed

Responsive embeds, like videos or iFrames. By default the ratio is 16:9. Other options are
'4:3', '1:2', '2:1', '1:1' or custom numbers. Also accepts lists.

```scss
.embed {
	@include embed-container();

	iframe,
	embed,
	object,
	video {
		@include embed-element();
	}
}
```

Compiles to:

```css
.embed {
	height: 0;
	position: relative;
	padding-bottom: 56.25%;
}

.embed iframe,
.embed embed,
.embed object,
.embed video {
	border: 0;
	height: 100%;
	left: 0;
	position: absolute;
	top: 0;
	width: 100%;
}
```

### Font-Face

```scss
@include font-face('OpenSans', '../fonts/OpenSans-Regular', $svg: 'OpenSansRegular');
```

Compiles to:

```css
@font-face {
	font-family: "OpenSans";
	src: url("../fonts/OpenSans-Regular.eot");
	src: url("../fonts/OpenSans-Regular.eot?#iefix") format("embedded-opentype"), url("../fonts/OpenSans-Regular.woff2") format("woff2"), url("../fonts/OpenSans-Regular.woff") format("woff"), url("../fonts/OpenSans-Regular.ttf") format("truetype"), url("../fonts/OpenSans-Regular.svg#OpenSansRegular") format("svg");
	font-style: normal;
	font-weight: normal;
}
```

Some font types are missing? Just update the `$exts` property:

```scss
@include font-face('Only-Woff', '../fonts/OnlyWoff', $exts: woff2 woff);
```

### Hidden

Only display content to screen readers

```scss
.hidden {
	@include hidden();
}
```

Compiles to:

```css
.hidden {
	border: 0;
	clip: rect(0, 0, 0, 0);
	height: 1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	white-space: nowrap;
	width: 1px;
}
```

### Position

```scss
.absolute {
	@include absolute(top 0 left 1rem);
}

.relative {
	@include relative(left 50%);
}

.fixed {
	@include fixed(0 0 0 0);
}

.sticky {
	@include sticky(top);
}
```

Compiles to:

```css
.absolute {
	position: absolute;
	top: 0;
	left: 1rem;
}

.relative {
	position: relative;
	left: 50%;
}

.fixed {
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
}

.sticky {
	position: sticky;
	top: 0;
}
```

### Text-Truncate

```scss
.text-truncate {
	@include text-truncate();
}
```

Compiles to:

```css
.text-truncate {
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
```

## Functions

```scss
@import 'sassy-mixins/functions';
```

### Font-Size

A font-size helper function for em and rem units

```scss
$font-size-base: 16px;  // Define base font-size

h1 {
	font-size: rem(30);

	> span {
		font-size: em(24, 30);
	}
}
```

Compiles to:

```css
h1 {
	font-size: 1.875rem;
}

h1 > span {
	font-size: 0.8em;
}
```

## License

[MIT](./LICENSE)
