#donwload php pre-built image from docker hub 
FROM php:8.1-fpm

#install some required apps and commands 
RUN apt-get update \
    && apt-get install -y \
    apt-utils \
    wget \
    mariadb-client \
    pv \
    vim \
    nano \
    bash-completion \
    openssh-server \
    sudo \
    dnsutils \
    iputils-ping \
    iputils-tracepath \
    host \
    strace \
    gnupg \
    gcc \
    lsof \
    git \
    && apt-get update \
    && apt-get clean all 

#create new user
ENV _USER=user 
ENV _HOME_DIRECTORY=/home/${_USER}
RUN useradd -m ${_USER} \
    && echo "${_USER}:${_USER}" | chpasswd && chsh ${_USER} -s /bin/bash && adduser ${_USER} sudo \
    && chown -R ${_USER}:${_USER} /var/www/* \
    && chown -R ${_USER}:${_USER} ${_HOME_DIRECTORY} 

#composer 
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --1\
    && apt -qy install $PHPIZE_DEPS && mkdir /${_HOME_DIRECTORY}/.composer

#bash completion
USER ${_USER} 
RUN echo "source /etc/bash_completion" >> ${_HOME_DIRECTORY}/.bashrc

#TUNE ENVIRONMENT
USER root
RUN echo "Defaults    timestamp_timeout=-1" >> /etc/sudoers

WORKDIR /var/www