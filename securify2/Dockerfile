FROM ubuntu:22.04
ARG SOLC=0.5.12

# ------------------------------
# Install basic system packages and build deps
# ------------------------------
RUN apt-get update && apt-get install -y \
    software-properties-common \
    locales \
    wget \
    git \
    curl \
    build-essential \
    cmake \
    m4 \
    libncurses5-dev \
    libffi-dev \
    bison \
    flex \
    gdebi-core \
    autoconf \
    automake \
    autotools-dev \
    libtool \
    pkg-config \
    python3 \
    python3-distutils \
    python3-pip \
    graphviz && \
    locale-gen en_US.UTF-8 && \
    rm -rf /var/lib/apt/lists/*

# ------------------------------
# Set locale
# ------------------------------
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# ------------------------------
# Build and install Soufflé 1.6.2 from source
# ------------------------------
RUN git clone https://github.com/souffle-lang/souffle.git && \
    cd souffle && \
    git checkout tags/1.6.2 && \
    ./bootstrap && ./configure && make -j$(nproc) && make install && \
    cd .. && rm -rf souffle

# ------------------------------
# Install specific solc version
# ------------------------------
RUN curl -L https://github.com/ethereum/solidity/releases/download/v$SOLC/solc-static-linux > /usr/bin/solc-$SOLC && \
    chmod +x /usr/bin/solc-$SOLC && \
    ln -s /usr/bin/solc-$SOLC /usr/local/bin/solc

# ------------------------------
# Copy project and install dependencies
# ------------------------------
WORKDIR /sec
COPY requirements.txt /requirements.txt
COPY . /sec
ENV PYTHONPATH /sec

RUN pip3 install --no-cache-dir -r /requirements.txt && \
    pip3 install requests && \
    python3 setup.py install

# ------------------------------
# Compile functors & analysis
# ------------------------------
RUN cd /sec/securify/staticanalysis/libfunctors/ && ./compile_functors.sh

RUN cd /sec/securify/staticanalysis/souffle_analysis && \
    souffle --dl-program=../dl-program \
        --fact-dir=/sec/securify/staticanalysis/facts_in \
        --output-dir=/sec/securify/staticanalysis/facts_out \
        -L../libfunctors -w analysis.dl

ENV LD_LIBRARY_PATH=/sec/securify/staticanalysis/libfunctors

# ------------------------------
# Verify with sample contract (optional warmup)
# ------------------------------
RUN cd /sec/securify/ && python3 __main__.py securify/staticanalysis/testContract.sol || true

# ------------------------------
# Entrypoint
# ------------------------------
ENTRYPOINT ["python3", "securify/__main__.py"]