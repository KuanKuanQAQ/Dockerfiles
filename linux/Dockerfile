# =============================================================================
# An Ubuntu docker file for llvm & gcc that compile Linux kernel via apt. 
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
ENV TZ=Asia/Shanghai
SHELL ["/bin/bash", "-c"]
COPY id_rsa /root/.ssh/

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt update
RUN apt install -y gcc-12 g++-12 build-essential libssl-dev libncurses-dev 
RUN apt install -y ninja-build \
    python3-minimal python3-pip python3-setuptools \
    software-properties-common flex bison bc cpio \
    && rm -rf /var/lib/apt/lists/*
RUN apt install -y sudo git cmake wget curl gdb vim zsh qemu-system iputils-ping

RUN eval `ssh-agent -s` && ssh-add /root/.ssh/id_rsa

RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN apt-add-repository "deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-17 main"
RUN apt update
RUN apt install -y llvm-17 llvm-17-dev llvm-17-tools clang-17

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 100 --slave /usr/bin/g++ g++ /usr/bin/g++-12
RUN git clone https://github.com/KuanKuanQAQ/My-Vim-Config.git /root/.vim && cp /root/.vim/.vimrc.example /root/.vimrc
RUN echo "y"|sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
