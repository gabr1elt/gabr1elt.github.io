# FROM ubuntu:20.04 as cpu
FROM ubuntu:22.04 as cpu
# FROM ubuntu:24.04 as cpu
# FROM ubuntu:latest as cpu
# FROM ubuntu:rolling as cpu

# init

ARG TYPE="cpu"

LABEL maintainer="gabr1elt"
LABEL repository="gabr1elt.github.io"
LABEL type=$TYPE

# switch to root

USER root
ARG USERNAME="root"
ARG HOME="/"$USERNAME
WORKDIR $HOME

ENV DEBIAN_FRONTEND=noninteractive

# install default packages

RUN apt-get update && \
    # apt-get install -y --no-install-recommends \
    apt-get install -y \
        # utils
        busybox \
        aptitude \
        bash \
        sudo \
        xsel \
        ranger \
        byobu \
        nano \
        htop \
        nmon \
        build-essential \
        git \
        git-lfs \
        curl \
        wget \
        gnupg \
        ca-certificates \
        pkg-config \
        software-properties-common \
        unzip \
        # data
        visidata \
        graphviz \
        lnav \
        # db
        sqlite \
        sqlite3-tools \
        # vision
        tesseract-ocr \
        # automation
        ansible \ 
        ansible-lint \
        # ml
        # libsndfile1-dev \
        # libgl1 \
        ## java ##
        # default-jdk-headless \
        # default-jdk \
        # openjdk-11-jdk \
        openjdk-21-jdk \
        # default-jre-headless \
        # default-jre \
        # openjdk-11-jre \
        # openjdk-21-jre \
        ## javascript ##
        nodejs \
        npm \
        ## python ##
        python3 \
        python3-pip \
        python3-wheel \
        python3-venv \
        python3-openpyxl \
        python3-arrow && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*


# Installs Node via nvm (Node Version Manager)

RUN curl -fsSL -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash && \
    # load nvm
    \. $HOME/.nvm/nvm.sh && \
    nvm install --lts && \
    node -v && \
    npm -v


# # Creating the user and usergroup

# ARG USERNAME="user"
# ARG USER_UID=2000
# ARG USER_GID=$USER_UID
# ARG HOME="/home/"$USERNAME

# # RUN adduser --disabled-password --gecos '' $USERNAME
# RUN groupadd --gid $USER_GID $USERNAME && \
#     useradd --uid $USER_UID --gid $USERNAME -m -s /bin/bash $USERNAME

# # sudo no password
# RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL >/etc/sudoers.d/$USERNAME && \
#     chmod 0440 /etc/sudoers.d/$USERNAME

# USER $USERNAME
# WORKDIR $HOME


# install vscode server

RUN curl -fsSL "https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64" -o /tmp/vscode-cli.tar.gz && \
    tar -xf /tmp/vscode-cli.tar.gz -C /usr/local/bin && \
    rm /tmp/vscode-cli.tar.gz

# # install openvscode server

# ARG OPENVSCODE_SERVER_ROOT="/opt/openvscode-server"
# # ARG OPENVSCODE_SERVER_RELEASE_TAG="openvscode-server-insiders-v1.90.0"

# RUN RELEASE_TAG="${OPENVSCODE_SERVER_RELEASE_TAG:-$(curl -fsSL -o /dev/null -w %{url_effective} https://github.com/gitpod-io/openvscode-server/releases/latest | cut -d '/' -f 8)}" && \
#     curl -fsSL https://github.com/gitpod-io/openvscode-server/releases/download/${RELEASE_TAG}/${RELEASE_TAG}-linux-x64.tar.gz -o /tmp/${RELEASE_TAG}-linux-x64.tar.gz && \
#     tar -xzf /tmp/${RELEASE_TAG}-linux-x64.tar.gz -C /tmp && \
#     rm -f /tmp/${RELEASE_TAG}-linux-x64.tar.gz && \
#     mv -f /tmp/${RELEASE_TAG}-linux-x64 ${OPENVSCODE_SERVER_ROOT} && \
#     ln -s  ${OPENVSCODE_SERVER_ROOT}/bin/remote-cli/openvscode-server ${OPENVSCODE_SERVER_ROOT}/bin/remote-cli/code && \
#     ln -s  ${OPENVSCODE_SERVER_ROOT}/bin/openvscode-server /usr/local/bin/code


# install python packages

# make sure to use venv
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# pre-install the heavy dependencies (these can later be overridden by the deps from setup.py)

RUN python3 -m pip install --no-cache-dir \
        py-cpuinfo \
        ipykernel \
        ipywidgets \
        python-dotenv \
        Jinja2 \
        lxml \ 
        odfpy \ 
        openpyxl \
        pyarrow \ 
        matplotlib \
        seaborn \
        plotly \
        requests \
        streamlit \
        pillow \
        opencv-python \
        pytesseract \
        numpy \
        scipy \
        pandas \
        numexpr \ 
        bottleneck \ 
        numba \ 
        scikit-learn \
        xgboost \
        keras \
        SQLAlchemy \ 
        pymysql
# psycopg2 \ 
# mplfinance \
# pandas_ta \
# TA-Lib \
# alpaca-py \
# pymarketstore

RUN python3 -m pip install --no-cache-dir \
        # TensorFlow Requirements (Python/cuDNN/CUDA): https://www.tensorflow.org/install/source#gpu
        # tensorflow \
        tensorflow[and-cuda] \
        # cuda-python \
        tensorboard \
        tensorflow-datasets \
        # TensorFlow Data Validation: https://www.tensorflow.org/tfx/data_validation/install#compatible_versions
        tensorflow-data-validation


# config git

RUN git config --global user.name "gabr1elt"


# wokdir

ARG WORKSPACE_ROOT=$HOME"/Development"
RUN mkdir -p $WORKSPACE_ROOT

WORKDIR $WORKSPACE_ROOT

# config env

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    EDITOR=code \
    VISUAL=code \
    GIT_EDITOR="code --wait" \
    WORKSPACE_ROOT=${WORKSPACE_ROOT}

# end

CMD [ "code", "tunnel", "--accept-server-license-terms", "--disable-telemetry" ]
# EXPOSE 3000
# CMD [ "code", "--host", "0.0.0.0", "--without-connection-token" ]
