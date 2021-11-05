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

## links

* https://tailwindcss.com/docs/guides/nextjs
