FROM node:12-alpine
LABEL maintainer=ICQL

RUN cd / \
    && echo "https://mirrors.ustc.edu.cn/alpine/v3.9/main/" > /etc/apk/repositories  \
    && npm config set registry https://registry.npm.taobao.org \
    && apk add --no-cache git \
    && npm install hexo-cli -g \
    && npm install gulp -g \
    && echo -e "#!/bin/bash\ncp -R /hexo/source /opt/hexo/source && cp -R /hexo/themes /opt/hexo/themes && cp /hexo/_config.yml /opt/hexo/_config.yml && cd /opt/hexo && hexo clean && hexo g && gulp && cp -R public /hexo/public && hexo s" > start.sh \
    && echo -e "#!/bin/bash\ncp -R /hexo/source /opt/hexo/source && cp -R /hexo/themes /opt/hexo/themes && cp /hexo/_config.yml /opt/hexo/_config.yml && cd /opt/hexo && hexo clean && hexo g && gulp && cp -R public /hexo/public" > generate.sh \
    && chmod +x start.sh \
    && chmod +x generate.sh \
    && mkdir /hexo \
    && mkdir /opt/hexo \
    && cd /opt/hexo \
    && hexo init \
    && npm install gulp --save \
    && npm install hexo-generator-json-content@2.2.0 --save \
    && npm install gulp-uglify gulp-cssmin gulp-htmlmin gulp-rev-append --save \
    && rm -rf source/ \
    && rm -rf themes/ \
    && rm -rf .gitignore \
    && rm -rf _config.yml \
    && echo -e "var gulp = require('gulp'),\n\
                     uglify = require('gulp-uglify'),\n\
                     cssmin = require('gulp-cssmin'),\n\
                     htmlmin = require('gulp-htmlmin'),\n\
                     rev = require('gulp-rev-append');\n\
                 //注册默认任务\n\
                 gulp.task('default', async () => {\n\
                     //压缩js\n\
                     gulp.src('./public/**/*.js')\n\
                         .pipe(uglify())\n\
                         .pipe(gulp.dest('./public'));\n\
                     //压缩css\n\
                     gulp.src('./public/**/*.css')\n\
                         .pipe(cssmin())\n\
                         .pipe(gulp.dest('./public'));\n\
                     //压缩html\n\
                     gulp.src('./public/**/*.html')\n\
                         .pipe(htmlmin({\n\
                             removeComments: true,\n\
                             collapseWhitespace: true,\n\
                             minfyJS: true,\n\
                             minfyCss: true,\n\
                         }))\n\
                         .pipe(gulp.dest('./public'));\n\
                     //版本号\n\
                     gulp.src('./public/**/*.html')\n\
                         .pipe(rev())\n\
                         .pipe(gulp.dest('./public'));\n\
                 });" > gulpfile.js

VOLUME /hexo

EXPOSE 4000

ENTRYPOINT ["sh","/start.sh"]