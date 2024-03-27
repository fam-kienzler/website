# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.137.0/containers/go/.devcontainer/base.Dockerfile
ARG VARIANT="1"
FROM mcr.microsoft.com/vscode/devcontainers/go:0-${VARIANT}

# Install HUGO
ENV H_VERSION "0.121.1"
RUN mkdir -p /usr/local/src
RUN  \
    arch=$(uname -m); \
    if [[ $arch == aarch64 ]]; then \
    cd /usr/local/src && curl -L https://github.com/gohugoio/hugo/releases/download/v${H_VERSION}/hugo_extended_${H_VERSION}_linux-arm64.tar.gz | tar -xz; \
    else \
    cd /usr/local/src && curl -L https://github.com/gohugoio/hugo/releases/download/v${H_VERSION}/hugo_extended_${H_VERSION}_linux-64bit.tar.gz | tar -xz; \
    fi;
RUN cp /usr/local/src/hugo /usr/local/bin/hugo


# Install Node.JS and VPM
RUN apt install -y ca-certificates curl gnupg
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
ENV NODE_MAJOR 20

RUN echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
RUN apt update -y
RUN apt install -y nodejs build-essential

# Install npm modules required for theme
RUN npm install postcss-cli tailwindcss autoprefixer

EXPOSE 1313
