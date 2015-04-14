# Pre-Commit Hook

## 目的
在我們 local 電腦上每次 commit 前，必須執行 test、 lint 和 code style check。

## 摘要
我們利用 [pre-commit](https://www.npmjs.com/package/pre-commit) 將 commit 前要執行的 tasks 寫入 npm scripts。

## 詳細方法

### 安裝 pre-commit
```
npm install --save-dev pre-commit
```
安裝後會在 .git/hooks 資料夾裡新增一個 pre-commit 檔。舊的 pre-commit 檔（如果有的話），會更名為 pre-commit.old 當作備份。

### 設定 package.json
pre-commit 預設會在每次 `git commit` 前都先跑 `npm test`，如果 `exit 0` 才執行 `git commit`。package.json 預設的 test script 是 `exit 1`，我們修改它讓他 `exit 0` 假裝有通過測試。

```
{
  "scripts": {
    "test": "echo \" 假裝有 test \" && exit 0"
  }
}
```


如果除了 test 還要執行其他 tasks，可以加入 `"pre-commit"` 到 package.json。例如下面這串設定就是讓 pre-commit 依序執行 `lint`、`jscs`、`test`，都通過才執行 `git commit`。

```
{
  "scripts": {
    "test": "echo \" 假裝有 test \" && exit 0",
    "lint": "echo \" 假裝有 lint \" && exit 0",
    "jscs": "echo \" 假裝有 check code style \" && exit 0"
  },
  "pre-commit": [
    "lint",
    "jscs",
    "test
  ]
}
```

## 結果
我們的 code 愈來愈漂亮。

## 參考資料
- [http://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks]()
- [https://www.npmjs.com/package/pre-commit]()





