# dify-check-sandbox-permissions
### How to use

You need to use it with the dify source code.

In the docker-compose.yaml file in the docker directory of dify, modify the volumes configuration in the configuration of sandbox as
```yaml
volumes.
      - . /volumes/sandbox/dependencies:/dependencies
      - . /volumes/sandbox/conf:/conf
```
Then copy the conf and dependencies files from this project into the dify->docker->volumes->sandbox directory

After docker compose up starts, go into the docker-sandbox-1 container and go into the /dependencies/code directory and execute
> bash test.sh
Copy the missing syscalls you get and merge them with the default ones

Default system calls
>318,334,307,262,16,8,217,1,3,257,0,202,9,12,10,11,15,25,105,106,102,39,110,186,60,231,234,13,16,24,273,274,334,228,96,35,291,233, 230,270,201,14,131,318,56,258,83,41,42,49,50,43,44,45,51,47,52,54,271,63,46,307,55,5,72,138,7,281

Similar to the configuration in conf/config.yaml
Modify 
> allowed_syscalls: [... Merged syscalls array]

Finally, restart docker compose up to make the calls.
### Sample test code
```shell
curl -X POST http://localhost:8194/v1/sandbox/run -H “X-Api-Key: dify-sandbox” -H “Content-Type: application/json” -d '{“language”: “python3”, “preload”: “preload”. “preload": ‘preload’, ‘enable_network’:true, ‘code’: ‘import pandas as pd’}'
```
