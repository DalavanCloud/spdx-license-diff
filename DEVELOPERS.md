# Making edits

## Entryfiles (bundles)

There are two kinds of entryfiles that create bundles when `gulp` is run.

 1. All js-files in the root of the `./app/scripts` directory
 2. All css-,scss- and less-files in the root of the `./app/styles` directory

The main logic is in `/app/scripts/background.js`, `/app/scripts/contentscript.js` and `app/scripts/worker.js`.

## Adding dependencies

1. Use yarn or npm to add the dependency.
2. Edit the [scripts.js](tasks/scripts.js) task that imports plugins for webpack.
3. Import the library where needed.

## Building from source

### Installation of Prerequisites

 1. Install [node](https://nodejs.org/en/download/).
 2. Use yarn (preferred):`$ yarn install` or npm: `$ npm install`

### Building and Loading

 1. Build the extension
  - Production:
      - Chrome: Run `$ gulp pack`
      - Firefox: Run `$ gulp pack --vendor firefox`
  - Development:
      - Chrome: Run `$ gulp`
      - Firefox: Run `$ gulp --vendor firefox`

 2. Load the extension:
  - Chrome:
      - Load `dist/chrome` directory using Load Unpacked.

![Extensions menu](https://developer.chrome.com/static/images/get_started/load_extension.png)
  - Firefox:
      - Enter "about:debugging" in the URL bar
      - Click "Load Temporary Add-on"
      - Load `dist/firefox/manifest.json`

[![Firefox Addons](https://img.youtube.com/vi/cer9EUKegG4/0.jpg)](https://www.youtube.com/watch?v=cer9EUKegG4)

## Tasks

### Build

    $ gulp


| Option         | Description                                                                                                                                           |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--watch`      | Starts a livereload server and watches all assets. <br>To reload the extension on change include `livereload.js` in your bundle. Chrome only.                      |
| `--production` | Minifies all assets                                                                                                                                   |
| `--verbose`    | Log additional data to the console.                                                                                                                   |
| `--vendor`     | Compile the extension for different vendors (chrome, firefox, opera, edge)  Default: chrome                                                                 |
| `--sourcemaps` | Force the creation of sourcemaps. Default: !production                                                                                                |


### pack

Zips your `dist` directory and saves it in the `packages` directory.

    $ gulp pack --vendor=firefox

### Version Control

Increments version number of `manifest.json` and `package.json`,
commits the change to git and adds a git tag.


    $ gulp patch      // => 0.0.X

or

    $ gulp feature    // => 0.X.0

or

    $ gulp release    // => X.0.0


## Globals

The build tool also defines a variable named `process.env.NODE_ENV` in your scripts. It will be set to `development` unless you use the `--production` option.


**Example:** `./app/background.js`

```javascript
  if (process.env.NODE_ENV === 'development') {
    console.log('We are in development mode!');
  }
```
