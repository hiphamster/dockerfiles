FROM centos:7.3.1611

MAINTAINER Alex Yelluas <ayelluas@gmail.com>

# -----------------------------------------------------------------------------
# Base Install + Import the RPM GPG keys for Repositories
# -----------------------------------------------------------------------------

RUN rpm --rebuilddb \
	&& rpm --import \
		http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7 \
	&& rpm --import \
		https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
	&& rpm --import \
		https://dl.iuscommunity.org/pub/ius/IUS-COMMUNITY-GPG-KEY \
	&& yum -y install \
		centos-release-scl \
		centos-release-scl-rh \
		epel-release \
		https://centos7.iuscommunity.org/ius-release.rpm \
		vim-minimal-7.4.160-1.el7 \
		xz-5.2.2-1.el7 \
		sudo-1.8.6p7-21.el7_3 \
		openssh-6.6.1p1-31.el7 \
		openssh-server-6.6.1p1-31.el7 \
		openssh-clients-6.6.1p1-31.el7 \
		python-setuptools-0.9.8-4.el7 \
		yum-plugin-versionlock-1.1.31-40.el7 \
    deltarpm-3.6-3.el7 \
    cmake \
    which \
    yum-utils \
  && yum groups list \
  && yum -y group install "Development Tools" \
	&& yum versionlock add \
		vim-minimal \
		xz \
		sudo \
		openssh \
		openssh-server \
		openssh-clients \
		python-setuptools \
		yum-plugin-versionlock \
	&& yum clean all \
	&& rm -rf /etc/ld.so.cache \
	&& rm -rf /sbin/sln \
	&& rm -rf /usr/{{lib,share}/locale,share/{man,doc,info,cracklib,i18n},{lib,lib64}/gconv,bin/localedef,sbin/build-locale-archive} \
	&& rm -rf /{root,tmp,var/cache/{ldconfig,yum}}/* \
	&& > /etc/sysconfig/i18n


RUN mkdir /opt/stuff \
  && git clone https://github.com/neovim/neovim.git /opt/stuff/neovim \
  && pushd /opt/stuff/neovim \
  && make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=/opt/neovim" \
  && make install



















