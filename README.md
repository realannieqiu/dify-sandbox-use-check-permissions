# dify-check-sandbox-permissions
### 简介
本视频为AI带路党Pro视频配套代码，介绍如何在Dify工作流中的代码执行节点（Code）运行pandas，并以此为切入点介绍Dify sandbox的原理

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

### 测试代码
```shell
curl -X POST http://localhost:8194/v1/sandbox/run -H "X-Api-Key: dify-sandbox" -H "Content-Type: application/json" -d '{"language":"python3","preload":"preload","enable_network":true,"code":"import pandas as pd"}'
```
