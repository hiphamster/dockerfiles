FROM ubuntu:latest
LABEL maintainer Alex Yelluas <ayelluas@gmail.com>

#############################################################################
# ubuntu container with neovim, tmux, python,
# zsh, oh-my-zsh. Creates a default user alex
#
# To build:
# docker build -t 'ayelluas:devbase' path/to/Dockerfile 
#
# To run:
# docker run -h devdev -it -v /Users/alex:/mnt/alex 'ayelluas:devbase'
#############################################################################

# Better terminal support
ENV TERM screen-256color
ENV DEBIAN_FRONTEND noninteractive

# Update and install
RUN apt-get update && apt-get install -y \
      bash \
      zsh \
      less \
      vim \
      sudo \
      man \
      htop \
      curl \
      wget \
      git \
      libterm-readline-gnu-perl \
      openssh-client \
      software-properties-common \
      python-dev \
      python-pip \
      python3-dev \
      python3-pip \
      ipython3 \
      ctags \
      shellcheck \
      netcat \
      net-tools \
      traceroute \
      iputils-ping \
      ranger \ 
      ack-grep \
      sqlite3 \
      tmux \
      w3m \
      # For python crypto libraries
      libssl-dev \
      libffi-dev \
      locales

# Add neovim repository
# needs apt-utils provided by software-properties-common
RUN add-apt-repository ppa:neovim-ppa/stable

# Install neovim 
RUN apt-get update && apt-get install -y neovim

ARG user=alex
ARG password=hello123
RUN sh -c "/usr/sbin/useradd -m -U -G sudo -s /bin/zsh $user"

# --build-arg password=<secret>
RUN sh -c "/bin/echo $user:$password | /usr/sbin/chpasswd"

ENV USER ${user:-alex}
ENV HOME /home/${USER}

USER ${user:-alex}
WORKDIR /home/${user:-alex}

RUN mkdir -p ${HOME}/.config

RUN git clone https://github.com/hiphamster/env.git ${HOME}/.config/env

WORKDIR ${HOME}/.config/env
RUN ./setup.sh
WORKDIR ${HOME}

# Command for the image
CMD /bin/zsh --login

