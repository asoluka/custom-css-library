### Purging our library

We need to purse our library so that all unused styles will be removed from our project file.

To get this done, we'd need a plugin for gulp called purge-css.

`npm install gulp-purgecss --save-dev`

Next, we'd require the plugin at the top of our gulpfile.

`const purgecss = require("gulp-purgecss");`

Now, we just have to chain in into our gulp process using the `.pipe` function like so;

```
function buildStyles () {
  return src(`/**/*.scss`)
    .pipe(purgecss({
      content: ['*.html']
    }))
}
```

The purgecss function takes in a config object. That object accepts a content key whose value is an array of files to look into.

In the example above, we have asked gulp to look for all html files in the project, identify the rules that are used in them and then remove those rules which aren't used in the final output.

### Watching for changes in html files.

Our current gulp configuration only watches for changes in our scss files. so we need to tell gulp to watch html files too so that it can rebuild when html files change.

```
function watchTask() {
  watch([`shinobi/**/*.scss`, ,`*.html`], buildStyles);
}
```
