# sassy-mixins

![Build](https://github.com/Schascha/sassy-mixins/workflows/Build/badge.svg)

> Just some Sass mixins

- [Usage](#usage)
- [Mixins](#mixins)
	- [Accessibility](#accessibility)
	- [Breakpoint](#breakpoint)
	- [Clearfix](#clearfix)
	- [Embed](#embed)
	- [Font-Face](#font-face)
	- [Position](#position)
	- [Text-Truncate](#text-truncate)
	- [Theme](#theme)
- [Functions](#functions)
	- [Font-Size](#font-size)

[Further examples](./tests/)

## Usage

```scss
@import '@schascha/sassy-mixins';
```

## Mixins

### Accessibility

Only display content to screen readers.

```scss
.sr-only {
	@include sr-only();
}
```

Compiles to:

```css
.sr-only {
	overflow: hidden;
	position: absolute;
	margin: -1px;
	padding: 0;
	width: 1px;
	height: 1px;
	clip: rect(0, 0, 0, 0);
	border-width: 0;
	white-space: nowrap;
}
```

### Breakpoint

Helper to organize your media queries.

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
	position: relative;
	padding-bottom: 56.25%;
	height: 0;
}

.embed iframe,
.embed embed,
.embed object,
.embed video {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	border: 0;
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
	font-weight: normal;
	font-style: normal;
}
```

Some font types are missing? Just update the `$exts` property:

```scss
@include font-face('Only-Woff', '../fonts/OnlyWoff', $exts: woff2 woff);
```

Compiles to:

```css
@font-face {
	font-family: "Only-Woff";
	src: url("../fonts/OnlyWoff.woff2") format("woff2"), url("../fonts/OnlyWoff.woff") format("woff");
	font-weight: normal;
	font-style: normal;
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

### Theme

Add styles depending on a theme variable.

```scss
$theme: 'foo';

.theme {
	@include theme('foo') {
		background: red;
	}
}
```

Compiles to:

```css
.theme {
	background: red;
}
```

## Functions

### Font-Size

A font-size helper function for em and rem units.

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

## Bugs?

Please let me know: https://github.com/Schascha/stylelint-config/issues

## Buy me a Coffee :coffee:

Support this project and [others](https://github.com/Schascha?tab=repositories) via [PayPal](https://www.paypal.me/LosZahlos). Thanks

## License

[MIT](./LICENSE)

Copyright (c) 2018 Sascha Künstler
