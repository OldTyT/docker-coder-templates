FROM ubuntu

RUN apt-get update \
	&& apt-get install -y \
	curl \
	git \
	sudo \
	vim \
	wget \
        nodejs \
        python3 \
        python3-pip \
        nano \
	&& rm -rf /var/lib/apt/lists/* \
    && wget https://go.dev/dl/go1.20.2.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.20.2.linux-amd64.tar.gz \
    && rm go1.20.2.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin
ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}
