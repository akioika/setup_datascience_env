# Ubuntu 18.04 (bionic) from 2018-05-26
# https://github.com/docker-library/official-images/commit/aac6a45b9eb2bffb8102353c350d341a410fb169
ARG BASE_CONTAINER=ubuntu:bionic-20180526@sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
FROM $BASE_CONTAINER


USER root
ENV DEBCONF_NOWARNINGS yes
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
 && apt-get -yq dist-upgrade \
 && apt-get install -yq locales fonts-liberation tzdata

RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen \
 && locale-gen

ENV SHELL=/bin/bash \
    LC_ALL=ja_JP.UTF-8 \
    LANG=ja_JP.UTF-8 \
    LANGUAGE=ja_JP.UTF-8 \
    TZ=Asia/Tokyo

RUN apt-get install -yq  python3-pip python3-dev \
 && pip3 install jupyter \
 && jupyter notebook --generate-config

RUN sed -i \
    -e "s/^#c.NotebookApp.token = .*/c.NotebookApp.token = ''/" \
    -e "s/^#c.NotebookApp.password = .*/c.NotebookApp.password = ''/" \
    -e "s/^#c.NotebookApp.ip = .*/c.NotebookApp.ip = '0.0.0.0'/" \
    -e "s/^#c.NotebookApp.allow_root = False/c.NotebookApp.allow_root = True/" \
    -e "s/^#c.NotebookApp.open_browser = True/c.NotebookApp.open_browser = False/" \
    -e "s/^#c.NotebookApp.notebook_dir = .*/c.NotebookApp.notebook_dir = '\/root\/work'/" \
    /root/.jupyter/jupyter_notebook_config.py

RUN echo "#!/bin/bash" > /usr/local/bin/start_jupyter.sh
RUN echo "jupyter notebook --NotebookApp.token='' --NotebookApp.password='' --NotebookApp.notebook_dir='/root/work' --ip=0.0.0.0 --allow-root --no-browser" >> /usr/local/bin/start_jupyter.sh
RUN chmod u+x /usr/local/bin/start_jupyter.sh

EXPOSE 8888
CMD ["/usr/local/bin/start_jupyter.sh"]
