# Web Server Deploy

## 軟體版本
| 軟體 | 版本 |
| -- | -- |
| node | 0.10.32 |
| nginx | 1.6.2 |
| git | 2.3.x |



## 部署步驟

### 安裝 git
1. 安裝 [git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
2. `git --version` 檢查是否成功


### 安裝 Node

1. 安裝 [nvm](https://github.com/creationix/nvm)
2. 執行下列指令

    ```
    nvm install 0.10.32         # install node
    nvm use 0.10.32
    nvm alias default 0.10.32   # 預設使用這個版本
    node -v                     # 檢查是否回傳 v0.10.32
    ```

### 安裝 Nginx

1. 安裝 [nginx](http://nginx.org/en/docs/install.html)
2. 檢查版版本

    ```
    nginx -v    # nginx version: nginx/1.6.2
    ```


### 載入 source code

```
git clone <node server code>
cd /path/to/node/server/ && npm install

git clone <nginx config files>
# then copy nginx.config files to nginx folder

git clone <other static files repo>
```

### 啟動
```
cd /path/to/node/server/ && npm run start # 啟動 node server
nginx                                     # 啟動 nginx
```

### CDN 設定
(TBD)
1. 用 CloudFront 還是 CloudFlare?
2. 靜態檔案由 S3 提供還是 nginx 提供？


## 參考資料

