FROM scistack/root:6.10.00
ARG version="2.3.4.4"
LABEL description="classes for high energy physics"
LABEL version="${version}"

# building clhep
RUN mkdir /softwares/CLHEP 
WORKDIR /softwares/CLHEP

RUN yum -y install wget && \
    yum -y clean all
    
RUN wget http://proj-clhep.web.cern.ch/proj-clhep/DISTRIBUTION/tarFiles/clhep-2.3.4.4.tgz
RUN tar zxvf clhep-2.3.4.4.tgz && rm clhep-2.3.4.4.tgz
RUN mkdir /softwares/CLHEP/2.3.4.4/build
WORKDIR /softwares/CLHEP/2.3.4.4/build

RUN cmake -DCMAKE_INSTALL_PREFIX=/softwares/CLHEP/2.3.4.4/CLHEP /softwares/CLHEP/2.3.4.4/CLHEP && \
    make && make install && \
    rm -rf /softwares/CLHEP/2.3.4.4/build

# Set CLHEP environment
ENV CLHEP_BASE_DIR         "/softwares/CLHEP/2.3.4.4/CLHEP"

    
