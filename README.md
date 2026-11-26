# `npm install` fails: @intlify/bundle-utils 11.x esbuild ^0.25 vs Vite 8

Minimal reproduction for intlify/bundle-tools.

`@nuxt/ui` 4.13 together with `@nuxtjs/i18n` 10.7: a clean `npm install` fails with ERESOLVE. `@intlify/bundle-utils` 11.2.8 brings `esbuild ^0.25.4`. npm hoists it to the root, where it conflicts with Vite 8.4's optional peer `esbuild ^0.27.0 || ^0.28.0`.

```sh
npm install
```

Tested locally on node v24.22.3 and npm 12.2.3.

- `@nuxt/ui` `~4.12.2` instead of `^4.13.1`: installs.
- Dropping `@nuxtjs/i18n`: installs.
- Adding `"overrides": { "@intlify/bundle-utils": { "esbuild": "^0.27.0" } }`: installs.
