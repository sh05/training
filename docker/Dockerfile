FROM python:3.7
WORKDIR /home/work
RUN apt update && \
    apt install -y --no-install-recommends apt-utils && \
    apt install -y \
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
    Pillow \
    gensim \
    sumy \
    tinysegmenter \
    tqdm \
    ipython[all] \
    jupyter && \
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
    echo "});" >> ~/.jupyter/custom/custom.js && \
    pip install -U scikit-learn
