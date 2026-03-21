ARG BASE_IMAGE=mcr.microsoft.com/devcontainers/base:ubuntu-22.04
FROM ${BASE_IMAGE}

RUN apt-get update \
	&& apt-get install -y --no-install-recommends ca-certificates curl \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -fsSL https://raw.githubusercontent.com/opengrep/opengrep/main/install.sh | bash \
	&& install -m 0755 /root/.opengrep/cli/latest/opengrep /usr/local/bin/opengrep \
	&& opengrep --version