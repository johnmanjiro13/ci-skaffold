FROM alpine:latest

ENV K8S_VERSION=1.14.6
ENV RELEASE_VERSION=2019-08-22
ENV SKAFFOLD_VERSION=v1.0.0

RUN : build dependencies \
    && apk --update --no-cache add ca-certificates python3 git \
    && apk --no-cache add --virtual build-dependencies curl openssl \
    && pip3 install --upgrade pip awscli \
    && : kubectl for eks \
    && curl -O https://amazon-eks.s3-us-west-2.amazonaws.com/$K8S_VERSION/$RELEASE_VERSION/bin/linux/amd64/kubectl \
    && curl -O https://amazon-eks.s3-us-west-2.amazonaws.com/$K8S_VERSION/$RELEASE_VERSION/bin/linux/amd64/kubectl.sha256 \
    && openssl sha1 -sha256 kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl \
    && rm -rf kubectl.sha256 \
    && : iam-authenticator \
    && curl -O https://amazon-eks.s3-us-west-2.amazonaws.com/$K8S_VERSION/$RELEASE_VERSION/bin/linux/amd64/aws-iam-authenticator \
    && curl -O https://amazon-eks.s3-us-west-2.amazonaws.com/$K8S_VERSION/$RELEASE_VERSION/bin/linux/amd64/aws-iam-authenticator.sha256 \
    && openssl sha1 -sha256 aws-iam-authenticator \
    && chmod +x aws-iam-authenticator \
    && mv aws-iam-authenticator /usr/local/bin \
    && rm -rf aws-iam-authenticator.sha256 \
    && : install skaffold \
    && curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/$SKAFFOLD_VERSION/skaffold-linux-amd64 \
    && chmod +x skaffold \
    && mv skaffold /usr/local/bin \
    && apk del build-dependencies
