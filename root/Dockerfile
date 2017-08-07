FROM centos:latest
ARG version="6.10.00"
LABEL description="CERN ROOT framework"
LABEL version="${version}"

RUN yum -y install epel-release
RUN yum -y install gcc-c++ bzip2 git vim libpng libjpeg \
     python-devel libSM libX11 libXext libXpm libXft gsl-devel python-pip make cmake3\
     && yum -y clean all
RUN pip install --upgrade pip && pip install jupyter
RUN ln -s /usr/bin/cmake3 /usr/bin/cmake

# make softwares path
RUN mkdir /softwares

# Set ROOT environment
ENV ROOTSYS         "/softwares/root"
ENV PATH            "$ROOTSYS/bin:$ROOTSYS/bin/bin:$PATH"
ENV LD_LIBRARY_PATH "$ROOTSYS/lib:$LD_LIBRARY_PATH"
ENV PYTHONPATH      "$ROOTSYS/lib:$PYTHONPATH"

# download pre-compiled root from cern
ADD https://root.cern.ch/download/root_v${version}.Linux-centos7-x86_64-gcc4.8.tar.gz /var/tmp/root.tar.gz
RUN tar xzf /var/tmp/root.tar.gz -C /softwares && rm /var/tmp/root.tar.gz


