# gulp-autoprefixer

[Autoprefixer](https://github.com/ai/autoprefixer) for
[gulp](https://github.com/wearefractal/gulp).

## Install

```sh
$ npm install gulp-autoprefixer
```

## Usage

```js
var gulp = require('gulp');
var prefix = require('gulp-autoprefixer');

gulp.task('default', function () {
  return gulp.src('src/styles/*.css')
    .pipe(prefix())
    .pipe(gulp.dest('dist/'));
});
```

### Examples

Specify the [browsers](https://github.com/postcss/autoprefixer#browsers) you
want to target:

```js
return gulp.src('src/styles/*.css')
  .pipe(prefix('last 2 versions', '> 1%', 'ie 9'))
  .pipe(gulp.dest('dist/'));
```

Disable the `cascade` option:

```js
return gulp.src('src/styles/*.css')
  .pipe(prefix('last 2 versions', '> 1%', 'ie 8', {cascade: false}))
  .pipe(gulp.dest('dist/'));
```

Enable `sourcemap` option:

```js
return gulp.src('src/styles/app.css')
  .pipe(prefix('last 2 versions', '> 1%', 'ie 9', { map: true, to: 'app.css' }))
  .pipe(gulp.dest('dist/'));
```

Enable `sourcemap` with dynamic filenames or multiple files (requires [`gulp-foreach`](https://www.npmjs.org/package/gulp-foreach)):

```js
...
var foreach = require('gulp-foreach');
...

return gulp.src('src/styles/*.css')
  .pipe(foreach (function (stream, file) {
    console.log(path.basename(file.path));
    return stream
      .pipe(prefix('last 2 versions', '> 1%', 'ie 8', {
        cascade: false,
        map: true,
        to: path.basename(file.path)
      }));
  }))
  .pipe(gulp.dest('css/'));

## License

Released under the MIT license.
