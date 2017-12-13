# postcss-px2rem
## fork 过来是为解决 因为webpack压缩时候会把css的注释先去除，然后在loader，导致带注释的编译无效 
### 现使用自定义的单位的方式标明处理 这里使用大写是因为我 使用的是scss 如果用小写的话  会被转义成px 233  = =并没有找到好的解决的方式就大写了。

>  如果是 直接使用postcss 的请使用（PS 我是看了他来改的） [postcss-plugin-px2rem](https://github.com/ggpp224/postcss-plugin-px2rem)

in
```css
.cls {
  width: 75px;
  font-size: 12DPX;
  border: 1RPX;
}
```

out
```css
.cls {
  width: 2rem;
  border: 1px;
}
[data-dpr="1"] .cls { font-size: 12px }
[data-dpr="2"] .cls { font-size: 24px }
[data-dpr="3"] .cls { font-size: 36px }
```

This is a [postcss](https://www.npmjs.com/package/postcss) plugin of [px2rem](https://www.npmjs.com/package/px2rem).

[![NPM version][npm-image]][npm-url]
[![Build status][travis-image]][travis-url]
[![Downloads][downloads-image]][downloads-url]

[npm-image]: https://img.shields.io/npm/v/postcss-px2rem.svg?style=flat-square
[npm-url]: https://npmjs.org/package/postcss-px2rem
[travis-image]: https://img.shields.io/travis/songsiqi/px2rem-postcss.svg?style=flat-square
[travis-url]: https://travis-ci.org/songsiqi/px2rem-postcss
[downloads-image]: http://img.shields.io/npm/dm/postcss-px2rem.svg?style=flat-square
[downloads-url]: https://npmjs.org/package/postcss-px2rem

## install 
```
yarn add @vayne/postcss-px2rem -D
npm i @vayne/postcss-px2rem -D
```

## Usage

### Node

```
var postcss = require('postcss');
var px2rem = require('postcss-px2rem');
var originCssText = '...';
var newCssText = postcss().use(px2rem({remUnit: 64})).process(originCssText).css;
```

**Please see [px2rem](https://www.npmjs.com/package/px2rem) for more information about the features and usage of px2rem.**

### Gulp

```
npm install gulp-postcss
```

```
var gulp = require('gulp');
var postcss = require('gulp-postcss');
var px2rem = require('postcss-px2rem');

gulp.task('default', function() {
  var processors = [px2rem({remUnit: 75})];
  return gulp.src('./src/*.css')
    .pipe(postcss(processors))
    .pipe(gulp.dest('./dest'));
});
```

### Webpack

```
npm install postcss-loader
```

```
var px2rem = require('postcss-px2rem');

module.exports = {
  module: {
    loaders: [
      {
        test: /\.css$/,
        loader: "style-loader!css-loader!postcss-loader"
      }
    ]
  },
  postcss: function() {
    return [px2rem({remUnit: 75})];
  }
}
```

### Grunt

```
npm install grunt-postcss
```

```
module.exports = function(grunt) {
  grunt.initConfig({
    postcss: {
      options: {
        processors: [
          px2rem({remUnit: 75})
        ]
      },
      dist: {
        src: 'src/*.css',
        dest: 'build'
      }
    }
  });
  grunt.loadNpmTasks('grunt-postcss');
  grunt.registerTask('default', ['postcss']);
}
```

## Change Log

### 0.3.0

* Deps: px2rem@~0.5.0
  * Support Animation keyframes (no `/*px*/` comment).

### 0.2.0

* Deps: postcss@^5.0.0

### 0.1.6

* Deps: px2rem@~0.4.0
  * The generated [data-dpr] rules follow the origin rule, no longer placed at the end of the whole style sheet.
  * Optimize 0px, do not generate 3 [data-dpr] rules.

### 0.1.5

* Do not extend current root node.

### 0.1.4

* Fix bug while working with webpack loader.

### 0.1.0

* First release.

## License

MIT
