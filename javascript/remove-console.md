# remove console

Using a babel plugin to remove the `console.log` from production build. (PS: I using vue-cli 3.)

Step 1: install the plugin
```
npm install babel-plugin-transform-remove-console --save-dev
```

Step 2: modify `babel.config.js`
```diff
+ const plugins = []
+ if (process.env.NODE_ENV === 'production') {
+   plugins.push("transform-remove-console")
+ }
  module.exports = {
    presets: [
      '@vue/cli-plugin-babel/preset'
    ],
+   plugins
  }
```

After reading this plugin's docs, I found that it not only can remove `console.log`, but also can remove `console.error` and `console.warn`.
[More detail.](https://www.npmjs.com/package/babel-plugin-transform-remove-console)