FROM ubuntu:16.04

LABEL maintainer="sumanthvrao <sumanthvrao@gmail.com>"

# Pick up some Python3 dependencies.
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python3 \
        python3-dev \
        python3-pip \
        python3-setuptools \
        rsync \
        software-properties-common \
        unzip \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Python3 general packages.
RUN pip3 install --upgrade pip \
        numpy \
        scipy \
        pandas \
        sklearn \
        ipykernel \
        jupyter \
        matplotlib \
        seaborn \
        Cython \
        Pillow \
        requests \
        awscli \
        && \
    python3 -m ipykernel.kernelspec

# Install machine learning packages.
RUN pip3 --no-cache-dir install --upgrade \
        tensorflow \
        tensorflow-tensorboard \
        keras \
        nltk \
        opencv-python

# Set up our notebook config.
COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_cmd.sh /

# Jupyter Notebook
EXPOSE 8888
# TensorBoard
EXPOSE 6006

WORKDIR /notebooks

RUN chmod +x /run_cmd.sh

CMD ["/run_cmd.sh"]