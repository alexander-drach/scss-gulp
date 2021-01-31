# Learn SCSS  
scss + gulp  

create project

1. npm init
1. npm i --save-dev gulp gulp-sass gulp-autoprefixer gulp-sourcemaps gulp-contact browser-sync

start:  
npm install  
gulp  

## gulpfile.js
include gulpackages

```js
var gulp = require('gulp');
var autoprefixer = require('gulp-autoprefixer');
var concat = require('gulp-concat');
var sass = require('gulp-sass');
var sourcemaps = require('gulp-sourcemaps');
```
## config in gulpfile.js

```js
var config = {
    path: {
        scss: './src/scss/**/*/.scss',
        html: './public/index.html'
    },
    output: {
        cssName: 'bundle.min.css',
        path: './public'
    }
}
```

## task in gulpfile.js

```js
gulp.task('scss', function() {
    return gulp.src(config.path.scss)
        .pipe(sourcemaps.init())
        .pipe(sass())
        .pipe(concat(config.output.cssName))
        .pipe(autoprefixer())
        .pipe(sourcemaps.write())
        .pipe(gulp.dest(config.output.path))
        .pipe(browserSync.stream());
});

gulp.task('serve', function() {
    browserSync.init({
        server: {
            baseDir: config.output.path
        }
    });

    gulp.watch(config.path.scss, ['scss']);
    gulp.watch(config.path.html).on('change', browserSync.reload);

});

gulp.task('default', ['scss', 'serve']);
```
## package.json

```js
{
  "name": "sass-theory",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "browser-sync": "^2.18.5",
    "gulp": "^3.9.1",
    "gulp-autoprefixer": "^3.1.1",
    "gulp-concat": "^2.6.1",
    "gulp-sass": "^3.0.0",
    "gulp-sourcemaps": "^1.9.1"
  }
}
```
