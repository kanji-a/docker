# Python3.8.2取得
FROM python:3.8.2-buster

WORKDIR /usr/src/app

# aptインストール
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get update
RUN apt-get install -y zsh nodejs neovim

# neovimの設定
RUN mkdir -p $HOME/.config/nvim
RUN wget https://raw.githubusercontent.com/kanji-a/dotfiles/master/nvim/init.vim -O $HOME/.config/nvim/init.vim

# pipインストール
COPY requirements.txt /usr/src/app
RUN pip3 install -r requirements.txt

# atcoder-cli
RUN npm install -g atcoder-cli
RUN acc config default-task-choice all
RUN mkdir `acc config-dir`/python
RUN wget https://raw.githubusercontent.com/kanji-a/competitive_programming/master/templates/atcoder-cli/python/main.py -O `acc config-dir`/python/main.py
RUN wget https://raw.githubusercontent.com/kanji-a/competitive_programming/master/templates/atcoder-cli/python/template.json -O `acc config-dir`/python/template.json
RUN acc config default-template python

# oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# シェル設定ファイル追記
COPY shell_config /usr/src/app
RUN cat shell_config >> ~/.zshrc
