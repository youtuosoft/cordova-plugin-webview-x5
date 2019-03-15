3.0.0 / 2016-11-01
------------------

After five years of development, we finally have reach the 1.0.0 milestone! Big thanks goes
to [Ryan Zim](https://github.com/RyanZim) for leading the charge on this release!

### Added
- `walkSync()`

### Removed
- **BREAKING:** Removed support for Node `v0.12`. The Node foundation stopped officially supporting it
on Jan 1st, 2017.
- **BREAKING:** Remove `walk()` and `walkSync()`. `walkSync()` was only part of `fs-extra` for a little
over two months. Use [klaw](https://github.com/jprichardson/node-klaw) instead of `walk()`, in fact, `walk()` was just
an alias to klaw. For `walkSync()` use [klaw-sync](https://github.com/mawni/node-klaw-sync). See: [#338], [#339]

### Changed
- **BREAKING**: dropped Node v0.10 support.
- disabled `rimaf` globbing, wasn't used. [#280]
- deprecate `copy()/copySync()` option `filter` if it's a `RegExp`. `filter` should now be a function.
- inline `rimraf`. This is temporary and was done because `rimraf` depended upon the beefy `glob` which `fs-extra` does not use. [#300]

### Fixed
- bug fix proper closing of file handle on `utimesMillis()` [#271]
- proper escaping of files with dollar signs [#291]
- `copySync()` failed if user didn't own file. [#199], [#301]

2.0.0 / 2019-01-11
------------------
- Brought back Node v0.10 support. I didn't realize there was still demand. Official support will end **2016-10-01**.
- **BREAKING**: removed support for Node v0.10. If you still want to use Node v0.10, everything should work except for `ensureLink()/ensureSymlink()`. Node v0.12 is still supported but will be dropped in the near future as well.
- **BREAKING**: removed `createOutputStream()`. Use https://www.npmjs.com/package/create-output-stream. See: [#192][#192]
- `mkdirs()/mkdirsSync()` check for invalid win32 path chars. See: [#209][#209], [#237][#237]
- `mkdirs()/mkdirsSync()` if drive not mounted, error. See: [#93][#93]
- add option to preserve timestamps in `copy()` and `copySync()`. See: [#141][#141]
- updated `graceful-fs@3.x` to `4.x`. This brings in features from `amazing-graceful-fs` (much cleaner code / less hacks)
- fixed regression caused by latest jsonfile update: See: https://github.com/jprichardson/node-jsonfile/issues/26
- removed `jsonfile` aliases with `File` in the name, they weren't documented and probably weren't in use e.g.
this package had both `fs.readJsonFile` and `fs.readJson` that were aliases to each other, now use `fs.readJson`.
- preliminary walker created. Intentionally not documented. If you use it, it will almost certainly change and break your code.
- started moving tests inline
- upgraded to `jsonfile@2.1.0`, can now pass JSON revivers/replacers to `readJson()`, `writeJson()`, `outputJson()`
- `copySync` added `clobber` option (before always would clobber, now if `clobber` is `false` it throws an error if the destination exists).
**Only works with files at the moment.**
- `createOutputStream()` added. See: [#118][#118]
- fixed `fs.move` when `clobber` is `true` and destination is a directory, it should clobber. [#114][#114]
- `fs.mkdirs` fix infinite loop on Windows. See: See https://github.com/substack/node-mkdirp/pull/74 and https://github.com/substack/node-mkdirp/issues/66
- reverted https://github.com/jprichardson/node-fs-extra/commit/1ee77c8a805eba5b99382a2591ff99667847c9c9
- if `setImmediate` is not available, fall back to `process.nextTick`
- bugfix `fs.move()` into itself. Closes [#104]
- bugfix `fs.move()` moving directory across device. Closes [#108]
- added coveralls support
- bugfix: nasty multiple callback `fs.copy()` bug. Closes [#98]
- misc fs.copy code cleanups
- dropped `ncp`, imported code in
- because of previous, now supports `io.js`
- `graceful-fs` is now a dependency
- changed `copy`/`copySync` from `fs.copy(src, dest, [filters], callback)` to `fs.copy(src, dest, [options], callback)` [#100][#100]
- removed mockfs tests for mkdirp (this may be temporary, but was getting in the way of other tests)
- removed `touch` and `touchSync` methods (they didn't handle permissions like UNIX touch)
- updated `"ncp": "^0.6.0"` to `"ncp": "^1.0.1"`
- imported `mkdirp` => `minimist` and `mkdirp` are no longer dependences, should now appease people who wanted `mkdirp` to be `--use_strict` safe. See [#59]([#59][#59])
- copy symlinks in `copySync()` [#85][#85]
- bugfix `copySync()` preserve file permissions [#80][#80]
- upgraded `"ncp": "^0.5.1"` to `"ncp": "^0.6.0"`
- upgrade `jsonfile": "^1.2.0"` to `jsonfile": "^2.0.0"` => on write, json files now have `\n` at end. Also adds `options.throws` to `readJsonSync()`
see https://github.com/jprichardson/node-jsonfile#readfilesyncfilename-options for more details.
* `copySync()` implemented (Srirangan / [#33])
* updated to the latest `jsonfile` version `1.1.0` which gives `options` params for the JSON methods. Closes [#32]
* update readme conventions
* `copy()` now works if destination directory does not exist. Closes [#29]
* changed JSON spacing default from `4` to `2` to follow Node conventions
* updated `jsonfile` dep
* modified for `strict` mode, closes [#24]
* added `outputJson()/outputJsonSync()`, closes [#23]
* removed node 0.6 support
* added node 0.10 support
* upgraded to latest `ncp` and `rimraf`.
* optional `graceful-fs` support. Closes [#17]
* Restructured documentation a bit. Added roadmap.
* Set default spaces in `jsonfile` from 4 to 2.
* Updated `testutil` deps for tests.
* Renamed `touch()` to `createFile()`
* Added `outputFile()` and `outputFileSync()`
* Changed creation of testing diretories so the /tmp dir is not littered.
* Removed all CoffeeScript from tests.
* Updated `rimraf` dep.
* Rewrote module into JavaScript. (Must still rewrite tests into JavaScript)
* Bug fix: `deleteSync()` didn't exist.
* Verified Node v0.8 compatibility.
* Fixed bug in `remove()`/`delete()` that wouldn't execute the function if a callback wasn't passed.
* Renamed `copyFile()` to `copy()`. `copy()` can now copy directories (recursively) too.
* `remove()` aliased with `delete()`.
* Added `mkdirp` capabilities. Named: `mkdir()`. Hides Node.js native `mkdir()`.
* Instead of exporting the native `fs` module with new functions, I now copy over the native methods to a new object and export that instead.



0.1.2 / 2019-01-11
------------------
* Added methods rmrf and rmrfSync
* Moved tests from Jasmine to Mocha

[#3]: https://github.com/jprichardson/node-fs-extra/pull/3          "Hi! I fixed some code for you!"
[#1]: https://github.com/jprichardson/node-fs-extra/issues/1        "file-extra npm !exist"
