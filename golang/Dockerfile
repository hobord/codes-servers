FROM golang:1.11.12-stretch as golang

RUN go get -v github.com/mdempsky/gocode && go install -i github.com/mdempsky/gocode
RUN go get -v github.com/uudashr/gopkgs/cmd/gopkgs && go install -i github.com/uudashr/gopkgs/cmd/gopkgs
RUN go get -v github.com/ramya-rao-a/go-outline && go install -i github.com/ramya-rao-a/go-outline
RUN go get -v github.com/acroca/go-symbols && go install -i github.com/acroca/go-symbols
RUN go get -v golang.org/x/tools/cmd/guru && go install -i golang.org/x/tools/cmd/guru
RUN go get -v golang.org/x/tools/cmd/gorename && go install -i golang.org/x/tools/cmd/gorename
RUN go get -v github.com/go-delve/delve/cmd/dlv && go install -i github.com/go-delve/delve/cmd/dlv
RUN go get -v github.com/stamblerre/gocode && go install -i github.com/stamblerre/gocode
RUN go get -v github.com/rogpeppe/godef && go install -i github.com/rogpeppe/godef
RUN go get -v github.com/sqs/goreturns && go install -i github.com/sqs/goreturns
RUN go get -v golang.org/x/lint/golint && go install -i golang.org/x/lint/golint
# RUN go get -v github.com/766b/go-outliner && go install -i github.com/766b/go-outliner
RUN chown -R 1000:1000 /go


FROM codercom/code-server

# Kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin

# Google cloud sdk
RUN sudo apt-get update; sudo apt-get install -y bsdtar curl telnet iputils-ping netcat ssh rsync dnsutils gnupg gnupg2 && \
    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
    sudo apt-get update; sudo apt-get install -y google-cloud-sdk && \
    wget -q https://storage.googleapis.com/kubernetes-helm/helm-v2.14.2-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > helm && \
    chmod +x helm && \
    sudo mv helm /usr/local/bin/helm

# VSCode extensions
RUN mkdir -p /home/coder/.local/share/code-server/extensions/

RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/eamodio/vsextensions/gitlens/9.6.3/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/eamodio.gitlens-9.6.3
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/donjayamanne/vsextensions/githistory/0.4.6/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/donjayamanne.githistory-0.4.6
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/huizhou/vsextensions/githd/2.1.0/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/huizhou.githd-2.1.0
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/waderyan/vsextensions/gitblame/2.8.1/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/waderyan.gitblame-2.8.1
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/CoenraadS/vsextensions/bracket-pair-colorizer/1.0.61/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/coenraads.bracket-pair-colorizer-1.0.61
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/mihelcic/vsextensions/colored-regions/0.0.3/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/mihelcic.colored-regions-0.0.3
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/streetsidesoftware/vsextensions/code-spell-checker/1.7.17/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/streetsidesoftware.code-spell-checker-1.7.17
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/EditorConfig/vsextensions/EditorConfig/0.13.0/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/editorconfig.editorconfig-0.13.0
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/christian-kohler/vsextensions/path-intellisense/1.4.2/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/christian-kohler.path-intellisense-1.4.2
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-vscode/vsextensions/sublime-keybindings/4.0.3/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/ms-vscode.sublime-keybindings-4.0.3
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-azuretools/vsextensions/vscode-docker/0.7.0/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/ms-azuretools.vscode-docker-0.7.0
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-kubernetes-tools/vsextensions/vscode-kubernetes-tools/1.0.1/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/ms-kubernetes-tools.vscode-kubernetes-tools-1.0.1
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ipedrazas/vsextensions/kubernetes-snippets/0.1.9/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/ipedrazas.kubernetes-snippets-0.1.9
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/GoogleCloudTools/vsextensions/cloudcode/0.0.10/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/googlecloudtools.cloudcode-0.0.10
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/redhat/vsextensions/vscode-yaml/0.4.1/vspackage| bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/redhat.vscode-yaml-0.4.1

#Golang Specific
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-vscode/vsextensions/Go/0.11.4/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/ms-vscode.go-0.11.4
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/neverik/vsextensions/go-critic/0.1.0/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/neverik.go-critic-0.1.0
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/msyrus/vsextensions/go-doc/0.1.1/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/msyrus.go-doc-0.1.1
# RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/766b/vsextensions/go-outliner/0.1.20/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/766b.go-outliner-0.1.20
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/premparihar/vsextensions/gotestexplorer/0.1.10/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/premparihar.gotestexplorer-0.1.10
RUN curl -JL https://marketplace.visualstudio.com/_apis/public/gallery/publishers/aleksandra/vsextensions/go-group-imports/1.0.1/vspackage | bsdtar -xvf - extension && mv extension /home/coder/.local/share/code-server/extensions/aleksandra.go-group-imports-1.0.1


ENV GOLANG_VERSION 1.12.7
ENV GOPATH /home/coder/project
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
COPY --from=golang /usr/local/go /usr/local/go
COPY --from=golang /go /home/coder/project


#RUN go get -u github.com/ramya-rao-a/go-outline
#RUN go get -u github.com/766b/go-outliner

