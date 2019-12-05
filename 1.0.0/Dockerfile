FROM gcr.io/k8s-skaffold/skaffold:v1.0.0

RUN : build dependencies \
    && apt-get update \
    && apt-get install -y python3 python3-pip docker \
    && pip3 install --upgrade pip awscli
