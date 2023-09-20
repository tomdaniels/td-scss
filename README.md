# td-scss ![npm-badge](https://badge.fury.io/js/td-scss.svg)

A small collection mixins, variables and animations which address common concerns in my projects.

### Colours

Base colours are exported as variables, core pallete conisists of `[$green, $yellow, $red, $purple, $aqua, $orange]`.
There are 5 shades of each also exported through a `palette` function which takes a colour and a shade, the default variables are the "base" `300` shade.

_"shade" is a number between 100 (being the lightest), to 500 (being the darkest)._

i.e `palette(green, 200)`;

additional colour options for:

- **background**: [`$bg`, `$bg-dim`, `$bg-current-word`, `$bg-[0-4]`] (0 being _darkest_ through to 4 the _lightest_).
- **greys**: [`$grey-[0-4]`]: (0 being the _darkest_ through to 4 being the _lightest_).
- **foreground**: [`$fg`, `$fg-[0-5]`] (0 being the _lightest_ and 5 being the _darkest_).
- **diffs**: All vars prefixed with `$bg-diff-`: [`green`, `green-soft`, `red`, `red-soft`, `blue`, `blue-soft`, `yellow-soft`].

### Mixins

#### breakpoints

Exported breakpoint variables exclude:

- `$width-small-mobile`: 370px
- `$width-mobile`: 640px;
- `$width-tablet`: 768px
- `$width-desktop`: 1024px
- `$width-expanded`: 1536px

common breakpoint media query mixins:

| name                 | query                                                                             |
| -------------------- | --------------------------------------------------------------------------------- |
| mobile               | `@media (max-width: #{$width-tablet - 1px})`                                      |
| small-mobile         | `@media (max-width: #{$width-small-mobile})`                                      |
| max-portrait-mobile  | `@media (max-width: #{$width-mobile - 1px})`                                      |
| max-landscape-mobile | `@media (max-width: #{$width-tablet - 1px})`                                      |
| tablet               | `@media (min-width: #{$width-tablet}) and (max-width: #{$width-desktop - 1px})`   |
| min-tablet           | `@media (min-width: #{$width-tablet})`                                            |
| max-tablet           | `@media (max-width: #{$width-desktop - 1px})`                                     |
| desktop              | `@media (min-width: #{$width-desktop}) and (max-width: #{$width-expanded - 1px})` |
| min-desktop          | `@media (min-width: #{$width-desktop})`                                           |
| max-desktop          | `@media (max-width: #{$width-expanded - 1px})`                                    |
| expanded             | `@media (min-width: #{$width-expanded}) `                                         |

#### theme

A mixin for generating theme based classes. It requires a `color` argument and will generate four classes ([`primary`, `secondary`, `tertiary`, `quarternary`]) of varying colours from the provided theme. You can optionally specify `rotate` and `darkenpct` arguments for more control over the generated theme.

Example usages:

```scss
.theme-1 {
  @include theme(green);
}
.theme-2 {
  @include theme(yellow, 90deg);
}
.theme-3 {
  @include theme(yellow, 180deg, 40%);
}
.theme-4 {
  @include theme(purple, $darkenpct: 10%);
}
```

The mixin works by rotating the colour wheel at certain angles to pick complimentary colours. It uses relative luminance to select the text color to keep a nice contrast that's still easy to read.

#### relative luminance

This was an interesting rabbit hole to fall into. _[Relative lumincance](https://www.w3.org/WAI/GL/wiki/Relative_luminance)_ is described as the relative brightness of any point in colour space. So this mixin is used for setting text colour on elements when we don't know what the background colour will be.

Example usages:

```scss
// get the lumiance value of white
$white_luminance: luminance(#fff);
.btn {
  // set the dark text colour
  color: #000;

  // compare relative brightness of our "unknown" colour against white
  @if abs(luminance($color) - $white_luminance) > 0.7 {
    color: #eee;
  }
}
```

#### btn

Base button styles for solid, outline and link variants:

```scss
.primary-button {
  @include btn-solid($colour);
}
.secondary-button {
  @include btn-outline($colour);
}
.link {
  @include btn-link($colour);
}
```

### Animations

#### pop

slight increase in scale temporarily, primarily design for hover interactions. Takes optional size and duration arguments.

Example usage:

```scss
.item {
  @include pop();
}
.item-1 {
  @include pop(1.1, 300ms);
}
.item-2 {
  @include pop($duration: 300ms, $size: 1.3);
}
```

#### shake

quick horizontal shake, good for errors/invalid actions. Takes an optional duration agument.

Example usage:

```scss
.item {
  @include shake();
}
.item-1 {
  @include shake(100ms);
}
```
