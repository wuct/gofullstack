# Deploy to AWS Elastic Beanstalk

## Deploy 流程
### 安裝 AWS Elastic Beanstalk Command Line Tool
1. [下載 AWS EB CLI](http://aws.amazon.com/code/6752709412171743)
2. 解壓縮下載的 .zip 檔後，把資料夾搬到你喜歡的地方
3. 所有的 eb 檔都在 eb 資料夾內，把適合的 eb 檔加到路徑

```
export PATH=$PATH:<path to eb>

# 例如我的是 macosx/python2.7

export PATH=$PATH:~/AWS-ElasticBeanstalk-CLI-2.6.4/eb/macosx/python2.7/

# 確認是否成功

eb --help
```

### EB 指令
1. 初次設定 `eb init`
2. 創造 enviromet `eb create`
3. 部署 `eb deploy`，這指令會花數分鐘開啟實體機器



## 如何自定 nginx.conf
因為 AWS EB 一直改版，需實機測試可行性

### 方法 1
根據 AWS 官方文件，在 __.ebextensions/__ 資料夾內加入 .config 檔，直接撰寫 nginx config。

參考資料：[http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_nodejs_custom_container.html]()

#### 範例

```
files:
  /etc/nginx/conf.d/gzip.conf:
    content: |
      gzip_types application/json;
```

### 方法 2
如果方法 1 會和 eb 預設的 nginx config 衝突，可在 __.ebextensions/__ 資料夾內加入 .config 檔改寫預設的 nginx.config 檔。

參考資料: [http://finik.net/2014/10/29/Beanstalk/]()

#### 範例
```
files:
  "/tmp/deployment/config/#etc#nginx#conf.d#00_elastic_beanstalk_proxy.conf" :
    mode: "000755"
    owner: root
    group: root
    content: |
        server {

        }
```

### 方法 3
官方文件雖然沒有紀錄，但有人發現 eb 在 depoly 後會執行所有 __/opt/elasticbeanstalk/hooks/appdeploy/post__  資料夾裡的 script，所以可以寫一支 script 改寫預設的 nginx.cong 並 reload nginx。

#### 範例
```
commands:
    create_post_dir:
        command: "mkdir /opt/elasticbeanstalk/hooks/appdeploy/post"
        ignoreErrors: true
files:
    "/etc/nginx/conf.d/00_elastic_beanstalk_proxy.conf.custom" :
        mode: "000755"
        owner: root
        group: root
        content: |
            server {

            }
    "/opt/elasticbeanstalk/hooks/appdeploy/post/99_restart_delayed_job.sh":
        mode: "000755"
        owner: root
        group: root
        content: |
            mv /etc/nginx/conf.d/00_elastic_beanstalk_proxy.conf.custom /etc/nginx/conf.d/00_elastic_beanstalk_proxy.conf
            /usr/sbin/nginx -s reload
```

## 其他問題
### 1. 是否有 cluster？若有 cluster code 要如何調整
（待實機測試）

有，不需要調整

參考文件：[http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_nodejs_express_elasticache.html]()

### 2. 要如何取得 private npm resgisty 的 node modules？
（待實機測試）把 EB deploy 在 VPC 內。

### 3. EB 目前支援 node 版本？
目前支援版本有
- 0.8.26
- 0.8.28
- 0.10.21
- 0.10.26
- 0.10.31
- 0.12.0


