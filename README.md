# td-scss

A small collection mixins, variables and animations which address common concerns in my projects.

| name        | type      | description                                                                                                     |
| ----------- | --------- | --------------------------------------------------------------------------------------------------------------- |
| btn-solid   | mixin     | base primary button stylesm requires a colour                                                                   |
| btn-outline | mixin     | base secondary button styles requires a colour                                                                  |
| pop         | animation | slight increase in scale temporarily, primarily design for hover interactions                                   |
| shake       | animation | quick horizontal shake, good for errors/invalid actions                                                         |
| palette     | function  | takes a colour (one of [green, yellow, red, purple, aqua, orange]) and a shade, 100 - 500, lightest to darkest. |
