<p align="center">
  <img alt="Base CSS" src="./public/assets/base-css-logo.svg" width="100">
</p>

<h1 align="center">
  Base CSS
</h1>

### Extendable SCSS framework with built in dark mode.

# [View Demo]()

## Usage

Grab the [latest release files](https://github.com/sschandi/basecss/releases), and add them to your project.

## Darkmode Toggle

Add the data-theme property to your html element `<html data-theme="light">`: values are `light` or `dark`

To easily toggle between light/dark and remember a user's choice, add the following script:

```javascript
<script>
  // target ID of button to change dark mode
  var el = document.getElementById('toggle')
  // Remember user's selected theme in localStorage, also respect a users `prefers-color-scheme: dark` setting
  var storedTheme = localStorage.getItem('theme') || (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light')

  if (storedTheme) {
    document.documentElement.setAttribute('data-theme', storedTheme)
  }

  // handle switching between themes on button click
  el.onclick = () => {
    var current = document.documentElement.getAttribute('data-theme')
    var target = current === 'light' ? 'dark' : 'light'

    document.documentElement.setAttribute('data-theme', target)
    // set updated theme to local storage
    localStorage.setItem('theme', target)
  }
</script>
```

## Extending

Update values in `_variables.scss`.

### Theme Variables

Theme variables are a SASS map of light and dark colors. The default values are:

```scss
(
  'primary': ('light': #007aff, 'dark': #0a84ff),
  'secondary': ('light': #5856d6, 'dark': #5e5ce6),
  'accent': ('light': #5ac8fa, 'dark': #64d2ff),
  'success': ('light': #34c759, 'dark': #30d158),
  'danger': ('light': #ff3b30, 'dark': #ff453a),
  'warning': ('light': #ff9500, 'dark': #ff9f0a),
  'info': ('light': #af52de, 'dark': #bf5af2),
  'mute': ('light': #c7c7cc, 'dark': #48484a)
)
```

Each variable will create a corresponding CSS variable `var(--primary)`, and a SASS variable `$primary`. These variables will automatically
swap between the light and dark values depending on the current `data-theme`.

You can override or add new values with the `$theme` variable. Note: Because SASS cannot dynamically create variables,
if you add new values to the theme ex. `'party-color': ('light: red, 'dark': blue)`, you will have to declare the accompanying SASS variable yourself.
In this case it would be `$party-color: var(--party-color)`.

### Color variables

Color variables are a SASS map of 9 colors, scaling from lightest to darkest. The default values are:

```scss
(
  'gray': (#e5e5ea, #d1d1d6, #c7c7cc, #aeaeb2, #8e8e93, #636366, #48484a, #3a3a3c, #2c2c2e),
  'red': (#FFF5F5, #FED7D7, #FEB2B2, #FC8181, #F56565, #E53E3E, #C53030, #9B2C2C, #742A2A),
  'orange': (#FFFAF0, #FEEBC8, #FBD38D, #F6AD55, #ED8936, #DD6B20, #C05621, #9C4221, #7B341E),
  'yellow': (#FFFFF0, #FEFCBF, #FAF089, #F6E05E, #ECC94B, #D69E2E, #B7791F, #975A16, #744210),
  'green': (#F0FFF4, #C6F6D5, #9AE6B4, #68D391, #48BB78, #38A169, #2F855A, #276749, #22543D),
  'teal': (#E6FFFA, #B2F5EA, #81E6D9, #4FD1C5, #38B2AC, #319795, #2C7A7B, #285E61, #234E52),
  'blue': (#EBF8FF, #BEE3F8, #90CDF4, #63B3ED, #4299E1, #3182CE, #2B6CB0, #2C5282, #2A4365),
  'indigo': (#EBF4FF, #C3DAFE, #A3BFFA, #7F9CF5, #667EEA, #5A67D8, #4C51BF, #434190, #3C366B),
  'purple': (#FAF5FF, #E9D8FD, #D6BCFA, #B794F4, #9F7AEA, #805AD5, #6B46C1, #553C9A, #44337A),
  'pink': (#FFF5F7, #FED7E2, #FBB6CE, #F687B3, #ED64A6, #D53F8C, #B83280, #97266D, #702459),
)
```

Each variable creates a correspoding CSS and SASS variables from 100-900 of that color.

ex: `var(--gray-100)` to `var(--gray-900)` and `$gray-100` to `$gray-900`

The color mappings reverse depending on dark and light mode. ex: `gray-100` will becomone `gray-900`, and `gray-200` will become `gray-800` in dark mode.

You can override or add new values with the `$color` variable; however, it is important to maintain 9 values for each color.
Note: similar to adding new theme variables, new color SASS variables must be declared yourself.

### Main

the `main.scss` file holds basic styling for a number of commonly used HTML elements (inputs, buttons, links). You can easily customize these styles as needed
based on your project.

## Why

Every time I start a new frontend project, I find myself re-writting the same css:

- Theme Variables
- Fonts
- Basic Styling for HTML elements (Buttons, Inputs, etc)
- Utilities

This library contains all of the above (and built in dark mode), allowing me to bootstrap a new project by simply grabbing the
[latest release files](https://github.com/sschandi/basecss/releases) and adding them into my repo. I can then modify/extend the
basic styling as needed.
