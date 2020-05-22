# icql/hexo

### hexo容器镜像
#### 使用说明
``` bash
# 挂载容器内部 /hexo 目录，只需要挂载 hexo 的以下3个文件/文件夹
|-hexo
    |-source/*
    |-themes/*
    |-_config.yml

# 启动
docker run -it -p 4000:4000 -v /root/hexo:/hexo  --name hexo-test icql/hexo:0.2.0 /bin/bash
```