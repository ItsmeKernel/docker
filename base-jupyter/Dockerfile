FROM python:3.9-slim-buster
ARG NB_USER="nbuser"
ARG NB_UID="1000"
ARG NB_GID="100"
ARG NB_DIR="/notebooks"
COPY requirements.txt .
RUN mkdir ${NB_DIR} && \
    useradd -l -m -s /bin/bash -N -u "${NB_UID}" "${NB_USER}" && \
    chown "${NB_USER}:${NB_GID}" "${NB_DIR}" && \
    chmod g+w /etc/passwd && \
    chgrp ${NB_GID} ${NB_DIR} &&\
    chmod g+rwX ${NB_DIR} && \
    pip3 install --no-cache-dir -r requirements.txt && \
    pip3 install jupyter jupyterlab
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["jupyter", "lab", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--notebook-dir=/notebooks/", "--allow-root"]