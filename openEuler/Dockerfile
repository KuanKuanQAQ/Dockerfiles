FROM ubuntu:22.04

SHELL ["/bin/bash", "-c"]
COPY id_rsa /root/.ssh/
RUN apt update 
RUN apt install -y sudo git wget curl gdb vim zsh qemu-system 
RUN apt install -y build-essential gcc-12 g++-12 flex bison bc cpio libssl-dev libncurses-dev 
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 100 --slave /usr/bin/g++ g++ /usr/bin/g++-12
RUN eval `ssh-agent -s` && ssh-add /root/.ssh/id_rsa
RUN git clone https://github.com/KuanKuanQAQ/My-Vim-Config.git /root/.vim && cp /root/.vim/.vimrc.example /root/.vimrc
RUN echo "y"|sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
