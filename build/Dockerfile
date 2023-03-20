FROM ubuntu

RUN apt-get update \
	&& apt-get install -y \
	curl \
	git \
	sudo \
	vim \
	wget \
        python3 \
        python3-pip \
        nano \
        && curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - \
        && apt-get install -y nodejs \
	&& rm -rf /var/lib/apt/lists/* \
    && wget https://go.dev/dl/go1.20.2.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.20.2.linux-amd64.tar.gz \
    && rm go1.20.2.linux-amd64.tar.gz \
    && npm install -g @commitlint/cli @commitlint/config-conventional \
    && npm install -g conventional-changelog-cli \
    && echo "#!/bin/bash" > /usr/local/sbin/commit \
    && echo 'echo "$1" | commitlint --config ~/commitlint.config.js && conventional-changelog -p angular -i CHANGELOG.md -s -r 0 && git add CHANGELOG.md && git commit -m "$1"' >> /usr/local/sbin/commit \
    && chmod +x /usr/local/sbin/commit

ENV PATH=$PATH:/usr/local/go/bin
ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}

USER ${USER}
WORKDIR /home/${USER}
RUN echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > /home/${USER}/commitlint.config.js
