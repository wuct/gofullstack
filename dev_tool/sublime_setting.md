# Sublime 開發 React 環境設定

## 版本
Sublime Text 3

[免費下載](http://www.sublimetext.com/3)


## 套件設定

### Emmet (a.k.a ZenCoding)

#### 目標

1. Using Emmet in `.jsx` files
2. Using `className` instead of `class` in `.jsx` files
3. type `div.myClass` then press **tab** button, Sublime will return `<div className="myClass"></div>`

#### 安裝

1. Install Sublime Text plugin **RegReplace** and **Chain Of Command**
2. Add following code in your `KeyBinding – Users. Default (OSX).sublime-keymap` in Preference

    ```
    [{
      "keys": ["tab"],
      "command": "chain",
      "args": {
          "commands": [
            ["expand_abbreviation_by_tab"],
            ["reg_replace", {"replacements": ["js_class"]}]
          ]
        },
      "context": [
        {
          "operand": "source.js",
          "operator": "equal",
          "match_all": true,
          "key": "selector"
        },
      ]
    }]
    ```

3. Add following code in your `reg_replace.sublime-settings` in Preference > Packages Setting

    ```json
    {
      "replacements": {
          "js_class": {
              "find": " class=\"",
              "replace": " className=\"",
              "greedy": true,
              "case": false
          }
      }
    }
    ```

#### 注意

安裝完成後，在文件內任何地方按下 `tab`，都會把 `class="` 轉換成 `className="`。編輯傳統 htmls 可以先 package disable > **RegPlace**，避免觸發這個轉換。

### esLint


1. Create a file called `.eslintrc` to the root of the project.

    ```
    {
      "parser": "babel-eslint",
      "env": {
        "browser": true,
        "node": true
      },
      "rules": {
        "quotes": [1, "single"],
        "strict": 0,
        "no-underscore-dangle": 0,
        "no-unused-vars": 0,
        "no-multi-spaces": 0,
        "key-spacing": 0,
        "no-return-assign": 0,
        "consistent-return": 0,
        "no-shadow": 0,
        "no-comma-dangle": 0,
        "no-use-before-define": 0,
        "no-empty": 0,
        "new-parens": 0,
        "no-cond-assign": 0,
        "new-cap": true
      }
    }
    ```

2. `npm install -g eslint babel-eslint`
    Or, install them locally if your Sublime can't find them
    `npm install --save-dev eslint babel-eslint`
3. Install `SublimeLinter` and `SublimeLinter-contrib-eslint` package via Package Control.
4. Remove (or disable) any other JavaScript linter for SublimeLinter, for example: `SublimeLinter-jshint`.
5. Install `babel-sublime` and remove other JSX-specific plugins (ex: `sublime-react`) if you have.
6. Tell Sublime to use `JavaScript (Babel)` syntax for all `.js` and `.jsx` files.
7. Open SublimeLinter > Setting - User, add the following line into `syntax_map`
	```
	"syntax_map" {
	    "javascript (babel)": "javascript"
	}
	```
Also add the path to the node bin in `paths` if your sublime can not find it.
```
    "paths": {
        "linux": [],
        "osx": [
            "/path/to/your/node/bin"
        ],
        "windows": []
    }
```

babel-eslint still have some bugs:

- Variable is not defined when used in JSX as a parameter [#15](https://github.com/babel/babel-eslint/issues/15)


(參考資料: [Link Like It's 2015](https://medium.com/@dan_abramov/lint-like-it-s-2015-6987d44c5b48))

### jscs

1. Create a file called `.jscsrc` to the root of the project.

    ```
    {
      "preset": "airbnb",
      "esprima" : "esprima-fb",
      "excludeFiles": ["node_modules/**", "build/**"]
    }
    ```

2. `npm install -g jscs esprima-fb`
    Or, install them locally if your Sublime can't find them
    `npm install --save-dev jscs esprima-fb`
3. Install `SublimeLinter` via Package Control if you have not installed it, yet.
4. Follow the 7th step in **esLint** to set SublimeLinter.
5. Install `SublimeLinter-jscs`. Done!

### jsxHint (不推薦)

不推薦原因：jsxHint 作者自己也推 eslint

1. npm install -g jsxhint
2. In Package Control, install [babel-sublime](https://github.com/babel/babel-sublime)

	- Find it as _Babel_ through Package Control
	- see the doc to setup syntax highlight

3. In Package Control, install [SublimeLinter 3](http://sublimelinter.readthedocs.org/en/latest/installation.html)

	- Find it as _SublimeLinter_ through Package Control

4. In Package Control, install [SublimeLinter-jsxhint](https://github.com/SublimeLinter/SublimeLinter-jsxhint)
5. In Package Control, Open Preferences > Package Settings > SublimeLinter > Setting - User

	- add jsxhint `path` to `paths` array, it would be something looks like
	```
	"paths": {
			"linux": [],
			"osx": [
					"/Users/mtk10835/.nvm/v0.10.32/bin"
			],
			"windows": []
	},
	```
	- you can use the command `which jsxhint` in terminal to find the `path`

6. Restart your Sublime Text and enjoy!

