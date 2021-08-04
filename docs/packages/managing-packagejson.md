---
id: managing-packagejson
title: Managing the package.json
---

The `package.json` for component packages can can be configured via the workspace config file (`workspace.jsonc`) using the PKG workspace API or via you own Bit extensions, using the PKG programmatic API.


This page discusses the former option. However, the structure of the configuration is the same for both methods.

:::info Configure only using the variants aspect
The PKG extension can only be configured using the [Variants](/workspace/cascading-rules) aspect.
:::

## Configurations

### Package properties

Use the `packageJson` property to add or override the default `package.json` for your component packages.

:::caution
Packages with a modified `name` property will not be published to Bit.dev's registry.
:::

```js
{
  "ui/*": {
    "teambit.pkg/pkg": {
      "packageJson": {
          "name": "@{scope}/{name}",
          "private": false,
          "main": "dist/{main}.js",
          "custom-prop": "value"
      }
    }
  }
}
```

#### Placeholders

Placeholders are an easy way to inject component-specific information into the 'pkg' configurations.

- `{name}` - The name of the component.
- `{scope}` - The name of the component scope.
- `{main}` - the name of the main file (leaving out the extension) - for example `index.js` will be `index`.

For example:

```js
 "packageJson": {
    "main": "dist/{main}.js"
  }
```