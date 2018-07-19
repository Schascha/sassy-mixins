# sassy-position

Just a Scss position mixin

## Usage

```scss
@import 'position';

.foo {
	@include absolute(top 0 left 1rem);
}

.bar {
	@include relative(top);
}
```

Compiles to:

```css
.foo {
	position: absolute;
	top: 0;
	left: 1rem;
}

.bar {
	position: relative;
	top: 0;
}
```

Further examples:
[test.scss](./src/test.scss)

## License

[MIT](./LICENSE)
