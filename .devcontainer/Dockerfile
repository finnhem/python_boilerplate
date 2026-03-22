ARG BASE_IMAGE=mcr.microsoft.com/devcontainers/base:ubuntu-22.04
FROM ${BASE_IMAGE}

# Install uv (pin version): https://docs.astral.sh/uv/guides/integration/docker/
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Keep uv's package cache on the workspace mount (see devcontainer.json remoteEnv UV_CACHE_DIR)
# so the cache and .venv share one filesystem; uv can hardlink instead of copying (much faster
# than UV_LINK_MODE=copy across separate mounts). See:
# https://docs.astral.sh/uv/guides/integration/docker/

# Do not run `uv sync` here: the devcontainer mounts the repo at runtime, so there is no
# project at build time. Run `uv sync` in postCreateCommand once pyproject.toml is available.

RUN apt-get update \
	&& apt-get install -y --no-install-recommends ca-certificates curl \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -fsSL https://raw.githubusercontent.com/opengrep/opengrep/main/install.sh | bash \
	&& install -m 0755 /root/.opengrep/cli/latest/opengrep /usr/local/bin/opengrep \
	&& opengrep --version