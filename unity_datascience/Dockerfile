FROM jupyter/datascience-notebook

# Switch to root user for build
USER root

# Install Dockstore
RUN apt-get update -q && \
    apt install -y openjdk-11-jdk && \
    curl -L -o /usr/local/bin/dockstore https://github.com/dockstore/dockstore-cli/releases/download/1.13.1/dockstore && \
    chmod +x /usr/local/bin/dockstore

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli && \
    rm -rf awscliv2.zip aws

RUN conda install nb_conda_kernels ipykernel screen

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}
