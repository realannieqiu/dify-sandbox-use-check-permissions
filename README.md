# dify-check-sandbox-permissions
## 简介
本视频为AI带路党Pro视频配套代码，介绍如何在Dify工作流中的代码执行节点（Code）运行pandas，并以此为切入点介绍Dify sandbox的原理

```shell
curl -X POST http://localhost:8194/v1/sandbox/run -H "X-Api-Key: dify-sandbox" -H "Content-Type: application/json" -d '{"language":"python3","preload":"preload","enable_network":true,"code":"import pandas as pd"}'
```