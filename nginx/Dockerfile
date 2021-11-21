# Getting Base Image
FROM ubuntu:20.04

SHELL ["/bin/bash", "-c"]
# Author Info
MAINTAINER ____easy

RUN apt-get update && apt-get install -y curl gnupg2 ca-certificates lsb-release build-essential git


# install nginx
RUN touch /etc/apt/sources.list.d/nginx.list
RUN echo "deb http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" | tee /etc/apt/sources.list.d/nginx.list
# RUN echo "deb-src http://nginx.org/packages/ubuntu/ precise nginx" >> /etc/apt/sources.list.d/nginx.list
RUN curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add -
RUN apt-get update && apt-get install -y nginx

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# RUN curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -

# lts版のnodeをインストール
RUN apt-get update
RUN . $HOME/.nvm/nvm.sh && \
    nvm install --lts && \
    nvm use --lts && \
    node -v && npm -v && \
    npm i -g yarn

# # nvmの初期化するように.bashrcに書き込む
RUN echo -e "\
export NVM_DIR=\"\$HOME/.nvm\"\n\
[ -s \"\$NVM_DIR/nvm.sh\" ] && \. \"\$NVM_DIR/nvm.sh\"\n\
" >> ~/.bashrc

COPY ./entrypoint.sh /entrypoint.sh


ADD ./conf.d/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "bash" ]
