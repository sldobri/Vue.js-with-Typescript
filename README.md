# my-app

> A Vue.js project

## Build Setup

```
vue init webpack my-app # or: vue init pwa my-app
cd my-app
We have to do 4 steps:
```
1. Create a tsconfig.json file
Let’s start with something very simple, later we’ll get back to the TypeScript configuration.
```
{
  "compilerOptions": {
    "lib": ["dom", "es5", "es2015"],
    "target": "es5",
    "module": "es2015",
    "moduleResolution": "node",
    "sourceMap": true,
    "allowSyntheticDefaultImports": true
  }
}
```
The most important part is the allowSyntheticDefaultImports setting. Since Vue types doesn’t use ES2015 default exports, this setting must be set to by-pass that. You can see more info in this VSCode docs page.

Setting "module": "es2015" would make the code tree-shakeable by producing ESM (EcmaScript Modules).

2. Add ts-loader and webpack tweaks
```
Install typescript an ts-loader with npm:

npm i -D typescript ts-loader
```
Then open build/webpack.base.conf.js, and place the following code at the beginning of module.rules, right before than vue-loader:
```
module: {
    rules: [
      {
        test: /\.ts$/,
        exclude: /node_modules|vue\/src/,
        loader: "ts-loader",
        options: {
          appendTsSuffixTo: [/\.vue$/]
        }
      },
    ...
```
In there, rename the entry to .ts and add it to the extensions:
```
...
entry: {
  app: './src/main.ts'
},
...
resolve: {
    extensions: ['.ts', '.js', '.vue', '.json'],
...
```
3. Add es-module: true to build/vue-loader.conf.js
That will tell vue-loader to use ES instead of CJS (CommonJS) modules, as describe in vue-loader docs:
```
module.exports = {
  loaders: utils.cssLoaders({
    sourceMap: isProduction
      ? config.build.productionSourceMap
      : config.dev.cssSourceMap,
    extract: isProduction
  }),
  esModule: true
}
```
4. Use TypeScript in files
So you must do 2 things here:

Rename .js to .ts extensions within the src folder
Use lang="ts" on the script tag of you Vue file. For example in App.vue:
```
<script lang="ts">
export default {
  name: 'app'
}
</script>
```
Troubleshooting
If your editor is yelling at the line import App from './App' in main.js file about not finding the App module, you can add a vue-shim.d.ts file to your project with the following content:
```
declare module "*.vue" {
  import Vue from 'vue'
  export default Vue
}
```

