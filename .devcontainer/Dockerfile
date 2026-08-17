# ベースイメージ : Ubuntu 22.04 LTS
FROM ubuntu:22.04

# 日本語ロケールとフォントのインストール
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
    locales \
    fonts-noto-cjk && \
    locale-gen ja_JP.UTF-8 && \
    rm -rf /var/lib/apt/lists/*

ENV LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP:ja \
    LC_ALL=ja_JP.UTF-8

# タイムゾーンの設定（ROS 2インストールに必要）
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
    tzdata && \
    ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    rm -rf /var/lib/apt/lists/*

# ROS 2 Humble のリポジトリ追加と必須ツールのインストール
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    curl \
    gnupg2 && \
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu jammy main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

# ROS 2本体(Desktop版)とビルドツール等のインストール
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
    ros-humble-desktop \
    python3-colcon-common-extensions \
    python3-rosdep \
    python3-pip \
    git \
    build-essential && \
    rm -rf /var/lib/apt/lists/*

# rosdepの初期化
RUN rosdep init && rosdep update

# ROS 2の環境変数を自動で読み込む設定
RUN echo "source /opt/ros/humble/setup.bash" >> /root/.bashrc