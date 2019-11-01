# Gulp - Task Runner

## Install

    npm install --save gulp@4.x

## package.json

```json
{
"name": "alltheit_boilerplate",
"version": "1.0.0",
"main": "index.js",
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
},
"keywords": [],
"author": "",
"license": "ISC",
"description": "",
"devDependencies": {
    "@babel/core": "^7.6.4",
    "@babel/preset-env": "^7.6.3",
    "browser-sync": "^2.26.7",
    "del": "^5.1.0",
    "gulp": "^4.0.2",
    "gulp-autoprefixer": "^7.0.1",
    "gulp-babel": "^8.0.0",
    "gulp-csso": "^3.0.1",
    "gulp-if": "^3.0.0",
    "gulp-imagemin": "^6.1.1",
    "gulp-sass": "^4.0.2",
    "gulp-uglify": "^3.0.2",
    "webpack-stream": "^5.2.1"
},
"dependencies": {}
}
```

## Sample gulpfile.js

```javascript
const {src, dest, series, parallel} = require('gulp')
const gulp = require('gulp')
const del = require('del')
const sass = require('gulp-sass')
const imagemin = require('gulp-imagemin')
const babel = require('gulp-babel')
const uglify = require('gulp-uglify')
const browserSync = require('browser-sync').create()
// const webpack = require('webpack-stream')

function watch() {
browserSync.init({
    server:{
    baseDir: "./dist",
    index: "/index.html"
    }
})

gulp.watch('src/scss/**/*.scss', cssTrans)
gulp.watch('src/js/**/*.js', series(jsTrans, browserSync.reload))
gulp.watch('dist/*.html').on('change', browserSync.reload)
}

function clean() {
return del([
    'dist/css/**',
    'dist/js/**',
    'dist/img/**',
])
}

function cssTrans() {
return src('src/scss/*.scss')
    .pipe(sass())
    .pipe(dest('dist/css'))
    .pipe(browserSync.stream())
}

function imgTrans() {
return src('src/img/*')
    .pipe(imagemin())
    .pipe(dest('dist/images'))
}

function jsTrans() {
return src('src/js/*.js')
    .pipe(babel({
    presets: ['@babel/preset-env']
    }))
    .pipe(uglify())
    .pipe(dest('dist/js'))

}

exports.clean = clean
exports.css = cssTrans
exports.img = imgTrans
exports.js = jsTrans
exports.watch = watch
exports.build = series(clean, parallel(cssTrans, jsTrans, imgTrans))
exports.default = function (done){
done()
}
```
