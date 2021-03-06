FROM nvidia/cuda:8.0-cudnn5-devel

MAINTAINER J Lovitt <lovi9573@hotmail.com>

# Pick up some TF dependencies
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python \
        python-dev \
        rsync \
	liblmdb-dev \
	liblmdb0 \
        software-properties-common \
        unzip \
	wget \
	bzip2 \
	ca-certificates \
	libmysqlclient-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

############################################################################## 
# anaconda python 
############################################################################## 
# Install Anaconda 
RUN wget --quiet https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh && \
 /bin/bash Anaconda2-4.2.0-Linux-x86_64.sh -b -p /opt/conda && \
 rm Anaconda2-4.2.0-Linux-x86_64.sh

ENV PATH /opt/conda/bin:$PATH

# change default encoding
RUN echo "\n \ 
	  import sys\n \
          sys.setdefaultencoding('utf-8')" >> /opt/conda/lib/python2.7/sitecustomize.py

#Follow up with keras and other desired packages not included in anaconda by default
RUN conda install -y seaborn pillow pyyaml hdf5 
RUN conda install -c conda-forge -y lmdb python-lmdb

RUN pip install --upgrade pip

############################################################################## 
# Tensorflow 
############################################################################## 
# Install TensorFlow GPU version.
RUN pip --no-cache-dir install \
  https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.0rc0-cp27-none-linux_x86_64.whl


############################################################################## 
# keras 
############################################################################## 
RUN pip install keras

# TensorBoard
EXPOSE 6006

# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD jupyter notebook --no-browser --ip=0.0.0.0 & tensorboard --logdir=/logs --host 0.0.0.0
