# Changelog

## Unreleased

- `serve` now respects the `entrypoint` configured in `polymer.json`.
- Update Node.js version pre-run check to match current Node.js version support.
- Remove global command-line behavior to run a locally install version of the CLI if it existed in the current working directory. This unexpected behavior was never documented but some users could be running an incorrect version of the CLI as a result.

## v0.18.0 [04-13-2017]

v0.18.0 contains our latest work to support both Polymer 1.x & 2.0 projects. There are a bunch of big new features included in this update, as well as several breaking changes since the latest version. Here is a quick summary of the major changes for anyone who is updating from our previous `latest`/`v0.17.0` version:

- **New Polymer 2.0 Templates**: `polymer init` has added new Polymer 2.0 templates for starter elements, applications, and our latest Polymer Starter Kit & Shop applications. Run `polymer init` to see the whole list.
- **Updated `lint` Command**: `polymer lint` is now powered by our newest version of [polymer-linter](https://github.com/Polymer/polymer-linter). The new linter can show you the exact location of any problems in your code, and is much more configurable. Run `polymer help lint` for more information.
- **Updated `build` Command**: `polymer build` is now powered by our newest version of [polymer-build](https://github.com/Polymer/polymer-linter), which provides even more optimizations and features for customizing your build. Run `polymer help build` for more information.
- **New Build Output**: The biggest change to `polymer build` behavior is that it no longer defaults to outputting two, optimized build targets. The new default behavior is to generate a single `/build/default` directory with all configurable optimizations turned off by default. To customize your build(s) and include different optimizations, you can either include CLI flags (like `--js-compile`) or custom polymer.json build configurations. See the latest [polymer.json "builds"](https://www.polymer-project.org/2.0/docs/tools/polymer-json#builds) specification for more information.
- **New `analyze` Command:** Generates a JSON blob of metadata about your element(s). This can be useful to have for tooling and analysis.
- **New `install` Command:** Like `bower install`, but with support for installing "variants" as defined in your `bower.json`. See [the glossary](https://www.polymer-project.org/2.0/docs/glossary#dependency-variants) for more information.
- Remove Node v4 support: Node v4 is no longer in Active LTS, so as per the [Polymer Tools Node.js Support Policy](https://www.polymer-project.org/2.0/docs/tools/node-support) the Polymer CLI will not support Node v4 going forward. Please update to Node v6 or later to continue using the latest verisons of Polymer tooling.

<details>
  <summary><strong>See the Full v0.18.0 Pre-Release Changelog</strong></summary><p>

#### v0.18.0 [04-13-2017]

- `build`: Add `--add-push-manifest`/`addPushManifest` option for generating a [`push-manifest.json`](https://github.com/GoogleChrome/http2-push-manifest) file for your project.
- `build`: Fix a bug where `--insert-prefetch-links` would generate 404ing imports.
- `build`: Update automatic `webcomponentsjs` polyfilling to move it and all affected elements following it into the body so that the `custom-elements-es5-adapter.js` can work properly in IE11. (See [#627](https://github.com/Polymer/polymer-cli/issues/627))
- `init`: Init template elements now properly inherit from the given element/app name.
- `init`: Fix `polymer-2-element` template serving by removing iron-component-page until it can support Polymer 2.0 class-based elements.
- `init`: Update polymer 2.0 application & element tests to improve and fix broken tests.
- `init`: Update polymer 1.x application & element template WCT dependency to `^6.0.0-prerelease.5`.
- `init`: Update polymer application & element READMEs.
- `serve`: Update to polyserve@v0.17.0 to support autocompilation when serving to Chromium, Edge browsers.
- [Breaking] Remove Node v4 support: Node v4 is no longer in Active LTS, so as per the [Polymer Tools Node.js Support Policy](https://www.polymer-project.org/2.0/docs/tools/node-support) the Polymer CLI will not support Node v4. Please update to Node v6 or later to continue using the latest verisons of Polymer tooling.

#### v0.18.0-pre.15 [03-22-2017]

- `build`: Update automatic `webcomponentsjs` polyfilling to use `custom-elements-es5-adapter.js` instead of broken `webcomponents-es5-loader.js`. Fixes compiled, bundled builds in Chrome. (See [#605](https://github.com/Polymer/polymer-cli/issues/605))

#### v0.18.0-pre.14 [03-20-2017]

- The experimental linter has graduated to be the new default. Removed `polymer experimental-lint` command. `polymer lint` now runs [polymer-linter](https://github.com/Polymer/polymer-linter). See the README and `polymer lint --help` for more info.

#### v0.18.0-pre.13 [03-08-2017]

- When running `polymer build` and compiling JS to ES5, we will also rewrite script includes of `webcomponents-loader.js` to `webcomponents-es5-loader.js`.

#### v0.18.0-pre.12 [03-07-2017]

- Add PSK 3.0 (Polymer 2.0 Polymer Starter Kit) template to the init command.
- Automatically include un-optimized `webcomponentsjs` polyfills in builds.
- Update Polymer Analyzer, Polymer Bundler and Polymer Linter dependencies
  - Bundles now include optimizations specified in builds.
  - Much more detailed output of `analyze` command.

#### v0.18.0-pre.10 [02-21-2017]

- **New `build` Behavior**: New build options have been added to give you more control over the generated build. These options can be defined in your project's `polymer.json`, or via CLI flags. Run `polymer build --help` to see a list of new supported CLI flags.
  - **Previously default behaviors (minifying JavaScript, generating service workers, etc) are now turned off by default.**
  - Multiple builds can now be defined in your project's `polymer.json`. See [the latest documentation](https://github.com/Polymer/docs/blob/ff74953fa93ad41d659a6f5a14c5f7072368edbd/app/2.0/docs/tools/polymer-json.md#builds) for information on configuring your project build(s).
- `init`: Add new 2.0 polymer element & application templates.
- Update dependencies.
- **New `experimental-lint` command**: configurable with per-project rulesets, either with cli args or in your polymer.json. Will soon replace the `lint` command, for now run it as `polymer experimental-lint`. Specify "polymer-2", "polymer-2-hybrid", or "polymer-1" to customize the lint warnings that you receive. Run `polymer help experimental-lint` for more detail.

#### v0.18.0-alpha.9

- Fixed a bug where `polymer init` would crash if run from a folder with a
  package.json that's missing a name property. https://github.com/Polymer/polymer-cli/issues/186
- Fixed a bug where `polymer build` wouldn't analyze behaviors correctly.
- Fixed a bug where `polymer test` would complain about the version of wct it was bundled with.
- Updated dependencies.

#### v0.18.0-alpha.8

- Updated dependencies.

#### v0.18.0-alpha.7

- **Added `analyze` command:** Generates a JSON blob of metadata about your element(s). Useful for tooling and analysis.
- **Added `install` command:** Installs "variants" defined in your `bower.json`.
- Upgrade `polyserve` to `v0.6.0-prerelease.6` to handle serving variants
- Upgrade `web-component-tester` to `6.0.0-prerelease.1` to handle testing variants
- Upgrade `polymer-build` to `v0.6.0-alpha.1`, which includes an upgrade to the new [`polymer-analyzer`](https://github.com/Polymer/polymer-analyzer).
- `build`: Rename the `--include-dependencies` flag to `--extra-dependencies`
- `build`: css is now minified
- `build`: Lots of bug fixes due to the new polymer-build library and analyzer.
- `polymer.json`: Rename the `includeDependencies` & `sourceGlobs` fields to `extraDependencies` & `sources`, respectively
- Added support for v7.x of Node.js, dropped support for v5.x. Please move to an [actively maintained version of Node.js](https://github.com/nodejs/LTS) for the best experience.
- Upgrade [web-component-tester 6.0](https://github.com/Polymer/web-component-tester/blob/master/CHANGELOG.md) which brings a number of breaking changes to the `test` command.
- `init`: Fix duplicate names for sub-generators in a directory

</p></details>

## v0.17.0

- Upgrade `web-component-tester` to `v5.0.0`, which includes a new major version of mocha. See [the wct changelog](https://github.com/Polymer/web-component-tester/blob/v5.0.0/CHANGELOG.md#500) for more details.
- Upgrade `polyserve` to `v0.13.0`. See [the polyserve changelog](https://github.com/PolymerLabs/polyserve/blob/master/CHANGELOG.md) for more details.
- `build`: Add support for relative root path in polymer.json
- `build`: clear the build directory before building (#332)
- `init`: Fix issue where the application element name always used the current working directory name by default
- `init`: Fix undefined template description
- Fix issue with command failures exiting as successes (#418)

## v0.16.0

- build: fail immediately if polymer.json is invalid
- build: Add missing support for `sourceGlobs` & `includeDependencies` in polymer.json
- polymer-build@v0.4.1 (fixes ignored `staticFileGlobs` bug)


## v0.15.0

- replace app-drawer-template with starter-kit


## v0.14.0

- replace unneccesary gulp dependency with vinyl-fs
- polymer-build@v0.4.0 fixes build path issues
- but wait... THERE'S MORE! polymer-build@v0.4.0 also handles external resources properly now
- fix bug where `--version` flag threw an exception


## v0.13.0

- Refactor build logic out into standalone library: https://github.com/Polymer/polymer-build. Build behavior should remain the same from v0.12.0, but lots of work has been done in the new library to fix bugs and reduce build time/size.
- Refactor build file optimization streams
- Send an error code on polymer command run error


## v0.12.0

- gulp-typings@2.0.0
- github@1.1.0
- Update command-line-* suite of dependency, refactor to accomodate
- Refactor init command to be more easily testable, reduce startup times
- Catch exception thrown by findup when finding gulpfiles
- Add input linting argument, and fix major bug with paths
- init: Don’t crash when a package.json is present with no name
- Speed up start time, move last of the commands to load their dependencies at runtime
- Add demo and description for element template (#229)
- specify the sync interface when searching templates for package.json
- Removes unneccesary liftoff dependency
- Add update-notify to notify users when their cli is out of date
- Add tests for init command
