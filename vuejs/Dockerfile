FROM codercom/code-server:v2

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
    && code-server --install-extension redhat.vscode-yaml \
    && code-server --install-extension kumar-harsh.graphql-for-vscode \
    && code-server --install-extension mohsen1.prettify-json \
    && code-server --install-extension humao.rest-client \
    && code-server --install-extension yzhang.markdown-all-in-one \
    && code-server --install-extension jmmeessen.jenkins-declarative-support \
    && code-server --install-extension secanis.jenkinsfile-support \
    && code-server --install-extension ms-vscode.sublime-keybindings \
    && code-server --install-extension ms-azuretools.vscode-docker \
    && code-server --install-extension ms-kubernetes-tools.vscode-kubernetes-tools \
    && code-server --install-extension ipedrazas.kubernetes-snippets \
    && code-server --install-extension googlecloudtools.cloudcode \
    && code-server --install-extension eg2.vscode-npm-script \
    && code-server --install-extension christian-kohler.npm-intellisense \
    && code-server --install-extension msjsdiag.debugger-for-chrome \
    && code-server --install-extension octref.vetur \
    && code-server --install-extension ducksoupdev.vue2 \
    && code-server --install-extension shinnn.stylelint

COPY --from=node:12 /usr/local /usr/local
COPY --from=node:12 /opt /opt
RUN sudo npm i -g typescript sass \
  && sudo chown -R coder:coder ~



