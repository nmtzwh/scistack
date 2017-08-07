FROM scistack/geant4:latest
ARG version="3.2"
LABEL description="MPICH library"
LABEL version="${version}"

# building mpich
RUN yum update -y && \
    yum -y install autoconf automake gcc-gfortran && \
    yum -y clean all
    
RUN cd /softwares && \
    wget http://www.mpich.org/static/downloads/3.2/mpich-3.2.tar.gz && \
    tar zxf mpich-3.2.tar.gz && rm /softwares/mpich-3.2.tar.gz && \
    cd /softwares/mpich-3.2 && \
    ./configure && make && make install && make clean

RUN /sbin/ldconfig

