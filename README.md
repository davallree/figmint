# 🍃 Figmint

Figmint can sync styles from a file in figma to json that can be used in a javascript project.

![example video](https://cl.ly/7edbcba03eb2/Screen%20Recording%202019-08-15%20at%2008.43%20PM.gif)

[This example site](https://tiltshift.github.io/figmint/) shows a figma file above html and css generated using the JSON that figmint outputs. This example can be found and run in the `example` folder in this repo.

🚨*Notes*:

- Currently only Fill styles and Text styles are supported. PR's welcome for Grid and Effect styles!
- Figmint will only pick up a style if it is used in the file you pass it. If you are finding a style isn't syncing make sure an element in the file is using that style.

## Install

Add figmint to your project:

```
yarn add figmint --dev
```

Config figmint see [below](#config).

You can then run figmint via the CLI:

```
yarn run figmint
```

Its also possible to run in watch mode so when you make changes in figma they are updated right away by figmint:

```
yarn run figmint watch
```

## Example Project

An example is included in this repo under the `example` directory. This project connects to the [example figma file](https://www.figma.com/file/tid5SFlwk8AqMGBP6dDJvw). To sync with the example figma file and run it:

```
> cd example
> yarn
> yarn figmint
> yarn start
```

Then visit the example page at [http://localhost:1234](http://localhost:1234).

### Using your own figma file with the example

You can connect the example to your own figma file by editing `.figmintrc.json` in the `example` directory. Just add your own `token` and `file` before running `yarn figmint`.

## Config

To connect to your own figma file you'll need to add both an access token and the file ID. See [Config Options](#config-options) for details.

Figmint uses [cosmiconfig](https://github.com/davidtheclark/cosmiconfig) for configuration file support. This means you can configure figmint via:

- A `.figmintrc` file, written in YAML or JSON, with optional extensions: .yaml/.yml/.json.
- A `.figmintrc.toml` file, written in TOML (the .toml extension is required).
- A `figmint.config.js` or `.figmintrc.js` file that exports an object.
- A "figmint" key in your package.json file.

The configuration file will be resolved starting from the location of the file being formatted, and searching up the file tree until a config file is (or isn't) found.

### Config Options

###### token

Your [figma token](https://www.figma.com/developers/docs#access-tokens)

###### file

The file ID you want to sync. In your figma file click `Share` and the copy the link. It'll look something like:

```
https://www.figma.com/file/P2X8Apme93sfEN8wACKziOxq/FileName
```

in this case the file ID is `P2X8Apme93sfEN8wACKziOxq`

###### output (default: `figmaStyles`)

Figmint writes any styles it finds to a js file. By default this file is written to a `./figmaStyles/` directory. If you would like to use a different location you can add an `output` to your config.

Output supports nested directories, so `some/directory/figma` as output would result in a new file `./some/directory/figma/` being created.

###### typescript (default: `false`)

If set to true this will generate typescript types in your export.