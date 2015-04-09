# PO 翻譯檔維護與管理

## 檔案類型
在 Gettext 的系統下，隨著翻譯工作進行，會見到以下三種檔案

- .po
- .pot
- .mo

.po 是最重要的檔案，翻譯人員的工作就是把翻譯內容加入這個檔案。.pot 其實跟 .po 是一樣的東西，只是用途不同。.pot 是由工程師產生，交給翻譯人員，讓翻譯人員更新手上的 .po 檔。.pot 新的或修改過的項目會被標註在 .po 上，其餘 .po 內容不會被更改。

.mo 檔是用來給機器讀的，通常翻譯編輯器（如 poedit）會自動產生這個檔案。不過我們用不到，可以不理它。

另為，因為專案需求，工程師會把 .po 檔編譯成 .js 檔，讓瀏覽器看得懂。

## 翻譯流程

1. 工程師掃描 html 檔，取出需要翻譯的文字，製作成 .pot 檔，將 .pot 交給翻譯人員
2. 翻譯人員將 .pot 更新進 .po，開始翻譯
3. 翻譯完成後，git push 至 remote repo，並開啟 pull request 供相關人員 review
4. review 完成後 merge
5. 工程師取得新的 .po 檔，將其編譯成 .js 檔

## 版本控制

利用 package.json 裡的 vesion 控制版本。翻譯檔版本號應與對應的專案版本相同。例如

```
project/package.json
{
    "name": "project",
    "version": "2.3.2"
}
```

```
project-translation/package.json
{
    "name": "project-translation",
    "version": "2.3.2"
}
```

並用 git tag 註記版本更新，方便日後 rollback [（註記方法）](https://help.github.com/articles/about-releases/)

## 在專案內載入翻譯檔
在專案的 package.json 內的 depdencies 加入翻譯檔的 git

```
project/package.json
{
    "name": "project",
    "version": "2.3.2",
    "dependencies": {
        "project-translation": "<remote git url>#<commit-ish>"
    }
}
```
其中 `#<commit-ish>` 可視需要加入，可用來指定 git tag
