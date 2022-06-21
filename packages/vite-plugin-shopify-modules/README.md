# vite-plugin-shopify-modules

This plugin enables Shopify theme developers to structure their code into "module" folders which keep Liquid template files (snippets and sections) organized together with their corresponding JS or CSS, while retaining the standard file structure of Shopify themes.

## Features

* Automatically associates each module folder with the matching snippet or section files based on file name
* Generates symbolic links to corresponding liquid files from module folders
* Moves liquid files created within module folders to correct theme folders and replaces them with symlinks
* Fully compatible with Shopify GitHub integration and Shopify CLI features for syncing updates from remote theme

## Install

```bash
npm i vite-plugin-shopify-modules -D

# yarn
yarn add vite-plugin-shopify-modules -D

# pnp
pnpm add vite-plugin-shopify-modules -D

```

## Usage

Add `shopifyModules` plugin to vite.config.js / vite.config.ts:

```ts
// vite.config.js / vite.config.ts
import { shopifyModules } from 'vite-plugin-shopify-modules'

export default {
  plugins: [
    shopifyModules({
      // Default options shown:
      modulesDir: 'modules'
    })
  ]
}
```

- Create a "modules" folder alongside your theme folders, or use the `modulesDir` plugin option to specify an alternate location.
- Create a subfolder for each theme module. The folder name should precisely match the filename of the corresponding liquid section and/or snippet file.
- If a section or snippet file exists matching the module folder name, a symlink will be generated pointing from the module folder to the actual file.
- If a file matching the `[module-name].section.liquid` or `[module-name].snippet.liquid` naming convention is found in the module folder, it will be moved to the corresponding theme folder and replaced with a symlink.
- You can place any other files in the module folder and they will not be affected by the plugin. If you add JS or CSS, make sure these files are imported from an entrypoint file somewhere to include them in the bundled output.

```bash
my-theme
  ├── assets
  │── config
  │── layout
  │── locales
  │── modules
  │   └── cart-drawer
  │       └── cart-drawer.js
  │       └── cart-drawer.css
  │       └── cart-drawer.section.liquid # Symlink to /sections/cart-drawer.liquid
  │       └── cart-drawer.snippet.liquid # Symlink to /snippets/cart-drawer.liquid
  │── sections
  │   └── cart-drawer.liquid
  │── snippets
  │   └── cart-drawer.liquid
  └── templates
```

## Example

See [seed-theme](https://github.com/barrel/barrel-shopify/tree/main/packages/seed-theme) for an example Shopify theme using this plugin.

## To-Do

- [ ] Unit tests

## Bugs

Please create an issue if you found any bugs, to help me improve this project!