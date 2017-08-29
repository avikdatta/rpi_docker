FROM resin/armv7hf-debian-qemu

RUN [ "cross-build-start" ]

USER root
ENV NB_USER pi
ENV NB_UID 1000

RUN apt-get update && apt-get install -y \
    git                  \
    locales              \
    wget                 \
    make                 \
    g++                  \
    patch                \
    build-essential      \
    libssl-dev           \
    zlib1g-dev           \
    libbz2-dev           \
    libsqlite3-dev       \
    libssl-dev           \
    libreadline6-dev     \
    libreadline6         \
    libopenblas-dev      \
    tk-dev               \
    gfortran              

RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER 

RUN set -x \
    && mkdir -p  /home/$NB_USER/.pyenv \
    && mkdir -p /home/$NB_USER/tmp 
    
ENV TMPDIR=/home/$NB_USER/tmp
ENV PYENV_ROOT="/home/$NB_USER/.pyenv"   
ENV PATH="$PYENV_ROOT/libexec/:$PATH" 
ENV PATH="$PYENV_ROOT/shims/:$PATH" 
    
RUN set -x \
    && eval "$(pyenv init -)"  \
    && pyenv install 3.5.2     \
    && pyenv global 3.5.2      \
    && pip install \
        cython     \
        ipython    \
        numpy      \
        scipy      \
        sklearn    \
        pandas     \
        matplotlib \
        seaborn    \
        jupyter    \
        picamera
       
RUN set -x \
     && chown -R $NB_USER /home/$NB_USER/.pyenv 
     
USER $NB_USER

WORKDIR /home/$NB_USER

USER root
RUN [ "cross-build-end" ]
USER $NB_USER
