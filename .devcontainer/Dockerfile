# Use NVIDIA CUDA base image
FROM nvidia/cuda:12.1.0-devel-ubuntu20.04

# Step 1: Install basic dependencies
RUN apt-get update && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Step 2: Install Python 3 and pip
RUN apt-get update
RUN apt-get install python3 -y
RUN apt-get install python3-pip -y

# Step 3: Install Poetry for Python dependency management
RUN curl -sSL https://install.python-poetry.org | POETRY_VERSION=1.8.0 python3 -
RUN echo 'export PATH="/root/.local/bin:$PATH"' >> ~/.bashrc

# Step 4: Install Miniconda (lightweight version of Anaconda)
# Ref: https://hub.docker.com/r/continuumio/miniconda3/dockerfile/
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

# Step 5: Install TINI for proper signal handling
ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

# Step 6: Add Poetry's local bin to PATH
ENV PATH="/root/.local/bin:$PATH"

# Step 7: Verify Poetry installation
RUN poetry --version

# Step 8: Set environment variable for Conda environment path
ENV CONDA_ENV_PATH=/opt/conda/envs/

# Step 9: Configure Poetry to use Conda environments and disable Poetry's virtualenv creation
# Ref: https://michhar.github.io/2023-07-poetry-with-conda/
RUN poetry config virtualenvs.path $CONDA_ENV_PATH && \
    poetry config virtualenvs.create false

# Step 10: Install additional Python packages
RUN pip3 install networkx
RUN pip3 install torch --index-url https://download.pytorch.org/whl/cu121
