# Python3.8.2取得
FROM python:3.8.2-buster

WORKDIR /usr/src/app

# aptインストール
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
RUN apt update
RUN apt install -y zsh nodejs neovim
# RUN apt upgrade -y

# シェルをzshに変更
SHELL ["/bin/zsh", "-c"]

# preztoインストール
RUN git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"
RUN runcoms=("${ZDOTDIR:-$HOME}/.zprezto/runcoms/zlogin" "${ZDOTDIR:-$HOME}/.zprezto/runcoms/zlogout" "${ZDOTDIR:-$HOME}/.zprezto/runcoms/zpreztorc" "${ZDOTDIR:-$HOME}/.zprezto/runcoms/zprofile" "${ZDOTDIR:-$HOME}/.zprezto/runcoms/zshenv" "${ZDOTDIR:-$HOME}/.zprezto/runcoms/zshrc")
RUN for rcfile in $runcoms; do ln -sf "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"; done
RUN zsh
# TODO: preztoの補完などの設定変更

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

# シェル設定ファイル追記
COPY shell_config /usr/src/app
RUN cat shell_config >> ~/.zshrc
