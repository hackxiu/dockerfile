FROM alpine:3.8

LABEL maintainer="mritd <mritd1234@gmail.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}
ENV V2RAY_VERSION v3.29 
ENV V2RAY_LOG_DIR /var/log/v2ray
ENV V2RAY_CONFIG_DIR /etc/v2ray/
ENV V2RAY_DOWNLOAD_URL https://github.com/v2ray/v2ray-core/releases/download/${V2RAY_VERSION}/v2ray-linux-64.zip

RUN sudo apt-get install bash tzdata curl -y \
    && mkdir -p \ 
        ${V2RAY_LOG_DIR} \
        ${V2RAY_CONFIG_DIR} \
        /tmp/v2ray \
    && sudo curl -L -H "Cache-Control: no-cache" -o /tmp/v2ray/v2ray.zip ${V2RAY_DOWNLOAD_URL} \
    && sudo unzip /tmp/v2ray/v2ray.zip -d /tmp/v2ray/ \
    && sudo mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/v2ray /usr/bin \
    && sudo mv /tmp/v2ray/v2ray-${V2RAY_VERSION}-linux-64/vpoint_vmess_freedom.json /etc/v2ray/config.json \
    && sudo chmod +x /usr/bin/v2ray \
    && sudo del curl \
    && sudo ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && sudo echo ${TZ} > /etc/timezone \
    && sudo rm -rf /tmp/v2ray /var/cache/apk/*

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
