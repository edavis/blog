---
title: "Overriding variables in Bulma"
date: 2018-02-03T11:11:37-08:00
---

[Bulma][] is an awesome CSS framework I'm using to build a new
WordPress theme.

However, I needed to override the default background color and font
along with increasing the size of a breakpoint. Here are my notes for
how I accomplished it. The Bulma part was easy, it was figuring out
npm and gulp that took the longest. There may be cleaner or better
ways to do this, but it's working pretty well for me so far.

Install the source files (`$ npm install bulma`) which will place the
latest Bulma release in `./node_modules/bulma/`.

I copied this directory to `./vendor/bulma/` as everything I found
said `./node_modules/` should be kept out of version control.

Create a `style.scss` with the following at the top:

```css
@import url('https://fonts.googleapis.com/css?family=Muli:400,700');

// Needed for $gap
@import "vendor/bulma/sass/utilities/initial-variables";

$family-sans-serif: "Muli", "Helvetica", "Arial", sans-serif;
$body-background-color: #F4F4F4;
$fullhd: 1480px + (2 * $gap);

// Now, import the full package
@import "vendor/bulma/bulma";

// Site styles start here
```

Now the compiled CSS will include Bulma (with the customized defaults)
along with the site-specific styles.

I then rigged up gulp to teach myself how that tool works by placing
the following in `gulpfile.js`:

```javascript
var gulp = require( 'gulp' );
var sass = require( 'gulp-sass' );

var paths = {
	styles: ['style.scss'],
}

gulp.task( 'styles', function () {
	return gulp.src( paths.styles )
	.pipe( sass({ outputStyle: 'compact' }))
	.pipe( gulp.dest( '.' ));
});

gulp.task( 'default', ['styles'] );
```

And run it with `gulp`. Kind of overkill for now, but with gulp in
place I can add more tasks as needed with ease.

(H/T to [Chuck Grimmett][] for sharing one of his gulpfiles which
clarified a few tricky bits for me.)

[Bulma]: https://bulma.io/
[Chuck Grimmett]: http://www.cagrimmett.com/
