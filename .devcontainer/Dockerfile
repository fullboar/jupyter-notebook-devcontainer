FROM mcr.microsoft.com/vscode/devcontainers/miniconda:0-3

# [Option] Install Node.js
ARG INSTALL_NODE="true"
ARG NODE_VERSION="lts/*"
RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] Uncomment this section to install additional OS packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql-client libpq-dev

# Copy environment.yml (if found) to a temp locaition so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && rm -rf /tmp/conda-tmp

COPY requirements.txt /tmp/pip-tmp/
COPY oc-49-linux-x86_64.tar.gz /tmp/

RUN /opt/conda/bin/python3 \
  -m pip \
  --disable-pip-version-check \
  --no-cache-dir install \
  -r /tmp/pip-tmp/requirements.txt \
  && rm -rf /tmp/pip-tmp

RUN conda install \
  -n base ipykernel \
  --update-deps \
  --force-reinstall

RUN tar -zxf /tmp/oc-49-linux-x86_64.tar.gz \
  -C /usr/bin/ && \
  rm -rf /tmp/oc-49-linux-x86_64.tar.gz
