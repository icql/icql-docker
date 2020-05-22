FROM node:12-alpine
LABEL maintainer=ICQL

RUN cd / \
    && echo "https://mirrors.ustc.edu.cn/alpine/v3.9/main/" > /etc/apk/repositories  \
    && npm config set registry https://registry.npm.taobao.org \
    && apk add --no-cache git \
    && npm install hexo-cli -g \
    && echo -e "#!/bin/bash\ncp -R /hexo/source /opt/hexo/source && cp -R /hexo/themes /opt/hexo/themes && cp /hexo/_config.yml /opt/hexo/_config.yml && cd /opt/hexo && hexo clean && hexo g && cp -R public /hexo/public && hexo s" > start.sh \
    && echo -e "#!/bin/bash\ncp -R /hexo/source /opt/hexo/source && cp -R /hexo/themes /opt/hexo/themes && cp /hexo/_config.yml /opt/hexo/_config.yml && cd /opt/hexo && hexo clean && hexo g && cp -R public /hexo/public" > generate.sh \
    && chmod +x start.sh \
    && chmod +x generate.sh \
    && mkdir /hexo \
    && mkdir /opt/hexo \
    && cd /opt/hexo \
    && hexo init \
    && npm install hexo-generator-json-content@2.2.0 --save \
    && rm -rf source/ \
    && rm -rf themes/ \
    && rm -rf .gitignore \
    && rm -rf _config.yml

VOLUME /hexo

EXPOSE 4000

ENTRYPOINT ["sh","/start.sh"]