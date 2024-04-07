# =============================================================================
# An Ubuntu docker file for llvm & gcc that compile Linux kernel via apt. Clones 
# It uses the precompiled LLVM packages from Ubuntu.
#
# USAGE:
# ```bash
# docker build -t=x:v0 .
# docker run --rm -it --hostname=x x:v0 zsh
# ```
# =============================================================================


FROM ubuntu:22.04

ENV LLVM_DIR /usr/lib/llvm-17/
SHELL ["/bin/bash", "-c"]
COPY id_rsa /root/.ssh/
ENV TZ=Europe/London


RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get update && apt-get install -y \
    git \
    cmake \
    ninja-build \
    build-essential \
    python3-minimal python3-pip\
    wget \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

RUN eval `ssh-agent -s` && ssh-add /root/.ssh/id_rsa
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN apt-add-repository "deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-17 main"
RUN apt-get update
RUN apt-get install -y llvm-17 llvm-17-dev llvm-17-tools clang-17
RUN apt-get install -y python3-setuptools

RUN pip3 install lit

RUN apt install -y sudo git wget curl gdb vim zsh qemu-system 
RUN apt install -y build-essential gcc-12 g++-12 flex bison bc cpio libssl-dev libncurses-dev 
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 100 --slave /usr/bin/g++ g++ /usr/bin/g++-12
RUN git clone https://github.com/KuanKuanQAQ/My-Vim-Config.git /root/.vim && cp /root/.vim/.vimrc.example /root/.vimrc
RUN echo "y"|sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
