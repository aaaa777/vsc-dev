FROM debian:11


# setting utils

RUN mkdir -p /workspace && cd /workspace \
 && apt update \
 && apt install -y curl git wget nano \
                   nodejs npm


# install n

RUN npm install -g n \
 && n install stable \
 && n stable


# install github-cli

RUN type -p curl >/dev/null || apt install curl -y \
 && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg \
 && chmod go+r /usr/share/keyrings/githubcli-archive-keyring.gpg \
 && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
 && apt update \
 && apt install gh -y

WORKDIR /workspace


# install vscode-server

RUN wget https://aka.ms/vscode-server-launcher/aarch64-unknown-linux-gnu \
 && chmod +x aarch64-unknown-linux-gnu && mkdir -p /usr/local/lib/vscode-server \
 && mv aarch64-unknown-linux-gnu /usr/local/lib/vscode-server/ \
 && ln -s /usr/local/lib/vscode-server/aarch64-unknown-linux-gnu /usr/local/bin/vscode-server

COPY --chmod=755 entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
