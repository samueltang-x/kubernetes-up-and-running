# STAGE 1: Build
FROM golang:1.17-alpine

# Config NPM proxy
RUN npm config set proxy http://www-proxy.ericsson.com:8080
RUN npm config set https-proxy http://www-proxy.ericsson.com:8080

# Install Node and NPM
RUN apk update && apk upgrade && apk add --no-cache git nodejs bash npm

# Get dependencies for Go part of build
RUN go get -u github.com/jteeuwen/go-bindata/...
RUN go get github.com/tools/godep
RUN go get github.com/kubernetes-up-and-running/kuard

WORKDIR /go/src/github.com/kubernetes-up-and-running/kuard

# Copy all sources in
Copy . .

# This is a set of variables that the build script expects
ENV VERBOSE=0
ENV PKG=github.com/kubernetes-up-and-running/kuard
ENV ARCH=amd64
ENV VERSION=test

# Do the build, This script is part of incoming sources.
RUN build/build.sh

CMD [ "/go/bin/kuard" ]
