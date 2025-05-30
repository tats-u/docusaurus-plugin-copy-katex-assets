# docusaurus-plugin-copy-katex-assets plugin

[![Version](https://img.shields.io/npm/v/@tats-u/docusaurus-plugin-copy-katex-assets)](https://npmjs.com/package/@tats-u/docusaurus-plugin-copy-katex-assets) [![NPM Downloads](https://img.shields.io/npm/dm/@tats-u/docusaurus-plugin-copy-katex-assets)](https://npmjs.com/package/@tats-u/docusaurus-plugin-copy-katex-assets) [![NPM Last Update](https://img.shields.io/npm/last-update/@tats-u/docusaurus-plugin-copy-katex-assets)](https://npmjs.com/package/@tats-u/docusaurus-plugin-copy-katex-assets)

This plugin copies KaTeX assets to the build directory. This makes it unnecessary to [load KaTeX assets from the CDN](https://docusaurus.io/docs/markdown-features/math-equations).

Demo: https://tats-u.github.io/docusaurus-plugin-copy-katex-assets

## How to Use

Install the plugin:

```
npm install @tats-u/docusaurus-plugin-copy-katex-assets
```

This package exports the following plugin and companion types and variables:

| Name | Description |
| --- | --- |
| `copyKaTeXAssetsPlugin` | Docusaurus plugin to copy KaTeX assets |
| `CopyKaTeXAssetsPluginOptions` | Configuration options for the plugin |
| `defaultKaTeXStyleSheet` | Default KaTeX style sheet entry for `config.stylesheets` array |
| `getKaTeXStyleSheet` | Ditto, but with custom base URL |
| `defaultKaTeXCssPath` | Default KaTeX CSS path |
| `getKaTeXCssPath` | Ditto, but with custom base URL |

Then add the plugin to `docusaurus.config.js`:

```js
import { copyKatexAssetsPlugin, defaultKaTeXStyleSheet } from '@tats-u/docusaurus-plugin-copy-katex-assets';

/**
 * @import { CopyKaTeXAssetsPluginOptions } from '@tats-u/docusaurus-plugin-copy-katex-assets';
 */

const config = {
  // ...
  stylesheets: [
    // ...
    defaultKaTeXStyleSheet,
  ],
  plugins: [
    // ...
    copyKatexAssetsPlugin,
  ],
}
```

> [!NOTE]
> For TypeScript, use the following instead:
>
> ```ts
> import { type CopyKaTeXAssetsPluginOptions, copyKatexAssetsPlugin, defaultKaTeXStyleSheet } from '@tats-u/docusaurus-plugin-copy-katex-assets';
> ```

### Compatibility with Docusaurus Faster

This plugin is compatible with [Docusaurus Faster](https://github.com/facebook/docusaurus/issues/10556).

### Configuration

The default deployed path is `/assets/katex-{KaTeX version}/katex.min.css`. If you want to change the path, pass `assetsRoot` to the plugin:

```js
const config = {
  // ...
  plugins: [
    // ...
    [
      copyKatexAssetsPlugin,
      // Important: Path shall not start with `/`.
      /** @satisfies {CopyKaTeXAssetsPluginOptions} */({ assetsRoot: 'assets/katex' }),
    ],
  ],
}
```

> [!NOTE]
> For TypeScript, use `{ ... } satisfies CopyKaTeXAssetsPluginOptions` instead.

If you want to use a custom base URL, pass `baseUrl` to the plugin, and use `getKaTeXStyleSheet` instead of `defaultKaTeXStyleSheet`:

```js
const baseUrl = '/your-repo-name/';

const config = {
  // ...
  baseUrl,
  // ...
  stylesheets: [
    // ...
    getKaTeXStyleSheet(baseUrl),
  ],
  plugins: [
    // ...
    [
      copyKatexAssetsPlugin,
      /** @satisfies {CopyKaTeXAssetsPluginOptions} */({ baseUrl }),
    ],
  ],
}
```

## Acknowledgement

This plugin is derived from [docusaurus-copy-plugin](https://github.com/rlamana/docusaurus-plugin-copy). Thanks to [Ramón Lamana (@rlamana)](https://github.com/rlamana) for the original work.
