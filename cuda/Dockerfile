FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04

COPY config /config

# Install SSH Service
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        curl \
        ca-certificates \
        libjpeg-dev \
        libpng-dev  \
        pkg-config \
        software-properties-common \
        unzip \
        openssh-server \
        screen \
        && mkdir /var/run/sshd \
        && echo 'root:GeekCloud' |chpasswd \
        && sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
        && sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
        && mkdir /root/.ssh \
        && rm -rf /var/lib/apt/lists/*


# See http://bugs.python.org/issue19846
ENV LANG C.UTF-8

RUN curl -o ~/miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh && \
     mv /config/.condarc /root

ENV PATH /opt/conda/bin:$PATH

# Installs the latest version by default.



EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]
