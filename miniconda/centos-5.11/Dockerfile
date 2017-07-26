############################################################
# Dockerfile for the CSDMS software stack
############################################################

# Set the base image to centos
FROM centos:centos5.11

# File Author / Maintainer
MAINTAINER Eric Hutton

RUN [ -e /etc/yum.conf ] && sed -i '/tsflags=nodocs/d' /etc/yum.conf || true

# Point yum to old repositories for centos 5
RUN for f in /etc/yum.repos.d/*.repo; do sed -i 's/^mirrorlist/# mirrorlist/g' $f; done
RUN for f in /etc/yum.repos.d/*.repo; do sed -i 's/^#baseurl/baseurl/g' $f; done
RUN for f in /etc/yum.repos.d/*.repo; do sed -i 's/mirror.centos.org\/centos/vault.centos.org/g' $f; done
RUN for f in /etc/yum.repos.d/*.repo; do sed -i 's/\$releasever/5.11/g' $f; done


# Install basic applications
RUN yum -y update && yum clean all
RUN rpm -Uvh http://archive.webtatic.com/yum/webtatic-5-archive/x86_64/webtatic-release-5-3.noarch.rpm
RUN yum install --enablerepo=webtatic --disableexcludes=main  git-all

RUN yum -y install \
  tar \
  bzip2 \
  curl \
  gcc44 \
  gcc44-c++ \
  gcc44-gfortran \
  patch \
  glib2-devel

RUN yum clean all

# Install Python and Basic Python Tools
RUN curl https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh > miniconda.sh
RUN /bin/bash ./miniconda.sh -b -f -p /usr/local/python
ENV PATH=/usr/local/python/bin:$PATH

RUN conda config --add channels conda-forge
RUN conda config --add channels csdms-stack
RUN conda clean --lock
RUN conda config --set always_yes yes --set changeps1 no
RUN conda install python=2.7
RUN conda install -q \
  conda-build \
  anaconda-client \
  scipy \
  matplotlib \
  ipython

RUN useradd --create-home --shell /bin/bash csdms
RUN echo 'csdms:dragon' | chpasswd

USER csdms
WORKDIR /home/csdms
