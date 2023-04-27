ARG BASE_IMAGE_NAME
FROM ${BASE_IMAGE_NAME}

# ARGの有効範囲は次のFROMまで
ARG L4T_VERSION
ARG DS_VERSION
ARG CUDA_VER

# intercativeな設定を無効化
ENV DEBIAN_FRONTEND=noninteractive
# rsekf-hosted-runnerのroot実行許可
ENV RUNNER_ALLOW_RUNASROOT=1
# バージョン埋め込み
ENV L4T_VERSION=$L4T_VERSION
ENV DS_VERSION=$DS_VERSION
ENV CUDA_VER=$CUDA_VER

RUN apt update && \
    apt install -y \
        ca-certificates \
        curl \
        gnupg \
        sudo \
        git \
# ここからは好みのパッケージを記述する
# GStreamer
        build-essential \
        pkg-config \
        libx11-dev \
        libgtk-3-dev \
        libexpat1-dev \
        libjpeg-dev \
        libgstreamer1.0-dev \
        libclang-dev \
        jq \
        libgstreamer-plugins-base1.0-dev \
# DeepStream
        libssl1.1 \
        libgstreamer1.0-0 \
        gstreamer1.0-tools \
        gstreamer1.0-plugins-good \
        gstreamer1.0-plugins-bad \
        gstreamer1.0-plugins-ugly \
        gstreamer1.0-libav \
        libgstreamer-plugins-base1.0-dev \
        libgstrtspserver-1.0-0 \
        libjansson4 \
        libyaml-cpp-dev \
# nvinfer関係のビルドや実行に必要だがdeepstreamで一緒にインストールされないものを含む
    	cuda-nvcc-11-4 \
        libcudla-11-4 \
        deepstream-${DS_VERSION} \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ARG USERNAME=vscode
ARG GROUPNAME=vscode
ARG USER_UID=2000
ARG USER_GID=$USER_UID
ARG PASSWORD=$USERNAME
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m -s /bin/bash -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER $USERNAME

WORKDIR workspace