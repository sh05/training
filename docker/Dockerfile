FROM python:3.7
WORKDIR /home/work

RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils
RUN apt-get install -y \
    sudo \
    swig \
    curl \
    wget \
    xz-utils \
    file \
    git \
    make \
    mecab \
    libmecab-dev \
    default-jdk \
    graphviz \
    redis-server \
    mecab-ipadic-utf8 && \
    git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git &&\
    echo yes | ./mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n && \
    pip install --upgrade setuptools && \
    pip install --upgrade pip && \
    pip install numpy \
    pandas \
    mecab-python3 \
    wordcloud \
    sentencepiece \
    matplotlib \
    japanize-matplotlib \
    Pillow \
    gensim \
    graphviz \
    sumy \
    tinysegmenter \
    "https://github.com/megagonlabs/ginza/releases/download/latest/ginza-latest.tar.gz" \
    tqdm 
RUN apt-get install -y \
    nodejs \
    npm && \
    pip install jupyterlab==1.0 && \
    jupyter serverextension enable --py jupyterlab && \
    jupyter labextension install jupyterlab_vim
RUN mkdir -p /home/jovyan/.jupyter/lab/user-settings/@jupyterlab/apputils-extension && \
    echo '{"theme":"JupyterLab Dark"}' > \
    /home/jovyan/.jupyter/lab/user-settings/@jupyterlab/apputils-extension/themes.jupyterlab-settings
# Install CRF++
RUN wget -O /tmp/CRF++-0.58.tar.gz "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7QVR6VXJ5dWExSTQ" \
  && cd /tmp \
  && tar zxf CRF++-0.58.tar.gz \
  && cd CRF++-0.58 \
  && ./configure \
  && make \
  && make install \
  && cd / \
  && rm /tmp/CRF++-0.58.tar.gz \
  && rm -rf /tmp/CRF++-0.58 \
  && ldconfig
# Install CaboCha
RUN cd /tmp \
  && curl -c cabocha-0.69.tar.bz2 -s -L "https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7SDd1Q1dUQkZQaUU" \
    | grep confirm | sed -e "s/^.*confirm=\(.*\)&amp;id=.*$/\1/" \
    | xargs -I{} curl -b  cabocha-0.69.tar.bz2 -L -o cabocha-0.69.tar.bz2 \
      "https://drive.google.com/uc?confirm={}&export=download&id=0B4y35FiV1wh7SDd1Q1dUQkZQaUU" \
  && tar jxf cabocha-0.69.tar.bz2 \
  && cd cabocha-0.69 \
  && export CPPFLAGS=-I/usr/local/include \
  && ./configure --with-mecab-config=`which mecab-config` --with-charset=utf8 \
  && make \
  && make install \
  && cd python \
  && python setup.py build \
  && python setup.py install \
  && cd / \
  && rm /tmp/cabocha-0.69.tar.bz2 \
  && rm -rf /tmp/cabocha-0.69 \
  && ldconfig
