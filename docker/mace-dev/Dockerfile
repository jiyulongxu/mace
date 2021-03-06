FROM registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev-lite:latest

# Install tools
RUN apt-get update -y
RUN apt-get install -y --no-install-recommends \
    telnet \
    net-tools \
    inetutils-ping \
    screen \
    htop

RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com \
    sphinx \
    sphinx-autobuild \
    sphinx_rtd_theme \
    recommonmark

# ============ Install same deps for python3 ============
RUN pyenv global 3.6.3

# Install tools
RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com setuptools
RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com \
    "numpy>=1.14.0" \
    scipy \
    jinja2 \
    pyyaml \
    sh==1.12.14 \
    pycodestyle==2.4.0 \
    filelock \
    PTable

# Install Tensorflow
RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com \
    tensorflow==1.8.0

# Install pytorch (refer to: https://pytorch.org/get-started/locally/)
RUN pip install future==0.17.1 torchvision_nightly
RUN pip install torch_nightly -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html

# Install ONNX
RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com \
    onnx==1.3.0 \
    onnx-tf==1.2.0

RUN pip install -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com \
    sphinx \
    sphinx-autobuild \
    sphinx_rtd_theme \
    recommonmark

RUN pyenv global 2.7.14
# ============ End installing same deps for python3 ============


# Customize vim
RUN mkdir -p ~/.vim/autoload ~/.vim/bundle && \
    curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
RUN mkdir -p ~/.vim/bundle
RUN cd ~/.vim/bundle && \
    git clone https://github.com/scrooloose/nerdtree.git && \
    git clone https://github.com/vim-syntastic/syntastic.git && \
    git clone https://github.com/vim-airline/vim-airline.git && \
    git clone https://github.com/altercation/vim-colors-solarized.git && \
    git clone https://github.com/bazelbuild/vim-ft-bzl.git && \
    git clone https://github.com/google/vim-maktaba.git && \
    git clone https://github.com/google/vim-codefmt.git
RUN curl -LSso ~/.vimrc  https://gist.githubusercontent.com/llhe/71c5802919debd5825c100c0135478a7/raw/16a35020cc65f9c25d0cf8f11a3ba7b345a1271d/.vimrc

# Upgrade CMake
RUN wget https://cmake.org/files/v3.11/cmake-3.11.3-Linux-x86_64.tar.gz -P /tmp/ && \
    tar zxf /tmp/cmake-3.11.3-Linux-x86_64.tar.gz --strip-components=1 -C /usr/local/ && \
    update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force && \
    rm -f /tmp/cmake-3.11.3-Linux-x86_64.tar.gz

# mace-dev-lite image already included NDK r15c
## Download other NDK r16
RUN cd /opt/ && \
    wget -q https://dl.google.com/android/repository/android-ndk-r16-linux-x86_64.zip && \
    unzip -q android-ndk-r16-linux-x86_64.zip && \
    rm -f android-ndk-r16-linux-x86_64.zip
## Download other NDK r17b
RUN cd /opt/ && \
    wget -q https://dl.google.com/android/repository/android-ndk-r17b-linux-x86_64.zip && \
    unzip -q android-ndk-r17b-linux-x86_64.zip && \
    rm -f android-ndk-r17b-linux-x86_64.zip
