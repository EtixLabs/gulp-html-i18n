# gulp-html-i18n
Internationalize your HTML files with [gulp](http://gulpjs.com/)!

## Language Definition Files

`gulp-html-i18n` supports two formats for definition fies: JavaScript and JSON

### JS
Given the following in a file named: `lang/en-US/index.js`

```js
define({
  heading: "Welcome!",
  footer:  "Copyright 2015"
};
```

`gulp-html-i18n` will produce an object called `index`. You can then use
`${{ index.heading }}$` to get a result of "Welcome!".

### JSON
Given the following in a file named: `lang/en-US/index.json`

```json
{
  "heading": "Welcome!",
  "footer":  "Copyright 2015"
}
```

`gulp-html-i18n` will produce an object called `index`. You can then use
`${{ index.heading }}$` to get a result of "Welcome!".

## HTML Markup
To use either of the examples from above, replace the text in your HTML files
with a formatted tag: `${{ library.tag.name }}$`

### Example: index.html

Initial:

```html
<html>
  <body>
    <h1>${{ index.heading }}$</h1>
    <div>
      <!-- Website content -->
    </div>
    <div>${{ index.footer }}$</div>
  <body>
</html>
```

Output:

```html
<html>
  <body>
    <h1>Welcome!</h1>
    <div>
      <!-- Website content -->
    </div>
    <div>Copyright 2015</div>
  <body>
</html>
```

## Gulp Usage

The following task:

```js
gulp.task('build:localize', function() {
  var dest  = './public';
  var index = './index.html';

  return gulp.src(index)
    .pipe(i18n({
      langDir: './lang',
      trace: true
    }))
    .pipe(gulp.dest(dest));
});
```

will compile `index.html` to `public/index-{lang}.html` for each language your
define in `./lang`.

## Options

Option | Default | Type | Description
-------|---------|------|------------
langDir | null (required, must be provided)| String | Specifies the path to find definitions
inline | null | String | If given, will use the provided language to create an output file of the same name as input. For example, passing `inline: 'en-US'` for `index.html` will result in `index.html` with English replacements.
createLangDirs | false | bool | If `true`, instead of translating `index.html` into `index-en.html`, etc, will translate to `en/index.html`, etc.
trace | false | bool | If `true`, will place comments in output HTML to show where the translated strings came from
