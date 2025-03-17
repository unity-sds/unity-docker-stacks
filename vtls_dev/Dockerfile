FROM jupyter/datascience-notebook

# Switch to root user for build
USER root

# Requires the build context to be one level up where common is located
COPY common/unity-sds /etc/unity-sds

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

RUN mamba install -y python>3.11 nb_conda_kernels ipykernel \
        s3fs boto3 netcdf4 xarray basemap cartopy h5netcdf 'basemap>=1.4.0' pysqlite3 \
        ipython numpy pandas matplotlib scipy && \
    conda clean -y --all 
RUN pip install unity_sds_client==0.7.0 podaac-data-subscriber PyWavelets

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}
