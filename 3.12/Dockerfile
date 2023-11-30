# Python 開発環境
#   Python version: 3.12
#
FROM python:3.12

# 環境変数
ENV DEBIAN_FRONTEND=noninteractive \  
    LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP:ja \ 
    TZ=Asia/Tokyo

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    fonts-takao \
    language-pack-ja-base \
    language-pack-ja \
    locales \
    sudo \
    tzdata \
    xdg-user-dirs \
    && \
# ロケールの生成
    locale-gen ja_JP.UTF-8 \
    && \
# Clean up
    apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# 日本語フォルダ名を英語に改名
RUN LANG=C xdg-user-dirs-update --force

# pipコマンドの更新
RUN pip install --upgrade pip

# pythonライブラリーをインストール
RUN pip install -r requirements.txt

# sudo可能な一般ユーザーを追加
ARG USERNAME=user
ARG GROUPNAME=user
ARG UID=1000
ARG GID=1000
ARG PASSWORD=user
RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID -G sudo $USERNAME && \
    echo $USERNAME:$PASSWORD | chpasswd && \
    echo "$USERNAME   ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
USER $USERNAME

# 作業ディレクトリを設定
WORKDIR /home/$USERNAME/workspace

# コンテナ起動時に実行するコマンド
CMD ["/bin/bash"]