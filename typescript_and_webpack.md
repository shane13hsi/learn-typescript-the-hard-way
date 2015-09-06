# TypeScript and webpack

---

## Getting Started

```sh
npm install -g typescript
```

```js
function greet(name: string) {  
  return 'Hello '+name;
}

export = greet;  
```

```js
import greeter = require('./greeter');  
import $ = require('jquery');

$(() => {
  $(document.body).html(greeter("World"));
});
```

```sh
tsc --module commonjs app.ts  
```

```sh
npm install -g tsd  
tsd install jquery --save  
tsc --module commonjs typings/tsd.d.ts  
```

tsconfig.json

```json
{
  "compilerOptions": {
    "module": "commonjs"
  },
  "files": [
    "app.ts",
    "typings/tsd.d.ts"
  ]
}

```

Then:

```
tsc
```


## Webpack

```sh
npm install -g webpack  
npm install ts-loader --save
```

```js
module.exports = {  
  entry: './app.ts',
  output: {
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['', '.webpack.js', '.web.js', '.ts', '.js']
  },
  module: {
    loaders: [
      { test: /\.ts$/, loader: 'ts-loader' }
    ]
  }
}
```

We need to install jquery (again) as npm dependencies.

```
npm install jquery --save  
webpack
```

## Sourcemaps

```js
var webpack = require('webpack');  
module.exports = {  
  entry: './app.ts',
  output: {
    filename: 'bundle.js'
  },
  // Turn on sourcemaps
  devtool: 'source-map',
  resolve: {
    extensions: ['', '.webpack.js', '.web.js', '.ts', '.js']
  },
  // Add minification
  plugins: [
    new webpack.optimize.UglifyJsPlugin()
  ],
  module: {
    loaders: [
      { test: /\.ts$/, loader: 'ts' }
    ]
  }
}
```

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "sourceMap": true
  },
  "files": [
    ...
  ]
}
```