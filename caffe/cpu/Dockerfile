FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    git \
    libatlas-base-dev \
    libboost-all-dev \
    libgflags-dev \
    libgoogle-glog-dev \
    libhdf5-serial-dev \
    libleveldb-dev \
    liblmdb-dev \
    libopencv-dev \
    libprotobuf-dev \
    libsnappy-dev \
    protobuf-compiler \
    python3-dev \
    python3-numpy \
    python3-pip \
    python3-scipy \
    python3-setuptools \
    python3-lmdb \
    python3-pydot \
    graphviz \
    wget \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install -U pip==9.0.3 \
    && pip3 install -U \
    cython \
    numpy \
    scipy \
    scikit-image \
    matplotlib \
    ipython \
    h5py \
    leveldb \
    networkx \
    nose \
    pandas \
    python-dateutil \
    protobuf \
    python-gflags \
    pyyaml \
    Pillow \
    six

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

ENV CLONE_TAG=1.0

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/BVLC/caffe.git . \
    && mkdir build \
    && cd build \
    && cmake -DCPU_ONLY=1 -Dpython_version=3 .. \
    && make -j$(nproc)

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo '$CAFFE_ROOT/build/lib' >> /etc/ld.so.conf.d/caffe.conf \
    && ldconfig

WORKDIR /workspace
