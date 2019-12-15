FROM python:3.7
WORKDIR /home/work
RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get install -y \
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
    pydot \
    torch \
    torchvision \
    sumy \
    tinysegmenter \
    "https://github.com/megagonlabs/ginza/releases/download/latest/ginza-latest.tar.gz" \
    tqdm \
    ipython[all] \
    jupyter && \
    pip install -U scikit-learn && \
    pip install jupyter-contrib-nbextensions && \
    jupyter contrib nbextension install --user && \
    pip install jupyter-nbextensions-configurator && \
    jupyter nbextensions_configurator enable --user && \
    mkdir -p $(jupyter --data-dir)/nbextensions && \
    git clone https://github.com/lambdalisue/jupyter-vim-binding $(jupyter --data-dir)/nbextensions/vim_binding && \
    jupyter nbextension enable vim_binding/vim_binding && \
    mkdir -p ~/.jupyter/custom/ && \
    touch ~/.jupyter/custom/custom.js && \
    echo " // Configure CodeMirror Keymap" >> ~/.jupyter/custom/custom.js && \
    echo "require([" >> ~/.jupyter/custom/custom.js && \
    echo "        'nbextensions/vim_binding/vim_binding',   // depends your installation" >> ~/.jupyter/custom/custom.js && \
    echo "], function() {" >> ~/.jupyter/custom/custom.js && \
    echo "// Map jj to <Esc>" >> ~/.jupyter/custom/custom.js && \
    echo "CodeMirror.Vim.map('jj', '<Esc>', 'insert');" >> ~/.jupyter/custom/custom.js && \
    # echo "// Swap j/k and gj/gk (Note that <Plug> mappings)" >> ~/.jupyter/custom/custom.js && \
    # echo "CodeMirror.Vim.map('j', '<Plug>(vim-binding-gj)', 'normal');" >> ~/.jupyter/custom/custom.js && \
    # echo "CodeMirror.Vim.map('k', '<Plug>(vim-binding-gk)', 'normal');" >> ~/.jupyter/custom/custom.js && \
    # echo "CodeMirror.Vim.map('gj', '<Plug>(vim-binding-j)', 'normal');" >> ~/.jupyter/custom/custom.js && \
    # echo "CodeMirror.Vim.map('gk', '<Plug>(vim-binding-k)', 'normal');" >> ~/.jupyter/custom/custom.js && \
    echo "});" >> ~/.jupyter/custom/custom.js
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
