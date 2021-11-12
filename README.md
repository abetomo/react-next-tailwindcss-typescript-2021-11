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

## SSG

Run `next export` to create a static files.

### Example of `scripts` setting in `package.json`

```diff
   "private": true,
   "scripts": {
     "lint": "next lint",
-    "dev": "next dev",
-    "build": "next build",
+    "clean": "rm -rf ./.next",
+    "dev": "npm run clean && next dev",
+    "build": "npm run clean && next build",
+    "export": "npm run build && next export",
     "start": "next start"
   },
   "dependencies": {
```

### `next/image`

You will get the following error.
Fix some files.

```
Error: Image Optimization using Next.js' default loader is not compatible with `next export`.
```

#### `pages/index.tsx`

```diff
 import Head from 'next/head'
-import Image from 'next/image'
+// import Image from 'next/image'
 import styles from '../styles/Home.module.css'

 export default function Home() {
```

```diff
         >
           Powered by{' '}
           <span className={styles.logo}>
-            <Image src="/vercel.svg" alt="Vercel Logo" width={72} height={16} />
+            <img src="/vercel.svg" alt="Vercel Logo" width={72} height={16} />
           </span>
         </a>
       </footer>
```

#### `.eslintrc.json`

```diff
@@ -2,5 +2,8 @@
   "extends": [
     "next/core-web-vitals",
     "plugin:tailwindcss/recommended"
-  ]
+  ],
+  "rules": {
+    "@next/next/no-img-element": "off"
+  }
 }
```

Fixed for the following warning.

```
Warning: Do not use <img>. Use Image from 'next/image' instead. See https://nextjs.org/docs/messages/no-img-element.  @next/next/no-img-element
```

### Note

In Node.js 17, the following error.

```
HookWebpackError: error:0308010C:digital envelope routines::unsupported
```

(It was tested with Node.js 16.)

## links

* https://tailwindcss.com/docs/guides/nextjs
