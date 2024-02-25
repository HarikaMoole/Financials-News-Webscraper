FROM amazonlinux:2

# Install required packages
RUN yum update -y \
    && yum install -y gcc openssl openssl-devel bzip2-devel libffi-devel make tar gzip zlib-devel wget

# Download and extract Python
RUN wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz \
    && tar -xzf Python-3.12.0.tgz \
    && rm Python-3.12.0.tgz

# Compile Python with shared library support and optimizations
WORKDIR /Python-3.12.0
RUN ./configure --enable-optimizations --enable-shared \
    && make altinstall

# Update LD_LIBRARY_PATH
ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# Set up pip
WORKDIR /python/lib/python3.12/site-packages
RUN wget https://bootstrap.pypa.io/get-pip.py \
    && python3.12 get-pip.py \
    && rm get-pip.py

# Clean up
RUN yum clean all
