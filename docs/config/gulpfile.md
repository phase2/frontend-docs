Gulp steps in to handle the gaps that Webpack misses. In two words, Twig support. In more words, Twig namespacing support for appropriate apps, some helper tasks for Pattern Lab, and the previously mentioned tasks for starting and refreshing the webpack dev server locally.

# Configuration 

All gulp tasks and associated configuration are declared inside **gulpfile.js**. 
You can see a full list of available tasks by running `npm run gulp -- -T`. The extra -- passes any flags to the gulp function. This method allows us to keep gulp as a local project dependency, instead of relying on global installs.

# Tasks
All gulp task functions are exported from `./tools/tasks/*.js`, wrapped in a callback. The callback signals to gulp to move through the task list.

For example, this is the task that compiles Pattern Lab, found in `./tools/tasks/pl-compile.js` 
 
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

This function is then included in our main `gulpfile.js` and wrapped in a task like so:

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

Every new task should be defined in a similar manner to this, to ensure gulp and webpack play nicely together.

# twig-namespaces

This task is the sauce that lets us compile pattern lab error-free, without manually adding every new pattern folder 
to the pattern lab config file. Each app that needs to know about twig namespaces needs an object like so: 

```json
      {
        // Note: PL will NOT compile unless the namespaces are explicitly declared
        configFile: path.join(PATH_PL, 'pattern-lab/config/config.yml'),
        atKey: 'plugins.twigNamespaces.namespaces',
        pathRelativeToDir: path.join(PATH_PL, 'pattern-lab/'),
      },
```

This is all the info gulp needs to plop down the namespace paths at. 
The namespaces themselves are defined right underneath those objects: 

```json
// What are the top-level namespace paths, and which sub paths should we ignore?
    sets: {
      protons: {
        root: 'source/_patterns/00-protons',
        ignore: '/demo',
      },
```
 
If you adjust the namespace sets, be sure to also adjust the accompanying namespace in `webpack.shared.config.js`.
