FROM golang:1.13-buster as golang

RUN go get -u -v github.com/mdempsky/gocode
RUN go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs
RUN go get -u -v github.com/ramya-rao-a/go-outline
RUN go get -u -v github.com/acroca/go-symbols
RUN go get -u -v golang.org/x/tools/cmd/godoc
RUN go get -u -v github.com/zmb3/gogetdoc
RUN go get -u -v golang.org/x/tools/cmd/guru
RUN go get -u -v golang.org/x/tools/cmd/gorename
RUN go get -u -v github.com/go-delve/delve/cmd/dlv
RUN go get -u -v github.com/stamblerre/gocode
RUN go get -u -v github.com/rogpeppe/godef
RUN go get -u -v github.com/sqs/goreturns
RUN go get -u -v golang.org/x/lint/golint
RUN go get -u -v github.com/go-delve/delve/cmd/dlv
RUN go get -u -v github.com/sourcegraph/go-langserver
RUN go get -u -v golang.org/x/tools/cmd/goimports
RUN go get -u -v github.com/cweill/gotests/...
RUN go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs
RUN go get -u -v github.com/fatih/gomodifytags
RUN go get -u -v github.com/josharian/impl
RUN go get -u -v github.com/davidrjenni/reftools/cmd/fillstruct
RUN go get -u -v github.com/golang/dep/cmd/dep
RUN GO111MODULE=on go get golang.org/x/tools/gopls@latest



FROM codercom/code-server:v2

# Kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin

# Google cloud sdk and some other tools
RUN sudo apt-get update; sudo apt-get install -y bsdtar curl telnet iputils-ping netcat ssh rsync dnsutils gnupg gnupg2 gcc python3-pip && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
    sudo apt-get update; sudo apt-get install -y google-cloud-sdk && \
    wget -q https://storage.googleapis.com/kubernetes-helm/helm-v2.14.2-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > helm && \
    chmod +x helm && \
    sudo mv helm /usr/local/bin/helm && \
    sudo pip3 install awscli --upgrade

# VSCode extensions
RUN mkdir -p /home/coder/.local/share/code-server/extensions/
ENV SERVICE_URL https://marketplace.visualstudio.com/_apis/public/gallery
RUN code-server  --install-extension eamodio.gitlens \
    && code-server --install-extension donjayamanne.githistory \
    && code-server --install-extension huizhou.githd \
    && code-server --install-extension mhutchie.git-graph \
    && code-server --install-extension waderyan.gitblame \
    && code-server --install-extension coenraads.bracket-pair-colorizer \
    && code-server --install-extension mihelcic.colored-regions \
    && code-server --install-extension streetsidesoftware.code-spell-checker \
    && code-server --install-extension fabiospampinato.vscode-diff \
    && code-server --install-extension ryu1kn.partial-diff \
    && code-server --install-extension editorconfig.editorconfig \
    && code-server --install-extension christian-kohler.path-intellisense \
    && code-server --install-extension PKief.material-icon-theme \
    && code-server --install-extension equinusocio.vsc-material-theme \
    && code-server --install-extension redhat.vscode-yaml \
    && code-server --install-extension kumar-harsh.graphql-for-vscode \
    && code-server --install-extension mohsen1.prettify-json \
    && code-server --install-extension humao.rest-client \
    && code-server --install-extension yzhang.markdown-all-in-one \
    && code-server --install-extension jmmeessen.jenkins-declarative-support \
    && code-server --install-extension secanis.jenkinsfile-support \
    && code-server --install-extension bungcip.better-toml \
    && code-server --install-extension ms-vscode.sublime-keybindings \
    && code-server --install-extension ms-azuretools.vscode-docker \
    && code-server --install-extension ms-kubernetes-tools.vscode-kubernetes-tools \
    && code-server --install-extension ipedrazas.kubernetes-snippets \
    && code-server --install-extension googlecloudtools.cloudcode \
    && code-server --install-extension ms-vscode.go \
    && code-server --install-extension neverik.go-critic \
    && code-server --install-extension msyrus.go-doc \
    && code-server --install-extension premparihar.gotestexplorer \
    && code-server --install-extension windmilleng.vscode-go-autotest \
    && code-server --install-extension aleksandra.go-group-imports

ENV GOLANG_VERSION 1.13.0
ENV GOPATH /home/coder/project
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
COPY --from=golang /usr/local/go /usr/local/go

COPY --chown=coder:coder --from=golang /go/bin /home/coder/project/bin
RUN mkdir -p /home/coder/project/src && chown -R coder:coder /home/coder

