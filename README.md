# grunt-magpie [![Build Status](https://travis-ci.org/dynamo-media/grunt-magpie.svg?branch=master)](https://travis-ci.org/dynamo-media/grunt-magpie)

> Version and save assets in a remote repository.

[![NPM](https://nodei.co/npm/grunt-magpie.png)](https://nodei.co/npm/grunt-magpie/)

## Getting Started
This plugin requires Grunt `~0.4.5`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-magpie --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-magpie');
```

## The "magpie" task

### Overview
In your project's Gruntfile, add a section named `magpie` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  magpie: {
    options: {
      serverUrl: "http://my-magpie-server.com:8888",
      versionedFilesMapPath: "my_versioned_files.json"
    },
    concat_all_the_things: {
      options: {
        tasks: ["concat:all_the_things"]
      }
    },
  },
});
```

### Options

#### options.serverUrl
Type: `String`
Default value: `http://127.0.0.1:8888`

Location of the Magpie assets repository. **Must** have either `http` or `https` before the URL.

### options.tasks
Type: `Array`
Default value: false

An array of tasks to download destination files from the repository (if possible), version and upload to the repository. The tasks are run in the order they are given in.

#### options.versionAfterBuild
Type: `Boolean`
Default value: `false`

Version the destination files _after_ the tasks listed in the `options.tasks` array have completed. Use this for tasks like LESS complication (`grunt-contrib-less`) where the source files can include other files not listed explicitly in the task.

#### options.versionedFilesMapPath
Type: `String`
Default value: `versioned_files.json`

Path to the file that will contain the mappings from the original destination paths to the versioned destination paths. This is used to avoid code updates for the new versioned asset path when they change.

#### options.versionedFilesMapTemplate
Type: `String`
Default value: `null`

Path to an [Underscore.js compatible template](http://underscorejs.org/#template) file. The array variable `mappings` is passed into the data object for the template to use - it is an array of objects with the keys: `hash`, `originalPath` and `versionedPath`. This is used in combination with `options.versionedFilesMapPath`.

### options.skipExisting
Type: `Boolean`
Default value: `false`

Don't download the file from the repository or run the associated task if the destination file exists.

### options.pipeline
Type: `Boolean`
Default value: `false`

Treat the tasks array as a pipeline of tasks. A pipeline is defined as a series of tasks which need to run in their defined order to produce a single output file. An example of a pipeline would be many JavaScript files joined together using the `concat` task, then the output of that task "uglified" with the `uglify` task.

### Magpie Repository
TODO: Provide information on the compilation/setup of the repository
