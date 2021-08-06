FROM golang:alpine

MAINTAINER "Renjith Menon<renjith.menon@gmail.com>"



ENV TERRAFORM_VERSION=1.0.3
ENV TERRAGRUNT_VERSION=0.31.3

RUN apk add --update git bash openssh curl

ENV TF_DEV=true
ENV TF_RELEASE=true

WORKDIR $GOPATH/src/github.com/hashicorp/terraform
RUN git clone https://github.com/hashicorp/terraform.git ./ && \
    git checkout v${TERRAFORM_VERSION} && \
    /bin/bash scripts/build.sh

RUN curl -sL https://github.com/gruntwork-io/terragrunt/releases/download/v$TERRAGRUNT_VERSION/terragrunt_linux_386 \
  -o /bin/terragrunt && chmod +x /bin/terragrunt

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.1/bin/linux/amd64/kubectl
RUN chmod u+x kubectl && mv kubectl /bin/kubectl


RUN \
  apk update && \
  apk add bash py-pip && \
  apk add --virtual=build gcc libffi-dev musl-dev openssl-dev python3-dev make && \
  pip --no-cache-dir install -U pip && \
  pip --no-cache-dir install azure-cli && \
  apk del --purge build

WORKDIR /root

#ENTRYPOINT ["terraform"]

