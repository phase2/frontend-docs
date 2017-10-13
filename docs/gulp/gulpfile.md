# Configuration 

All gulp tasks and associated configuration are declared inside **gulpfile.js**. 
You can see a full list of available tasks by running `npm run gulp -- -T`. The extra -- passes any flags to the gulp function. This method allows us to keep gulp as a local project dependency, instead of relying on global installs.

# Tasks
All gulp task functions are exported from `./tools/tasks/*.js`, wrapped in a callback. The callback signals to gulp to move through the task list.

# Example

```js
const { exec } = require('child_process');

/**
 * Compile Pattern Lab
 * @param plPath Full path to PL
 * @returns {function(*)} A compile function that takes a callback
 */
module.exports = function plCompile(plPath) {
  // Note returns a function with the plPath in closure
  return (done) => {
    exec(`php ${plPath}/core/console --generate`, (err, stdout, stderr) => {
      console.log(stdout);

      if (err) {
        console.log(stderr);
        done();
        return false;
      }

      done();
      return true;
    });
  };
};
```


This function is then included in our main gulpfile.js and wrapped in a task like so:

```js
/**
 * Pattern Lab raw compile function.
 */
// Config: Path to Pattern Lab installation.
const plPath = path.resolve(__dirname, 'tools/pattern-lab');
// PL compilation function, loaded up with the the PL path
const plCompile = require('./tools/tasks/pl-compile')(plPath);

/**
 * Compile Pattern Lab completely.
 */
gulp.task('compile:pl', plCompile);
```
