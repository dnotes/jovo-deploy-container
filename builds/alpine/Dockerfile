FROM gcr.io/google.com/cloudsdktool/cloud-sdk:alpine as gcloud

FROM node:14-alpine

RUN apk update && apk upgrade && \
    apk add --no-cache \
      curl \
      python3 \
      py3-crcmod \
      py3-openssl \
      bash \
      libc6-compat \
      openssh-client \
      git \
      gnupg \
      make \
    && \
    wget -c https://dl.google.com/gactions/v3/release/gactions-sdk_linux.tar.gz -O - | tar -xz -C /usr/local/bin --strip-components 1 && \
    chmod +x /usr/local/bin/gactions && \
    npm config set unsafe-perm true && \
    npm install -g ask-cli jovo-cli

COPY --from=gcloud /google-cloud-sdk /google-cloud-sdk

RUN mkdir /app && \
    chown node:node /app

USER node

WORKDIR /app

ENV PATH="$PATH:/google-cloud-sdk/bin"

CMD "/bin/bash"