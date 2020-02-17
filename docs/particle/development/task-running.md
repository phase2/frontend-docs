# Task Running

## Gulp

Gulp 4 is used to run a small set of tasks that can't be accomplished by Webpack alone. Examine `gulpfile.js` for all tasks available. Feel free to edit and add tasks to this file.

Gulp 4 is used and the `npm run` commands above basically trigger gulp without having to install a global dependency. If you want to run specific gulp tasks, run `npm run gulp -- TASKNAME`. The `--` passes whatever comes after to the `gulp` command. Run `npm run gulp -- --tasks` to see the whole list, here's some examples of what you can do:

* `npm run gulp -- --help` - See the help menu
* `npm run gulp -- compile` - Compile Pattern Lab

For more info on Gulp:

* [Gulp 4 Docs](https://github.com/gulpjs/gulp/tree/4.0/docs)
* [Gulp 4 Readme](https://github.com/gulpjs/gulp/blob/4.0/README.md)

