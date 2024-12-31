# dify-check-sandbox-permissions
### 简介
本视频为AI带路党Pro视频[如何在Dify沙盒中安装运行pandas、numpy-深入Dify沙盒原理-Dify深入学习系列2
](https://www.bilibili.com/video/BV1EtBTYHE1y/) 配套代码，介绍如何在Dify工作流中的代码执行节点（Code）运行pandas，并以此为切入点介绍Dify sandbox的原理和如何安装其他包

### 使用方式

需要结合dify源码使用

在dify的docker目录中的docker-compose.yaml文件中，修改sandbox的配置中的volumes配置，确保配置为
```yaml
volumes:
      - ./volumes/sandbox/dependencies:/dependencies
      - ./volumes/sandbox/conf:/conf
```
然后将项目中的conf和dependencies的文件拷贝进入dify->docker->volumes->sandbox目录中

docker compose up启动后，进入docker-sandbox-1容器中，进入/dependencies/code目录中执行
> bash test.sh
将获得的缺少的系统调用拷贝出来，和默认的系统调用合并

默认系统调用
>318,334,307,262,16,8,217,1,3,257,0,202,9,12,10,11,15,25,105,106,102,39,110,186,60,231,234,13,16,24,273,274,334,228,96,35,291,233,230,270,201,14,131,318,56,258,83,41,42,49,50,43,44,45,51,47,52,54,271,63,46,307,55,5,72,138,7,281

类似conf/config.yaml中配置
修改 
> allowed_syscalls: [...合并后的系统调用数组]

最后重启docker compose up即可调用
### 测试代码示例
```shell
curl -X POST http://localhost:8194/v1/sandbox/run -H "X-Api-Key: dify-sandbox" -H "Content-Type: application/json" -d '{"language":"python3","preload":"preload","enable_network":true,"code":"import pandas as pd"}'
```
