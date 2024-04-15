# ベースイメージ
FROM rocker/rstudio:4.3.0

# OS環境設定
## ロケール
ENV LANG ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
RUN sed -i '$d' /etc/locale.gen \
      && echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen \
      && locale-gen ja_JP.UTF-8 \
      && /usr/sbin/update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN /bin/bash -c "source /etc/default/locale"
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo/etc/localtime
## フォント
RUN apt-get update && apt-get install -y \
      fonts-ipaexfont \
      fonts-noto-cjk \
      openssh-client libxt-dev

# R
## ライブラリ
RUN R -e "install.packages(c('renv'))"
      
# Quarto
## インストール
RUN sudo rm -rf /opt/quarto
ENV QUARTO_VERSION 1.5.6
RUN /rocker_scripts/install_quarto.sh
## 拡張
RUN quarto install extension quarto-ext/fontawesome  --no-prompt

# Python
## インストール
RUN apt-get update && apt-get install -y python3 python3-pip

## ライブラリ

# Reticulate
RUN R -e "Sys.setenv(RETICULATE_PYTHON = '/usr/bin/python3.10')"

RUN cd /home/rstudio && mkdir .pip .cache .cache/R .cache/R/renv .TinyTeX && \
      chown rstudio:rstudio .pip .cache .cache/R .cache/R/renv .TinyTeX