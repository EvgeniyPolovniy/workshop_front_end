####Table of Contents

**[Emmet](#emmet)**

**[SCSS](#scss-sass)**

**[GULP](#gulp)**

**[CSS](#css)**

#Emmet
[Emmet official site](http://docs.emmet.io/)

#### !
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	
</body>
</html>
```

#### div+div>p>span+em^bq
```html
<div></div>
<div>
    <p>
      <span></span>
      <em></em>
    </p>
    <blockquote></blockquote>
</div>
```

#### ul.generic-list>lorem5.item*4
```html
<ul class="generic-list">
	<li class="item">Lorem ipsum dolor sit amet.</li>
	<li class="item">Illum corrupti, non earum voluptatum.</li>
	<li class="item">Eius unde blanditiis et eligendi!</li>
	<li class="item">Quasi sequi maxime accusamus nesciunt!</li>
</ul>
```
# SCSS (SASS)
[SASS official site](http://sass-lang.com//)
### Вложенность
SCSS
```scss
#some {
  border: 1px solid red;
  .some { background: white; }
}
```
CSS
```css
#some {
  border: 1px solid red;
}
#some .some {
  background: white;
}
```
### Переменные и операции с ними
SCSS
```scss
$blue: #3bbfce;
$margin: 16px;
$url: url(../img/icons/ui-ios-sprite.png);

.content-navigation {
  border-color: $blue;
  color: darken($blue, 9%);
}
.border {
  padding: $margin / 2;
  margin: $margin / 2;
  border-color: $blue;
}
.wrapper {
  background: $url;
}
```
CSS
```css
.content-navigation {
  border-color: #3bbfce;
  color: #2ca2af;
}
.border {
  padding: 8px;
  margin: 8px;
  border-color: #3bbfce;
}
.wrapper {
  background: url(../img/icons/ui-ios-sprite.png);
}
```
### Подключение других scss файлов
SCSS
```scss
@import "./core/variables";
@import "./core/mixin";
@import "./core-project/variables";
```

### Миксинны
SCSS
```scss
@mixin text-truncate {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
@mixin transition( $transition-property, $transition-time, $transition-method ) {
  -webkit-transition: $transition-property $transition-time $transition-method;
  -moz-transition: $transition-property $transition-time $transition-method;
  -ms-transition: $transition-property $transition-time $transition-method;
  -o-transition: $transition-property $transition-time $transition-method;
  transition: $transition-property $transition-time $transition-method;
}

.block-wrap {
  .block {
    @include text-truncate;
  }
  @include transition(all, .2ms, ease);
}
```
CSS
```css
.block-wrap {
  -webkit-transition: all 0.2ms ease;
  -moz-transition: all 0.2ms ease;
  -ms-transition: all 0.2ms ease;
  -o-transition: all 0.2ms ease;
  transition: all 0.2ms ease;
}
.block-wrap .block {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
```
### Наследование
SCSS
```scss
%extend_1 {
  display: inline-block;
}
%extend_2 {
  @extend %extend_1;
  width: 34px;
  height: 19px;
}
.wrap {
  @extend %extend_1;
  .block {
    @extend %extend_2;
  }
}
```
CSS
```css
.wrap,
.wrap .block {
  display: inline-block;
}
.wrap .block {
  width: 34px;
  height: 19px;
}
```
#Gulp
[Gulp official site](http://gulpjs.com/)

package.json
```json
{
  "name": "tishman",
  "version": "1.0.0",
  "description": "",
  "main": "build.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git@gitlab.a2a.co:webinerds/tishman.git"
  },
  "author": "Max Klishevych",
  "license": "ISC",
  "devDependencies": {
    "del": "^1.2.0",
    "gulp": "^3.8.11",
    "gulp-concat": "^2.5.2",
    "gulp-order": "^1.1.1",
    "gulp-resolve-dependencies": "^2.1.0",
    "gulp-sass": "^2.0.1",
    "require-dir": "^0.3.0"
  }
}
```
./gulpfile.js
```js
require('./ichannel-base/gulpfile.js'); 
```
./ichannel-base/gulpfile.js
```js
var requireDir = require('require-dir');
// Require all tasks in gulp/tasks, including sub folders
requireDir('./gulp/tasks', { recurse: true });
```
./ichannel-base/gulp/config.js
```js
module.exports = {
    files: {
        scss: {
            base: './ichannel-base/assets/scss/**/*.scss',
            project: './assets/scss/**/*.scss',
            mergeFolder: './merged-scss',
            buildName: 'build.css',
            compileFolder: './compiled-css',
            buildFolder: './public/css',
            concatFilesOrder: [
                'global.scss',
                'global-*.scss'
            ]
        },
        fonts: {
            project: './assets/fonts/**/**',
            buildFolder: './public/fonts'
        },
        img: {
            base: './ichannel-base/assets/img/**/**',
            project: './assets/img/**/**',
            buildFolder: './public/img'
        },
        js: {
            base: './ichannel-base/js/**/*.js',
            project: './js/**/*.js',
            buildName: 'build.js',
            buildFolder: './public/js',
            mergeFolder: './merged-js',
            concatFilesOrder: [
                'constants.js',
                'config-base.js',
                'config.js',
                'app.js',
                'utils/*',
                'services/*',
                'controllers/**/**',
                'ui/*',
                'views/**/**',
                'bootstrap.js'
            ]
        },
        views: {
            base: './ichannel-base/views/**/*.html',
            project: './views/**/*.html',
            buildName: 'index.html',
            buildFolder: '.',
            mergeFolder: './merged-html',
            concatFilesOrder: [
                'index.start.html',
                'body.html',
                'templates/**/**',
                'index.end.html'
            ]
        }
    }
};
```
#### Путь одной таски
запуск сборщика
```
E:\OpenServer\domains\jen.a2a.co>gulp
```
./ichannel-base/gulp/tasks/dafault.js
```js
var gulp = require('gulp');

gulp.task('default', [
    'js:default',
    'scss:default',
    'img:default',
    'views:default',
    'fonts:default'
]);
```
./ichannel-base/gulp/tasks/sscss:default.js
```js
var gulp = require('gulp');

gulp.task('scss:default', ['scss:merge', 'scss:concat', 'scss:compile', 'scss:cleanup']);
```
одна из задачь - сборка scss
./ichannel-base/gulp/tasks/scss-compile.js
```js
var gulp = require('gulp');
var sass = require('gulp-sass');
var config = require('../config');

gulp.task('scss:compile', ['scss:merge'], function (cb) {
    var stream = gulp
        .src([config.files.scss.mergeFolder + '/**/**'])
        .pipe(sass().on('error', sass.logError))
        .pipe(gulp.dest(config.files.scss.compileFolder))
    ;

    stream.on('end', function () {
        cb();
    });
});
```
Выполнение сборки проекта
```
E:\OpenServer\domains\jen.a2a.co>gulp
[17:20:36] Using gulpfile E:\OpenServer\domains\jen.a2a.co\gulpfile.js
[17:20:36] Starting 'js:merge'...
[17:20:36] Starting 'scss:merge'...
[17:20:36] Starting 'img:merge'...
[17:20:36] Starting 'views:merge'...
[17:20:36] Starting 'fonts:concat'...
[17:20:36] Finished 'fonts:concat' after 25 ms
[17:20:36] Starting 'fonts:default'...
[17:20:36] Finished 'fonts:default' after 13 µs
[17:20:36] Finished 'scss:merge' after 420 ms
[17:20:36] Starting 'scss:compile'...
[17:20:36] Finished 'img:merge' after 559 ms
[17:20:36] Starting 'img:default'...
[17:20:36] Finished 'img:default' after 5.53 µs
[17:20:36] Finished 'scss:compile' after 301 ms
[17:20:36] Starting 'scss:concat'...
[17:20:36] Finished 'scss:concat' after 44 ms
[17:20:36] Starting 'scss:cleanup'...
[17:20:36] Finished 'scss:cleanup' after 1.17 ms
[17:20:36] Starting 'scss:default'...
[17:20:36] Finished 'scss:default' after 5.13 µs
[17:20:37] Finished 'views:merge' after 949 ms
[17:20:37] Starting 'views:concat'...
[17:20:37] Finished 'js:merge' after 1.11 s
[17:20:37] Starting 'js:concat'...
[17:20:37] Finished 'views:concat' after 370 ms
[17:20:37] Starting 'views:cleanup'...
[17:20:37] Finished 'views:cleanup' after 185 µs
[17:20:37] Starting 'views:default'...
[17:20:37] Finished 'views:default' after 6.71 µs
[17:20:37] Finished 'js:concat' after 274 ms
[17:20:37] Starting 'js:cleanup'...
[17:20:37] Finished 'js:cleanup' after 150 µs
[17:20:37] Starting 'js:default'...
[17:20:37] Finished 'js:default' after 6.32 µs
[17:20:37] Starting 'default'...
[17:20:37] Finished 'default' after 5.92 µs

E:\OpenServer\domains\jen.a2a.co>
```
# CSS
Основные правила чистаты кода
```css
/* Плохой CSS */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* Хороший CSS */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin: 0 0 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```
