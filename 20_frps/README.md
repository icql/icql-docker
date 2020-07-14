# icql/frps

#### 介绍
1. frp作者仓库地址：fatedier/frp https://github.com/fatedier/frp

2. docker-compose使用示例：
    ``` shell
    version: '3.1'

    services:
		frps:
			image: icql/frps:0.33.0
			container_name: icql-frps
			restart: always
			ports:
			- 8200-8299:8200-8299
			volumes:
			- /icql/frps/conf:/conf
			- /icql/frps/log:/log
    ```
