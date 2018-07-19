# sassy-position

Just a Scss position mixin

## Usage

```scss
@import 'position';

.foo {
	@include absolute(top 0 left 1rem);
}
```

Compiles to:

```css
.foo {
  position: absolute;
  top: 0;
  left: 1rem;
}
```

## License

[MIT](./LICENSE)
