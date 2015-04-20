# AWS Elastic Beanstalk

## Components

### Application
包含所有東西，其實就是資料夾

### Application Version
Application 可以有版控，每個版本都會壓成一包放在 S3，方便隨時切換版本

### Enviroment
Enviroment 部署在 AWS 資源上的某個 Application Version。一個 Enviroment 只能跑一個 Version。

### Enviroment Configuration
就是 Enviroment 的 config。更新 config 有可能視需要直接更新至目前使用的 AWS 資源，或是刪除舊的並開新的 AWS 資源。

### Configuration Template
在開啟新 Enviroment，可以先選擇 config 模板。config 模板只能透過 eb cli 或是 api 建立與更新。



