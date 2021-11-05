# react-next-tailwindcss-typescript-2021-11

## Creating project

```
% npx create-next-app --typescript example
Need to install the following packages:
  create-next-app
Ok to proceed? (y)
...
```

```
% cd example
```

## Setting up Tailwind CSS

(In example directory.)

```
% npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

```
% npx tailwindcss init -p

Created Tailwind CSS config file: tailwind.config.js
Created PostCSS config file: postcss.config.js
```

### `tailwind.config.js`

```diff
 module.exports = {
-  purge: [],
+  mode: 'jit', // https://tailwindcss.com/docs/just-in-time-mode
+  purge: [
+    './pages/**/*.{js,ts,jsx,tsx}',
+    './components/**/*.{js,ts,jsx,tsx}'
+  ],
   darkMode: false, // or 'media' or 'class'
   theme: {
     extend: {},
```

### `pages/_app.tsx`

```diff
-import '../styles/globals.css'
+import 'tailwindcss/tailwind.css'
 import type { AppProps } from 'next/app'

 function MyApp({ Component, pageProps }: AppProps) {
```

```
% rm styles/globals.css
```
## Lint

```
% npx next lint
```

(I just ran it and it was set from the beginning, so it may not be necessary.)

~~The first time you run it, it will install eslint and other pakcage.~~

~~I think it is better to set it in `scripts` in `package.json`.~~

```diff
   "version": "0.1.0",
   "private": true,
   "scripts": {
+    "lint": "next lint",
     "dev": "next dev",
     "build": "next build",
     "start": "next start"
```

### `eslint-plugin-tailwindcss`

```
% npm install -D eslint-plugin-tailwindcss
```

Update `.eslintrc.json`.

```diff
 {
-  "extends": "next/core-web-vitals"
+  "extends": [
+    "next/core-web-vitals",
+    "plugin:tailwindcss/recommended"
+  ]
 }
 ```

## links

* https://tailwindcss.com/docs/guides/nextjs
