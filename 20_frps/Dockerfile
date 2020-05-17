FROM alpine:3.10.2
LABEL maintainer=ICQL

ENV TZ=Asia/Shanghai
ENV FRP_VERSION 0.33.0

RUN apk add --update tzdata \
    && wget https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz \
    && tar -xf frp_${FRP_VERSION}_linux_amd64.tar.gz \
    && mkdir /frps \
    && cp frp_${FRP_VERSION}_linux_amd64/frps* /frps/ \
    && rm -rf frp_${FRP_VERSION}_linux_amd64* \
    && rm -rf /var/cache/apk/* \
    && mkdir /conf \
    && mkdir /log

VOLUME /conf \
       /log

WORKDIR /frps
ENTRYPOINT ["./frps","-c","/conf/frps.ini"]