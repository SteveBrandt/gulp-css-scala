# gulp-css-scala

[![Build Status](https://travis-ci.org/SteveBrandt/gulp-css-scala.svg?branch=master)](https://travis-ci.org/SteveBrandt/gulp-css-scala)

Gulp Custom Plugin to convert style classes from css file into a scala object

## Installation 

`npm install gulp-css-scala --save-dev`


## Usage

 Have alook at the example directory. 

```js
var rename = require('gulp-rename'),
    cssScala = require('gulp-css-scala');

gulp.task('default', function() {
    return gulp.src('style/foo.css').
    pipe(cssScala()).
    pipe(rename('Css.scala')).
    pipe(gulp.dest('dest'));
});
```
This will create a new `Css.scala` object in the directory `dest` from the given css file `foo.css`.
**Only style classes are considered.**

**Input (foo.css):**
```css
.foo{
    color:red;
}
.foo__bar{
    color:red;
}
.foo--bar{
    color:red;
}

```

**Output (Css.scala):**
```scala
package com.example.css

// File is generated by gulp-css-scala

object Css {
  val foo: String = "foo"
  val fooAsBar: String = "foo--bar"
  val fooChildBar: String = "foo__bar"
}
```

## Additional css style selectors

```
gulp.task('default', function() {
    return gulp.src(['styles/*.css', 'additional-style-class-selectors.txt']).
    pipe(cssScala()).
    pipe(rename('Css.scala')).
    pipe(gulp.dest('dest'));
});
```


## Options

```js
cssScala({
    packageName:'com.example.css', 
    objectName:'Css'
})
```

|Name|Description|Default|
|---|---|---|
|packageName|The name of the package of the generated object|com.example.css|
|objectName|The name of the generated object|Css|




