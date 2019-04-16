FROM centos:latest

ARG GOLANG_VERSION=1.12.2

LABEL mantainer="Gabriele Vassallo <gabri.vassallo01@gmail.com>" \
      summary="Golang base container image based on CentOS"

# install base packages.
RUN INSTALL_PKGS="git" \
    && yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS \
    && rm -rf /var/cache/yum/* \
    && yum clean all

RUN cd /tmp \
    && GOLANG_TARBAL="https://dl.google.com/go/go${GOLANG_VERSION}.linux-amd64.tar.gz" \
    && curl -s -L -o golang.tar.gz "$GOLANG_TARBAL" \
    && tar -xzf golang.tar.gz \
    && mv go /usr/local \
    && rm -rf /tmp/go*

ENV GOROOT=/usr/local/go
ENV GOPATH=/go
ENV PATH=$GOROOT/bin:$GOPATH/bin:$PATH

RUN GOLANG_DEP="https://github.com/golang/dep/releases/download/v0.5.0/dep-linux-amd64" \
    && curl -s -L -o /usr/bin/dep $GOLANG_DEP  \
    && chmod +x /usr/bin/dep

WORKDIR $GOPATH/src

ENTRYPOINT ["sh", "-c"]
