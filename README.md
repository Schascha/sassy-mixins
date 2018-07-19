# sassy-position

Just a Scss position mixin

## Usage

```scss
@import 'position';

.foo {
	@include absolute(top 0 left 1rem);
}

.bar {
	@include relative(left 50%);
}

.baz {
	@include fixed(0 0 0 0);
}

.qux {
	@include sticky(top);
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
	left: 50%;
}

.baz {
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
}

.qux {
	position: sticky;
	top: 0;
}
```

Further examples:
[test.scss](./test/test.scss)

## License

[MIT](./LICENSE)
