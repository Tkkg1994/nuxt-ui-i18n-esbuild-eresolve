# `npm install` fails on npm 12: @intlify/bundle-utils 11.x esbuild ^0.25 vs Vite 8

Minimal reproduction for intlify/bundle-tools.

`@nuxt/ui` 4.13 together with `@nuxtjs/i18n` 10.7: a clean `npm install` with npm 12 fails with ERESOLVE. `@intlify/bundle-utils` 11.2.8 brings `esbuild ^0.25.4`. npm 12 puts that copy at the root, where it conflicts with Vite 8.4's optional peer `esbuild ^0.27.0 || ^0.28.0`.

Open in StackBlitz: https://stackblitz.com/github/Tkkg1994/nuxt-ui-i18n-esbuild-eresolve. Its terminal runs `npx -y npm@12.2.3 install` on start and ends in the ERESOLVE.

```sh
npx -y npm@12.2.3 install
```

| Setup | Result |
|---|---|
| npm 12.2.3 (local, node v24.22.3, and in StackBlitz) | ERESOLVE |
| npm 10.8.2 (local and StackBlitz's own npm) | installs; npm puts esbuild 0.28.2 at the root and nests bundle-utils' 0.25.12 |
| npm 12, `@nuxt/ui` `~4.12.2` instead of `^4.13.1` | installs |
| npm 12, without `@nuxtjs/i18n` | installs |
| npm 12, `"overrides": { "@intlify/bundle-utils": { "esbuild": "^0.27.0" } }` | installs |
