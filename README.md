# boiler_plate-typescript
without cra, with typescript,react

# CRA없이 typescript 프로젝트를 진행하기 위한 bioler-plate입니다.
## 소스코드
- babel.config.js
```
module.exports = {
  presets: [
    "@babel/preset-react",
    "@babel/preset-env",
    "@babel/preset-typescript",
  ],
};

```

- webpack.cong.js
```
const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require("path");
const webpack = require("webpack");
const prod = process.env.NODE_ENV === "production";

module.exports = {
  mode: prod ? "production" : "development",
  devtool: prod ? "hidden-source-map" : "eval",

  entry: "./src/index.tsx",

  resolve: {
    extensions: [".js", ".jsx", ".ts", ".tsx"],
  },

  module: {
    rules: [
      {
        test: /\.tsx?$/,
        use: ["babel-loader", "ts-loader"],
      },
    ],
  },

  output: {
    path: path.join(__dirname, "/dist"),
    filename: "bundle.js",
  },
  devServer: {
    historyApiFallback: true,
    port: 3000,
    hot: true,
  },

  plugins: [
    new webpack.ProvidePlugin({
      React: "react",
    }),
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
    new webpack.HotModuleReplacementPlugin(),
  ],
};

```

- tsconfig.js
```
{
  "compilerOptions": {
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
    "jsx": "preserve",                                /* Specify what JSX code is generated. */
    "module": "CommonJS",                                /* Specify what module code is generated. */
    // "moduleResolution": "node",                       /* Specify how TypeScript looks up a file from a given module specifier. */
    "baseUrl": "./",                                  /* Specify the base directory to resolve non-relative module names. */
    "allowJs": true,                                  /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */
    "sourceMap": true,                                /* Create source map files for emitted JavaScript files. */
    "outDir": "./",                                   /* Specify an output folder for all emitted files. */
    "isolatedModules": true,                          /* Ensure that each file can be safely transpiled without relying on other imports. */
    "allowSyntheticDefaultImports": true,             /* Allow 'import x from y' when a module doesn't have a default export. */
    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */
    "strict": true,                                      /* Enable all strict type-checking options. */
    "skipLibCheck": true ,                                /* Skip type checking all .d.ts files. */
    "allowUnreachableCode": false                       /* 실행안되는 코드  */                 
  },
  "exclude": ["node_modules"],
  "include": ["src/**/*.ts", "src/**/*.tsx"]
}

```
