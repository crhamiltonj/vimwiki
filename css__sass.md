# Sass

## Boilerplate Repo for 7 - 1 Pattern

`git clone https://github.com/HugoGiraudel/sass-boilerplate.git`

## NPM Build Process (package.json)

```json
{
  "name": "alltheit_mocks",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "watch-sass": "node-sass sass/main.scss css/style.css --watch",
    "compile-sass": "node-sass sass/main.scss css/style.css",
    "concat-css": "concat -o css/style.concat.css css/additional.css",
    "prefix-css": "postcss --use autoprefixer -b 'last 5 versions' css/style.concat.css -o css/style.prefix.css",
    "compress-css": "node-sass css/style.prefix.css css/style.css --output-style compressed",
    "build-css": "npm-run-all compile-sass concat-css prefix-css compress-css"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "autoprefixer": "^9.6.1",
    "concat": "^1.0.3",
    "node-sass": "^4.12.0",
    "npm-run-all": "^4.1.5",
    "postcss-cli": "^6.1.3"
  }
}
```

## 7 - 1 Folder Structure

```
sass/
|
|– abstracts/ (or utilities/)
|   |– _variables.scss    // Sass Variables
|   |– _functions.scss    // Sass Functions
|   |– _mixins.scss       // Sass Mixins
|
|– base/
|   |– _reset.scss        // Reset/normalize
|   |– _typography.scss   // Typography rules
|
|– components/ (or modules/)
|   |– _buttons.scss      // Buttons
|   |– _carousel.scss     // Carousel
|   |– _slider.scss       // Slider
|
|– layout/
|   |– _navigation.scss   // Navigation
|   |– _grid.scss         // Grid system
|   |– _header.scss       // Header
|   |– _footer.scss       // Footer
|   |– _sidebar.scss      // Sidebar
|   |– _forms.scss        // Forms
|
|– pages/
|   |– _home.scss         // Home specific styles
|   |– _about.scss        // About specific styles
|   |– _contact.scss      // Contact specific styles
|
|– themes/
|   |– _theme.scss        // Default theme
|   |– _admin.scss        // Admin theme
|
|– vendors/
|   |– _bootstrap.scss    // Bootstrap
|   |– _jquery-ui.scss    // jQuery UI
|
`– main.scss              // Main Sass file
```

## 7 - 1 Pattern import structure

@import 'abstracts/variables';
@import 'abstracts/functions';
@import 'abstracts/mixins';

@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/slider';

@import 'pages/home';
@import 'pages/about';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';

[Back](css.md)