# Webpack

所有的 sample code [在 Github 這](https://github.com/wuct/webpack-examples)，每一步驟對應一個資料夾

## To Install
`npm install`

# 1. Getting Started

1. try `webpack ./entry.js ./bundle.js` in your terminal.
2. see `webpack.config.js`, then try `webpack` in your terminal.


# 2. Babel Loader

We use `babel-loader` to compile ES6 and .jsx files to ES5 files.

See `webpack.config.js`, then try `webpack` in your terminal.


# 3. webpack-dev-server

We use `webpack-dev-server` to serve static files to a browser.

Try `webpack-dev-server` in your terminal, then go to `http://localhost:8080/`

You can also add some colors by add `--colors`.

## Source Map

We also use `sourcemap` to map `bundle.js` to our source code. It let us debug our code easily.

Comment out `devtool` in the `webpack.config.js` then see how it works.

## Hot Mode
By turning on the hot mode, you will be able to get live reload when doing changes to your files.

The easiest way to do this is use add `--inline --hot` to your command.

For example,
```
webpack-dev-server --colors --inline --hot
```
## 進階用法

Allow instantaneous live refresh without losing state while editing React components.

- [React Hot](http://gaearon.github.io/react-hot-loader/getstarted/)

## 參考資料
- [http://webpack.github.io/docs/webpack-dev-server.html]()


# 4. Webpack with Node
We combine a webpack-dev-server with a node server.

The node server provide the `index.html` on port `3000`, while the webpack-dev-server provide the `bundle.js` on port `8080`.

See `package.json` to know how we set this up, then try `npm run watch` in your terminal. Finally, go to `http://localhost:3000` to see the result.

Both servers will reload lively when you edit a file.

## Tips

We can configure `webpack-dev-server` to proxy all requests other than assets to our node.js server, so now the entry point is just at port `8080`. See http://git.io/vUD1i

# 5. Webpack in Backend

We want to use an old version of node but write ES6. We also want to reload the node sever lively.

Here is how we do.

1. Use `webpack.server.config.js` to setup webpack for the backend. Do not forget to make `node_moduled` as external. For more info [http://jlongster.com/Backend-Apps-with-Webpack--Part-I]().

2. Setup `package.json` to run `webpack --config webpack.server.config.js` before `npm run start`
