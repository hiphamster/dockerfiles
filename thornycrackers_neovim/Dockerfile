FROM ubuntu:16.04
MAINTAINER Alex Yelluas <ayelluas@gmail.com>

########################################
# System Stuff
########################################

# Better terminal support
ENV TERM screen-256color
ENV DEBIAN_FRONTEND noninteractive

# Update and install
RUN apt-get update && apt-get install -y \
      htop \
      bash \
      curl \
      wget \
      git \
      software-properties-common \
      python-dev \
      python-pip \
      python3-dev \
      python3-pip \
      ctags \
      shellcheck \
      netcat \
      ranger \ 
      ack-grep \
      sqlite3 \
      # For python crypto libraries
      libssl-dev \
      libffi-dev \
      locales

# Generally a good idea to have these, extensions sometimes need them
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Add neovim repository
RUN add-apt-repository ppa:neovim-ppa/stable

# Install custom packages
RUN apt-get update && apt-get install -y \
      sudo \  
      tmux \
      neovim

########################################
# Python
########################################

# Install python linting and neovim plugin
RUN pip install neovim jedi flake8 flake8-docstrings flake8-isort flake8-quotes
RUN pip install pep8-naming pep257 isort
RUN pip3 install neovim jedi flake8 flake8-docstrings flake8-isort flake8-quotes
RUN pip3 install pep8-naming pep257 isort mypy ansible-lint flake8-bugbear
RUN pip3 install flake8-commas flake8-comprehensions


########################################
# Dasht Documentation
########################################
###ADD dasht/bin/* /usr/local/bin/
###ENV DASHT_DOCSETS_DIR /root/.local/share/dasht/docsets
###RUN mkdir -p /root/.local/share/dasht/docsets
###RUN dasht-docsets-install --force django
###RUN dasht-docsets-install --force python_3

ADD add_user.sh /root
RUN ["chmod","755","add_user.sh"] 
RUN /root/add_user.sh




########################################
# Personalizations
########################################
# Add some aliases
# ADD bashrc /root/.bashrc
# Add my git config
# ADD gitconfig /etc/gitconfig
# Change the workdir, Put it inside root so I can see neovim settings in finder
WORKDIR /root/app
# Neovim needs this so that <ctrl-h> can work
RUN infocmp $TERM | sed 's/kbs=^[hH]/kbs=\\177/' > /tmp/$TERM.ti
RUN tic /tmp/$TERM.ti
# Command for the image
CMD ["/bin/bash"]
# Add nvim config. Put this last since it changes often
# ADD nvim /root/.config/nvim
# Install neovim Modules
# RUN nvim -i NONE -c PlugInstall -c quitall > /dev/null 2>&1
# RUN nvim -i NONE -c UpdateRemotePlugins -c quitall > /dev/null 2>&1
# Add flake8 config, don't trigger a long build process
# ADD flake8 /root/.flake8
# Add local vim-options, can override the one inside
# ADD vim-options /root/.config/nvim/plugged/vim-options
# Add isort config, also changes often
# ADD isort.cfg /root/.isort.cfg
